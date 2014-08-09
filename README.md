qgis-server-installation procedure (Based on Windows 7, August 2014)
===================

This instruction is constructed from resources available on the web.

CONTENTS
- Installation
- Edit config file

Installation
------------
(This is based on the instruction from the following site:
http://anitagraser.com/2012/04/06/qgis-server-on-windows7-step-by-step/)

1. Download OSGeo4W installer from [HERE]
2. I have downloaded the 32-bit version although running a 64-bit machine.
3. Execute the file and follow the prompt.
  - Select advanced Install, **NEXT**
  - Select Install from internet, **NEXT**
  - Accept the default (unless you want to change), **NEXT**
  - Accept the default (unless you want to change), **NEXT**
  - Select connection option (I've used 'Direct connection'), **NEXT**
  - Select available download sites: Should only one available **NEXT**
  - Once you get to the 'Select packages' window, select the following options (All other dependencies will be automatically selected and installed).
    - Under DESKTOP, select `qgis: QGIS Desktop` & `qgis-dev: QGIS nightly build of the master`
    ![alt text](https://cloud.githubusercontent.com/assets/8164012/3790271/e8c9bb06-1af4-11e4-9ee7-fa122374970e.png)
    - Under WEB, select `Apache Webserver` & `qgis-server: QGIS Server`
    ![alt text](https://cloud.githubusercontent.com/assets/8164012/3790272/eaf76838-1af4-11e4-9e37-f5f15b76eec8.png)

Edit config file
----------------

1. EDIT httpd_qgis.conf:<br/>
   This is required because QGIS on windows seems not to work as FastCGI<br/>
	1.1 Locate the following file and open in text editor.<br/>
   	`c:/osgeo4w/httpd.d/httpd_qgis.conf`<br/>
	
	1.2 Change the following lines of code
	```
	LoadModule fcgid_module modules/mod_fcgid.so
	to
	LoadModule cgi_module modules/mod_cgi.so
	```
	```
	DefaultInitEnv
	to
	SetEnv
	```

2. Locate the following file <br/> `C:\OSGeo4W\apps\qgis\bin\qgis_mapserv.fcgi.exe`<br/>
   
	```
	This is required because the QGIS WebClient which you will install later, can NOT address *.exe files, although 	the QGIS Server could.
	
	

[HERE]:https://www.qgis.org/en/site/forusers/download.html
