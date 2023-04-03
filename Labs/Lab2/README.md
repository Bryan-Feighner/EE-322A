# Lab 2
For this lab, we run some simple code through the command prompt to see their uses.
## hostname
Running this command returns the following: 
```
C:\Users\bnfle>hostname
DESKTOP-SG1PIE2
```
This returns the name of the computer or device
## env
Running this command returns the following:
```
C:\Users\bnfle>env
!::=::\
!C:=C:\Users\bnfle
!D:=D:\
!E:=E:\
!ExitCode=00000000
ALLUSERSPROFILE=C:\ProgramData
APPDATA=C:\Users\bnfle\AppData\Roaming
asl.log=Destination=file
COMMONPROGRAMFILES=C:\Program Files\Common Files
CommonProgramFiles(x86)=C:\Program Files (x86)\Common Files
CommonProgramW6432=C:\Program Files\Common Files
COMPUTERNAME=DESKTOP-SG1PIE2
COMSPEC=C:\Windows\system32\cmd.exe
DriverData=C:\Windows\System32\Drivers\DriverData
FPS_BROWSER_APP_PROFILE_STRING=Internet Explorer
FPS_BROWSER_USER_PROFILE_STRING=Default
ghdl=C:\eda\ghdl
gtkwave=C:\eda\gtkwave
HOMEDRIVE=C:
HOMEPATH=\Users\bnfle
LOCALAPPDATA=C:\Users\bnfle\AppData\Local
LOGONSERVER=\\DESKTOP-SG1PIE2
NUMBER_OF_PROCESSORS=16
OneDrive=C:\Users\bnfle\OneDrive
OS=Windows_NT
PATH=/c/Program Files (x86)/Common Files/Oracle/Java/javapath:/c/Windows/system32:/c/Windows:/c/Windows/System32/Wbem:/c/Windows/System32/WindowsPowerShell/v1.0:/c/Windows/System32/OpenSSH:/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/c/Program Files/NVIDIA Corporation/NVIDIA NvDLISR:/c/Program Files/MATLAB/R2021b/bin:/c/Program Files/Git/cmd:/c/Program Files/nodejs:/c/Users/bnfle/AppData/Local/Microsoft/WindowsApps:/mingw64/bin:/usr/bin:/home/bnfle/Microsoft VS Code/bin:/c/Users/bnfle/AppData/Roaming/npm
PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
PROCESSOR_ARCHITECTURE=AMD64
PROCESSOR_IDENTIFIER=Intel64 Family 6 Model 165 Stepping 5, GenuineIntel
PROCESSOR_LEVEL=6
PROCESSOR_REVISION=a505
ProgramData=C:\ProgramData
PROGRAMFILES=C:\Program Files
ProgramFiles(x86)=C:\Program Files (x86)
ProgramW6432=C:\Program Files
PROMPT=$P$G
PSModulePath=C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules;C:\Program Files\Intel\Wired Networking\
PUBLIC=C:\Users\Public
SESSIONNAME=Console
SYSTEMDRIVE=C:
SYSTEMROOT=C:\Windows
TEMP=/c/Users/bnfle/AppData/Local/Temp
TMP=/c/Users/bnfle/AppData/Local/Temp
USERDOMAIN=DESKTOP-SG1PIE2
USERDOMAIN_ROAMINGPROFILE=DESKTOP-SG1PIE2
USERNAME=bnfle
USERPROFILE=C:\Users\bnfle
WINDIR=C:\Windows
TERM=xterm-256color
HOME=/home/bnfle
```
Env displays all of the systems environment variables.
## ps
Running this command returns the following:
```
C:\Users\bnfle>ps
      PID    PPID    PGID     WINPID   TTY         UID    STIME COMMAND
      685       1     685      26908  cons0     197609 20:03:37 /usr/bin/ps
```
This command returns all processes currently running.
## pwd
Running this command returns the following:
```
C:\Users\bnfle>pwd
/c/Users/bnfle
```
This command simply returns the path to your current directory
## git clone
Since I had already cloned the repository in before, I utilized the `git pull` command to return to following:
```
\Users\bnfle\iot>git pull
remote: Enumerating objects: 383, done.
remote: Counting objects: 100% (383/383), done.
remote: Compressing objects: 100% (201/201), done.
remote: Total 383 (delta 200), reused 225 (delta 121), pack-reused 0
Receiving objects: 100% (383/383), 123.68 KiB | 11.24 MiB/s, done.
Resolving deltas: 100% (200/200), completed with 4 local objects.
From https://github.com/kevinwlu/iot
   60d4a20e..22e167e9  master     -> origin/master
Updating 60d4a20e..22e167e9
Fast-forward
 README.md                                      | 11 +++++++++
 cases/README.md                                | 33 +++++++++++++++++++++++---
 economics/README.md                            |  6 ++++-
 health/README.md                               | 32 +++++++++++++++++++++++++
 lesson1/README.md                              | 16 ++++++++++---
 lesson6/README.md                              | 20 +++++++++-------
 lesson6/{xiao/fft => ds18b20}/thermistor-1.ino |  0
 lesson6/{xiao/fft => ds18b20}/thermistor.ino   |  0
 lesson6/xiao/fft/README.md                     | 12 +++-------
 lesson8/README.md                              |  7 ++++--
 lesson9/README.md                              | 15 ++++++++++++
 make/README.md                                 | 11 +++++++++
 tools/README.md                                | 22 ++++++++++++++++-
 13 files changed, 158 insertions(+), 27 deletions(-)
 create mode 100644 health/README.md
 rename lesson6/{xiao/fft => ds18b20}/thermistor-1.ino (100%)
 rename lesson6/{xiao/fft => ds18b20}/thermistor.ino (100%)
 ```
 `git clone` is used to download a directory from the GitHub repository to your local storage. `git pull` is used when the directory has already been cloned, and updates all files to match the currently uploaded files on GitHub.
 ## cd
Running this command returns the following:
```
C:\Users\bnfle>cd iot
```
This command is used to traverse between directories. Depending on the argument it can be used to travel forward or backwards.
## ls
Running this command returns the following:
```
C:\Users\bnfle\iot>ls
README.md  cases      health  lesson1   lesson2  lesson4  lesson6  lesson8  make      special_problems  tools
apps       economics  hype    lesson10  lesson3  lesson5  lesson7  lesson9  projects  standards
```
This command returns all files in the current directory
## df
Running this command returns the following:
```
C:\Users\bnfle\iot>df
Filesystem     1K-blocks      Used Available Use% Mounted on
C:/msys64      243568636 215342468  28226168  89% /
D:             976629756 807056764 169572992  83% /d
E:             500089852 199358032 300731820  40% /e
```
This command returns the drive utilization, size, and name of all drives in the system.
## mkdir
Running this command returns the following:
```
C:\Users\bnfle\iot>mkdir demo
```
This command creates a new directory and names it
## nano
Running this command returns the following:
```
C:\Users\bnfle\iot\demo>nano file
```
This command creates a text file and allows edits to be made using nano
## cat
Running this command returns the following:
```
C:\Users\bnfle\iot\demo>cat file
hello world!
```
This command returns the text contained in a file
## cp
Running this command returns the following:
```
C:\Users\bnfle\iot\demo>cp file file1
```
This command copies the contents of one file to another, cp [old file] [new file]
## mv
Running this command returns the following:
```
C:\Users\bnfle\iot\demo>mv file file2
```
This command moves or renames files inside the current directory
## rm
Running this command returns the following:
```
C:\Users\bnfle\iot\demo>rm file2
```
This command removes and deletes a file
## clear
Running this command clears the command prompt as if it was just opened
## man
This command is a Linux command to display the user manual of any command
## uname -a
Running this command returns the following:
```
C:\Users\bnfle>uname -a
MSYS_NT-10.0-19045 DESKTOP-SG1PIE2 3.3.3-341.x86_64 2022-01-18 13:00 UTC x86_64 Msys
```
This command prints all system information
## ifconfig
Running this command returns the following:
```
pi@raspberrypi:~ $ ifconfig
eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether e4:5f:01:79:5e:28  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 22  bytes 2436 (2.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 22  bytes 2436 (2.3 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.165  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 2600:4041:41e6:a100:60fd:9ebb:b254:a7a1  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::8082:2e8:2b1c:8bc9  prefixlen 64  scopeid 0x20<link>
        ether e4:5f:01:79:5e:29  txqueuelen 1000  (Ethernet)
        RX packets 113  bytes 20432 (19.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 109  bytes 13873 (13.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
Being a Linux command, I SSHed into my raspberry pi and ran the command. This command returns all network interfaces you currently have configured.
## ping localhost
Running this command returns the following:
```
C:\Users\bnfle>ping localhost

Pinging DESKTOP-SG1PIE2 [::1] with 32 bytes of data:
Reply from ::1: time<1ms
Reply from ::1: time<1ms
Reply from ::1: time<1ms
Reply from ::1: time<1ms

Ping statistics for ::1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
This command sends a message to a server and times the response time.
## netstat
Running this command returns the following:
```
C:\Users\bnfle>netstat

Active Connections

  Proto  Local Address          Foreign Address        State
  TCP    127.0.0.1:5354         DESKTOP-SG1PIE2:49675  ESTABLISHED
  TCP    127.0.0.1:5354         DESKTOP-SG1PIE2:49676  ESTABLISHED
  TCP    127.0.0.1:9010         DESKTOP-SG1PIE2:60009  ESTABLISHED
  TCP    127.0.0.1:9010         DESKTOP-SG1PIE2:60017  ESTABLISHED
  TCP    127.0.0.1:9100         DESKTOP-SG1PIE2:60001  ESTABLISHED
  TCP    127.0.0.1:45654        DESKTOP-SG1PIE2:60103  ESTABLISHED
  TCP    127.0.0.1:49673        DESKTOP-SG1PIE2:59979  ESTABLISHED
  TCP    127.0.0.1:49674        DESKTOP-SG1PIE2:59951  ESTABLISHED
  TCP    127.0.0.1:49675        DESKTOP-SG1PIE2:5354   ESTABLISHED
  TCP    127.0.0.1:49676        DESKTOP-SG1PIE2:5354   ESTABLISHED
  TCP    127.0.0.1:59800        DESKTOP-SG1PIE2:65001  ESTABLISHED
  TCP    127.0.0.1:59903        DESKTOP-SG1PIE2:59920  ESTABLISHED
  TCP    127.0.0.1:59920        DESKTOP-SG1PIE2:59903  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:59930  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:59932  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:59946  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:59949  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:59950  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:60099  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:60101  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:60348  ESTABLISHED
  TCP    127.0.0.1:59924        DESKTOP-SG1PIE2:60986  ESTABLISHED
  TCP    127.0.0.1:59929        DESKTOP-SG1PIE2:60098  ESTABLISHED
  TCP    127.0.0.1:59929        DESKTOP-SG1PIE2:60100  ESTABLISHED
  TCP    127.0.0.1:59930        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:59932        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:59946        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:59949        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:59950        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:59951        DESKTOP-SG1PIE2:49674  ESTABLISHED
  TCP    127.0.0.1:59979        DESKTOP-SG1PIE2:49673  ESTABLISHED
  TCP    127.0.0.1:60001        DESKTOP-SG1PIE2:9100   ESTABLISHED
  TCP    127.0.0.1:60009        DESKTOP-SG1PIE2:9010   ESTABLISHED
  TCP    127.0.0.1:60017        DESKTOP-SG1PIE2:9010   ESTABLISHED
  TCP    127.0.0.1:60098        DESKTOP-SG1PIE2:59929  ESTABLISHED
  TCP    127.0.0.1:60099        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:60100        DESKTOP-SG1PIE2:59929  ESTABLISHED
  TCP    127.0.0.1:60101        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:60103        DESKTOP-SG1PIE2:45654  ESTABLISHED
  TCP    127.0.0.1:60104        DESKTOP-SG1PIE2:60236  ESTABLISHED
  TCP    127.0.0.1:60105        DESKTOP-SG1PIE2:65066  ESTABLISHED
  TCP    127.0.0.1:60105        DESKTOP-SG1PIE2:65075  ESTABLISHED
  TCP    127.0.0.1:60105        DESKTOP-SG1PIE2:65076  ESTABLISHED
  TCP    127.0.0.1:60105        DESKTOP-SG1PIE2:65077  ESTABLISHED
  TCP    127.0.0.1:60105        DESKTOP-SG1PIE2:65082  ESTABLISHED
  TCP    127.0.0.1:60236        DESKTOP-SG1PIE2:60104  ESTABLISHED
  TCP    127.0.0.1:60348        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:60986        DESKTOP-SG1PIE2:59924  ESTABLISHED
  TCP    127.0.0.1:65001        DESKTOP-SG1PIE2:59800  ESTABLISHED
  TCP    127.0.0.1:65066        DESKTOP-SG1PIE2:60105  ESTABLISHED
  TCP    127.0.0.1:65075        DESKTOP-SG1PIE2:60105  ESTABLISHED
  TCP    127.0.0.1:65076        DESKTOP-SG1PIE2:60105  ESTABLISHED
  TCP    127.0.0.1:65077        DESKTOP-SG1PIE2:60105  ESTABLISHED
  TCP    127.0.0.1:65082        DESKTOP-SG1PIE2:60105  ESTABLISHED
  TCP    192.168.1.162:50123    53:https               ESTABLISHED
  TCP    192.168.1.162:50131    229:https              ESTABLISHED
  TCP    192.168.1.162:50203    lga25s71-in-f14:https  ESTABLISHED
  TCP    192.168.1.162:50525    170:https              ESTABLISHED
  TCP    192.168.1.162:50654    lga25s74-in-f14:https  TIME_WAIT
  TCP    192.168.1.162:50655    lga25s74-in-f14:https  TIME_WAIT
  TCP    192.168.1.162:50679    lga34s40-in-f14:https  ESTABLISHED
  TCP    192.168.1.162:50718    21:https               TIME_WAIT
  TCP    192.168.1.162:50750    146:https              TIME_WAIT
  TCP    192.168.1.162:50778    82:https               TIME_WAIT
  TCP    192.168.1.162:50784    236:https              TIME_WAIT
  TCP    192.168.1.162:50933    62:https               TIME_WAIT
  TCP    192.168.1.162:50941    218:https              TIME_WAIT
  TCP    192.168.1.162:50963    1:https                TIME_WAIT
  TCP    192.168.1.162:51138    ec2-52-55-204-172:https  ESTABLISHED
  TCP    192.168.1.162:51139    ec2-52-73-225-253:https  ESTABLISHED
  TCP    192.168.1.162:51215    ec2-44-194-115-253:https  CLOSE_WAIT
  TCP    192.168.1.162:51221    cdn-185-199-108-133:https  ESTABLISHED
  TCP    192.168.1.162:51226    lga34s34-in-f10:https  ESTABLISHED
  TCP    192.168.1.162:51227    ec2-3-222-11-75:https  CLOSE_WAIT
  TCP    192.168.1.162:51245    lga34s34-in-f10:https  ESTABLISHED
  TCP    192.168.1.162:51258    lb-140-82-113-26-iad:https  ESTABLISHED
  TCP    192.168.1.162:51268    lga34s37-in-f3:https   ESTABLISHED
  TCP    192.168.1.162:51287    lga25s70-in-f3:https   TIME_WAIT
  TCP    192.168.1.162:51288    lga34s37-in-f3:https   TIME_WAIT
  TCP    192.168.1.162:51291    lga25s74-in-f10:https  ESTABLISHED
  TCP    192.168.1.162:51294    lga25s74-in-f2:https   ESTABLISHED
  TCP    192.168.1.162:51310    CR1000A:domain         TIME_WAIT
  TCP    192.168.1.162:51311    CR1000A:domain         TIME_WAIT
  TCP    192.168.1.162:51313    47:https               TIME_WAIT
  TCP    192.168.1.162:51316    CR1000A:domain         TIME_WAIT
  TCP    192.168.1.162:51317    CR1000A:domain         TIME_WAIT
  TCP    192.168.1.162:51323    13.107.21.200:https    ESTABLISHED
  TCP    192.168.1.162:51324    40.97.188.242:https    ESTABLISHED
  TCP    192.168.1.162:51325    bingforbusiness:https  ESTABLISHED
  TCP    192.168.1.162:51326    40.97.188.242:https    ESTABLISHED
  TCP    192.168.1.162:51327    20.42.72.131:https     ESTABLISHED
  TCP    192.168.1.162:51330    13.107.253.254:https   ESTABLISHED
  TCP    192.168.1.162:51331    72.21.81.200:https     ESTABLISHED
  TCP    192.168.1.162:51332    13.107.136.254:https   ESTABLISHED
  TCP    192.168.1.162:51333    204.79.197.222:https   ESTABLISHED
  TCP    192.168.1.162:51334    20.69.137.228:https    ESTABLISHED
  TCP    192.168.1.162:51339    CR1000A:domain         TIME_WAIT
  TCP    192.168.1.162:51340    CR1000A:domain         TIME_WAIT
  TCP    192.168.1.162:51341    lga34s32-in-f2:https   ESTABLISHED
  TCP    192.168.1.162:51350    172.67.194.181:https   ESTABLISHED
  TCP    192.168.1.162:51359    25:https               ESTABLISHED
  TCP    192.168.1.162:51360    47:https               TIME_WAIT
  TCP    192.168.1.162:51362    a23-54-68-144:https    ESTABLISHED
  TCP    192.168.1.162:55728    ec2-3-227-116-81:https  ESTABLISHED
  TCP    192.168.1.162:55738    ec2-18-117-17-143:https  ESTABLISHED
  TCP    192.168.1.162:59766    52.159.127.243:https   ESTABLISHED
  TCP    192.168.1.162:60271    162-254-192-71:27031   ESTABLISHED
  TCP    192.168.1.162:60282    ec2-52-3-34-222:https  ESTABLISHED
  TCP    192.168.1.162:60304    ec2-52-23-149-130:https  ESTABLISHED
  TCP    192.168.1.162:60516    52.188.179.207:https   CLOSE_WAIT
  TCP    192.168.1.162:60715    162.159.130.234:https  ESTABLISHED
  TCP    192.168.1.162:62879    mc:https               ESTABLISHED
  TCP    192.168.1.162:63027    bl-in-f188:5228        ESTABLISHED
  TCP    192.168.1.162:64652    lga34s37-in-f4:https   ESTABLISHED
  TCP    192.168.1.162:64811    lga25s78-in-f14:https  ESTABLISHED
  TCP    192.168.1.162:64886    server-18-164-96-15:https  ESTABLISHED
  TCP    192.168.1.162:65398    lga25s81-in-f14:https  ESTABLISHED
```
This command returns all connections to the current device


