Deploy Klopsi
=============

SSH Access
**********

For convenience, copy your ssh-key to the BlueROV to enable passwordless login and create an entry in your :file:`~/.ssh/config` for the BlueROV similiar to:

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

.. tabs::

   .. code-tab:: console klopsi-main-01
      
      $ ros2 launch hardware bluerov.launch.py vehicle_name:=bluerov01
   
   .. code-tab:: console klopsi-buddy-01
      
      $ ros2 launch hardware bluerov_buddy.launch.py vehicle_name:=bluerov01

