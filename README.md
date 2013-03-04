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
   chown -R lloyd:lloyd /opt/fascinator</br><br>
   cd /opt/fascinator</br>
2. Clone the-fascinator repository from git@github.com:uws-eresearch/the-fascinator.git:<br>
   git clone git@github.com:uws-eresearch/the-fascinator.git</br>
3. Build the downloaded source using maven:<br>
   mvn clean install</br>
  
This should build the fascinator and once it's successful, start the server using the tf.sh script:<br>
  ./tf.sh start</br>
