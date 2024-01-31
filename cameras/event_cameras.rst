Event Cameras
#############

Driver
======

.. note::
   This is a getting-started-quickly guide, more complete instructions are documented in the repository's `README <https://github.com/ros-event-camera/libcaer_driver/>`__.

Define the workspace path

.. code-block:: console

   $ WS_DIR="$HOME/ros2_underlay/src"

go to the workspace

.. code-block:: console

   $ cd $WS_DIR

clone the repository and its dependencies

.. code-block:: console

   $ git clone https://github.com/ros-event-camera/libcaer_driver.git \
   && vcs import < libcaer_driver/libcaer_driver.repos

Install the remaining dependencies

.. code-block:: console

   $ rosdep-underlay

Build

.. code-block:: console

   $ build_underlay

Repower USB
***********

After booting the camera is often not found.
Switching off and on again fixes the problem.

This can be done with `uhubctl <https://github.com/mvp/uhubctl>`__.

Installation
   .. code-block:: console

      $ git clone https://github.com/mvp/uhubctl.git \
      && cd uhubctl \
      && make \
      && sudo make install


Off
   .. code-block:: console

      $ sudo uhubctl -l 2 -a 0
On
   .. code-block:: console

      $ sudo uhubctl -l 2 -a 1
   
Laucnh
******

.. code-block:: console

   $ ros2 launch libcaer_driver driver_node.launch.py device_type:=dvxplorer



Renderer
========

Only required to visualize the event camera data as frames.
**Not** required to be installed on the Raspberry Pi.

Define the workspace path

.. code-block:: console

   $ WS_DIR="$HOME/ros2_underlay/src"

go to the workspace

.. code-block:: console

   $ cd $WS_DIR

clone the repository and its dependencies

.. code-block:: console

   $ git clone https://github.com/ros-event-camera/event_camera_renderer.git \
   && vcs import < event_camera_renderer/event_camera_renderer.repos

Install the remaining dependencies

.. code-block:: console

   $ rosdep-underlay

Build

.. code-block:: console

   $ build_underlay
