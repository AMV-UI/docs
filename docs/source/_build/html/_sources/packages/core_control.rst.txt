core_control
============================

This section contains documentation for core_control package in the system. 

Initial Idea:

Core Control Package acts as a utility package that provides essential functionalities and services that are commonly used across various components of the system. It includes modules for control, navigation, sensors, and communication.

Initial Structure:

- core_control/
    - microcontroller_asv.py // Microcontroller ASV control module, fetching data from Pixhawk to publishing it into ROS2 topics
    - microcontroller_rov.py // Microcontroller ROV control module, fetching data from Pixhawk to publishing it into ROS2 topics


ASV's Motor Configuration
-----------------------------
.. image:: ../assets/packages/ASV_MotorConfig.png
   :width: 600
   :alt: ASV Motor Configuration
   :align: center

The idea is to manually set PWM through standarized ROS2 topic, /cmd_vel, which is used to control the ASV's motors. The microcontroller will then convert these commands into appropriate PWM signals for the motors.
Then the result would be configured movement template, like move_forward, move_backward, turn_left, turn_right, etc.


ASV's Motor Movement Example: Turn Right
-----------------------------
.. image:: ../assets/packages/ASV_MotorMovementExample_Right.png
   :width: 600
   :alt: ASV Motor Configuration
   :align: center

ASV's Motor Movement Example: Intensity
-----------------------------
.. image:: ../assets/packages/ASV_MotorMovementExample_ExtremeRight.png
   :width: 600
   :alt: ASV Motor Configuration
   :align: center

