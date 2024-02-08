Event Camera Collaboration
##########################

The Bag Files
=============

The vehicle name used in our set up is ``uuv02``, hence all vehicle related topic names are prefixed with ``uuv02``.

With Gantry
***********

.. code-block:: console

   $ ros2 bag info gantry_lemniscate_v_0.1

   Files:             gantry_lemniscate_v_0.1_0.mcap
   Bag size:          1.0 GiB
   Storage id:        mcap
   Duration:          204.246s
   Start:             Feb  7 2024 17:40:23.450 (1707327623.450)
   End:               Feb  7 2024 17:43:47.696 (1707327827.696)
   Messages:          206770
   Topic information: Topic: /uuv02/event_camera/imu | Type: sensor_msgs/msg/Imu | Count: 165290 | Serialization Format: cdr
                      Topic: /uuv02/event_camera/events | Type: event_camera_msgs/msg/EventPacket | Count: 20328 | Serialization Format: cdr
                      Topic: /gantry/motor_y/position | Type: gantry_msgs/msg/MotorPosition | Count: 2034 | Serialization Format: cdr
                      Topic: /gantry/motor_x/position | Type: gantry_msgs/msg/MotorPosition | Count: 2034 | Serialization Format: cdr
                      Topic: /uuv02/vertical_camera/image_raw/compressed | Type: sensor_msgs/msg/CompressedImage | Count: 6871 | Serialization Format: cdr
                      Topic: /uuv02/odometry | Type: nav_msgs/msg/Odometry | Count: 10213 | Serialization Format: cdr

The gantry position is published in the topics ``/gantry/motor_x/position`` and ``gantry/motor_y/position``.
Event camera data is published as ``/uuv02/event_camera/events`` and ``/uuv02/event_camera/imu``.

Without Gantry
**************

.. code-block:: console

   $ ros2 bag info onboard_lemniscate_v_0.3/

   Files:             onboard_lemniscate_v_0.3_0.mcap
   Bag size:          1014.5 MiB
   Storage id:        mcap
   Duration:          105.250s
   Start:             Feb  7 2024 17:59:27.763 (1707328767.763)
   End:               Feb  7 2024 18:01:13.14 (1707328873.14)
   Messages:          105150
   Topic information: Topic: /uuv02/event_camera/imu | Type: sensor_msgs/msg/Imu | Count: 83939 | Serialization Format: cdr
                      Topic: /uuv02/event_camera/events | Type: event_camera_msgs/msg/EventPacket | Count: 10323 | Serialization Format: cdr
                      Topic: /gantry/motor_y/position | Type: gantry_msgs/msg/MotorPosition | Count: 1042 | Serialization Format: cdr
                      Topic: /gantry/motor_x/position | Type: gantry_msgs/msg/MotorPosition | Count: 1043 | Serialization Format: cdr
                      Topic: /uuv02/odometry | Type: nav_msgs/msg/Odometry | Count: 5262 | Serialization Format: cdr
                      Topic: /uuv02/vertical_camera/image_raw/compressed | Type: sensor_msgs/msg/CompressedImage | Count: 3541 | Serialization Format: cdr

As long as our Qualisys cameras are still in service, we have to rely on the onboard visual localization.
The estimated pose and velocity is published as ``/uuv02/odometry``.
The event camera specific topics are the same as for the gantry setup.

Reading the Data
================

We have prepared a basic example on how to to read the event_camera data.

