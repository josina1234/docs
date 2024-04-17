Usage
#####

Run the xyz Setup
=================

.. code-block:: console

   $ ros2 launch gantry xyz_motors.launch.py

This will start the three motors for the x-, y-, and z-axis, respectively.
The configuration files for the motors are found in ``gantry/config/motor_<axis_name>.yaml``.

Home the Motors
===============

.. important::

   Always make sure that the motors are homed before sending any setpoints!

.. note::

   The motor position is stored inside the motion controller and not inside any code running on the Raspberry Pi or any ROS node.
   Relaunching any node does **not** make it necessary to rerun the homing procedure 🥳.

#. Move the motors to the home position.

   The motors provide a service to move to the home position.

   .. tabs::

      .. code-tab:: console x

         $ ros2 service call /gantry/motor_x/start_homing std_srvs/srv/Trigger{}

      .. code-tab:: console y
         
         $ ros2 service call /gantry/motor_y/start_homing std_srvs/srv/Trigger {}

      .. code-tab:: console z
         
         $ ros2 service call /gantry/motor_z/start_homing std_srvs/srv/Trigger {}

#. Set the current position.
   Usually this will be 0 but we can also specify arbitrary values either in motor dimensions (i.e. increments) or in physical dimensions ([m]).

   .. tabs::

      .. code-tab:: console x

         $ ros2 service call /gantry/motor_x/set_home_position gantry_msgs/srv/SetHomePosition {} 

      .. code-tab:: console y
         
         $ ros2 service call /gantry/motor_y/set_home_position gantry_msgs/srv/SetHomePosition {} 

      .. code-tab:: console z
         
         $ ros2 service call /gantry/motor_z/set_home_position gantry_msgs/srv/SetHomePosition {} 

   .. todo:: Add an example for non zero values


Smooth Accelerations in Position Mode
=====================================

The maximum acceleration can be set via the :file:`~/set_max_accel` service.
If the maximum acceleration is higher than what the motor can acutally achieve (it has to move quite a bit of mass) it will overshoot the target position.
For smoother accelerations we can reduce the acceleration to a smaller value.

To get the currently set value run

.. tabs::

   .. code-tab:: console x

      $ ros2 service call /gantry_motor_x/get_max_accel gantry_msgs/srv/GetFloatDrive {}

   .. code-tab:: console y

      $ ros2 service call /gantry_motor_y/get_max_accel gantry_msgs/srv/GetFloatDrive {}

   .. code-tab:: console z

      $ ros2 service call /gantry_motor_z/get_max_accel gantry_msgs/srv/GetFloatDrive {}

To set a new value run

.. tabs::

   .. code-tab:: console x

      $ ros2 service call /gantry_motor_x/set_max_accel gantry_msgs/srv/SetFloatDrive '{motorside_value: 500}'

   .. code-tab:: console y

      $ ros2 service call /gantry_motor_y/set_max_accel gantry_msgs/srv/SetFloatDrive '{motorside_value: 500}'

   .. code-tab:: console z

      $ ros2 service call /gantry_motor_z/set_max_accel gantry_msgs/srv/SetFloatDrive '{motorside_value: 500}'

.. note::

   We could also set the ``driveside_value`` in SI units instead of value in motor dimensions.

Limit the Motor Velocity in Position Mode
=========================================

This is equivalent to acceleration limit settings, but the service names are

* ``~/get_max_speed``
* ``~/set_max_speed``

Run a Single Motor
==================

.. code-block:: console

   $ ros2 run gantry single_motor --ros-args \
   --params-file <path_to_config_file> \
   -r __node:=<motor_name> \
   -r __ns:=<namespace>

.. note::

   The path to the config file can be relative or absolute.

.. attention::

   Keep in mind that namespaces have to start with a leading ``/``.
   Setting the node name and the namespace is optional but recommended.


Example
   Assuming we are inside the ``gantry`` package directory, we can directly run

   .. code-block:: console

      $ ros2 run gantry single_motor --ros-args \
      --params-file config/motor_x.yaml \
      -r __node:=single_x \
      -r __ns:=gantry
   
