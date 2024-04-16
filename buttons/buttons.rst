.. _sec-buttons:

Buttons
#######

Basic Function
==============

.. todo::

   Add an image of the buttons

While operating a real vehicle it is quit nice to have some buttons to easily control the vehicle.
This includes, for example, arming and disarming (probably the most important and most used feature) the vehicle quickly switch between different modes of operation or rebooting the FCU.
Hence, we have written a `buttons <https://github.com/HippoCampusRobotics/buttons>`__ package.

The ``button_interface_node`` emits :file:`buttons_msgs/msg/Button` messages with the corresponding button index when the respective button has been pressed.

Since armin/disarming is an essential feature, we have it already implemented in a `button_handler node <https://github.com/HippoCampusRobotics/buttons/blob/main/nodes/button_handler_node>`__.
It also serves as an example for the implementation of own button handler nodes.
Therefore there is no need to modify anything in the buttons package.

Additional Functions
====================

.. todo::

   Add an image of the LED indicator.

Unlike the same of the package suggests, the package has additional functions.
It can control a WS2812 LED strip as indicator lights to display the arming state, the battery level, and the general health state of the button module.

Arming State
   Blinking red means armed (potentially dangerous). Green stands for disarmed.

Battery Level
   As soon as the battery level indicator light turns to anything else then green for more than a few seconds (a few like 5 at maximum), it is time to more or less immediately switch off the vehicle and remove the battery.
   A deep discharge of the battery is no fun.
