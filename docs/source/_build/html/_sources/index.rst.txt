Core - ASV & ROV Robotics Platform
====================================

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
