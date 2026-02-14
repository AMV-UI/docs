core_gcs
========

Ringkasan
---------
Package ini adalah node ROS 2 untuk GCS (Ground Control Station) yang membaca data dari berbagai topik ROS (mis. ``pixhawk``, kamera, mode, dan misi), lalu menyiarkan (broadcast) data tersebut lewat WebSocket agar UI eksternal bisa subscribe.

Struktur dan relasi
-------------------
- Node utama ada di ``core_gcs/core_gcs/gcs.py`` dan dieksekusi sebagai ``gcs`` lewat entry point di ``core_gcs/setup.py``.
- Launch file ada di ``core_gcs/launch/launch.py`` untuk menjalankan node ``gcs`` dan mengatur parameter ``track``.
- Metadata package (ROS 2/ament) ada di ``core_gcs/package.xml``, ``core_gcs/setup.py``, ``core_gcs/setup.cfg``, dan ``core_gcs/resource/core_gcs``.
- Folder mock ada di ``core_gcs/core_gcs/mock`` sebagai generator data uji untuk topik tertentu (diringkas di bagian *Mock*).

Penjelasan setiap file 
---------------------------------
- ``core_gcs/package.xml`` — Manifest ROS 2 package. Menyatakan nama package, versi, dependency, dan build type ``ament_python``.
- ``core_gcs/setup.py`` — Konfigurasi packaging Python. Mendaftarkan entry point ``gcs`` serta script mock. Mengikutsertakan launch file pada instalasi.
- ``core_gcs/setup.cfg`` — Konfigurasi lokasi script saat develop/install.
- ``core_gcs/resource/core_gcs`` — Resource marker untuk ament index (file kosong, namun wajib untuk discovery package).
- ``core_gcs/core_gcs/__init__.py`` — Inisialisasi package Python (kosong).
- ``core_gcs/core_gcs/gcs.py`` — Implementasi node GCS + WebSocket server.
- ``core_gcs/launch/launch.py`` — Launch description untuk menjalankan ``gcs`` dengan parameter ``track``.

Relasi antar komponen
---------------------
#. ``gcs`` (node ROS 2) membuat subscriber ke beberapa topik dari package lain (mis. ``core`` dan ``core_msgs``).
#. Data dari topik diubah menjadi payload JSON dan disiarkan melalui WebSocket (host ``0.0.0.0``, port ``8000``).
#. Launch file menyediakan argumen ``track`` dan mem-passing parameter ke node ``gcs``.

Kelas dan fungsi 
---------------------------

``core_gcs/core_gcs/gcs.py``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- ``class Gcs(Node)``

  - **Tugas utama:** Node ROS 2 yang mengumpulkan data dari berbagai topik dan broadcast ke klien WebSocket.
  - ``__init__(self, loop)`` — Inisialisasi node, state internal (history posisi, mode, arena), dan memanggil ``setup()``.
  - ``setup(self)`` — Mendaftarkan seluruh subscriber ROS (pwm, arena, kamera, box detection, pixhawk, misi, pxmode).
  - ``pwm_callback(self, msg)`` — Mengambil nilai channel untuk ``speed``, ``yaw``, ``comm``.
  - ``arena_callback(self, msg)`` — Memperbarui arena/track aktif.
  - ``pxmode_callback(self, msg)`` — Memperbarui mode Pixhawk.
  - ``image_callback(self, msg)`` — Menyiarkan data kamera yang sudah diproses.
  - ``blue_box_callback(self, msg)`` — Menyiarkan deteksi box biru.
  - ``green_box_callback(self, msg)`` — Menyiarkan deteksi box hijau.
  - ``mission_callback(self, msg)`` — Menyiarkan nomor misi aktif.
  - ``pixhawk_callback(self, msg)`` — Memproses data navigasi (lat/lon history, altitude, speed, heading, track), lalu broadcast.
  - ``_handle_incoming_data(self, topic_name, data)`` — Membungkus data ke format JSON internal dan men-trigger ``broadcast_message()`` via event loop.
  - ``broadcast_message(self, message)`` — Mengirim JSON ke semua klien WebSocket yang aktif, serta membersihkan klien yang sudah putus.

- ``async websocket_handler(websocket, path, node)`` — Menangani lifecycle koneksi WebSocket (connect/listen/disconnect) untuk satu klien.

- ``make_websocket_handler(node)`` — Wrapper agar kompatibel dengan signature ``websockets`` versi lama dan baru.

- ``async main_async()`` — Inisialisasi ROS 2, membuat node ``Gcs``, menjalankan WebSocket server, dan menjalankan executor ROS di thread terpisah.

- ``main()`` — Entry point sinkron untuk menjalankan ``main_async()``.

``core_gcs/launch/launch.py``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- ``generate_launch_description()`` — Mendeklarasikan argumen ``track`` (default ``B``) dan menjalankan node ``gcs`` dengan parameter tersebut.

Mock 
--------------
Folder ``core_gcs/core_gcs/mock`` berisi node-node uji untuk mensimulasikan data yang biasanya berasal dari sensor/komponen lain:

- ``core_gcs/core_gcs/mock/mock_mission.py`` — Publisher sederhana untuk data kamera yang diproses (contoh payload string) sebagai simulasi.
- ``core_gcs/core_gcs/mock/mock_pixhawk.py`` — Simulator data ``Pixhawk`` dengan pergerakan acak di area kecil.
- ``core_gcs/core_gcs/mock/mock_pxmode.py`` — Publisher mode Pixhawk (mis. ``AUTO``).
- ``core_gcs/core_gcs/mock/mock_trial.py`` — Simulator ``Pixhawk`` dengan pola zigzag di area tertentu.

Cara menjalankan core_gcs
----------------------------------------

Build package
~~~~~~~~~~~~~
- Pastikan workspace sudah di-root folder proyek, lalu build package ``core_gcs``.

Jalankan node ``gcs``
~~~~~~~~~~~~~~~~~~~~~

Menjalankan langsung:

.. code-block:: bash

   ros2 run core_gcs gcs

Menjalankan via launch file (dengan pilihan track):

.. code-block:: bash

   ros2 launch core_gcs launch.py track:=B

WebSocket endpoint
~~~~~~~~~~~~~~~~~~
- Server WebSocket berjalan di ``ws://0.0.0.0:8000``. Klien UI bisa berlangganan ke endpoint ini untuk menerima payload JSON.

.. note::
   Pastikan seluruh dependency ROS 2 dan package lain yang dibutuhkan (mis. ``core_msgs``, ``core``) sudah ter-build dan environment ROS 2 sudah di-source.


Basic-GCS (UI)
--------------

Dokumentasi ini menjelaskan file-file penting, relasi antar bagian, fungsi/fungsi utama, dan cara menjalankan proyek Basic-GCS.

Ringkasan
~~~~~~~~~~~~~~~~
Basic-GCS adalah antarmuka Ground Control Station berbasis Next.js (App Router) dengan Tailwind CSS. UI menampilkan telemetry, posisi, status misi, feed kamera, dan hasil deteksi (green/blue box). Data realtime masuk melalui WebSocket.

Struktur dan relasi utama
~~~~~~~~~~~~~~~~~~~~~~~~~
Alur data utama:

#. ``useTelemetry()`` di ``src/hook/telemetry.ts`` membuka WebSocket via ``src/lib/ws.ts``.
#. Data WebSocket di-parse dan disimpan ke state React.
#. Komponen UI di ``src/app/page.tsx`` mengambil state dari ``useTelemetry()`` lalu menampilkan ke komponen-komponen UI.

Relasi file inti:

- ``src/app/page.tsx`` **mengimpor** komponen UI (Title, GeoTag, GenInfo, PositionLog, Image, Position, Video, Motor) dan **menggunakan** ``useTelemetry()``.
- ``src/hook/telemetry.ts`` **menggunakan** ``connectWebSocket``, ``onMessage``, ``onClose``, ``healthcheck`` dari ``src/lib/ws.ts``.
- ``src/lib/ws.ts`` **mengambil** konfigurasi host/port dari ``.env.local`` (lihat ``.env.local.example``).

Dokumentasi file penting
~~~~~~~~~~~~~~~~~~~~~~~~

Entry UI
^^^^^^^^
- ``src/app/page.tsx``

  - **Fungsi utama:** ``Home()``
  - Mengambil data telemetry dari ``useTelemetry()``.
  - Mendistribusikan data ke komponen-komponen UI.
  - Mengatur layout utama halaman.

- ``src/app/layout.tsx``

  - **Fungsi utama:** ``RootLayout()``
  - Membungkus semua halaman, menambahkan font lokal Geist, dan metadata.
  - Mengimpor ``src/app/globals.css``.

- ``src/app/globals.css`` — Styling global dan variabel CSS untuk tema Tailwind.

Hook telemetry
^^^^^^^^^^^^^^
- ``src/hook/telemetry.ts``

  - **Fungsi utama:** ``useTelemetry()``
  - Membuka koneksi WebSocket (``connectWebSocket``).
  - Berlangganan pesan menggunakan ``onMessage``.
  - Memetakan topik ke state seperti ``image``, ``greenBox``, ``blueBox``, ``mission``, dan data ``pixhawk`` (lat/lon, speed, yaw, comm, track).
  - Reset state saat koneksi terputus via ``onClose``.

WebSocket layer
^^^^^^^^^^^^^^^
- ``src/lib/ws.ts``

  - ``connectWebSocket(url?)``: Membuka koneksi WebSocket, auto-reconnect saat putus.
  - ``onMessage(cb)``: Subscribe pesan masuk.
  - ``onOpen(cb)``: Subscribe event open.
  - ``onClose(cb)``: Subscribe event close.
  - ``healthcheck()``: Cek status koneksi.
  - ``started()``: Dipakai untuk reset canvas saat koneksi pertama kali aktif.

  Menggunakan env ``NEXT_PUBLIC_GCS_HOST`` dan ``NEXT_PUBLIC_GCS_PORT`` (lihat ``.env.local.example``).

Interface (tipe data)
^^^^^^^^^^^^^^^^^^^^^
- ``src/lib/interface.ts`` — Mendefinisikan ``interface GCS`` dan ``interface Initial``.

Komponen UI
^^^^^^^^^^^
- ``src/app/components/title.tsx`` — ``Title()`` menampilkan logo dan judul UI.
- ``src/app/components/geoTag.tsx`` — ``GeoTag({ sog, cog, lon, lat })`` menampilkan waktu, tanggal, SOG, COG, dan koordinat.
- ``src/app/components/genInfo.tsx`` — ``GenInfo({ battery, temprature })`` menampilkan informasi baterai dan suhu.
- ``src/app/components/positionLog.tsx`` — ``PositionLog({ status })`` menampilkan list misi dan statusnya.
- ``src/app/components/video.tsx`` — ``Video({ image, name })`` menampilkan feed kamera (base64 PNG).
- ``src/app/components/image.tsx`` — ``Image({ image, text })`` menampilkan gambar hasil deteksi (surface/underwater) dan waktu pertama kali gambar diterima.
- ``src/app/components/motor.tsx`` — ``Motor({ speed, yaw, communication })`` menampilkan data kontrol motor dan komunikasi.
- ``src/app/components/position.tsx`` — ``Position({ track, lon, lat, initial_lon, initial_lat, prev_lon, prev_lat })`` menggambar posisi pada canvas.
- ``src/app/components/row.tsx`` — ``Row({ row })`` menggambar grid statis (saat ini tidak dipakai; komentar di ``Position``).

Konfigurasi
^^^^^^^^^^^
- ``package.json`` — Script penting: ``dev``, ``build``, ``start``, ``lint``.
- ``next.config.mjs`` — Konfigurasi Next.js.
- ``tailwind.config.ts`` dan ``postcss.config.mjs`` — Konfigurasi Tailwind dan PostCSS.
- ``components.json`` — Konfigurasi shadcn/ui (alias, tailwind config, dll).
- ``.env.local.example`` — Contoh konfigurasi host/port WebSocket.

Folder ``install/`` dan ``log/`` berisi artefak build/colcon (terlihat terkait ROS2/colcon). Untuk menjalankan UI Next.js, folder ini tidak wajib, namun berguna bila proyek ini diintegrasikan dengan pipeline ROS.

Cara menjalankan
~~~~~~~~~~~~~~~~~~~~

Prasyarat:

- Node.js (disarankan versi LTS).
- Server WebSocket GCS berjalan (default port 8000).

Langkah:

#. Salin konfigurasi env: copy ``.env.local.example`` menjadi ``.env.local`` dan sesuaikan ``NEXT_PUBLIC_GCS_HOST`` serta ``NEXT_PUBLIC_GCS_PORT``.
#. Install dependency:

   .. code-block:: bash

      npm install

#. Jalankan mode development:

   .. code-block:: bash

      npm run dev

#. Buka browser: ``http://localhost:3000``

Build dan production:

- Build:

  .. code-block:: bash

     npm run build

- Run:

  .. code-block:: bash

     npm run start

Catatan integrasi
~~~~~~~~~~~~~~~~~

- Data telemetry diproses berdasarkan ``topic`` pada payload WebSocket.
- Topik yang dikenali di ``useTelemetry()``:

  - ``processed`` → ``image``
  - ``show_green`` → ``greenBox``
  - ``show_blue`` → ``blueBox``
  - ``mission`` → ``mission``
  - ``pixhawk`` → lat/lon, speed, yaw, comm, track