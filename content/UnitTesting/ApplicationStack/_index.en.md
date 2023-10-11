---
title: Application Stack
tags : ["Composing"]
---

## OS Details
CentOS version 7.latest

## Application Stack
|Application Name|Reference Links|
|----------------|---------------|
|HA Proxy| Latest Version |
|Open JDK| Latest Version |
|Tomcat|Latest Version|
|Percona XtraDB|Latest Version|
|ScyllaDB|Latest Version|
|Redpanda|Latest Version|

### HA Proxy

{{% notice info %}}
Please check the latest version at [HA Proxy Website](http://www.haproxy.org/)
{{% /notice %}}

Find the following instructions to install the HA Proxy
```
sudo groupadd haproxy
sudo useradd -r haproxy -g haproxy
```

```
yum -y install wget tar gcc make binutils pcre-devel pcre2-devel.x86_64 openssl-devel zlib-devel selinux-policy-devel systemd-devel readline- devel systemd-devel lua lua-devel
```
```
mkdir -p /etc/haproxy/errors
```
```
cd /opt
```
```
wget http://www.haproxy.org/download/2.1/src/haproxy-2.1.3.tar.gz 
tar -xvzf haproxy-2.1.3.tar.gz
cd haproxy-2.1.3
```
```
make -j5 USE_SYSTEMD=1 USE_REGPARM=1 USE_PCRE_JIT=1 TARGET=generic USE_THREAD=1 USE_LINUX_TPROXY=1 USE_TFO=1 CPU=generic USE_PCRE=1 USE_OPENSSL=1 USE_ZLIB=1
make install
```
```
cd contrib/systemd
make
cp haproxy.service /lib/systemd/system/haproxy.service
```
```
systemctl daemon-reload
```
```
useradd haproxy
```
```
systemctl enable haproxy.service
```
```
cd ../../
cp examples/errorfiles/* /etc/haproxy/errors/
```
```
mkdir /etc/ssl/xip.io
```

Create or Edit the file 
```
vi /etc/haproxy/haproxy.cfg
```

```
global
  maxconn 1028
  daemon
  user haproxy
  group haproxy
defaults
  timeout connect 5000ms
  timeout client 50000ms
  timeout server 50000ms
frontend https_443_frontend
bind *:443 ssl crt /etc/ssl/xip.io/xip.io.pem
mode http
option forwardfor
option http-server-close
option httpclose
default_backend http_8181_backend
backend http_8181_backend 
  mode http
  balance roundrobin
  timeout connect 5s
  timeout server 30s
  server app01 127.0.0.1:8181
```

Create a file /etc/ssl/xip.io/xip.io.pem

```
vi /etc/ssl/xip.io/xip.io.pem
```


```
-----BEGIN CERTIFICATE-----
MIIGbjCCBVagAwIBAgISBPSZHB/3ajlPPY8AGOYFRRu/MA0GCSqGSIb3DQEBCwUA
MEoxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MSMwIQYDVQQD
ExpMZXQncyBFbmNyeXB0IEF1dGhvcml0eSBYMzAeFw0yMDAzMjkxNDI5MzVaFw0y
MDA2MjcxNDI5MzVaMCYxJDAiBgNVBAMTG2dyYW1zZXZhay50ZWxhbmdhbmEuZ292
OS5pbjCCAiIwDQYJKoZIhvcNAQEBBQADggIPADCCAgoCggIBAK7DERPtH2uQlThG
OkV56869EnzAILiJN8D6wMFd0+oBVo46B2wWCJWRwAkuNii4yN0CRoDmrQWr9AeQ
rqhi7Yk77RElduW8fMewqzCQmiVD4xHBCr3vkkqUzGk5fTdE/nMk9l6PhE+eqowu
nPjOenRbnyFA3kegXhIreafoYpNluAW/X3h8Y6L2IB4X1ob/82rqD6LJV6E1OUmh
zY+1KzQ/DthKnplqKwWMACnjrc2FCp0xbSFyGXt+w0hOurdwQB/HZqPq41cOHCyJ
VOR4fNCvKeKW6g4dRW6vmApEqvRj19qunmzVYmFEZvnojd2QFxmUXsRRZzby0T5V
9RQbz6vJI57mbQ4AtjcoVyrKy3Xm5lumcdIFe4jjNSt81pCJvL6jMcu0TB6Rr7ZP
3T6ffCwLpYRsshalbROSHXqkuyyqMNQVeRHdVevQqJnL8iZ6nkxVmT5VavZ4DFzZ
u8mRmKWFt8AjbZM+NyGImTvSTFc3zdDl9Yz5Z3aKquOln3swGZ8uDMpkSKn34YNe
nEXsapDPNJrKCu7dThYumheQaGTTiz92eY/Jvic3gqK/pFeeoVuD6bKE9NozI/jg
UfNn3n/O4nL5ZcAWKbKAqMSPZWzV8oZ94Smi6xt++W6RsjGMwtIeUEReuErwbLlh
x/SVz5f+9cgqlNrowiEtzOBsbk/5AgMBAAGjggJwMIICbDAOBgNVHQ8BAf8EBAMC
BaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMAwGA1UdEwEB/wQCMAAw
HQYDVR0OBBYEFNmJi5YujDv95DuZiTUrjZFKFuwuMB8GA1UdIwQYMBaAFKhKamME
fd265tE5t6ZFZe/zqOyhMG8GCCsGAQUFBwEBBGMwYTAuBggrBgEFBQcwAYYiaHR0
cDovL29jc3AuaW50LXgzLmxldHNlbmNyeXB0Lm9yZzAvBggrBgEFBQcwAoYjaHR0
cDovL2NlcnQuaW50LXgzLmxldHNlbmNyeXB0Lm9yZy8wJgYDVR0RBB8wHYIbZ3Jh
bXNldmFrLnRlbGFuZ2FuYS5nb3Y5LmluMEwGA1UdIARFMEMwCAYGZ4EMAQIBMDcG
CysGAQQBgt8TAQEBMCgwJgYIKwYBBQUHAgEWGmh0dHA6Ly9jcHMubGV0c2VuY3J5
cHQub3JnMIIBBAYKKwYBBAHWeQIEAgSB9QSB8gDwAHYA5xLysDd+GmL7jskMYYTx
6ns3y1YdESZb8+DzS/JBVG4AAAFxJumasgAABAMARzBFAiEAscogQ0B0tdR9Ox0Q
G3QyRtbIGrdt6fWEAyvy1cjPFnwCIGH7WYPpwrR+12sBxWGVL/uWBn2tfSGSRYmI
nfA0BOn0AHYAsh4FzIuizYogTodm+Su5iiUgZ2va+nDnsklTLe+LkF4AAAFxJuma
qAAABAMARzBFAiEA+3RF+xr5zKhyYM0yxAHDzf38oBzEgNtGnebGXvzYcm4CIErf
tnAAfTzqWnLfqVx0mYczzKQRieOo9sjA9jHM6LffMA0GCSqGSIb3DQEBCwUAA4IB
AQBnp3NueOdf/Zpoqw+o3tEPd/cqY2VisA+hJ5qFx+3u4P8rO9m4u1+o8Yf40I3q
tLCX+dtkSnBJHzDtHnSdPjjRFhqgogCLj6gaFEbh+Apq2grhzabzR9oZcrTXWtuf
A5B4mWuyO6hhNcB42r0/UPu/E1Tq4pNny0w8NaoZFUzdDdv2l0w2lwPFHOu09MwM
UccVXaALxhnaRVVR3LdefKrWpW8ZvMF81sYbnNnCP9ogZHnwiGHOD3uSxsOeWuOL
qSSor6a6BJtI9sIW1y1KIjqVPe7qpwIdiJ5Gsf/NpTWakqJuqsTodUhSUcCRado3
qR3ZhiVNBbKanOIC9EC0fINE
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
MIIEkjCCA3qgAwIBAgIQCgFBQgAAAVOFc2oLheynCDANBgkqhkiG9w0BAQsFADA/
MSQwIgYDVQQKExtEaWdpdGFsIFNpZ25hdHVyZSBUcnVzdCBDby4xFzAVBgNVBAMT
DkRTVCBSb290IENBIFgzMB4XDTE2MDMxNzE2NDA0NloXDTIxMDMxNzE2NDA0Nlow
SjELMAkGA1UEBhMCVVMxFjAUBgNVBAoTDUxldCdzIEVuY3J5cHQxIzAhBgNVBAMT
GkxldCdzIEVuY3J5cHQgQXV0aG9yaXR5IFgzMIIBIjANBgkqhkiG9w0BAQEFAAOC
AQ8AMIIBCgKCAQEAnNMM8FrlLke3cl03g7NoYzDq1zUmGSXhvb418XCSL7e4S0EF
q6meNQhY7LEqxGiHC6PjdeTm86dicbp5gWAf15Gan/PQeGdxyGkOlZHP/uaZ6WA8
SMx+yk13EiSdRxta67nsHjcAHJyse6cF6s5K671B5TaYucv9bTyWaN8jKkKQDIZ0
Z8h/pZq4UmEUEz9l6YKHy9v6Dlb2honzhT+Xhq+w3Brvaw2VFn3EK6BlspkENnWA
a6xK8xuQSXgvopZPKiAlKQTGdMDQMc2PMTiVFrqoM7hD8bEfwzB/onkxEz0tNvjj
/PIzark5McWvxI0NHWQWM6r6hCm21AvA2H3DkwIDAQABo4IBfTCCAXkwEgYDVR0T
AQH/BAgwBgEB/wIBADAOBgNVHQ8BAf8EBAMCAYYwfwYIKwYBBQUHAQEEczBxMDIG
CCsGAQUFBzABhiZodHRwOi8vaXNyZy50cnVzdGlkLm9jc3AuaWRlbnRydXN0LmNv
bTA7BggrBgEFBQcwAoYvaHR0cDovL2FwcHMuaWRlbnRydXN0LmNvbS9yb290cy9k
c3Ryb290Y2F4My5wN2MwHwYDVR0jBBgwFoAUxKexpHsscfrb4UuQdf/EFWCFiRAw
VAYDVR0gBE0wSzAIBgZngQwBAgEwPwYLKwYBBAGC3xMBAQEwMDAuBggrBgEFBQcC
ARYiaHR0cDovL2Nwcy5yb290LXgxLmxldHNlbmNyeXB0Lm9yZzA8BgNVHR8ENTAz
MDGgL6AthitodHRwOi8vY3JsLmlkZW50cnVzdC5jb20vRFNUUk9PVENBWDNDUkwu
Y3JsMB0GA1UdDgQWBBSoSmpjBH3duubRObemRWXv86jsoTANBgkqhkiG9w0BAQsF
AAOCAQEA3TPXEfNjWDjdGBX7CVW+dla5cEilaUcne8IkCJLxWh9KEik3JHRRHGJo
uM2VcGfl96S8TihRzZvoroed6ti6WqEBmtzw3Wodatg+VyOeph4EYpr/1wXKtx8/
wApIvJSwtmVi4MFU5aMqrSDE6ea73Mj2tcMyo5jMd6jmeWUHK8so/joWUoHOUgwu
X4Po1QYz+3dszkDqMp4fklxBwXRsW10KXzPMTZ+sOPAveyxindmjkW8lGy+QsRlG
PfZ+G6Z6h7mjem0Y+iWlkYcV4PIWL1iwBi8saCbGS5jN2p8M+X+Q7UNKEkROb3N6
KOqkqm57TH2H3eDJAkSnh6/DNFu0Qg==
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
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
-----END RSA PRIVATE KEY-----


```

```
systemctl start haproxy.service
```
```
netstat -anpt | grep LIST
```

### Install OpenJDK11
```
yum -y install java-11-openjdk java-11-openjdk-devel
```
```
cat > /etc/profile.d/java11.sh <<EOF
export JAVA_HOME=$(dirname $(dirname $(readlink $(readlink $(which javac)))))
export PATH=\$PATH:\$JAVA_HOME/bin
EOF
```
```
source /etc/profile.d/java11.sh
java --version
```
### Install Tomcat
```
sudo groupadd tomcat
sudo useradd -M -s /bin/nologin -g tomcat -d /opt/tomcat tomcat
```
```
sudo mkdir /opt/tomcat
cd /opt
wget https://mirrors.estointernet.in/apache/tomcat/tomcat-9/v9.0.44/bin/apache-tomcat-9.0.44.tar.gz
tar xvf apache-tomcat-*tar.gz -C /opt/tomcat --strip-components=1
cd /opt/tomcat
chgrp -R tomcat /opt/tomcat
chmod -R g+r conf
chmod g+x conf
chown -R tomcat webapps/ work/ temp/ logs/
```

{{% notice info %}}
Please modify the /opt/tomcat/bin/catalina.sh
Replace following line CLASSPATH="$CLASSPATH""$CATALINA_HOME"/bin/bootstrap.jar: 
with
CLASSPATH="$CLASSPATH""$CATALINA_HOME"/bin/bootstrap.jar:$CATALINA_HOME/log4j2/lib/*:$CATALINA_HOME/log4j2/conf
{{% /notice %}}

create a file at /etc/systemd/system/tomcat.service
```
vi /etc/systemd/system/tomcat.service
```
```
# Systemd unit file for tomcat
[Unit]
Description=Apache Tomcat Web Application Container 
After=syslog.target network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment=JAVA_HOME=/usr/lib/jvm/jre 
Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:////dev/urandom'

Environment=CATALINA_BASE=/opt/tomcat 
Environment=CATALINA_HOME=/opt/tomcat 
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid 
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'

ExecStart=/opt/tomcat/bin/startup.sh ExecStop=/bin/kill -15 $MAINPID
ExecStop=/opt/tomcat/bin/shutdown.sh

UMask=0007
RestartSec=10
Restart=always

[Install] 
WantedBy=multi-user.target
```

```
systemctl daemon-reload 
```
```
systemctl start tomcat 
```
```
systemctl status tomcat 
```
```
systemctl enable tomcat
```

### Percona XtraDB Cluster
{{% notice info %}}
Please check the latest version at [Percona Website](https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/apt.html)
{{% /notice %}}

{{% notice info %}}
Open the TCPv4ports though the firewall : 3306, 4444, 4567, 4568
{{% /notice %}}

```
firewall-cmd --zone=public --add-port=3306/tcp --permanent
firewall-cmd --zone=public --add-port=4444/tcp --permanent
firewall-cmd --zone=public --add-port=4567/tcp --permanent
firewall-cmd --zone=public --add-port=4568/tcp --permanent

systemctl restart firewalld
firewall-cmd --list-all
```

Install YUM Reporsitories
```
sudo yum -y install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
sudo percona-release enable pxc-80
sudo yum -y install percona-xtradb-cluster
```
```
sudo service mysql start
```
```
sudo grep 'temporary password' /var/log/mysqld.log
```

Capture the password from the above command output and change the password with the following commands
Output of the command similar to the following
{{% notice info %}}
2021-03-13T07:53:10.901419Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: Rp=B3zrY?d.F
{{% /notice %}}

```
mysql -uroot -p <Enter the password cpature from the above command>
ALTER USER 'root'@'localhost' IDENTIFIED BY '1!QMysqlRoot';
FLUSH PRIVILEGES;
exit
```

#### Configuring Nodes for Write-Set Replication
{{% notice info %}}
Please check the latest version at [Percona Website](https://www.percona.com/doc/percona-xtradb-cluster/LATEST/configure.html)
{{% /notice %}}

After installing Percona XtraDB Cluster on each node, you need to configure the cluster. In this section, we will demonstrate how to configure a three node cluster:

|Node|Host|IP|
|----|----|--|
|node1|gsts-sdc-01|192.168.165.216|
|node2|gsts-sdc-02|192.168.165.210|
|node3|gsts-sdc-03|192.168.165.222|

+ Stop the Percona XtraDB Cluster server. After the installation completes the server is not started. You need this step if you have started the server manually.
```
sudo service mysql stop
```
+ Edit the configuration file of the first node to provide the cluster settings. Edit /etc/my.cnf
```
wsrep_provider=/usr/lib64/galera4/libgalera_smm.so
wsrep_cluster_name=gsts_erdb_cluster
wsrep_cluster_address=gcomm://192.168.165.216,192.168.165.210,192.168.165.222
```
+ Configure node1, add the following to the above file
```
wsrep_node_name=gsts_erdb_node01
wsrep_node_address=192.168.165.216
pxc_strict_mode=ENFORCING
```
+ Configure node2, add the following to the above file
```
wsrep_node_name=gsts_erdb_node02
wsrep_node_address=192.168.165.210
pxc_strict_mode=ENFORCING
```
+ Configure node3, add the following to the above file
```
wsrep_node_name=gsts_erdb_node03
wsrep_node_address=192.168.165.222
pxc_strict_mode=ENFORCING
```

{{% notice info %}}
If you must disable pxc-encrypt-cluster-traffic, you need to stop the cluster and update [mysqld] section of the configuration file: **pxc-encrypt-cluster-traffic=OFF** of each node of /etc/my.cnf. Then, restart the cluster.
{{% /notice %}}

#### Bootstrapping the First Node
After you configure all PXC nodes, initialize the cluster by bootstrapping the first node. The initial node must contain all the data that you want to be replicated to other nodes.
Bootstrapping implies starting the first node without any known cluster addresses: if the wsrep_cluster_address variable is empty, Percona XtraDB Cluster assumes that this is the first node and initializes the cluster.
Instead of changing the configuration, start the first node using the following command:
```
systemctl start mysql@bootstrap.service

```
When you start the node using the previous command, it runs in bootstrap mode with wsrep_cluster_address=gcomm://. This tells the node to initialize the cluster with wsrep_cluster_conf_id set to 1. After you add other nodes to the cluster, you can then restart this node as normal, and it will use standard configuration again.
To make sure that the cluster has been initialized, run the following & validate the parameters.

```
mysql@pxc1> show status like 'wsrep%';
```
| Variable_name              | Value                                |
|----------------------------|--------------------------------------|
| wsrep_local_state_uuid     | c2883338-834d-11e2-0800-03c9c68e41ec |
| wsrep_local_state          | 4                                    |
| wsrep_local_state_comment  | Synced                               |
| wsrep_cluster_size         | 1                                    |
| wsrep_cluster_status       | Primary                              |
| wsrep_connected            | ON                                   |
| wsrep_ready                | ON                                   |


The previous output shows that the cluster size is 1 node, it is the primary component, the node is in the Synced state, it is fully connected and ready for write-set replication.

#### Adding Nodes to Cluster
New nodes that are properly configured are provisioned automatically. When you start a node with the address of at least one other running node in the **wsrep_cluster_address** variable, this node automatically joins and synchronizes with the cluster.

{{% notice info %}}
Any existing data and configuration will be overwritten to match the data and configuration of the DONOR node. Do not join several nodes at the same time to avoid overhead due to large amounts of traffic when a new node joins.
Percona XtraDB Cluster uses Percona XtraBackup for State Snapshot Transfer and the wsrep_sst_method variable is always set to **xtrabackup-v2**
{{% /notice %}}

##### Starting the Second Node
Start the second node using the following command:
```
systemctl start mysql
```
After the server starts, it receives SST automatically.

To check the status of the second node, run the following query in the MySQL CLi:
```
show status like 'wsrep%';
```

| Variable_name                    | Value                                            |
|----------------------------------|--------------------------------------------------|
| wsrep_local_state_uuid           | a08247c1-5807-11ea-b285-e3a50c8efb41             |
| wsrep_local_state                | 4                                                |
| wsrep_local_state_comment        | Synced                                           |
| wsrep_cluster_size               | 2                                                |
| wsrep_cluster_status             | Primary                                          |
| wsrep_connected                  | ON                                               |
| wsrep_provider_capabilities      | :MULTI_MASTER:CERTIFICATION: ...                 |
| wsrep_provider_name              | Galera                                           |
| wsrep_provider_vendor            | Codership Oy <info@codership.com>                |
| wsrep_provider_version           | 4.3(r752664d)                                    |
| wsrep_ready                      | ON                                               |

The output of SHOW STATUS shows that the new node has been successfully added to the cluster. The cluster size is now 2 nodes, it is the primary component, and it is fully connected and ready to receive write-set replication.

If the state of the second node is Synced as in the previous example, then the node received full SST is synchronized with the cluster, and you can proceed to add the next node.


##### Starting the Third Node
Start the second node using the following command:
```
systemctl start mysql
```
After the server starts, it receives SST automatically.

To check the status of the second node, run the following query in the MySQL CLi:
```
show status like 'wsrep%';
```

| Variable_name                    | Value                                            |
|----------------------------------|--------------------------------------------------|
| wsrep_local_state_uuid           | a08247c1-5807-11ea-b285-e3a50c8efb41             |
| wsrep_local_state                | 4                                                |
| wsrep_local_state_comment        | Synced                                           |
| wsrep_cluster_size               | 2                                                |
| wsrep_cluster_status             | Primary                                          |
| wsrep_connected                  | ON                                               |
| wsrep_provider_capabilities      | :MULTI_MASTER:CERTIFICATION: ...                 |
| wsrep_provider_name              | Galera                                           |
| wsrep_provider_vendor            | Codership Oy <info@codership.com>                |
| wsrep_provider_version           | 4.3(r752664d)                                    |
| wsrep_ready                      | ON                                               |

The output of SHOW STATUS shows that the new node has been successfully added to the cluster. The cluster size is now 2 nodes, it is the primary component, and it is fully connected and ready to receive write-set replication.

If the state of the second node is Synced as in the previous example, then the node received full SST is synchronized with the cluster, and you can proceed to add the next node.

##### Restarting the First node as Clusternode
Now, we need to restart the First node as cluster node using the following commands
```
systemctl stop mysql@bootstrap.service
```
```
systemctl start mysql
```

### Redpanda Installation
Use the latest installer script to install the Redpanda [Website](https://vectorized.io/redpanda/)

```
curl -1sLf 'https://packages.vectorized.io/nzc4ZYQK3WRGd9sy/redpanda/cfg/setup/bash.rpm.sh' | sudo -E bash && sudo yum install redpanda -y
```

Then Enable Redpanda

```
systemctl enable redpanda
```

#### Configure and Start the Root Node
Now that the software is installed we need to configure it. The first step is to setup the root node. The root node will start as a standalone node, and every other one will join it, forming a cluster along the way.

For the root node we’ll choose 0 as its ID. --self tells the node which interface address to bind to. Usually you want that to be its private IP.

```
sudo rpk config bootstrap --id 0 --self 192.168.165.216 && sudo systemctl start redpanda-tuner redpanda
```

#### Configure and Start the Rest of the Nodes
For every other node, we just have to choose a unique integer id for it and let it know where to reach the root node.
```
sudo rpk config bootstrap --id 2 --self 192.168.165.210 --ips 192.168.165.210,192.168.165.216,192.168.165.222 &&  sudo systemctl start redpanda-tuner redpanda
```

```
sudo rpk config bootstrap --id 3 --self 192.168.165.222 --ips 192.168.165.210,192.168.165.216,192.168.165.222 &&  sudo systemctl start redpanda-tuner redpanda
```


#### Verify Installation
Check the following command verify the cluster connectivity
```
rpk cluster info
```

{{% notice info %}}
The the output of the above should as follows
[root@gsts-sdc-03 ~]# rpk cluster info
  Redpanda Cluster Info                      
  0 (192.168.165.216:9092)  (No partitions)  
  2 (192.168.165.210:9092)  (No partitions)  
  3 (192.168.165.222:9092)  (No partitions)  
{{% /notice %}}

### ScyllaDB Installation
Use the latest installer script to install the Redpanda [Website](https://www.scylladb.com/download/)

Add the following package repo
```
sudo curl -o /etc/yum.repos.d/scylla.repo -L http://repositories.scylladb.com/scylla/repo/57ddf75b-c51c-4904-a8d2-8e19a7cc1d02/centos/scylladb-4.0.repo
```

Install the ScyllaDB version
```
sudo yum install scylla
```

Enable Developer mode
```
scylla_dev_mode_setup --developer-mode 1
```

#### Configure Scyalladb
|Parameter|Value|Descr|
|---------|-----|-----|
|cluster_name|gspod-ts|Name of the cluster, all the nodes in the cluster must have the same name|
|seeds|ip1,ip2,...|Seed nodes are used during startup to bootstrap the gossip process and join the cluster|
|listen_address|IP of the Host|IP address that Scylla uses to connect to other Scylla nodes in the cluster|
|rpc_address|IP of the Host|IP address of the interface for client connections (Thrift, CQL)|
|dc|gsts_pdc|Name of the datacenter|
|rack|gsts_pdc_rack01|Name of the Rack|


#### valodate the Cluster installation
Run the following command
```
nodetool status
```


{{% children  %}}
