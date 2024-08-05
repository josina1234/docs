Workspace Setup
===============

In the following, we describe our ROS2 system setup.

.. note::
   This guide assumes `Ubuntu 24.04 <https://releases.ubuntu.com/24.04/>`_ is used as OS. We use ROS2 `jazzy <https://docs.ros.org/en/jazzy/index.html>`_.


Our Workspace Setup
-------------------

There are a few packages that we will need to build from source, but probably will not touch (or at least not too much).
In order to keep the compilation time of our workspace as short as possible during development, we will use a setup with two overlayed workspaces. 
We use :file:`ros2` as development workspace und :file:`ros2_underlay` for larger manually compiled non-development packages that take a lot of time to compile/recompile.
In :file:`ros2`, we will keep all of the packages we will develop more or less actively.

To create this directory structure, execute:

.. code-block:: console

   $ mkdir -p ~/ros2/src \
   && mkdir -p ~/ros2_underlay/src


Getting the external packages
-----------------------------

AprilTag-ROS
************

We currently use a slightly adapted version of the ROS2 port of the :code:`apriltag_ros` package by `Christian Rauch <https://github.com/christianrauch/apriltag_ros>`__.

Download our version:

.. tabs::

   .. code-tab:: console ssh

      $ cd ~/ros2_underlay/src \
      && git clone -b hippo git@github.com:HippoCampusRobotics/apriltag_ros.git

   .. code-tab:: console https
      
      $ cd ~/ros2_underlay/src \
      && git clone -b hippo https://github.com/HippoCampusRobotics/apriltag_ros.git


PlotJuggler
***********

PlotJuggler is a very convenient plotting tool. 
Using ROS Iron, the normal release version should work just fine:

.. code:: console

   $ sudo apt install ros-${ROS_DISTRO}-plotjuggler


Building the Workspaces
-----------------------

With :code:`colcon`, the new build tool for ROS2, you cannot build your custom workspace when it is sourced.
This would mean that you either cannot source your workspace in :file:`.zshrc` (or :file:`.bashrc` if you use bash), or you have to manually make sure to run the build command in an environment where you only source workspaces outside the workspace you want to build. 

Since this is very tedious, we define some aliases. Put these two lines into your :file:`.zshrc`:

.. code:: sh

   echo "alias build_ros=\"env -i HOME=\$HOME USER=\$USER TERM=xterm-256color bash -l -c 'source \$HOME/ros2_underlay/install/setup.bash && cd \$HOME/ros2 && colcon build --symlink-install --cmake-args -DCMAKE_EXPORT_COMPILE_COMMANDS=ON'\"" >> ~/.zshrc
   echo "alias build_underlay=\"env -i HOME=\$HOME USER=\$USER TERM=xterm-256color bash -l -c 'source /opt/ros/jazzy/setup.bash && cd \$HOME/ros2_underlay && colcon build'\"" >> ~/.zshrc
   source ~/.zshrc
   echo "alias rosdep-ros2=\"env -i HOME=$HOME USER=$USER TERM=xterm-256color bash -l -c 'source $HOME/ros2_underlay/install/setup.bash && cd $HOME/ros2 && rosdep install --from-paths src -y --ignore-src'\"" >> ~/.zshrc
   source ~/.zshrc
   echo "alias rosdep-underlay=\"env -i HOME=$HOME USER=$USER TERM=xterm-256color bash -l -c 'source /opt/ros/jazzy/setup.bash && cd $HOME/ros2_underlay && rosdep install --from-paths src -y --ignore-src'\"" >> ~/.zshrc
   source ~/.zshrc

.. important::
   Make sure to source the :file:`.zshrc` in your terminal each time you make changes. 

Underlay Workspace
******************

We can now build the first *underlayed* workspace :file:`ros2_underlay`.
But first, let's check for unresolved dependencies.

.. code:: console

   $ rosdep-underlay

And to build:

.. code:: console

   $ build_underlay

Note that you do not have to be inside the respective workspace directory to build by executing the defined alias. Very convenient!

Add sourcing the ROS installation in your :code:`.zshrc`

.. code:: console

   $ echo "source /opt/ros/${ROS_DISTRO}/setup.zsh" >> ~/.zshrc && \
   source ~/.zshrc

After a successful build, we can source this workspace in the :file:`.zshrc`, so that our main, overlayed workspace will find it.

.. code:: console

   $ echo 'source $HOME/ros2_underlay/install/setup.zsh' >> ~/.zshrc && \
   source ~/.zshrc

Main Workspace
**************

Now, we can build our main workspace. Let's get our packages:

Core packages
#############

.. tabs::

   .. code-tab:: console ssh

      $ cd ~/ros2/src \
      && git clone --recursive git@github.com:HippoCampusRobotics/hippo_common.git \
      && git clone --recursive git@github.com:HippoCampusRobotics/hippo_msgs.git \
      && git clone git@github.com:HippoCampusRobotics/hippo_control_msgs.git \
      && git clone git@github.com:HippoCampusRobotics/hippo_sim.git \
      && git clone git@github.com:HippoCampusRobotics/hippo_gz_plugins.git \
      && git clone --recursive git@github.com:HippoCampusRobotics/esc.git \
      && git clone git@github.com:HippoCampusRobotics/hippo_control.git \
      && git clone git@github.com:HippoCampusRobotics/remote_control.git \
      && git clone git@github.com:HippoCampusRobotics/state_estimation.git \
      && git clone git@github.com:HippoCampusRobotics/visual_localization.git

   .. code-tab:: console https
      
      $ cd ~/ros2/src \
      && git clone --recursive https://github.com/HippoCampusRobotics/hippo_common.git \
      && git clone --recursive https://github.com/HippoCampusRobotics/hippo_msgs.git \
      && git clone https://github.com/HippoCampusRobotics/hippo_control_msgs.git \
      && git clone https://github.com/HippoCampusRobotics/hippo_sim.git \
      && git clone https://github.com/HippoCampusRobotics/hippo_gz_plugins.git \
      && git clone --recursive https://github.com/HippoCampusRobotics/esc.git \
      && git clone https://github.com/HippoCampusRobotics/hippo_control.git \
      && git clone https://github.com/HippoCampusRobotics/remote_control.git \
      && git clone https://github.com/HippoCampusRobotics/state_estimation.git \
      && git clone https://github.com/HippoCampusRobotics/visual_localization.git

DVL
###

.. tabs::

   .. code-tab:: console ssh

      $ cd ~/ros2/src \
      && git clone git@github.com:HippoCampusRobotics/dvl.git \
      && git clone git@github.com:HippoCampusRobotics/dvl_msgs.git 

   .. code-tab:: console ssh

      $ cd ~/ros2/src \
      && git clone https://github.com/HippoCampusRobotics/dvl.git \
      && git clone https://github.com/HippoCampusRobotics/dvl_msgs.git

These packages have some more dependencies. Let's resolve them by executing

.. code:: console

   $ rosdep-ros2


Make sure that the underlay workspace containing external packages is sourced for this.

Then, we can build this workspace using our defined alias.

.. code:: console

   $ build_ros

Now, source this workspace in your :file:`.zshrc`, too, using the local setup this time:

.. code:: console

   $ echo 'source $HOME/ros2/install/local_setup.zsh' >> ~/.zshrc

Note that since this workspace overlays the :file:`ros2_underlay` workspace, this setup file needs to be sourced afterwards.


Auto-Complete
*************

.. todo::

   This might have changed for Ubuntu 24.04.
   Check and complete this todo!

ROS2 command line tools do not autocomplete as of this `GitHub Issue <https://github.com/ros2/ros2cli/issues/534>`_. While this issue has since been closed, the problem still occurs. To fix this

.. code-block:: console
   
   $ echo "eval \"\$(register-python-argcomplete ros2)\"" >> ~/.zshrc
   $ echo "eval \"\$(register-python-argcomplete colcon)\"" >> ~/.zshrc

Auto-completing topic names seems to work only after an execution of `ros2 topic list`. Before the auto-complete gets stuck and has to be canceled by :kbd:`Ctrl` + :kbd:`C`.

Sourcing :file:`install/setup.zsh` might reset this. Better source :file:`install/local_setup.zsh`.


Final Check
***********

Your :file:`.zshrc` should look similar to this now:

.. code:: sh 
   
   ...


   alias build_ros="env -i HOME=$HOME USER=$USER TERM=xterm-256color bash -l -c 'source $HOME/ros2_underlay/install/setup.bash && cd $HOME/ros2 && colcon build --symlink-install --cmake-args --no-warn-unused-cli -DCMAKE_EXPORT_COMPILE_COMMANDS=ON'"
   alias build_underlay="env -i HOME=$HOME USER=$USER TERM=xterm-256color bash -l -c 'source /opt/ros/jazzy/setup.bash && cd $HOME/ros2_underlay && colcon build --symlink-install --cmake-args --no-warn-unused-cli -DCMAKE_EXPORT_COMPILE_COMMANDS=ON'"

   alias rosdep-ros2="env -i HOME=$HOME USER=$USER TERM=xterm-256color bash -l -c 'source $HOME/ros2_underlay/install/setup.bash && cd $HOME/ros2 && rosdep install --from-paths src -y --ignore-src'"
   alias rosdep-underlay="env -i HOME=$HOME USER=$USER TERM=xterm-256color bash -l -c 'source /opt/ros/jazzy/setup.bash && cd $HOME/ros2_underlay && rosdep install --from-paths src -y --ignore-src'"

   source /opt/ros/jazzy/setup.zsh
   source $HOME/ros2_underlay/install/local_setup.zsh
   source $HOME/ros2/install/local_setup.zsh

   eval "$(register-python-argcomplete ros2)"
   eval "$(register-python-argcomplete colcon)"
