Camera Calibration
##################

We have a convenience launch file for camera calibration.
We use the standard ROS (monocular) camera calibrator.

To start our launch file

.. code-block:: console

   $ ros2 launch visual_localization calibration.launch.py vehicle_name:=bluerov01 camera_name:=vertical_camera compressed:=true

Make sure to adjust the :file:`vehicle_name` and :file:`camera_name` as you need.

The checkerboard settings are set to match the checkerboard at MuM. If you are using a different pattern, make sure to adjust this as well via launch arguments.

The ROS camera calibration tool should open in a seperate window. 

Try to move the checkerboard so that all categories on the right side turn green.
Note: the "size" bar only fills up to the middle. There is no benefit of including samples with the checkerboard far away.

Click calibrate, then click save. This saves the calibration data in :file:`/tmp/calibrationdata.tar.gz`.

Move the data in :file:`ost.yaml` to the Raspberry Pi on the vehicle (the one connected to the camera).
Make sure to change the :file:`camera_name` in this file to the correct camera name, e.g. :file:`vertical_camera`.
The calibration file should be placed in :file:`~/.ros/camera_calibration` and should be named as the camera name. 

For the example above, the file should be :file:`~/.ros/camera_calibration/vertical_camera.yaml`.





