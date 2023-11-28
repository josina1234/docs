Usage
#####

Run the xyz Setup
=================

.. code-block:: console

   $ ros2 launch gantry xyz_motors.launch.py

This will start the three motors for the x-, y-, and z-axis, respectively.
The configuration files for the motors are found in ``gantry/config/motor_<axis_name>.yaml``.


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
   
