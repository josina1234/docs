Pre-built Packages
##################

For convenience, we provide our own packages as pre-built binaries at `repositories.hippocampus-robotics.net <repositories.hippocampus-robotics.net>`__.
The advantage is that we do **not** need to compile the packages we are not developing actively ourselfs.

.. note:: 

   In case that we do not wish to install the pre-built binaries, it is perfectly fine to skip this part and clone all the required packages into our workspace and build them on our own.

Add Sources
===========

#. Adding the key

   .. code-block:: console

      $ sudo curl https://repositories.hippocampus-robotics.net/hippo-archive.key -o /etc/apt/keyrings/hippocampus-robotics.asc

#. Adding the sources

   .. code-block:: console

      $ echo "deb [arch=$(dpkg --print-architecture) signed-by/etc/apt/keyrings/hippocampus-robotics.asc] https://repositories.hippocampus-robotics.net/ubuntu $(lsb_release -cs) main" > sudo tee /etc/apt/sources.list.d/hippocampus.list

``rosdep``
==========

#. Add keys for ``rosdep`` so it knows that our packages can be resolved via ``apt install ros-iron-<pkg-name>``.

   .. code-block:: console

      $ echo 'yaml https://raw.githubusercontent.com/HippoCampusRobotics/hippo_common/main/rosdep.yaml' | sudo tee /etc/ros/rosdep/sources.list.d/50-hippocampus-packages.list

#. Apply the changes

   .. code-block:: console

      $ rosdep update


