## Lab 9
# Install and run Pyang
Installing pyang is done by running the following commands (outputs indluded)
```
pi@raspberrypi:~ $ sudo apt install libxml2-dev libxslt1-dev
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libfuse2 raspinfo
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  icu-devtools libicu-dev
Suggested packages:
  icu-doc
The following NEW packages will be installed:
  icu-devtools libicu-dev libxml2-dev libxslt1-dev
0 upgraded, 4 newly installed, 0 to remove and 25 not upgraded.
Need to get 10.7 MB of archives.
After this operation, 51.3 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bullseye/main arm64 icu-devtools arm64 67.1-7 [189 kB]
Get:2 http://deb.debian.org/debian bullseye/main arm64 libicu-dev arm64 67.1-7 [9,468 kB]
Get:3 http://deb.debian.org/debian bullseye/main arm64 libxml2-dev arm64 2.9.10+dfsg-6.7+deb11u3 [753 kB]
Get:4 http://deb.debian.org/debian bullseye/main arm64 libxslt1-dev arm64 1.1.34-4+deb11u1 [329 kB]
Fetched 10.7 MB in 2s (6,091 kB/s)
Selecting previously unselected package icu-devtools.
(Reading database ... 92932 files and directories currently installed.)
Preparing to unpack .../icu-devtools_67.1-7_arm64.deb ...
Unpacking icu-devtools (67.1-7) ...
Selecting previously unselected package libicu-dev:arm64.
Preparing to unpack .../libicu-dev_67.1-7_arm64.deb ...
Unpacking libicu-dev:arm64 (67.1-7) ...
Selecting previously unselected package libxml2-dev:arm64.
Preparing to unpack .../libxml2-dev_2.9.10+dfsg-6.7+deb11u3_arm64.deb ...
Unpacking libxml2-dev:arm64 (2.9.10+dfsg-6.7+deb11u3) ...
Selecting previously unselected package libxslt1-dev:arm64.
Preparing to unpack .../libxslt1-dev_1.1.34-4+deb11u1_arm64.deb ...
Unpacking libxslt1-dev:arm64 (1.1.34-4+deb11u1) ...
Setting up icu-devtools (67.1-7) ...
Setting up libicu-dev:arm64 (67.1-7) ...
Setting up libxml2-dev:arm64 (2.9.10+dfsg-6.7+deb11u3) ...
Setting up libxslt1-dev:arm64 (1.1.34-4+deb11u1) ...
Processing triggers for man-db (2.9.4-2) ...
pi@raspberrypi:~ $ sudo pip3 install -U lxml pyang
Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple
Requirement already satisfied: lxml in /usr/lib/python3/dist-packages (4.6.3)
Collecting lxml
  Downloading lxml-4.9.2-cp39-cp39-manylinux_2_17_aarch64.manylinux2014_aarch64.manylinux_2_24_aarch64.whl (6.8 MB)
     |████████████████████████████████| 6.8 MB 54 kB/s
Collecting pyang
  Downloading https://www.piwheels.org/simple/pyang/pyang-2.5.3-py2.py3-none-any.whl (593 kB)
     |████████████████████████████████| 593 kB 400 kB/s
Installing collected packages: lxml, pyang
  Attempting uninstall: lxml
    Found existing installation: lxml 4.6.3
    Not uninstalling lxml at /usr/lib/python3/dist-packages, outside environment /usr
    Can't uninstall 'lxml'. No files were found to uninstall.
Successfully installed lxml-4.9.2 pyang-2.5.3
```
Next, we copy and go to the demo folder using `$ cp ~/iot/lesson9/intrusiondetection.yang ~/demo` and `$ cd ~/demo`
After this, we can verify that pyang is working by running the following commands (with outputs)
```
pi@raspberrypi:~/demo $ cat intrusiondetection.yang
module intrusiondetection {

 namespace "http://netconfcentral.org/ns/intrusiondetection";

 prefix "intrusion";

 description
  "YANG module for Intrusion Detection IoT system";

 revision 2014-07-15 {
  description "Intrusion Detection System";
 }

 grouping room {
  leaf doorsensorID {
   type string;
   description
    "ID of door sensor in the room";
  }
  leaf motionsensorID {
   type string;
   description
    "ID of motion sensor in the room";
  }
 }

 container intrusiondetection {
  presence
   "Indicates the service is available";

  description
   "Top-level container for all system objects.";

  leaf systemID {
   type string;
   config false;
   mandatory true;
   description
   "ID of the system";
  }

  leaf systemLocation {
   type string;
   config false;
   mandatory true;
   description
   "The location of the system";
  }

  leaf systemStatus {
   type enumeration {
    enum up {
    value 1;
    description
     "This is powered up";
    }
    enum down {
    value 2;
    description
     "This is powered down";
    }
    enum armed {
    value 3;
    description
     "This is armed";
    }
    enum disarmed {
    value 4;
    description
     "This is disarmed";
    }
   }
   config false;
   mandatory true;
   description
   "This variable indicates the current state of
    the system.";
  }
    container sensors {
   uses room;
   config false;
  }
 }

 rpc arm-system {
  description
   "Arm the system";
 }

 rpc disarm-system {
  description
   "Disarm the system";
 }

 notification systemArmed {
  description
   "Indicates that system has been armed.";

  leaf armStatus {
   description
    "Indicates the system arming status";

   type enumeration {
    enum armed {
    description
     "The system was armed.";
    }

    enum disarmed {
    description
     "The system was disarmed.";
    }

    enum error {
    description
     "The system is broken.";
    }
   }
  }
 }
}
pi@raspberrypi:~/demo $ pyang -f yin -o intrusiondetection.yin intrusiondetection.yang
pi@raspberrypi:~/demo $ cat intrusiondetection.yin
<?xml version="1.0" encoding="UTF-8"?>
<module name="intrusiondetection"
        xmlns="urn:ietf:params:xml:ns:yang:yin:1"
        xmlns:intrusion="http://netconfcentral.org/ns/intrusiondetection">
  <namespace uri="http://netconfcentral.org/ns/intrusiondetection"/>
  <prefix value="intrusion"/>
  <description>
    <text>YANG module for Intrusion Detection IoT system</text>
  </description>
  <revision date="2014-07-15">
    <description>
      <text>Intrusion Detection System</text>
    </description>
  </revision>
  <grouping name="room">
    <leaf name="doorsensorID">
      <type name="string"/>
      <description>
        <text>ID of door sensor in the room</text>
      </description>
    </leaf>
    <leaf name="motionsensorID">
      <type name="string"/>
      <description>
        <text>ID of motion sensor in the room</text>
      </description>
    </leaf>
  </grouping>
  <container name="intrusiondetection">
    <presence value="Indicates the service is available"/>
    <description>
      <text>Top-level container for all system objects.</text>
    </description>
    <leaf name="systemID">
      <type name="string"/>
      <config value="false"/>
      <mandatory value="true"/>
      <description>
        <text>ID of the system</text>
      </description>
    </leaf>
    <leaf name="systemLocation">
      <type name="string"/>
      <config value="false"/>
      <mandatory value="true"/>
      <description>
        <text>The location of the system</text>
      </description>
    </leaf>
    <leaf name="systemStatus">
      <type name="enumeration">
        <enum name="up">
          <value value="1"/>
          <description>
            <text>This is powered up</text>
          </description>
        </enum>
        <enum name="down">
          <value value="2"/>
          <description>
            <text>This is powered down</text>
          </description>
        </enum>
        <enum name="armed">
          <value value="3"/>
          <description>
            <text>This is armed</text>
          </description>
        </enum>
        <enum name="disarmed">
          <value value="4"/>
          <description>
            <text>This is disarmed</text>
          </description>
        </enum>
      </type>
      <config value="false"/>
      <mandatory value="true"/>
      <description>
        <text>This variable indicates the current state of
the system.</text>
      </description>
    </leaf>
    <container name="sensors">
      <uses name="room"/>
      <config value="false"/>
    </container>
  </container>
  <rpc name="arm-system">
    <description>
      <text>Arm the system</text>
    </description>
  </rpc>
  <rpc name="disarm-system">
    <description>
      <text>Disarm the system</text>
    </description>
  </rpc>
  <notification name="systemArmed">
    <description>
      <text>Indicates that system has been armed.</text>
    </description>
    <leaf name="armStatus">
      <description>
        <text>Indicates the system arming status</text>
      </description>
      <type name="enumeration">
        <enum name="armed">
          <description>
            <text>The system was armed.</text>
          </description>
        </enum>
        <enum name="disarmed">
          <description>
            <text>The system was disarmed.</text>
          </description>
        </enum>
        <enum name="error">
          <description>
            <text>The system is broken.</text>
          </description>
        </enum>
      </type>
    </leaf>
  </notification>
</module>
pi@raspberrypi:~/demo $ pyang -f uml -o intrusiondetection.uml intrusiondetection.yang --uml-no=stereotypes,annotation,typedef
pi@raspberrypi:~/demo $ cat intrusiondetection.uml
'Download plantuml from http://plantuml.sourceforge.net/
'Generate png with java -jar plantuml.jar <file>
'Output in img/<module>.png
'If Java spits out memory error increase heap size with java -Xmx1024m  -jar plantuml.jar <file>
@startuml img/intrusiondetection.png
hide empty fields
hide empty methods
hide <<case>> circle
hide <<augment>> circle
hide <<choice>> circle
hide <<leafref>> stereotype
hide <<leafref>> circle
hide stereotypes
page 1x1
Title intrusiondetection
package "intrusion:intrusiondetection" as intrusion_intrusiondetection {
class "intrusiondetection" as intrusiondetection << (M, #33CCFF) module>>
class "room" as intrusiondetection_I_room_grouping <<(G,Lime) grouping>>
intrusiondetection_I_room_grouping : doorsensorID : string
intrusiondetection_I_room_grouping : motionsensorID : string
class "intrusiondetection" as  intrusiondetection_I_intrusiondetection <<container>>
intrusiondetection *-- "0..1" intrusiondetection_I_intrusiondetection
intrusiondetection_I_intrusiondetection : systemID : string   {mandatory} {Config : false}
intrusiondetection_I_intrusiondetection : systemLocation : string   {mandatory} {Config : false}
intrusiondetection_I_intrusiondetection : systemStatus : enumeration : {up,down,armed,...}   {mandatory} {Config : false}
class "sensors" as  intrusiondetection_I_intrusiondetection_I_sensors <<container>>
intrusiondetection_I_intrusiondetection *-- "1" intrusiondetection_I_intrusiondetection_I_sensors
intrusiondetection_I_intrusiondetection_I_sensors : room {uses}
intrusiondetection : arm-system()
intrusiondetection : disarm-system()
class "systemArmed" as intrusiondetection_I_systemArmed << (N,#00D1B2) notification>>
intrusiondetection -- intrusiondetection_I_systemArmed : notification
intrusiondetection_I_systemArmed : armStatus : enumeration : {armed,disarmed,error,}
}

intrusiondetection_I_intrusiondetection_I_sensors --> intrusiondetection_I_room_grouping : uses
center footer
 <size:20> UML Generated : 2023-04-28 13:02 </size>
 endfooter
@enduml
```
# Install PlantUML
This is done by running `sudo pip3 install -U plantuml`
```
pi@raspberrypi:~/demo $ sudo pip3 install -U plantuml
Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple
Collecting plantuml
  Downloading plantuml-0.3.0-py3-none-any.whl (5.8 kB)
Collecting httplib2
  Downloading https://www.piwheels.org/simple/httplib2/httplib2-0.22.0-py3-none-any.whl (96 kB)
     |████████████████████████████████| 96 kB 508 kB/s
Collecting pyparsing!=3.0.0,!=3.0.1,!=3.0.2,!=3.0.3,<4,>=2.4.2
  Downloading https://www.piwheels.org/simple/pyparsing/pyparsing-3.0.9-py3-none-any.whl (98 kB)
     |████████████████████████████████| 98 kB 530 kB/s
Installing collected packages: pyparsing, httplib2, plantuml
Successfully installed httplib2-0.22.0 plantuml-0.3.0 pyparsing-3.0.9
```
# Run PlantUML
```
pi@raspberrypi:~/demo $ python3 -m plantuml intrusiondetection.uml
[{'filename': 'intrusiondetection.uml', 'gen_success': True}]
```
# Run GIMP/Pinta
For some reason i was unable to download the Pinta software on my Raspberry Pi, but I was able to successfully install GIMP.
The following code shows the outputs of the commands entered
```
pi@raspberrypi:~/demo $ sudo apt install gimp
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libfuse2 raspinfo
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  fonts-liberation gimp-data graphviz gsfonts libamd2 libann0 libbabl-0.1-0
  libcamd2 libccolamd2 libcdt5 libcgraph6 libcholmod3 libcolamd2 libexiv2-27
  libgegl-0.4-0 libgegl-common libgexiv2-2 libgimp2.0 libgts-0.7-5 libgts-bin
  libgvc6 libgvpr2 libheif1 liblab-gamut1 libmetis5 libmng1 libmypaint-1.5-1
  libmypaint-common libpathplan4 libraw20 libsuitesparseconfig5 libumfpack5
  libwmf0.2-7
Suggested packages:
  gimp-help-en | gimp-help gimp-data-extras graphviz-doc exiv2 libwmf0.2-7-gtk
The following NEW packages will be installed:
  fonts-liberation gimp gimp-data graphviz gsfonts libamd2 libann0
  libbabl-0.1-0 libcamd2 libccolamd2 libcdt5 libcgraph6 libcholmod3 libcolamd2
  libexiv2-27 libgegl-0.4-0 libgegl-common libgexiv2-2 libgimp2.0 libgts-0.7-5
  libgts-bin libgvc6 libgvpr2 libheif1 liblab-gamut1 libmetis5 libmng1
  libmypaint-1.5-1 libmypaint-common libpathplan4 libraw20
  libsuitesparseconfig5 libumfpack5 libwmf0.2-7
0 upgraded, 34 newly installed, 0 to remove and 38 not upgraded.
Need to get 38.3 MB of archives.
After this operation, 159 MB of additional disk space will be used.
Do you want to continue? [Y/n] yt
Get:1 http://deb.debian.org/debian bullseye/main arm64 fonts-liberation all 1:1.07.4-11 [828 kB]
Get:2 http://deb.debian.org/debian bullseye/main arm64 libbabl-0.1-0 arm64 1:0.1.82-1 [248 kB]
Get:3 http://deb.debian.org/debian bullseye/main arm64 libraw20 arm64 0.20.2-1 [333 kB]
Get:4 http://deb.debian.org/debian bullseye/main arm64 libsuitesparseconfig5 arm64 1:5.8.1+dfsg-2 [22.8 kB]
Get:5 http://deb.debian.org/debian bullseye/main arm64 libamd2 arm64 1:5.8.1+dfsg-2 [33.1 kB]
Get:6 http://deb.debian.org/debian bullseye/main arm64 libcamd2 arm64 1:5.8.1+dfsg-2 [33.9 kB]
Get:7 http://deb.debian.org/debian bullseye/main arm64 libccolamd2 arm64 1:5.8.1+dfsg-2 [36.6 kB]
Get:8 http://deb.debian.org/debian bullseye/main arm64 libcolamd2 arm64 1:5.8.1+dfsg-2 [31.0 kB]
Get:9 http://deb.debian.org/debian bullseye/main arm64 libmetis5 arm64 5.1.0.dfsg-7 [154 kB]
Get:10 http://deb.debian.org/debian bullseye/main arm64 libcholmod3 arm64 1:5.8.1+dfsg-2 [290 kB]
Get:11 http://deb.debian.org/debian bullseye/main arm64 libumfpack5 arm64 1:5.8.1+dfsg-2 [201 kB]
Get:12 http://deb.debian.org/debian bullseye/main arm64 libgegl-common all 1:0.4.26-2 [706 kB]
Get:13 http://deb.debian.org/debian bullseye/main arm64 libgegl-0.4-0 arm64 1:0.4.26-2 [848 kB]
Get:14 http://deb.debian.org/debian bullseye/main arm64 libexiv2-27 arm64 0.27.3-3+deb11u1 [1,519 kB]
Get:15 http://deb.debian.org/debian bullseye/main arm64 libgexiv2-2 arm64 0.12.1-1 [52.4 kB]
Get:16 http://deb.debian.org/debian bullseye/main arm64 libgimp2.0 arm64 2.10.22-4 [3,563 kB]
Get:17 http://deb.debian.org/debian bullseye/main arm64 gimp-data all 2.10.22-4 [16.8 MB]
Get:18 http://deb.debian.org/debian bullseye/main arm64 libann0 arm64 1.1.2+doc-7 [25.1 kB]
Get:19 http://deb.debian.org/debian bullseye/main arm64 libcdt5 arm64 2.42.2-5 [61.2 kB]
Get:20 http://deb.debian.org/debian bullseye/main arm64 libcgraph6 arm64 2.42.2-5 [82.7 kB]
Get:21 http://deb.debian.org/debian bullseye/main arm64 libgts-0.7-5 arm64 0.7.6+darcs121130-4+b1 [143 kB]
Get:22 http://deb.debian.org/debian bullseye/main arm64 libpathplan4 arm64 2.42.2-5 [62.6 kB]
Get:23 http://deb.debian.org/debian bullseye/main arm64 libgvc6 arm64 2.42.2-5 [632 kB]
Get:24 http://deb.debian.org/debian bullseye/main arm64 libgvpr2 arm64 2.42.2-5 [201 kB]
Get:25 http://deb.debian.org/debian bullseye/main arm64 liblab-gamut1 arm64 2.42.2-5 [220 kB]
Get:26 http://deb.debian.org/debian bullseye/main arm64 graphviz arm64 2.42.2-5 [586 kB]
Get:27 http://deb.debian.org/debian bullseye/main arm64 libheif1 arm64 1.11.0-1 [173 kB]
Get:28 http://deb.debian.org/debian bullseye/main arm64 libmng1 arm64 1.0.10+dfsg-3.1+b5 [192 kB]
Get:29 http://deb.debian.org/debian bullseye/main arm64 libmypaint-common all 1.6.0-2 [140 kB]
Get:30 http://deb.debian.org/debian bullseye/main arm64 libmypaint-1.5-1 arm64 1.6.0-2 [44.2 kB]
Get:31 http://deb.debian.org/debian bullseye/main arm64 libwmf0.2-7 arm64 0.2.8.4-17 [153 kB]
Get:32 http://deb.debian.org/debian bullseye/main arm64 gimp arm64 2.10.22-4 [6,764 kB]
Get:33 http://deb.debian.org/debian bullseye/main arm64 gsfonts all 1:8.11+urwcyr1.0.7~pre44-4.5 [3,125 kB]
Get:34 http://deb.debian.org/debian bullseye/main arm64 libgts-bin arm64 0.7.6+darcs121130-4+b1 [48.6 kB]
Fetched 38.3 MB in 7s (5,188 kB/s)                                             
Extracting templates from packages: 100%
Selecting previously unselected package fonts-liberation.
(Reading database ... 93388 files and directories currently installed.)
Preparing to unpack .../00-fonts-liberation_1%3a1.07.4-11_all.deb ...
Unpacking fonts-liberation (1:1.07.4-11) ...
Selecting previously unselected package libbabl-0.1-0:arm64.
Preparing to unpack .../01-libbabl-0.1-0_1%3a0.1.82-1_arm64.deb ...
Unpacking libbabl-0.1-0:arm64 (1:0.1.82-1) ...
Selecting previously unselected package libraw20:arm64.
Preparing to unpack .../02-libraw20_0.20.2-1_arm64.deb ...
Unpacking libraw20:arm64 (0.20.2-1) ...
Selecting previously unselected package libsuitesparseconfig5:arm64.
Preparing to unpack .../03-libsuitesparseconfig5_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libsuitesparseconfig5:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libamd2:arm64.
Preparing to unpack .../04-libamd2_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libamd2:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libcamd2:arm64.
Preparing to unpack .../05-libcamd2_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libcamd2:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libccolamd2:arm64.
Preparing to unpack .../06-libccolamd2_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libccolamd2:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libcolamd2:arm64.
Preparing to unpack .../07-libcolamd2_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libcolamd2:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libmetis5:arm64.
Preparing to unpack .../08-libmetis5_5.1.0.dfsg-7_arm64.deb ...
Unpacking libmetis5:arm64 (5.1.0.dfsg-7) ...
Selecting previously unselected package libcholmod3:arm64.
Preparing to unpack .../09-libcholmod3_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libcholmod3:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libumfpack5:arm64.
Preparing to unpack .../10-libumfpack5_1%3a5.8.1+dfsg-2_arm64.deb ...
Unpacking libumfpack5:arm64 (1:5.8.1+dfsg-2) ...
Selecting previously unselected package libgegl-common.
Preparing to unpack .../11-libgegl-common_1%3a0.4.26-2_all.deb ...
Unpacking libgegl-common (1:0.4.26-2) ...
Selecting previously unselected package libgegl-0.4-0:arm64.
Preparing to unpack .../12-libgegl-0.4-0_1%3a0.4.26-2_arm64.deb ...
Unpacking libgegl-0.4-0:arm64 (1:0.4.26-2) ...
Selecting previously unselected package libexiv2-27:arm64.
Preparing to unpack .../13-libexiv2-27_0.27.3-3+deb11u1_arm64.deb ...
Unpacking libexiv2-27:arm64 (0.27.3-3+deb11u1) ...
Selecting previously unselected package libgexiv2-2:arm64.
Preparing to unpack .../14-libgexiv2-2_0.12.1-1_arm64.deb ...
Unpacking libgexiv2-2:arm64 (0.12.1-1) ...
Selecting previously unselected package libgimp2.0:arm64.
Preparing to unpack .../15-libgimp2.0_2.10.22-4_arm64.deb ...
Unpacking libgimp2.0:arm64 (2.10.22-4) ...
Selecting previously unselected package gimp-data.
Preparing to unpack .../16-gimp-data_2.10.22-4_all.deb ...
Unpacking gimp-data (2.10.22-4) ...
Selecting previously unselected package libann0.
Preparing to unpack .../17-libann0_1.1.2+doc-7_arm64.deb ...
Unpacking libann0 (1.1.2+doc-7) ...
Selecting previously unselected package libcdt5:arm64.
Preparing to unpack .../18-libcdt5_2.42.2-5_arm64.deb ...
Unpacking libcdt5:arm64 (2.42.2-5) ...
Selecting previously unselected package libcgraph6:arm64.
Preparing to unpack .../19-libcgraph6_2.42.2-5_arm64.deb ...
Unpacking libcgraph6:arm64 (2.42.2-5) ...
Selecting previously unselected package libgts-0.7-5:arm64.
Preparing to unpack .../20-libgts-0.7-5_0.7.6+darcs121130-4+b1_arm64.deb ...
Unpacking libgts-0.7-5:arm64 (0.7.6+darcs121130-4+b1) ...
Selecting previously unselected package libpathplan4:arm64.
Preparing to unpack .../21-libpathplan4_2.42.2-5_arm64.deb ...
Unpacking libpathplan4:arm64 (2.42.2-5) ...
Selecting previously unselected package libgvc6.
Preparing to unpack .../22-libgvc6_2.42.2-5_arm64.deb ...
Unpacking libgvc6 (2.42.2-5) ...
Selecting previously unselected package libgvpr2:arm64.
Preparing to unpack .../23-libgvpr2_2.42.2-5_arm64.deb ...
Unpacking libgvpr2:arm64 (2.42.2-5) ...
Selecting previously unselected package liblab-gamut1:arm64.
Preparing to unpack .../24-liblab-gamut1_2.42.2-5_arm64.deb ...
Unpacking liblab-gamut1:arm64 (2.42.2-5) ...
Selecting previously unselected package graphviz.
Preparing to unpack .../25-graphviz_2.42.2-5_arm64.deb ...
Unpacking graphviz (2.42.2-5) ...
Selecting previously unselected package libheif1:arm64.
Preparing to unpack .../26-libheif1_1.11.0-1_arm64.deb ...
Unpacking libheif1:arm64 (1.11.0-1) ...
Selecting previously unselected package libmng1:arm64.
Preparing to unpack .../27-libmng1_1.0.10+dfsg-3.1+b5_arm64.deb ...
Unpacking libmng1:arm64 (1.0.10+dfsg-3.1+b5) ...
Selecting previously unselected package libmypaint-common.
Preparing to unpack .../28-libmypaint-common_1.6.0-2_all.deb ...
Unpacking libmypaint-common (1.6.0-2) ...
Selecting previously unselected package libmypaint-1.5-1:arm64.
Preparing to unpack .../29-libmypaint-1.5-1_1.6.0-2_arm64.deb ...
Unpacking libmypaint-1.5-1:arm64 (1.6.0-2) ...
Selecting previously unselected package libwmf0.2-7:arm64.
Preparing to unpack .../30-libwmf0.2-7_0.2.8.4-17_arm64.deb ...
Unpacking libwmf0.2-7:arm64 (0.2.8.4-17) ...
Selecting previously unselected package gimp.
Preparing to unpack .../31-gimp_2.10.22-4_arm64.deb ...
Unpacking gimp (2.10.22-4) ...
Selecting previously unselected package gsfonts.
Preparing to unpack .../32-gsfonts_1%3a8.11+urwcyr1.0.7~pre44-4.5_all.deb ...
Unpacking gsfonts (1:8.11+urwcyr1.0.7~pre44-4.5) ...
Selecting previously unselected package libgts-bin.
Preparing to unpack .../33-libgts-bin_0.7.6+darcs121130-4+b1_arm64.deb ...
Unpacking libgts-bin (0.7.6+darcs121130-4+b1) ...
Setting up libmng1:arm64 (1.0.10+dfsg-3.1+b5) ...
Setting up libmypaint-common (1.6.0-2) ...
Setting up libwmf0.2-7:arm64 (0.2.8.4-17) ...
Setting up libbabl-0.1-0:arm64 (1:0.1.82-1) ...
Setting up libheif1:arm64 (1.11.0-1) ...
Setting up liblab-gamut1:arm64 (2.42.2-5) ...
Setting up libmetis5:arm64 (5.1.0.dfsg-7) ...
Setting up libmypaint-1.5-1:arm64 (1.6.0-2) ...
Setting up libgts-0.7-5:arm64 (0.7.6+darcs121130-4+b1) ...
Setting up libexiv2-27:arm64 (0.27.3-3+deb11u1) ...
Setting up libpathplan4:arm64 (2.42.2-5) ...
Setting up gsfonts (1:8.11+urwcyr1.0.7~pre44-4.5) ...
Setting up libann0 (1.1.2+doc-7) ...
Setting up libraw20:arm64 (0.20.2-1) ...
Setting up gimp-data (2.10.22-4) ...
Setting up fonts-liberation (1:1.07.4-11) ...
Setting up libgegl-common (1:0.4.26-2) ...
Setting up libcdt5:arm64 (2.42.2-5) ...
Setting up libcgraph6:arm64 (2.42.2-5) ...
Setting up libgexiv2-2:arm64 (0.12.1-1) ...
Setting up libsuitesparseconfig5:arm64 (1:5.8.1+dfsg-2) ...
Setting up libamd2:arm64 (1:5.8.1+dfsg-2) ...
Setting up libgts-bin (0.7.6+darcs121130-4+b1) ...
Setting up libcolamd2:arm64 (1:5.8.1+dfsg-2) ...
Setting up libcamd2:arm64 (1:5.8.1+dfsg-2) ...
Setting up libgvc6 (2.42.2-5) ...
Setting up libgvpr2:arm64 (2.42.2-5) ...
Setting up libccolamd2:arm64 (1:5.8.1+dfsg-2) ...
Setting up libcholmod3:arm64 (1:5.8.1+dfsg-2) ...
Setting up graphviz (2.42.2-5) ...
Setting up libumfpack5:arm64 (1:5.8.1+dfsg-2) ...
Setting up libgegl-0.4-0:arm64 (1:0.4.26-2) ...
Setting up libgimp2.0:arm64 (2.10.22-4) ...
Setting up gimp (2.10.22-4) ...
Processing triggers for desktop-file-utils (0.26-1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1) ...
Processing triggers for libc-bin (2.31-13+rpt2+rpi1+deb11u5) ...
Processing triggers for man-db (2.9.4-2) ...
Processing triggers for mailcap (3.69) ...
Processing triggers for fontconfig (2.13.1-4.2) ...
pi@raspberrypi:~/demo $ sudo apt install pinta
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package pinta is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'pinta' has no installation candidate
pi@raspberrypi:~/demo $ gimp -h
Usage:
  gimp [OPTION…] [FILE|URI...]

GNU Image Manipulation Program

Help Options:
  -h, --help                              Show help options
  --help-all                              Show all help options
  --help-gegl                             Show GEGL Options
  --help-gtk                              Show GTK+ Options

Application Options:
  -v, --version                           Show version information and exit
  --license                               Show license information and exit
  --verbose                               Be more verbose
  -n, --new-instance                      Start a new GIMP instance
  -a, --as-new                            Open images as new
  -i, --no-interface                      Run without a user interface
  -d, --no-data                           Do not load brushes, gradients, patterns, ...
  -f, --no-fonts                          Do not load any fonts
  -s, --no-splash                         Do not show a splash screen
  --no-shm                                Do not use shared memory between GIMP and plug-ins
  --no-cpu-accel                          Do not use special CPU acceleration functions
  --session=<name>                        Use an alternate sessionrc file
  -g, --gimprc=<filename>                 Use an alternate user gimprc file
  --system-gimprc=<filename>              Use an alternate system gimprc file
  -b, --batch=<command>                   Batch command to run (can be used multiple times)
  --batch-interpreter=<proc>              The procedure to process batch commands with
  -c, --console-messages                  Send messages to console instead of using a dialog
  --pdb-compat-mode=<mode>                PDB compatibility mode (off|on|warn)
  --stack-trace-mode=<mode>               Debug in case of a crash (never|query|always)
  --debug-handlers                        Enable non-fatal debugging signal handlers
  --g-fatal-warnings                      Make all warnings fatal
  --dump-gimprc                           Output a gimprc file with default settings
  --show-playground                       Show a preferences page with experimental features
  --display=DISPLAY                       X display to use

pi@raspberrypi:~/demo $ gimp -a instrusiondetection.png
gimp_get_monitor_resolution(): GDK returned bogus values for the monitor resolution, using 96 dpi instead.
gimp_get_monitor_resolution(): GDK returned bogus values for the monitor resolution, using 96 dpi instead.
gimp_get_monitor_resolution(): GDK returned bogus values for the monitor resolution, using 96 dpi instead.
gimp_get_monitor_resolution(): GDK returned bogus values for the monitor resolution, using 96 dpi instead.
gimp_get_monitor_resolution(): GDK returned bogus values for the monitor resolution, using 96 dpi instead.
```

```
pi@raspberrypi:~/demo $ sudo apt install pinta
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package pinta is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'pinta' has no installation candidate
```
As you can see here, the pinta package was not installing properly on my machine.
![GIMP Image](/GIMP.png)