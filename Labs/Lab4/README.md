# Django and Flask
I had previously attempted to complete this lab but encountered an error, so some code may have been pre-downloaded/run in each section.
## Django & Django REST
First we begin by installing the required tootls using 
```
$ pip3 -V
$ pip3 list
$ sudo pip3 install -U setuptools
$ sudo pip3 install -U django
$ sudo pip3 install -U djangorestframework
$ sudo pip3 install -U django-filter
$ sudo pip3 install -U markdown
$ sudo pip3 install -U requests
```
And afer we run this, running `pip3 list` gives us a list of all downloaded packages
```
pi@raspberrypi:~ $ pip3 -V
pip 20.3.4 from /usr/lib/python3/dist-packages/pip (python 3.9)
pi@raspberrypi:~ $ pip3 list
Package             Version
------------------- ---------
arandr              0.1.10
asgiref             3.6.0
astral              3.2
astroid             2.5.1
asttokens           2.0.4
automationhat       0.2.0
beautifulsoup4      4.9.3
blinker             1.4
blinkt              0.1.2
buttonshim          0.0.2
Cap1xxx             0.1.3
certifi             2020.6.20
chardet             4.0.0
charset-normalizer  3.1.0
click               7.1.2
colorama            0.4.4
colorzero           1.1
cryptography        3.3.2
cupshelpers         1.0
dbus-python         1.2.16
distro              1.5.0
Django              4.2
django-filter       23.1
djangorestframework 3.14.0
docutils            0.16
drumhat             0.1.0
envirophat          1.0.0
ExplorerHAT         0.4.2
Flask               1.1.2
fourletterphat      0.1.0
geographiclib       2.0
geopy               2.3.0
gpiozero            1.6.2
html5lib            1.1
httplib2            0.22.0
idna                2.10
importlib-metadata  6.1.0
isort               5.6.4
itsdangerous        1.1.0
jdcal               1.4.1
jedi                0.18.0
Jinja2              2.11.3
lazy-object-proxy   0.0.0
logilab-common      1.8.1
lxml                4.9.2
Markdown            3.4.3
MarkupSafe          2.0.1
mccabe              0.6.1
microdotphat        0.2.1
mote                0.0.4
motephat            0.0.3
mypy                0.812
mypy-extensions     0.4.3
mysql-client        0.0.1
mysqlclient         1.4.4
numpy               1.19.5
oauthlib            3.1.0
olefile             0.46
paho-mqtt           1.6.1
pantilthat          0.0.7
parso               0.8.1
pexpect             4.8.0
pgzero              1.2
phatbeat            0.1.1
pianohat            0.1.0
piglow              1.2.5
pigpio              1.78
Pillow              8.1.2
pip                 20.3.4
plantuml            0.3.0
psutil              5.9.4
pyang               2.5.3
pycairo             1.16.2
pycups              2.0.1
pygame              1.9.6
Pygments            2.7.1
PyGObject           3.38.0
pyinotify           0.9.6
PyJWT               1.7.1
pylint              2.7.2
pyOpenSSL           20.0.1
pyparsing           3.0.9
pyserial            3.5b0
pysmbc              1.0.23
python-apt          2.2.1
pytz                2023.3
rainbowhat          0.1.0
reportlab           3.5.59
requests            2.28.2
requests-oauthlib   1.0.0
responses           0.12.1
roman               2.0.0
RPi.GPIO            0.7.0
RTIMULib            7.2.1
scrollphat          0.0.7
scrollphathd        1.2.1
Send2Trash          1.6.0b1
sense-hat           2.4.0
setuptools          67.6.1
simplejson          3.17.2
six                 1.16.0
skywriter           0.0.7
sn3218              1.2.7
soupsieve           2.2.1
spidev              3.5
sqlparse            0.4.3
ssh-import-id       5.10
thonny              4.0.1
toml                0.10.1
touchphat           0.0.1
twython             3.8.2
typed-ast           1.4.2
typing-extensions   3.7.4.3
unicornhathd        0.0.4
urllib3             1.26.5
webencodings        0.5.1
Werkzeug            1.0.1
wheel               0.34.2
wrapt               1.12.1
zipp                3.15.0
```
## Start Django Project
```
pi@raspberrypi:~ $ django-admin startproject stevens
CommandError: '/home/pi/stevens' already exists
pi@raspberrypi:~ $ cd stevens
pi@raspberrypi:~/stevens $ ls
manage.py  myapp  stevens
```
## Start a Django App
```
pi@raspberrypi:~/stevens $ python3 manage.py startapp myapp
CommandError: 'myapp' conflicts with the name of an existing Python module and cannot be used as an app name. Please try another name.
pi@raspberrypi:~/stevens $ ls
manage.py  myapp  stevens
```
## MySQL and MariaDB
```
pi@raspberrypi:~/stevens $ sudo mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.5.18-MariaDB-0+deb11u1 Debian 11

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [mysql]> select user, host from mysql.user;
+-------------+-----------+
| User        | Host      |
+-------------+-----------+
| mariadb.sys | localhost |
| mysql       | localhost |
| pi          | localhost |
| root        | localhost |
+-------------+-----------+
4 rows in set (0.004 sec)

MariaDB [mysql]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| stevens            |
+--------------------+
4 rows in set (0.001 sec)

MariaDB [mysql]> create database stevens
    -> ;
ERROR 1007 (HY000): Can't create database 'stevens'; database exists
MariaDB [mysql]> grant all privileges on stevens.* to pi@localhost;
Query OK, 0 rows affected (0.003 sec)
```
## Edit settings.py
```
pi@raspberrypi:~/stevens $ cd stevens
pi@raspberrypi:~/stevens/stevens $ ls
asgi.py  __init__.py  __pycache__  settings.py  urls.py  wsgi.py
pi@raspberrypi:~/stevens/stevens $ nano settings.py
```
## Copy urls.py to ~/stevens/stevens
```
pi@raspberrypi:~/stevens/stevens $ cp ~/iot/lesson4/stevens/urls.py .
pi@raspberrypi:~/stevens/stevens $ cd ..
```
## Copy admin.py, models.py, and views.py to ~/stevens/myapp
```
pi@raspberrypi:~/stevens $ cd myapp/
pi@raspberrypi:~/stevens/myapp $ ls
admin.py  apps.py  __init__.py  migrations  models.py  __pycache__  tests.py  views.py
pi@raspberrypi:~/stevens/myapp $ cp ~/iot/lesson4/stevens/admin.py .
pi@raspberrypi:~/stevens/myapp $ cp ~/iot/lesson4/stevens/models.py .
pi@raspberrypi:~/stevens/myapp $ cp ~/iot/lesson4/stevens/views.py .
```
## Copy index.html
```
pi@raspberrypi:~/stevens/myapp $ mkdir static templates
pi@raspberrypi:~/stevens/myapp $ cd templates/
pi@raspberrypi:~/stevens/myapp/templates $ mkdir myapp
pi@raspberrypi:~/stevens/myapp/templates $ cd myapp/
pi@raspberrypi:~/stevens/myapp/templates/myapp $ cp ~/iot/lesson4/stevens/index.html .
pi@raspberrypi:~/stevens/myapp/templates/myapp $ 
```
## Edit index.html to add the Google Maps API Key
My google API key is AIzaSyBvYIJABn7HxKtMT1vQjiOCxlB1mM6DbdU
```
pi@raspberrypi:~/stevens/myapp/templates/myapp $ nano index.html
```
## Copy static files
```
pi@raspberrypi:~/stevens/myapp/templates/myapp $ cd ~/stevens/myapp/static/
pi@raspberrypi:~/stevens/myapp/static $ cp ~/iot/lesson4/static/favicon.ico 
cp: missing destination file operand after '/home/pi/iot/lesson4/static/favicon.ico'
Try 'cp --help' for more information.
pi@raspberrypi:~/stevens/myapp/static $ cp ~/iot/lesson4/static/favicon.ico .
pi@raspberrypi:~/stevens/myapp/static $ mkdir myapp
pi@raspberrypi:~/stevens/myapp/static $ cd myapp
pi@raspberrypi:~/stevens/myapp/static/myapp $ cp ~/iot/lesson4/static/*css .
pi@raspberrypi:~/stevens/myapp/static/myapp $ cp ~/iot/lesson4/static/*js .
pi@raspberrypi:~/stevens/myapp/static/myapp $ cd ~/stevens/
```
## Create superuser
```
pi@raspberrypi:~/stevens $ python3 manage.py makemigrations myapp
Migrations for 'myapp':
  myapp/migrations/0001_initial.py
    - Create model TemperatureData
pi@raspberrypi:~/stevens $ python3 manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, myapp, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying myapp.0001_initial... OK
  Applying sessions.0001_initial... OK
pi@raspberrypi:~/stevens $ python3 manage.py createsuperuser
Username (leave blank to use 'pi'): 
Email address: bnflego@gmail.com
Password: 
Password (again): 
Superuser created successfully.
```
## Run Django server
```
pi@raspberrypi:~/stevens $ python3 manage.py runserver
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
May 02, 2023 - 17:52:17
Django version 4.2, using settings 'stevens.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
## Start site
```
pi@raspberrypi:~/stevens $ python3 manage.py runserver
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
May 02, 2023 - 18:12:43
Django version 4.2, using settings 'stevens.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.

[02/May/2023 18:12:45] "GET / HTTP/1.1" 200 1535
[02/May/2023 18:12:45] "GET /static/myapp/bootstrap.min.css HTTP/1.1" 304 0
[02/May/2023 18:12:45] "GET /static/myapp/jquery.min.js HTTP/1.1" 304 0
[02/May/2023 18:12:45] "GET /static/myapp/bootstrap.min.js HTTP/1.1" 304 0
[02/May/2023 18:12:46] "GET /favicon.ico HTTP/1.1" 302 0
[02/May/2023 18:12:46] "GET /static/favicon.ico HTTP/1.1" 304 0
```
And here is an image of the website running
![Django server](Django.PNG)
# MyCpu
## Start a Django project and app
```
pi@raspberrypi:~/mycpu $ ls
controller.py  manage.py  myapp  mycpu
pi@raspberrypi:~/mycpu $ cd mycpu/
pi@raspberrypi:~/mycpu/mycpu $ ls
asgi.py  __init__.py  __pycache__  settings.py  urls.py  wsgi.py
```
## Copy urls.py to ~/mycpu/mycpu & Copy admin.py, models.py, views.py, and serializers.py to ~/mycpu/myapp
```
pi@raspberrypi:~/mycpu $ cd myapp/
pi@raspberrypi:~/mycpu/myapp $ ls
admin.py  __init__.py  models.py       static     tests.py
apps.py   migrations   serializers.py  templates  views.py
pi@raspberrypi:~/mycpu/myapp $ cp ~/iot/lesson4/mycpu/admin.py .
pi@raspberrypi:~/mycpu/myapp $ cp ~/iot/lesson4/mycpu/models.py .
pi@raspberrypi:~/mycpu/myapp $ cp ~/iot/lesson4/mycpu/views.py .
pi@raspberrypi:~/mycpu/myapp $ cp ~/iot/lesson4/mycpu/serializers.py .
```
## copy index.html and add API key
```
pi@raspberrypi:~/mycpu/myapp $ cd templates/
pi@raspberrypi:~/mycpu/myapp/templates $ ls
myapp
pi@raspberrypi:~/mycpu/myapp/templates $ cd myapp/
pi@raspberrypi:~/mycpu/myapp/templates/myapp $ ls
index.html
pi@raspberrypi:~/mycpu/myapp/templates/myapp $ nano index.html 
```
## Copy static files
```
pi@raspberrypi:~/mycpu/myapp/templates/myapp $ cd ~/mycpu/myapp/static/
pi@raspberrypi:~/mycpu/myapp/static $ ls
favicon.ico  myapp
pi@raspberrypi:~/mycpu/myapp/static $ cd myapp/
pi@raspberrypi:~/mycpu/myapp/static/myapp $ ls
bootstrap.min.css  bootstrap.min.js  jquery.min.js  script.js
```
## Create superuser and run
```
pi@raspberrypi:~/mycpu $ python manage.py runserver
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
May 02, 2023 - 15:02:57
Django version 4.2, using settings 'mycpu.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.

[02/May/2023 15:03:00] "GET /dt/1/ HTTP/1.1" 200 51
[02/May/2023 15:03:01] "GET /mem/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:02] "GET /cpu/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:11] "GET /dt/1/ HTTP/1.1" 200 51
[02/May/2023 15:03:11] "GET /mem/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:12] "GET /cpu/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:12] "GET /home/ HTTP/1.1" 200 1635
[02/May/2023 15:03:12] "GET /static/myapp/bootstrap.min.css HTTP/1.1" 304 0
[02/May/2023 15:03:12] "GET /static/myapp/jquery.min.js HTTP/1.1" 304 0
[02/May/2023 15:03:12] "GET /static/myapp/bootstrap.min.js HTTP/1.1" 304 0
[02/May/2023 15:03:13] "GET /favicon.ico HTTP/1.1" 302 0
[02/May/2023 15:03:24] "GET /dt/1/ HTTP/1.1" 200 51
[02/May/2023 15:03:25] "GET /mem/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:26] "GET /home/ HTTP/1.1" 200 1635
[02/May/2023 15:03:26] "GET /cpu/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:26] "GET /favicon.ico HTTP/1.1" 302 0
Forbidden: /dt/1/
[02/May/2023 15:03:32] "PUT /dt/1/ HTTP/1.1" 403 39
Forbidden: /mem/1/
[02/May/2023 15:03:32] "PUT /mem/1/ HTTP/1.1" 403 39
Forbidden: /cpu/1/
[02/May/2023 15:03:33] "PUT /cpu/1/ HTTP/1.1" 403 39
[02/May/2023 15:03:34] "GET /dt/1/ HTTP/1.1" 200 51
[02/May/2023 15:03:35] "GET /mem/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:36] "GET /cpu/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:37] "GET /dt/1/ HTTP/1.1" 200 51
[02/May/2023 15:03:38] "GET /mem/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:38] "GET /cpu/1/ HTTP/1.1" 200 50
[02/May/2023 15:03:38] "GET /home/ HTTP/1.1" 200 1635
[02/May/2023 15:03:39] "GET /favicon.ico HTTP/1.1" 302 0
Forbidden: /dt/1/
[02/May/2023 15:03:44] "PUT /dt/1/ HTTP/1.1" 403 39
Forbidden: /mem/1/
[02/May/2023 15:03:45] "PUT /mem/1/ HTTP/1.1" 403 39
Forbidden: /cpu/1/
[02/May/2023 15:03:46] "PUT /cpu/1/ HTTP/1.1" 403 39
[02/May/2023 15:03:50] "GET /dt/1/ HTTP/1.1" 200 51
[02/May/2023 15:03:50] "GET /mem/1/ HTTP/1.1" 200 50
```
This is a screenshot of the website
![MyCPU](MyCpu.PNG)