The Fascinator
==============

Please visit our [Public site](https://sites.google.com/site/fascinatorhome/)

A [release history](release-history.md) is available.

Note: Currently two development projects are beign carried out on the fascinator for CrateIt feature and some customizations related to Mint hence there are two branches called curateit and mint. To build and play with either of them, follow the instructions as mentioned below.

Fascinator Installation
=======================

Prerequisites
-------------

  You need to have the Git client, Java 7 and Maven2 (recommended Maven 2.2.1) software installed. On Ubuntu this can be done using apt-get:<br>
  sudo apt-get install git-core openjdk-7-jdk maven2</br>
  
  Then replace the content of the maven settings file located at /etc/maven2 with the following. Please note the proxy settings are for UWS. Change them accordingly.
  
    <?xml version="1.0" encoding="UTF-8"?>
    <settings xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <proxies>

    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <host>proxy.uws.edu.au</host>
      <port>3128</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    </proxies>

    <profiles>
      <profile>
      <id>alwaysActiveProfile</id>
      <repositories>
	       <repository>
		       <id>ReDBoxNexus</id>
		       <name>ReDBox Community Nexus Server</name>
		       <url>http://dev.redboxresearchdata.com.au/nexus/content/groups/public/</url>
	      </repository>
	    </repositories>
      </profile>
    </profiles>
      <activeProfiles>
        <activeProfile>alwaysActiveProfile</activeProfile>
      </activeProfiles>
    </settings>
  
Installation
------------

1. First create a directory to keep the repository and switch to it:<br>
   mkdir /opt/fascinator </br><br>
   chown -R $User:$User /opt/fascinator</br><br>
   cd /opt/fascinator</br>
2. Clone the-fascinator repository from git@github.com:uws-eresearch/the-fascinator.git:<br>
   git clone git@github.com:uws-eresearch/the-fascinator.git</br>
3. Switch to the branch you want to build:<br>
   git checkout curatelt</br>
4. Build the downloaded source using maven:<br>
   mvn clean install</br>
  
This should build the fascinator and once it's successful, start the server using the tf.sh script:<br>
  ./tf.sh start</br>

Upgrading
---------

If you have an existing fascinator installation and want to upgrade it to the latest version, follow the below instructions.

1. Go to fascinator home directory(~/.fascinator in linux platform) and delete the existing system-config.json file
2. Assuming that the existing repository is used to upgrade, change to that directory:<br>
   cd /opt/fascinator</br>
3. Pull the latest version from github:<br>
   git pull origin curatelt</br>
4. Switch to the branch you want to build:<br>
   git checkout curatelt</br>
5. Build the latest version from source using maven:<br>
   mvn clean install</br>

Fascinator Configuration
========================

General configuration
---------------------

For the general configuration of the fascinator go to the [fascinator configuration](https://sites.google.com/site/fascinatorhome/home/documentation/technical/configuration)

File Harvester Configuration
----------------------------
1. In system-config.json, locate<br>
   
   "permissions" : {
	"path" : "${fascinator.home}/security/permissions.json",
	"useDirectoryAccess" : true,
	"defaultAccess" : "admin"
    },

   Above section defines the path to the permissions file where users are assigned to various groups to which they have access. When "useDirectoryAccess" is true, 
   use top level directory names in the drive being harvested as group names. When it's false, all the files in the drive are considered as a whole bunch and assign "defaultAccess" value
   as the group name.
   
