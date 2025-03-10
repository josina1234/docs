Calibration
###########

In general, the cameras should be calibrated every time they have not been used for a while.
If you can be sure that the cameras have not been moved (accidentally), calibration should not be necessary (e.g. resuming experiments on the next day).


L-Frame Orientation & Position
==============================

We align the L-Frame with the x- and y-axis of the tank. 
The long arm axis aligns with the x-axis and the short arm with the y-axis.

It is a good idea to align the L-frame with one of the tags. That way, you can look up the (approximate) position of the tag.


.. figure:: /res/images/qualisys/l_frame_in_tank.jpg

   L-Frame position in tank.

Calibration Settings 
====================

Setting the orientation
+++++++++++++++++++++++

*Before* you calibrate, you should set the L-Frame orientation. Changing this afterwards is a pain.

In the settings, under :file:`Input Devices`  - :file:`Camera System` - :file:`Calibration`, set the :file:`coordinate system orientation`, set the coordinate frame orientaiton.


- **Axis pointing upwards:** Positive z-axis (should be default)

- **Long arm axis:** positive x-axis

.. figure:: /res/images/qualisys/calibration_orientation.png


Setting the translation
+++++++++++++++++++++++

*After* you have successfully calibrated, you can translate the origin of the original coordinate system to be aligned with our definition in ROS.

.. figure:: /res/images/qualisys/calibration_translation.png

Calibration Results
===================
An average residual under 1mm is desirable. 

.. attention:: 

   Remember to remove the L-Frame from the tank after finishing the calibration. Unfortunately, the markers are not waterproof...