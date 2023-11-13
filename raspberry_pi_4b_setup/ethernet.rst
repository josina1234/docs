Ethernet
########

.. attention::

   Sometimes the ethernet interface of the Raspberry Pi is lagging.
   We have not ultimately identified the cause, but the following steps might help with that.

Most likely the Gigabit connection via our manually crimped RJ45 connectors is not stable.
Hence, the connection speed (100 Mbit/s vs Gbit) is repetitively negotiated which results in an unstable connection.

We try to avoid this by manually setting the advertised link mode to 100 MBit/s.

.. code-block:: sh
   :linenos:
   :caption: /etc/network/if-pre-up.d/eththool

   $ETHTOOL --change eth0 advertise 0x008

