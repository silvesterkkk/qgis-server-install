#QGIS Server and QGIS WebClient installation procedure (Based on Windows 7, August 2014)#




##CONTENTS##
* Installation
* Edit config file / Modify file extention
* QGIS server validation
* Download & install QGIS WebClient
* References

##Installation##

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

##Edit config file##

####1. EDIT httpd_qgis.conf####
:This is required because QGIS on windows seems not to work as FastCGI<br/>
  * Locate the following file and open in text editor.<br/>
    `c:\osgeo4w\httpd.d\httpd_qgis.conf`<br/>
  * Change the following lines of code<br/>
```
LoadModule fcgid_module modules/mod_fcgid.so
to
LoadModule cgi_module modules/mod_cgi.so
```
<br/>
```
DefaultInitEnv
to
SetEnv
```

####2. CHANGE qgis_mapserv.fcgi.exe####
: This is required because the QGIS WebClient which you will install later, can NOT address *.exe files, although 	the QGIS Server could.<br/>
  * Locate the following file.<br/>
    `c:\OSGeo4W\apps\qgis\bin\qgis_mapserv.fcgi.exe`<br/>
  * Delete the extention of the file so that it looks like the following.<br/>
    `c:\OSGeo4W\apps\qgis\bin\qgis_mapserv.fcgi`

###QGIS server validation###
: This step will validate the installation of QGIS server.<br/>
  * Type the following URL to your web browser.<br/>
    `http://localhost/qgis/qgis_mapserv.fcgi?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetCapabilities`
  * If you receive XML formatted information on your browser, this means your QGIS server has been installed correctly.<br/>
  * (OPTIONAL) You will receive a map image by sending `GetMap` request  as URL shown below (if you have a QGIS project on your machine).<br/>
    `http://localhost/qgis/qgis_mapserv.fcgi?SERVICE=WMS&VERSION=1.3.0&SRS=EPSG:31467&REQUEST=GetMap&map=C:/path-to-a-simple-qgis-project.qgs&WIDTH=1000&HEIGHT=800&LAYERS=weg,bach&FORMAT=image/png`
  
###Download and install QGIS WebClient###
####1. What is QGIS WebClient & why do you need it?####
  * Under construction

####2. Download QGIS WebClient####
  * Go to the following GitHub site: https://github.com/qgis/QGIS-Web-Client
  * Download the project as ZIP file (there is a link to your right pane).
  * Unzip the file to the following location.
    `c:\OSGeo4W\apache\htdocs`
  * So you now have the QGIS WebClient files in: <br/>
    `c:\OSGeo4W\apache\htdocs\QGIS-Web-Client-master`

####3. Edit config file ####
  * Locate the following file and open in the text editor.
    `C:\OSGeo4W\apache\conf\httpd.conf`
  * Go to the line 324 (approx.), and change the line of code as follows.
```
ScriptAlias /cgi-bin/ "C:\OSGeo4W/bin/"
to
ScriptAlias /cgi-bin/ "C:\OSGeo4W/apps/qgis/bin/"
```
####4. Restart Apache####
  * You need to restart Apache everytime you make changes to the Apache config file.
  * You can do this by:
    `START MENU --> Programs --> OSGeo4W --> Apache`

####5. Validate installation
  * Enter the following URL in your web browser.
    `http://localhost/QGIS-Web-Client-master/site/index.html`
  * You will end up in the QGIS WebClient Default Client Landing Page. This means you have installed it correctly.
  * If you have your own QGIS project on your machine, you can edit the above URL to point it to the project like:
    `http://localhost/QGIS-Web-Client-master/site/qgiswebclient.html?map=C:/OSGeo4W/apache/htdocs/QGIS-Web-Client-master/projects/helloworld.qgs`



##References##
  * http://anitagraser.com/2012/04/06/qgis-server-on-windows7-step-by-step/
  * http://osgeo-org.1560.x6.nabble.com/QGIS-Web-Client-for-Windows-7-td5128712.html


[HERE]:https://www.qgis.org/en/site/forusers/download.html
