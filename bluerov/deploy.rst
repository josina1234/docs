Deployment
==========

We have 2 BlueROV2s: 

- The old BlueROV. We use it mainly for the SEMS/FAV class. It's vehicle name is :code:`bluerov01`.
- The newer BlueROV. This one is used for the UVMS setup and has the Alpha arm mounted to it. It's vehicle name is :code:`bluerov02`.

.. todo:: 

   This section is still work in progress.


SSH Access
**********

For convenience, you can copy your ssh-key to the BlueROV to enable passwordless login and create an entry in your :file:`~/.ssh/config` for the BlueROV similiar to:

.. tabs::
   .. code-tab:: sh Pi in upper tube

      Host klopsi-main-01
          User pi
          Hostname klopsi-main-01.local
          IdentitiyFile "~/.ssh/id_ed25519"
   
   .. code-tab:: sh Pi in lower tube

      Host klopsi-buddy-01
          User pi
          Hostname klopsi-buddy-01.local
          IdentitiyFile "~/.ssh/id_ed25519"

.. note::

   Replace the path for the identity file with the name of your key.

This entry allows you to use :code:`ssh klopsi-main-01` instead of :code:`ssh pi@klopsi-main-01.local`.

Start the usual Setup
*********************

Automated start of nodes (bluerov01)
#####################################

For the :code:`bluerov01`, we currently use an automated setup, where all necessary nodes are started at booting.

Make sure you have read and understood :ref:`deployment_concept`.


Manual start of nodes (bluerov02)
##################################


.. tabs::

   .. code-tab:: console klopsi-main-01
      
      $ ros2 launch hardware bluerov.launch.py vehicle_name:=bluerov01
   
   .. code-tab:: console klopsi-buddy-01
      
      $ ros2 launch hardware bluerov_buddy.launch.py vehicle_name:=bluerov01

