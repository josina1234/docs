Deployment
##########

Some ROS nodes are required to be running on the on-board Pis for all typical deployment setups and are started automatically.
This mainly refers to nodes representing hardware interfaces.
We use ``systemd`` for starting these nodes.

In many cases no manual interaction with the Raspberry Pis inside the vehicles is required. 

Where can I find the services that are starting the nodes?
==========================================================

The files are in :file:`~/.config/systemd/user/`

.. code-block:: console

   $ tree ~/.config/systemd/user
   
   ~/.config/systemd/user
   ├── default.target.wants
   │   └── ...
   ├── ros-camera.service
   ├── ros-camera-servo.service
   ├── ros-dvl.service
   ├── ros-esc.service
   ├── ros-spotlight.service
   ├── ros-startup-sequence.service
   ├── ros-wait-for-pigpiod.service
   ├── ros-xrce-agent.service
   ├── tmux-main.service
   └── tmux-monitoring.service

For all *enabled* services symlinks are created automatically inside :file:`default.target.wants/`.
The term *enabled* means that these services are started automatically.

How can I tell if my services are alright?
==========================================

The respective service's status can be checked via (in this example for ``ros-esc.service``)

.. code-block:: console

   $ systemctl --user status ros-esc.service
   ● ros-esc.service - ESC Commander
        Loaded: loaded (/home/pi/.config/systemd/user/ros-esc.service; enabled; vendor preset: enabled)
        Active: active (running) since Wed 2024-06-26 13:29:55 CEST; 1h 25min ago
      Main PID: 1017 (ros2)
         Tasks: 17 (limit: 9244)
        Memory: 45.2M
           CPU: 35.537s
        CGroup: /user.slice/user-1000.slice/user@1000.service/app.slice/ros-esc.service
                ├─1017 /usr/bin/python3 /opt/ros/iron/bin/ros2 launch esc teensy_esc.launch.py vehicle_name:=bluerov01 use_sim_time:=false
                └─2075 /home/pi/ros2/install/esc/lib/esc/teensy_commander_node --ros-args -r __node:=esc_commander -r __ns:=/bluerov01 --params-file /tmp/launch_params_7liomyxq --params-file /home/pi/ros2/install/esc/share/esc/config/teensy_config.yaml

   Jun 26 13:29:55 klopsi-main-01 systemd[1007]: Started ESC Commander.
   Jun 26 13:30:09 klopsi-main-01 zsh[1017]: [INFO] [launch]: All log files can be found below /home/pi/.ros/log/2024-06-26-13-30-09-507833-klopsi-main-01-1017
   Jun 26 13:30:09 klopsi-main-01 zsh[1017]: [INFO] [launch]: Default logging verbosity is set to INFO
   Jun 26 13:30:10 klopsi-main-01 zsh[1017]: [INFO] [teensy_commander_node-1]: process started with pid [2075]
   Jun 26 13:30:11 klopsi-main-01 zsh[1017]: [teensy_commander_node-1] [WARN] [1719401411.546179201] [bluerov01.esc_commander]: '/bluerov01/thruster_command' controls timed out.

We can observe that is is active and running.

For more convenience we have a ``tmux`` monitoring session.
We can switch to another session by :kbd:`ctrl-a s` and choose the desired session from the list.

.. note::

   The monitoring session is not meant for interaction but for reading the logs only.
   Neither enter anything nor hit :kbd:`ctrl-c` there.
   If you you failed to so do it is possible to restart the monitoring session with

   .. code-block:: console

      $ systemctl --user restart tmux-monitoring.service

.. note::

   Monitoring does not hurt nobody.
   It does no harm to the underlying processes that are monitored and restarting the monitoring session will cleanup the old one before starting the new session.
   
What about optional nodes that I want to run occasionally?
==========================================================

If there is already a service available we can start it without enabling it.
It will run until

* it finishes/crashes
* it is stopped via ``systemctl --user stop my-service.service``
* the Raspberry Pi is rebooted

If we require a certain setup for a certain period and do not want to start it manually each time, we can enable the service for this period for sure!

.. code-block:: console

   $ systemctl --user enable --now my-newly-enabled-service.service

We can disable it on some future date.
A problem for future-you!

.. code-block:: console

   $ systemctl --user disable --now my-newly-enabled-service.service

How do I write such a service?
==============================

The following example might be already self-explanatory.
Simply change ``Description`` and ``ExecStart``.

.. code-block:: systemd

   [Unit]
   Description=ESC Commander

   [Service]
   Type=simple
   ExecStart=/usr/bin/zsh -i -c 'ros2 launch esc teensy_esc.launch.py vehicle_name:="$VEHICLE_NAME" use_sim_time:=false'

   [Install]
   WantedBy=default.target
