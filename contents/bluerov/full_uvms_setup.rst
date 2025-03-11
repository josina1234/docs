Full UVMS Setup
###############


.. todo:: 

   Add all relevant infos. Appropriate structures + titles of sections TBD.


Installation Setup
==================

Ubuntu 24.04 + ROS2 Jazzy - see :ref:`ROS installation <ros-installation>`

What packages are needed?
-------------------------

We have most of our packages available as pre-built packages - see :ref:`pre-built-packages <pre-built-packages>`

The easiest is probably to install all, e.g. :file:`hippo_full`

.. code-block:: console 

   $ sudo apt install ros-${ROS_DISTRO}-hippo-full

Alternatively, install them separately. These should be necessary:

* hippo_common
* hippo_sim
* hippo_gz_plugins
* hippo_msgs
* hippo_control_msgs
* uvms_msgs
* alpha_msgs

Example: 

.. code-block:: console 

   $ sudo apt install ros-${ROS_DISTRO}-hippo-sim

The private repository :file:`alpha_arm` is not available via apt (for obvious reasons) and needs to be cloned and build from source.

The package :file:`uvms` also needs to be build from source.
