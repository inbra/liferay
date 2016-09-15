# LiferayIDE Setup

- __required:__ MySQL server installation
- __required:__ JDK 7 
- create folder "LiferayDev" on harddisk, e.g. `C:\LiferayDev` :exclamation: **important:** *keep the path short!*
- Download LiferayIDE (__v2.2.4GA5__) from [sourceforge.net](https://sourceforge.net/projects/lportal/files/Liferay%20IDE/2.2.4%20GA5/)
- Download the following files from [sourceforge.net]( https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.4%20GA5/)
 - [Liferay portal-Tomcat bundle](
https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.4%20GA5/liferay-portal-tomcat-6.2-ce-ga5-20151119152357409.zip/download)
 - [Liferay Plugin SDK](
https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.4%20GA5/liferay-plugins-sdk-6.2-ce-ga5-20151118111117117.zip/download) :exclamation: _optional, if later synchronization with GitLab will be done_
 - [Liferay source files](
https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.4%20GA5/liferay-portal-src-6.2-ce-ga5-20151118111117117.zip/download)
 - [Liferay Javadoc](
https://sourceforge.net/projects/lportal/files/Liferay%20Portal/6.2.4%20GA5/liferay-portal-doc-6.2-ce-ga5-20151118111117117.zip/download)
 
 - unzip everything  to folder, e.g. `C:\LiferayDev`
 - <u>rename</u> the following folders:
     - liferay-portal-tomcat-6.2-ce-ga5-20151119152357409 &rarr; __liferay-portal__
     - liferay-portal-src-6.2-ce-ga5-20151118111117117 &rarr; __portal-master__
     - liferay-portal-doc-6.2-ce-ga5-20151118111117117 &rarr; __portal-doc__
     - liferay-plugins-sdk-6.2-ce-ga5-20151118111117117 &rarr; __plugins-sdk__

- start the MySQL server
    - create a database, e.g. "acanto_cpsn"
    - create a new user and grant access to database (all access rights but 'grant option')
    - _remember_ username and password of the new user, we will need it later!
- start the LiferayIDE (eclipse.exe)
- go to Preferences → Liferay → Installed Plugin SDK
  - add liferay plugins SDK from the unzipped folder 
- go to Preferences → Server → Runtime Environments
  - add server "Liferay v6.2 (Tomcat 7)" pointing to folder of unzipped Liferay portal - tomcat, e.g.  `C:\LiferayDev\liferay-portal\tomcat-7.0.62`
  - do __not__ check _*create new server*_ checkbox

- go to server tab (Liferay view!!)
  - right click on newly created server "Liferay v6.2 CE Server (Tomcat 7)"
  - choose "create portal settings file" 
  - open (double click) portal-ext.properties and add following entries:
   `jdbc.default.url=jdbc\:mysql\://localhost/acanto_cpsn?useUnicode\=true&characterEncoding\=UTF-8&useFastDateParsing\=false`
   `jdbc.default.driverClassName=com.mysql.jdbc.Driver`
   `jdbc.default.username=liferay`
   `jdbc.default.password=mysecretpassword`

  - [_optional_] for first run augment startup-timeout
    `double click server "Liferay v6.2 CE Server (Tomcat 7)"`
    `open panel "Timeouts" on the right side and set Start to 1200 seconds`


- Download [JDBC-MySQL connector](
  http://dev.mysql.com/downloads/connector/j/)
 - unzip it somewhere and copy only the JAR file (`mysql-connector-java-5.1.38-bin.jar`) to the folder `C:\LiferayDev\liferay-portal-tomcat-6.2-ce-ga5\tomcat-7.0.62\lib\ext`
		

- __Apache Ivy__ issue:
     - check if Jar `org.apache.ivy-2.4.0.LIFERAY-PATCHED-1-SNAPSHOT.jar` exists in folder `C:\Users\[username]\.liferay\mirrors\cdn.repository.liferay.com\nexus\content\repositories\liferay-snapshots-ce\com\liferay\org.apache.ivy\2.4.0.LIFERAY-PATCHED-1-SNAPSHOT`(beware of Windows localized path name of `Users` folder, and with `[username]` being your Windows login name)
     - if folder is empty or does not exist download the jar from [**here**](https://repository.liferay.com/nexus/content/groups/public/com/liferay/org.apache.ivy/2.4.0.LIFERAY-PATCHED-1-SNAPSHOT/org.apache.ivy-2.4.0.LIFERAY-PATCHED-1-SNAPSHOT.jar) and place it into the folder

- (re-)publish, start server, ready for some work :)
