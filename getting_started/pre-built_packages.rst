Pre-built Packages
##################

For convenience, we provide our own packages as pre-built binaries at `repositories.hippocampus-robotics.net <repositories.hippocampus-robotics.net>`__.
The advantage is that we do **not** need to compile the packages we are not developing actively ourselfs.

.. note::

   Packages in a local workspace have a higher priority than the ones installed in :file:`/opt/ros/` via debian packages.
   So we can install all our packages via `apt install` and still use a custom/modifed version of them by having them included in our workspace.

.. note:: 

   In case that we do not wish to install the pre-built binaries, it is perfectly fine to skip this part and clone all the required packages into our workspace and build them on our own.

Add Sources
===========

#. Adding the key

   .. code-block:: console

      $ sudo curl https://repositories.hippocampus-robotics.net/hippo-archive.key -o /etc/apt/keyrings/hippocampus-robotics.asc

#. Adding the sources

   .. code-block:: console

      $ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/hippocampus-robotics.asc] https://repositories.hippocampus-robotics.net/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/hippocampus.list

#. Updating ``apt``

   .. code-block:: console

      $ sudo apt update
   

``rosdep``
==========

#. Add keys for ``rosdep`` so it knows that our packages can be resolved via ``apt install ros-${ROS_DISTRO}-<pkg-name>``.

   .. attention::

      Make sure that ``ROS_DISTRO`` is set to the installed ROS version.
      If you followed :ref:`the previous section <ros-installation>`, this should already be done.
      It can be checked by

      .. code-block:: console

         $ echo $ROS_DISTRO
         jazzy # (or whatever ROS version is used.)

      If it not set, it can be set manually by

      .. code-block:: console

         $ export ROS_DISTRO=jazzy
      
   .. code-block:: console

      $ echo "yaml https://raw.githubusercontent.com/HippoCampusRobotics/hippo_infrastructure/main/rosdep-${ROS_DISTRO}.yaml" | sudo tee /etc/ros/rosdep/sources.list.d/50-hippocampus-packages.list

#. Apply the changes

   .. code-block:: console

      $ rosdep update

Installation
============

For desktop use ``hippo_full`` is most likely the appropriate choice, while for Raspberry Pis deployed with the Ubuntu server image the ``hippo_robot`` package without graphical dependencies is the better choice.

.. tabs::

   .. code-tab:: console hippo_full
      
      $ sudo apt install ros-${ROS_DISTRO}-hippo-full

   .. code-tab:: console hippo_robot

      $ sudo apt install ros-${ROS_DISTRO}-hippo-robot

To find out which packages can be installed from our repository, execute

   .. code-block:: console

      $ curl -s https://repositories.hippocampus-robotics.net/ubuntu/dists/noble/main/binary-amd64/Packages \
      | grep "^Package: " \
      | cut -d" " -f2 | sort -u
      ros-jazzy-acoustic-msgs
      ros-jazzy-alpha-msgs
      ros-jazzy-buttons-msgs
      ros-jazzy-dvl
      ros-jazzy-dvl-msgs
      ros-jazzy-esc
      ros-jazzy-gantry-msgs
      ros-jazzy-hardware
      ros-jazzy-hippo-common
      ros-jazzy-hippo-common-msgs
      ros-jazzy-hippo-control
      ros-jazzy-hippo-control-msgs
      ros-jazzy-hippo-msgs
      ros-jazzy-mjpeg-cam
      ros-jazzy-path-planning
      ros-jazzy-px4-msgs
      ros-jazzy-rapid-trajectories-msgs
      ros-jazzy-remote-control
      ros-jazzy-state-estimation-msgs
      ros-jazzy-uvms-msgs

We can install them by

.. code-block:: console

   $ sudo apt install ros-${ROS_DISTRO}-<PACKAGE_NAME>

for example, if we want to install the remote control package the command would be

.. code-block:: console

   $ ros-${ROS_DISTRO}-remote-control


Most message packages of our framework can be installed via

.. code-block:: console

   $ sudo apt install ros-${ROS_DISTRO}-hippo-common-msgs

