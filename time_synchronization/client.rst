Client
######

.. attention::
   We define the local server as only available time server.
   A wrong system time can cause many problems.
   So make sure, the local NTP server is available.

Setting Up Chrony
=================

.. code-block:: console

   $ sudo apt install chrony

.. note::
   Besides from the highlighted lines, the following configuration for ``chrony`` should be equivalent to the default configuration.

.. code-block:: sh
   :linenos:
   :caption: /etc/chrony/chrony.conf
   :emphasize-lines: 42

   # Welcome to the chrony configuration file. See chrony.conf(5) for more
   # information about usable directives.

   confdir /etc/chrony/conf.d

   # Use time sources from DHCP.
   sourcedir /run/chrony-dhcp

   # Use NTP sources found in /etc/chrony/sources.d.
   sourcedir /etc/chrony/sources.d

   # This directive specify the location of the file containing ID/key pairs for
   # NTP authentication.
   keyfile /etc/chrony/chrony.keys

   # This directive specify the file into which chronyd will store the rate
   # information.
   driftfile /var/lib/chrony/chrony.drift

   # Save NTS keys and cookies.
   ntsdumpdir /var/lib/chrony

   # Log files location.
   logdir /var/log/chrony

   # Stop bad estimates upsetting machine clock.
   maxupdateskew 100.0

   # This directive enables kernel synchronisation (every 11 minutes) of the
   # real-time clock. Note that it can’t be used along with the 'rtcfile' directive.
   rtcsync

   # Step the system clock instead of slewing it if the adjustment is larger than
   # one second, but only in the first three clock updates.
   makestep 1 3

   # Get TAI-UTC offset and leap seconds from the system tz database.
   # This directive must be commented out when using time sources serving
   # leap-smeared time.
   leapsectz right/UTC

   server 192.168.0.115 iburst

.. code-block:: console

   $ sudo systemctl restart chrony

Check Clock Offset
==================

.. code-block:: console
   :emphasize-lines: 5-7

   $ chronyc tracking
   Reference ID    : C0A80073 (192.168.0.115)
   Stratum         : 3
   Ref time (UTC)  : Wed Jan 24 11:53:55 2024
   System time     : 0.000000034 seconds fast of NTP time
   Last offset     : -0.000031117 seconds
   RMS offset      : 0.000035274 seconds
   Frequency       : 11.621 ppm fast
   Residual freq   : -0.023 ppm
   Skew            : 0.543 ppm
   Root delay      : 0.016247051 seconds
   Root dispersion : 0.000187333 seconds
   Update interval : 64.8 seconds
   Leap status     : Normal

