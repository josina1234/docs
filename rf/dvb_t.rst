DVB-T Stick
###########

NooElec R820T2 SDR & DVB-T NESDR Mini 2

Firmware Installation
=====================

.. code-block:: sh

   git clone https://gitea.osmocom.org/sdr/rtl-sdr.git
   cd rtl-sdr
   mkdir build
   cd build
   cmake ../ -DINSTALL_UDEV_RULES=ON -DDETACH_KERNEL_DRIVER=ON
   make
   sudo make install
   sudo ldconfig



Blacklisting the :code:`dvb_usb_rtl28xxu` module
------------------------------------------------

Add the following to :file:`etc/modprobe.d/blacklist.conf` (will need root access)

.. code-block:: sh

   blacklist dvb_usb_rtl28xxu
   blacklist rtl2832
   blacklist rtl2830