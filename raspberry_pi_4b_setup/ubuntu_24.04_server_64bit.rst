Ubuntu 24.04 Server 64bit
#########################


Modify Cloud-Init
=================

Modify :file:`user-data` on the :file:`system-boot` partition to your liking. An example configuration is provided below:

.. code-block:: yaml
   :caption: user-data

   #cloud-config
   
   hostname: hippo-main-04
   manage_etc_hosts: true
   locale: en_US.UTF-8
   timezone: Europe/Berlin
   
   users:
       - name: pi
         groups: sudo, dialout, video
         sudo: "ALL=(ALL) NOPASSWD:ALL"
         # false -> allow password login
         lock_passwd: false
         shell: /bin/bash
         plain_text_passwd: "hippocampus"
         ssh_authorized_keys:
         - ssh-ed25519    AAAAC3NzaC1lZDI1NTE5AAAAIF0xs6V9Lp2xzh/+hs+S919KpwAj9VHWO5NeHEuTYTpQ thies.lennart.alff@tuhh.de
   
   # allow password ssh login
   ssh_pwauth: true

   package_update: true
   package_upgrade: true
   packages:
       - avahi-daemon

   power_state: 
       mode: reboot
       delay: now
       condition: True

.. note:: Make sure to connect the Raspberry Pi with the Internet via Ethernet before booting the first time.

Boot Config
===========
On the :file:`system-boot` partition of the SD Card prepared for the Pi, edit :file:`config.txt`
and append the required lines for the specific setup.

.. note::

   This can also be done from the live system later on.
   The path to the file is then :file:`/boot/firmware/config.txt`

See `the documentation <https://github.com/raspberrypi/firmware/blob/master/boot/overlays/README>`__ for details on device tree overlays.

I2C
***

.. code-block:: ini

   dtoverlay=i2c4,pins_6_7

UART
****

.. code-block:: ini

   dtoverlay=uart2
   dtoverlay=uart3
   dtoverlay=uart4
   dtoverlay=uart5

Disable Interactive Upgrade
===========================

Edit :file:`needrestart.conf` so it contains the following entries (uncomment and modify as required)

.. code-block:: conf

   $nrconf{restart} = 'a';
   $nrconf{kernelhints} = 0

Create Workspace
================

.. code-block:: console

   $ mkdir -p ~/ros2/src \
   && mkdir -p ~/ros2_underlay/src

Concept
*******







   
   
