---
title: Jenkins Installation
tags : ["Installation Process"]

---

## Install Jenkins on Oracle Linux


### Prerequisites

#### Install Java on Oracle linux
For Jenkins to function, you need to install either Java JRE 8 or Java 11. In the example below, we decided to go with the installation of Java 11. Therefore, to install Java 11, run the command.

```
dnf install java-11-openjdk-devel
```
To verify the installation of Java 11, run the command.

```
java --version
```
The output confirms that Java 11 has been successfully installed.

````
openjdk version "11.0.13" 2021-10-19
OpenJDK Runtime Environment (build 11.0.13+8-Ubuntu-0ubuntu1.20.04)
OpenJDK 64-Bit Server VM (build 11.0.13+8-Ubuntu-0ubuntu1.20.04, mixed mode, sharing)
````

#### Add Jenkins Repository on Oracle linux
Since Jenkins is not available in Oracle linux repositories, therefore we are going to add Jenkins Repository manually to the system.

Begin by adding Jenkins Key as shown.
```
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
Now append Jenkin’s repository to Oracle linux.

```
cd /etc/yum/repos.d/
curl -O https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
### Install Jenkins on Oracle linux



Having successfully added Jenkins repository, you can proceed to install Jenkins by running. 
```
dnf install jenkins
```
![This is an image](https://www.tecmint.com/wp-content/uploads/2019/11/Install-Jenkins-on-CentOS-8.png)

Once installed, start and verify the status of Jenkins by executing the commands.
```
systemctl start jenkins
systemctl status jenkins
```
The output shows that Jenkins is up and running.

![This is an image](https://www.tecmint.com/wp-content/uploads/2019/11/Start-and-Verify-Jenkins-Status.png)


Next, you need to configure the firewall to allow access to port 8080 which is used by Jenkins. To open the port on the firewall, run the commands.
```
firewall-cmd --add-port=8080/tcp --permanent
firewall-cmd --reload
```
### Setting up Jenkins on Oracle linux

With the initial configurations done, the only remaining part is setting up Jenkins on a web browser. To achieve this, browse your server’s IP address as shown:```
dnf install docker-ce
```
http://server-IP:8080
```

The first section requires you to unlock Jenkins using a password. This password is placed in the file /var/lib/Jenkins/secrets/initialAdminPassword file.

```
cat /var/lib/Jenkins/secrets/initialAdminPassword
```
Copy& paste the password in the Administrator password text field & click ‘Continue‘.




