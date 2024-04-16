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

Install Python Wrapper

.. code-block:: sh

   pip install pyrtlsdr pyrtlsdrlib

Fix Access Error
================

If you try to use the DVB-T stick using pyrtlsdr, for example using

.. code-block:: sh

   ros2 launch sdr sdr.launch.py

You might get the following error message:

.. code-block:: sh

   [sdr_node.py-1]     raise LibUSBError(result, 'Could not open SDR (device index = %d)' % (device_index))
   [sdr_node.py-1] rtlsdr.rtlsdr.LibUSBError: <LIBUSB_ERROR_ACCESS (-3): Access denied (insufficient permissions)> "Could not open SDR (device index = 0)"
   [ERROR] [sdr_node.py-1]: process has died [pid 59289, exit code 1, cmd '/home/nathalie/ros2/install/sdr/lib/sdr/sdr_node.py --ros-args'].

Blacklisting the :code:`dvb_usb_rtl28xxu` module fixes this.
Add the following to :file:`etc/modprobe.d/blacklist.conf` (will need root access)

.. code-block:: sh

   blacklist dvb_usb_rtl28xxu
   blacklist rtl2832
   blacklist rtl2830

You will need to reboot.