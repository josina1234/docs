Install Source Dependencies
===========================

Some ROS packages might have dependencies that you have to install from source. For this case, the git repository URLs are written in a :file:`.repos` file.

To clone all source dependencies of e.g. :file:`hippo_full`:


.. code-block:: console

   $ cd ~/ros2/src \ 
   && vcs import < hippo_full/hippo_full.repos

Note that the repositories will be cloned using :file:`https`. If you need to push changes, you will need to manually switch to :file:`ssh`.
