Introduction
====================================


Devs:
----------

Years of cumulative efforts from our dedicated team members.


.. list-table:: 2021
   :widths: 20 80
   :header-rows: 0

   * - .. image:: https://avatars.githubusercontent.com/althafnafi?size=200
          :width: 80px
          :height: 80px
          :alt: Althaf Nafi
          :target: https://github.com/althafnafi
     - **Althaf Nafi**
       
       `@althafnafi <https://github.com/althafnafi>`_
   * - .. image:: https://avatars.githubusercontent.com/bryannaufal?size=200
          :width: 80px
          :height: 80px
          :alt: Bryan Naufal
          :target: https://github.com/bryannaufal
     - **Bryan Naufal**
       
       `@bryannaufal <https://github.com/bryannaufal>`_
   * - .. image:: https://avatars.githubusercontent.com/steffinatalie?size=200
          :width: 80px
          :height: 80px
          :alt: Steffi Natalie
          :target: https://github.com/steffinatalie
     - **Steffi Natalie**
       
       `@steffinatalie <https://github.com/steffinatalie>`_


.. list-table:: 2022
   :widths: 20 80
   :header-rows: 0

   * - .. image:: https://avatars.githubusercontent.com/JasonJasu?size=200
          :width: 80px
          :height: 80px
          :alt: Jason 
          :target: https://github.com/JasonJasu
     - **JasonJasu**
       
       `@JasonJasu <https://github.com/JasonJasu>`_

   * - .. image:: https://avatars.githubusercontent.com/AtharAdista?size=200
          :width: 80px
          :height: 80px
          :alt: AtharAdista
          :target: https://github.com/AtharAdista
     - ****
       
       `@AtharAdista <https://github.com/AtharAdista>`_

.. list-table:: 2023
   :widths: 20 80
   :header-rows: 0

   * - .. image:: https://avatars.githubusercontent.com/coolcmyk?size=200
          :width: 80px
          :height: 80px
          :alt: Ryan Adidaru
          :target: https://github.com/coolcmyk
     - **coolcmyk**
       
       `@coolcmyk <https://github.com/coolcmyk>`_
   * - .. image:: https://avatars.githubusercontent.com/DaoistXuandu?size=200
          :width: 80px
          :height: 80px
          :alt: Raihan Akbar
          :target: https://github.com/DaoistXuandu
     - **DaoistXuandu**
       
       `@DaoistXuandu <https://github.com/DaoistXuandu>`_
   * - .. image:: https://avatars.githubusercontent.com/SangKalaS?size=200
          :width: 80px
          :height: 80px
          :alt: Arty
          :target: https://github.com/SangKalaS
     - **Arty**
       
       `@SangKalaS <https://github.com/SangKalaS>`_
   * - .. image:: https://avatars.githubusercontent.com/HendhyW?size=200
          :width: 80px
          :height: 80px
          :alt: HendhyW
          :target: https://github.com/HendhyW
     - **HendhyW**
       
       `@HendhyW <https://github.com/HendhyW>`_

.. list-table:: 2024
   :widths: 20 80
   :header-rows: 0

   * - .. image:: https://avatars.githubusercontent.com/apenchuu?size=200
          :width: 80px
          :height: 80px
          :alt: Steven
          :target: https://github.com/apenchuu
     - **Steven**
       
       `@apenchuu <https://github.com/apenchuu>`_
   * - .. image:: https://avatars.githubusercontent.com/Cyaside?size=200
          :width: 80px
          :height: 80px
          :alt: Tristan Rasheed Satria
          :target: https://github.com/Cyaside
     - **Tristan Rasheed Satria**
       
       `@Cyaside <https://github.com/Cyaside>`_
   * - .. image:: https://avatars.githubusercontent.com/D3zNt?size=200
          :width: 80px
          :height: 80px
          :alt: Nic
          :target: https://github.com/D3zNt
     - **Nic**
       
       `@D3zNt <https://github.com/D3zNt>`_
   * - .. image:: https://avatars.githubusercontent.com/evan052006?size=200
          :width: 80px
          :height: 80px
          :alt: evan052006
          :target: https://github.com/evan052006
     - **evan052006**
       
       `@evan052006 <https://github.com/evan052006>`_
   * - .. image:: https://avatars.githubusercontent.com/muhammadakfz?size=200
          :width: 80px
          :height: 80px
          :alt: Muhammad Akhyar Fahrurrozi
          :target: https://github.com/muhammadakfz
     - **Muhammad Akhyar Fahrurrozi**
       
       `@muhammadakfz <https://github.com/muhammadakfz>`_


Welcome to the **Core** repository - a comprehensive robotics platform for Autonomous Surface Vehicles (ASV) and Remotely Operated Vehicles (ROV) development and simulation.

🚀 Overview
-----------

This repository contains the core packages and simulation environments for developing and testing ASV and ROV systems. The platform integrates multiple simulation environments with a robust ROS2-based backend to provide a complete development ecosystem for marine robotics.

🏗️ Architecture
---------------

Backend
~~~~~~~
- **ROS2**: Primary communication framework
- **Python**: Core development language
- **Mission Planning**: Automated mission execution and behavior trees

Simulation Environments
~~~~~~~~~~~~~~~~~~~~~~~
- **Unity**: ASV (Autonomous Surface Vehicle) simulation
- **Godot**: ROV (Remotely Operated Vehicle) simulation

📁 Repository Structure
-----------------------

.. code-block:: text

   core/
   ├── core/                    # Core ROS2 packages
   ├── core_behavior_tree/      # Mission behavior tree implementation
   ├── core_control/           # Control systems and algorithms
   ├── core_feature_test/      # Feature testing modules
   ├── core_msgs/              # Custom ROS2 message definitions
   ├── core_msgs_asv/          # ASV-specific message types
   ├── ros_docker_shenanigans/ # Docker configuration for ROS
   └── scripts/                # Utility and deployment scripts

🤖 Platforms Supported
-----------------------

ASV (Autonomous Surface Vehicle)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Simulation**: Unity-based environment
- **Features**: 
  
  - Autonomous navigation
  - Mission planning
  - Surface vehicle dynamics
  - Sensor integration

ROV (Remotely Operated Vehicle)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Simulation**: Godot-based environment
- **Features**:
  
  - Underwater vehicle control
  - Teleoperation capabilities
  - Underwater physics simulation
  - Sensor modeling

🛠️ Development Status
---------------------

.. warning::
   This project is currently under active development. Both ASV and ROV simulations are in progress and may contain experimental features.

Current Development Focus
~~~~~~~~~~~~~~~~~~~~~~~~~
- Mission planning and behavior tree implementation
- Simulation environment refinement
- Control system optimization
- Message protocol standardization

🚀 Getting Started
------------------

Prerequisites
~~~~~~~~~~~~~
- ROS2 (Humble/Iron recommended)
- Python 3.8+
- Docker (for containerized deployment)
- Unity (for ASV simulation development)
- Godot (for ROV simulation development)

Quick Setup
~~~~~~~~~~~

1. **Clone the repository**

   .. code-block:: bash

      git clone <repository-url>
      cd core

2. **Build ROS2 packages**

   .. code-block:: bash

      colcon build
      source install/setup.bash

3. **Run simulation** (when available)

   .. code-block:: bash

      # ASV simulation
      ros2 launch core_asv simulation.launch.py
      
      # ROV simulation  
      ros2 launch core_rov simulation.launch.py

📋 Core Components
------------------

Mission Planning
~~~~~~~~~~~~~~~~
- Behavior tree-based mission execution
- Waypoint navigation
- Task sequencing and coordination

Control Systems  
~~~~~~~~~~~~~~~
- PID controllers for vehicle dynamics
- Adaptive control algorithms
- Safety and emergency protocols

Communication
~~~~~~~~~~~~~
- Custom ROS2 message definitions
- Inter-vehicle communication protocols
- Ground station interface

Simulation
~~~~~~~~~~
- Physics-based vehicle models
- Environmental conditions modeling
- Sensor simulation and noise modeling

🔧 Configuration
----------------

Configuration files and parameters can be found in each respective package. Key configuration areas include:

- Vehicle parameters and dynamics
- Sensor configurations
- Mission planning parameters
- Communication settings

🐛 Known Issues
---------------

As this is an active development project, please check the `Issues <../../issues>`_ section for current known problems and their status.

🤝 Contributing
---------------

This project is under active development. For contribution guidelines and development workflows, please refer to the project maintainers.

📄 Documentation
-----------------

Detailed documentation for each component will be available as the project matures. Current documentation includes:

- API documentation (auto-generated)
- Configuration guides
- Simulation setup instructions
- Development best practices

.. toctree::
   :maxdepth: 2
   :caption: Contents:
   :hidden:

   api/index
   guides/index
   tutorials/index

📞 Support
----------

For questions, issues, or contributions, please use the GitHub Issues system or contact the development team.

----

*This documentation is for the Core ASV/ROV robotics platform. Last updated: June 2025*
