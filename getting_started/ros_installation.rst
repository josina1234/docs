.. _ros-installation:

ROS Installation
################

We use ROS2 Jazzy.
The following installations steps work for a Ubuntu 24.04 amd64 version **and** for the Ubuntu 24.04 arm64 server image for the Raspberry Pi.

Preparation
===========

#. Make sure you have a UTF-8 supported locale with
   
   .. code-block:: console
      
      $ locale
   
   If not, refer to the `ROS documentation <https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debians.html#set-locale>`__.

#. Enable universe repository
   
   .. code-block:: console
      
      $ sudo apt install software-properties-common \
      && sudo add-apt-repository universe

#. Add the key

   .. code-block:: console

      $ sudo apt update && sudo apt install curl -y \
      && sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

#. Add sources

   .. code-block:: console

      $ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null




#. Update

   .. warning:: This is critial!
   

   .. code-block:: console

      $ sudo apt update && sudo apt upgrade -y

Installation
============

Choose the installation option depending on your needs, e.g. use a more lightweight installation for Raspberry Pis. 

#. Install ROS

   .. tabs::
      .. code-tab:: sh desktop-full

         sudo apt install ros-jazzy-desktop-full
      
      .. code-tab:: sh perception (e.g. for Raspberry Pi)

         sudo apt install ros-jazzy-perception


#. Install development tools

   .. code-block:: console

      $ sudo apt install ros-dev-tools python3-pip

rosdep Initialization
=====================

.. code-block:: console

   $ sudo rosdep init && rosdep update

.. note:: Do **not** execute :code:`rosdep update` with root privileges. This would lead to permission issues.

Source the ROS Setup
====================

.. code-block:: console

   $ echo 'source /opt/ros/jazzy/setup.zsh' >> ~/.zshrc \
   && . ~/.zshrc

A Brief Test (Optional)
=======================

To check whether ROS2 installation is working:

.. code-block:: console

   $ ros2 run turtlesim turtlesim_node


