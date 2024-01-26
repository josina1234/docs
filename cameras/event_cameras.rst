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
