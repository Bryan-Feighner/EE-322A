# Lab 4
## Python on Raspberry Pi
This week, we begin learning Python. Python is a high level operating language with many built in libraries and externally downloadable packages.
## Code Returns
```
pi@raspberrypi:~ $ cd ~/iot
pi@raspberrypi:~/iot $ cd *3
pi@raspberrypi:~/iot/lesson3 $ python3 julian.py
Calendar Date: 2023-04-03
Julian Date: 2460037.5
Modified Julian Date: 60037.0
pi@raspberrypi:~/iot/lesson3 $ python3 date_example.py
Date: 2023-04-03
Date: 04-03-23
Day of Week: Monday
Month: April
Year: 2023
75 days after the first day of classes
31 days before the last day of classes
pi@raspberrypi:~/iot/lesson3 $ python3 date
date_example.py      datetime_example.py
pi@raspberrypi:~/iot/lesson3 $ python3 datetime_example.py
2023-04-03 08:22:00.978651
2023-04-03 08:22:00.978835
2023-04-03 12:22:00.978864
1680524520.9788902
Mon Apr  3 08:22:00 2023
2023-04-03 08:22:00.978990
2023-04-03 12:22:00.979016
pi@raspberrypi:~/iot/lesson3 $ python3 time_example.py
Mon Apr  3 08:22:08 2023
pi@raspberrypi:~/iot/lesson3 $ python3 sun.py 'New York'
Information for New York/USA

Timezone: US/Eastern
Latitude: 40.72; Longitude: -74.00

Dawn:    2023-04-03 06:08:38.900946-04:00
Sunrise: 2023-04-03 06:36:50.523610-04:00
Noon:    2023-04-03 12:59:28-04:00
Sunset:  2023-04-03 19:22:24.163265-04:00
Dusk:    2023-04-03 19:50:40.477918-04:00
pi@raspberrypi:~/iot/lesson3 $ python3 moon.py
2023-04-03 Moon Phase: 11
2023-04-04 Moon Phase: 12
2023-04-05 Moon Phase: 13
2023-04-06 Moon Phase: 14
2023-04-07 Moon Phase: 15
2023-04-08 Moon Phase: 16
2023-04-09 Moon Phase: 17
2023-04-10 Moon Phase: 18
2023-04-11 Moon Phase: 19
2023-04-12 Moon Phase: 20
2023-04-13 Moon Phase: 21
2023-04-14 Moon Phase: 22
2023-04-15 Moon Phase: 23
2023-04-16 Moon Phase: 24
2023-04-17 Moon Phase: 25
2023-04-18 Moon Phase: 26
2023-04-19 Moon Phase: 27
2023-04-20 Moon Phase: 0
2023-04-21 Moon Phase: 1
2023-04-22 Moon Phase: 2
2023-04-23 Moon Phase: 3
2023-04-24 Moon Phase: 4
2023-04-25 Moon Phase: 5
2023-04-26 Moon Phase: 5
2023-04-27 Moon Phase: 6
2023-04-28 Moon Phase: 7
2023-04-29 Moon Phase: 8
2023-04-30 Moon Phase: 9
2023-05-01 Moon Phase: 10
2023-05-02 Moon Phase: 11
pi@raspberrypi:~/iot/lesson3 $ python3 coordinates.py 'Samuel C Williams Library'
Samuel C. Williams Library, Field House Road, Hoboken, Hudson County, New Jersey, 07030, United States
(40.74480675, -74.02532861159351)
pi@raspberrypi:~/iot/lesson3 $ python3 address.py  '40.74480675, -74.02532862031404'
Samuel C. Williams Library, Field House Road, Hoboken, Hudson County, New Jersey, 07030, United States
(40.74480675, -74.02532861159351)
pi@raspberrypi:~/iot/lesson3 $ python3 cpu.py
The number of physical cores =  4
The number of logical CPUs =  4
The utilization per second as a percentage for each CPU
[0.0, 0.0, 0.0, 0.0]
[1.0, 0.0, 0.0, 0.0]
[0.0, 0.0, 0.0, 0.0]
[0.0, 0.0, 0.0, 0.0]
[24.5, 0.0, 0.0, 0.0]
[56.2, 0.0, 0.0, 0.0]
[3.1, 0.0, 0.0, 0.0]
[1.0, 0.0, 1.0, 0.0]
[0.0, 0.0, 0.0, 0.0]
[0.0, 0.0, 0.0, 0.0]
pi@raspberrypi:~/iot/lesson3 $ python3 battery.py
None
pi@raspberrypi:~/iot/lesson3 $ python3 documentstats.py document.txt
Word Count: 1343
Top Ten Words: [('our', 26), ('their', 20), ('has', 20), ('he', 19), ('them', 15), ('these', 13), ('have', 11), ('we', 11), ('us', 11), ('people', 10)]
```