## Lab 5
For this lab we will make 2 terminals communicate with each other.
# mosquitto (Raspberry PI)
first, we install mosquitto onto the device through the terminal by running
```
pi@raspberrypi:~ $ sudo apt update
Hit:1 http://deb.debian.org/debian bullseye InRelease
Hit:2 http://deb.debian.org/debian bullseye-updates InRelease
Hit:3 http://security.debian.org/debian-security bullseye-security InRelease
Hit:4 http://archive.raspberrypi.org/debian bullseye InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
25 packages can be upgraded. Run 'apt list --upgradable' to see them.
pi@raspberrypi:~ $ sudo apt install mosquitto mosquitto-clients
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libfuse2 raspinfo
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libcjson1 libdlt2 libev4 libmosquitto1 libwebsockets16
Suggested packages:
  apparmor
The following NEW packages will be installed:
  libcjson1 libdlt2 libev4 libmosquitto1 libwebsockets16 mosquitto mosquitto-clients
0 upgraded, 7 newly installed, 0 to remove and 25 not upgraded.
Need to get 748 kB of archives.
After this operation, 1,943 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bullseye/main arm64 libcjson1 arm64 1.7.14-1 [22.5 kB]
Get:2 http://deb.debian.org/debian bullseye/main arm64 libdlt2 arm64 2.18.6-1+deb11u1 [50.9 kB]
Get:3 http://deb.debian.org/debian bullseye/main arm64 libev4 arm64 1:4.33-1 [41.3 kB]
Get:4 http://deb.debian.org/debian bullseye/main arm64 libmosquitto1 arm64 2.0.11-1 [89.4 kB]
Get:5 http://deb.debian.org/debian bullseye/main arm64 libwebsockets16 arm64 4.0.20-2 [173 kB]
Get:6 http://deb.debian.org/debian bullseye/main arm64 mosquitto arm64 2.0.11-1 [258 kB]
Get:7 http://deb.debian.org/debian bullseye/main arm64 mosquitto-clients arm64 2.0.11-1 [112 kB]
Fetched 748 kB in 5s (137 kB/s)
Selecting previously unselected package libcjson1:arm64.
(Reading database ... 92854 files and directories currently installed.)
Preparing to unpack .../0-libcjson1_1.7.14-1_arm64.deb ...
Unpacking libcjson1:arm64 (1.7.14-1) ...
Selecting previously unselected package libdlt2:arm64.
Preparing to unpack .../1-libdlt2_2.18.6-1+deb11u1_arm64.deb ...
Unpacking libdlt2:arm64 (2.18.6-1+deb11u1) ...
Selecting previously unselected package libev4:arm64.
Preparing to unpack .../2-libev4_1%3a4.33-1_arm64.deb ...
Unpacking libev4:arm64 (1:4.33-1) ...
Selecting previously unselected package libmosquitto1:arm64.
Preparing to unpack .../3-libmosquitto1_2.0.11-1_arm64.deb ...
Unpacking libmosquitto1:arm64 (2.0.11-1) ...
Selecting previously unselected package libwebsockets16:arm64.
Preparing to unpack .../4-libwebsockets16_4.0.20-2_arm64.deb ...
Unpacking libwebsockets16:arm64 (4.0.20-2) ...
Selecting previously unselected package mosquitto.
Preparing to unpack .../5-mosquitto_2.0.11-1_arm64.deb ...
Unpacking mosquitto (2.0.11-1) ...
Selecting previously unselected package mosquitto-clients.
Preparing to unpack .../6-mosquitto-clients_2.0.11-1_arm64.deb ...
Unpacking mosquitto-clients (2.0.11-1) ...
Setting up libmosquitto1:arm64 (2.0.11-1) ...
Setting up libev4:arm64 (1:4.33-1) ...
Setting up libcjson1:arm64 (1.7.14-1) ...
Setting up mosquitto-clients (2.0.11-1) ...
Setting up libdlt2:arm64 (2.18.6-1+deb11u1) ...
Setting up libwebsockets16:arm64 (4.0.20-2) ...
Setting up mosquitto (2.0.11-1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/mosquitto.service → /lib/systemd/system/mosquitto.service.
Processing triggers for man-db (2.9.4-2) ...
Processing triggers for libc-bin (2.31-13+rpt2+rpi1+deb11u5) ...
pi@raspberrypi:~ $ mosquitto_sub -h localhost -v -t "\$SYS/#"
$SYS/broker/version mosquitto version 2.0.11
$SYS/broker/uptime 165 seconds
$SYS/broker/uptime 176 seconds
$SYS/broker/clients/total 1
$SYS/broker/clients/maximum 1
$SYS/broker/clients/active 1
$SYS/broker/clients/connected 1
$SYS/broker/load/messages/received/1min 1.83
$SYS/broker/load/messages/sent/1min 8.22
$SYS/broker/load/publish/sent/1min 6.40
$SYS/broker/load/bytes/received/1min 24.67
$SYS/broker/load/bytes/sent/1min 227.51
$SYS/broker/load/sockets/1min 0.91
$SYS/broker/load/connections/1min 0.91
$SYS/broker/load/messages/received/5min 0.39
$SYS/broker/load/messages/sent/5min 1.77
$SYS/broker/load/publish/sent/5min 1.37
$SYS/broker/load/bytes/received/5min 5.30
$SYS/broker/load/bytes/sent/5min 48.90
$SYS/broker/load/sockets/5min 0.20
$SYS/broker/load/connections/5min 0.20
$SYS/broker/load/messages/received/15min 0.13
$SYS/broker/load/messages/sent/15min 0.60
$SYS/broker/load/publish/sent/15min 0.46
$SYS/broker/load/bytes/received/15min 1.79
$SYS/broker/load/bytes/sent/15min 16.50
$SYS/broker/load/sockets/15min 0.07
$SYS/broker/load/connections/15min 0.07
$SYS/broker/messages/stored 27
$SYS/broker/store/messages/count 27
$SYS/broker/store/messages/bytes 132
$SYS/broker/subscriptions/count 1
$SYS/broker/retained messages/count 31
$SYS/broker/heap/current 42264
$SYS/broker/heap/maximum 44072
$SYS/broker/messages/received 2
$SYS/broker/messages/sent 38
$SYS/broker/publish/messages/sent 37
$SYS/broker/bytes/received 27
$SYS/broker/bytes/sent 1532
$SYS/broker/publish/bytes/sent 170
```
this downloads and tests to see if mosquitto has been properly installed.
We next run the following commands
```
pi@raspberrypi:~ $ service mosquitto status
● mosquitto.service - Mosquitto MQTT Broker
     Loaded: loaded (/lib/systemd/system/mosquitto.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2023-04-08 14:42:14 EDT; 3min 57s ago
       Docs: man:mosquitto.conf(5)
             man:mosquitto(8)
    Process: 85923 ExecStartPre=/bin/mkdir -m 740 -p /var/log/mosquitto (code=exited, status=0/SUCCESS)
    Process: 85924 ExecStartPre=/bin/chown mosquitto /var/log/mosquitto (code=exited, status=0/SUCCESS)
    Process: 85925 ExecStartPre=/bin/mkdir -m 740 -p /run/mosquitto (code=exited, status=0/SUCCESS)
    Process: 85926 ExecStartPre=/bin/chown mosquitto /run/mosquitto (code=exited, status=0/SUCCESS)
   Main PID: 85927 (mosquitto)
      Tasks: 1 (limit: 3933)
        CPU: 112ms
     CGroup: /system.slice/mosquitto.service
             └─85927 /usr/sbin/mosquitto -c /etc/mosquitto/mosquitto.conf

Apr 08 14:42:14 raspberrypi systemd[1]: Starting Mosquitto MQTT Broker...
Apr 08 14:42:14 raspberrypi systemd[1]: Started Mosquitto MQTT Broker.
pi@raspberrypi:~ $ setstat -tln
-bash: setstat: command not found
pi@raspberrypi:~ $ netstat -tln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:5900            0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:1883          0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN
tcp6       0      0 :::5900                 :::*                    LISTEN
tcp6       0      0 ::1:631                 :::*                    LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
tcp6       0      0 ::1:1883                :::*                    LISTEN
```
This tells us what mosquitto is listening to
Now we begin running code on two seperate terminals.
T1
```
pi@raspberrypi:~ $ mosquitto_sub -h localhost -v -t test/topic &
[1] 86094
pi@raspberrypi:~ $ test/topic Hello
```
T2
```
pi@raspberrypi:~ $ mosquitto_pub -h localhost -t test/topic -m "Hello"
```
We can see here that by running the code on the second terminal, it prints Hello on the first terminal instead.
# Paho
Now we download paho and begin to use it.
```
sudo pip3 install -U paho-mqtt
Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple
Collecting paho-mqtt
  Downloading https://www.piwheels.org/simple/paho-mqtt/paho_mqtt-1.6.1-py3-none-any.whl (75 kB)
     |████████████████████████████████| 75 kB 326 kB/s
Installing collected packages: paho-mqtt
Successfully installed paho-mqtt-1.6.1
pi@raspberrypi:~ $ git clone https://github.com/eclipse/paho.mqtt.python.git
Cloning into 'paho.mqtt.python'...
remote: Enumerating objects: 4531, done.
remote: Counting objects: 100% (981/981), done.
remote: Compressing objects: 100% (109/109), done.
remote: Total 4531 (delta 910), reused 872 (delta 872), pack-reused 3550
Receiving objects: 100% (4531/4531), 1.21 MiB | 4.84 MiB/s, done.
Resolving deltas: 100% (2483/2483), done.
pi@raspberrypi:~ $ cd ~/iot/lesson5
pi@raspberrypi:~/iot/lesson5 $ python3 client.py
Connected with result code 0
$SYS/broker/publish/bytes/received 864983917548
$SYS/broker/publish/bytes/sent 22628041754070
$SYS/broker/publish/messages/dropped 2108443610279
$SYS/broker/publish/messages/received 6557227070
$SYS/broker/publish/messages/sent 167891773582
$SYS/broker/publish/messages/dropped 2108444759058
$SYS/broker/publish/messages/received 6557269632
$SYS/broker/publish/messages/sent 167892547683
$SYS/broker/publish/bytes/received 864990727360
$SYS/broker/publish/bytes/sent 22628207630044
$SYS/broker/publish/messages/dropped 2108446262970
$SYS/broker/publish/messages/received 6557321221
$SYS/broker/publish/messages/sent 167893350962
$SYS/broker/publish/bytes/received 864998392892
$SYS/broker/publish/bytes/sent 22628343699098
$SYS/broker/publish/messages/dropped 2108449357649
$SYS/broker/publish/messages/received 6557410999
$SYS/broker/publish/messages/sent 167894149861
$SYS/broker/publish/bytes/received 865009769872
$SYS/broker/publish/bytes/sent 22628421911412
```
# pub/subcpu.py
Now we connect the two terminals to display various information, including the cpu usage
T1
```
pi@raspberrypi:~/iot/lesson5 $ python3 sub.py
Connected with result code 0
paho/test Hello
^CTraceback (most recent call last):
  File "/home/pi/iot/lesson5/sub.py", line 11, in <module>
    client.loop_forever()
  File "/usr/local/lib/python3.9/dist-packages/paho/mqtt/client.py", line 1756, in loop_forever
    rc = self._loop(timeout)
  File "/usr/local/lib/python3.9/dist-packages/paho/mqtt/client.py", line 1150, in _loop
    socklist = select.select(rlist, wlist, [], timeout)
KeyboardInterrupt

pi@raspberrypi:~/iot/lesson5 $ python3 sub-multiple.py
Connected with result code 0
paho/test/multiple multiple 1
paho/test/multiple multiple 2
^CTraceback (most recent call last):
  File "/home/pi/iot/lesson5/sub-multiple.py", line 11, in <module>
    client.loop_forever()
  File "/usr/local/lib/python3.9/dist-packages/paho/mqtt/client.py", line 1756, in loop_forever
    rc = self._loop(timeout)
  File "/usr/local/lib/python3.9/dist-packages/paho/mqtt/client.py", line 1150, in _loop
    socklist = select.select(rlist, wlist, [], timeout)
KeyboardInterrupt

pi@raspberrypi:~/iot/lesson5 $ python3 subcpu.py
Connected with result code 0
MyCPU 2023-04-08 14:53:28
MyCPU CPU Usage:   8.6 %
MyCPU 2023-04-08 14:53:38
MyCPU CPU Usage:   2.2 %
MyCPU 2023-04-08 14:53:48
MyCPU CPU Usage:   2.0 %
MyCPU 2023-04-08 14:53:58
MyCPU CPU Usage:   2.2 %
MyCPU 2023-04-08 14:54:08
MyCPU CPU Usage:   3.6 %
MyCPU 2023-04-08 14:54:18
MyCPU CPU Usage:   0.9 %
MyCPU 2023-04-08 14:54:28
MyCPU CPU Usage:   1.8 %
MyCPU 2023-04-08 14:54:38
MyCPU CPU Usage:   2.0 %
MyCPU 2023-04-08 14:54:48
MyCPU CPU Usage:   2.1 %
MyCPU 2023-04-08 14:54:58
MyCPU CPU Usage:   2.1 %
MyCPU 2023-04-08 14:55:08
MyCPU CPU Usage:   2.0 %
MyCPU 2023-04-08 14:55:18
MyCPU CPU Usage:   1.7 %
MyCPU 2023-04-08 14:55:28
MyCPU CPU Usage:   0.3 %
```
T2
```
pi@raspberrypi:~ $ python3 pub.py
python3: can't open file '/home/pi/pub.py': [Errno 2] No such file or directory
pi@raspberrypi:~ $ cd ~iot/lesson5
-bash: cd: ~iot/lesson5: No such file or directory
pi@raspberrypi:~ $ cd iot/lesson5/
pi@raspberrypi:~/iot/lesson5 $ python3 pub.py
pi@raspberrypi:~/iot/lesson5 $ ^C
pi@raspberrypi:~/iot/lesson5 $ python3 pub-multiple.py
pi@raspberrypi:~/iot/lesson5 $ ^C
pi@raspberrypi:~/iot/lesson5 $ python3 pubcpu.py
2023-04-08 14:53:28
CPU Usage:   8.6 %

2023-04-08 14:53:38
CPU Usage:   2.2 %
2023-04-08 14:53:48
CPU Usage:   2.0 %
2023-04-08 14:53:58
CPU Usage:   2.2 %
2023-04-08 14:54:08
CPU Usage:   3.6 %
2023-04-08 14:54:18
CPU Usage:   0.9 %
2023-04-08 14:54:28
CPU Usage:   1.8 %
2023-04-08 14:54:38
CPU Usage:   2.0 %
2023-04-08 14:54:48
CPU Usage:   2.1 %
2023-04-08 14:54:58
CPU Usage:   2.1 %
2023-04-08 14:55:08
CPU Usage:   2.0 %
2023-04-08 14:55:18
CPU Usage:   1.7 %
2023-04-08 14:55:28
CPU Usage:   0.3 %
2023-04-08 14:55:38
CPU Usage:   2.0 %
2023-04-08 14:55:48
CPU Usage:   2.0 %
```
