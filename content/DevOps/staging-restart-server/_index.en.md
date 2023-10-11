---
title: Staging Restart Servers
tags : ["Composing"]
---

## Mysql
We should not start the MySQL server in a random sequence
First check the configuration on the each node

```
cat /opt/mysql-data/mysql/grastate.dat
```
The output of the above command is as follows

```
[root@gsts1ship01 ~]# cat /opt/mysql-data/mysql/grastate.dat
# GALERA saved state
version: 2.1
uuid:    0fbaf102-ea0a-11eb-a7b6-9b73ccb714cd
seqno:   6950264
safe_to_bootstrap: 0
```

Find out the largest seqno value from all the nodes, then use that as a bootstrap node.
In this case it is gsts1ship01

Now, update the value to 1 for safe_to_bootstrap
Then, run the following command on gsts1ship01

```
systemctl start mysql@bootstrap.service
```
If it is successfully started, then start the mysql servers on all other nodes using the following commands

```
systemctl start mysqld
```
Once all the servers are started, then run the following commands on the Bootstratp node

```
mysql> show status like 'wsrep_incoming_addresses';
+--------------------------+----------------------------------------------------------------------------------------------------------+
| Variable_name            | Value                                                                                                    |
+--------------------------+----------------------------------------------------------------------------------------------------------+
| wsrep_incoming_addresses | gsts2ship02:3306,172.17.135.228:3306,gsts1ship01:3306,gsts1ship02:3306,gsts1ship03:3306,gsts2ship01:3306 |
+--------------------------+----------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)

mysql>
mysql> show status like 'wsrep_cluster_weight';
+----------------------+-------+
| Variable_name        | Value |
+----------------------+-------+
| wsrep_cluster_weight | 6     |
+----------------------+-------+
1 row in set (0.01 sec)
```

Validate the cluster size and Incoming IP Addresses


## Scylladb
Make sure we put all the in the 'seeds' in the file /etc/scylla/scylla.yaml
then restart/start scylladb in each node

```
systemctl start scylla-server
```

## Redpanda

First we need to Identify the Root node of the Redpanda

Run the following Cmd and check the value of "redpanda.node_id", it should be "0" for the Root node
```
rpk debug info
```
The output of the above query is something similar to the following

```
[root@gsts1ship01 ~]# rpk debug info
Omitting runtime metrics: the local redpanda process isn't running.
  Version                              v21.7.6 (rev f93eed1)
  OS                                   x86_64 5.4.17-2102.203.5.el8uek.x86_64 #2 SMP Mon Jun 28 16:44:26 PDT 2021
  CPU Model                            Intel(R) Xeon(R) Gold 6152 CPU @ 2.10GHz
  config_file                          /etc/redpanda/redpanda.yaml
  node_uuid                            SC6jMcvHHvvzA3z5Er5o2gRAhshiM3RyVFjdxyxSqDVVoXp4D
  pandaproxy
  redpanda.admin.0                     172.16.119.21:9644
  redpanda.auto_create_topics_enabled  true
  redpanda.data_directory              /opt/redpanda-data/data
  redpanda.developer_mode              true
  redpanda.kafka_api.0                 172.16.119.21:9092
  redpanda.node_id                     0
  redpanda.rpc_server                  172.16.119.21:33145
  rpk.coredump_dir                     /var/lib/redpanda/coredump
  rpk.enable_memory_locking            false
  rpk.enable_usage_stats               true
  rpk.overprovisioned                  false
  rpk.tune_aio_events                  false
  rpk.tune_clocksource                 false
  rpk.tune_coredump                    false
  rpk.tune_cpu                         false
  rpk.tune_disk_irq                    false
  rpk.tune_disk_nomerges               false
  rpk.tune_disk_scheduler              false
  rpk.tune_disk_write_cache            false
  rpk.tune_fstrim                      false
  rpk.tune_network                     false
  rpk.tune_swappiness                  false
  rpk.tune_transparent_hugepages       false
```

Start the first node with the following Parameters, In this case gsts1ship01 is the root node

```
sudo rpk config bootstrap --id 0 --self 172.16.119.21 && sudo systemctl start redpanda-tuner redpanda
```
Start the rest of the servers with following commands

For gsts1ship02
```
sudo rpk config bootstrap --id 102 --self 172.16.119.22 --ips 172.16.119.21,172.16.119.22,172.16.119.23 &&  sudo systemctl start redpanda-tuner redpanda
```

For gsts1ship03
```
sudo rpk config bootstrap --id 103 --self 172.16.119.23 --ips 172.16.119.21,172.16.119.22,172.16.119.23 &&  sudo systemctl start redpanda-tuner redpanda
```

For gsts2ship01
```
sudo rpk config bootstrap --id 201 --self 172.17.135.226 --ips 172.16.119.21,172.16.119.22,172.16.119.23,172.17.135.226,172.17.135.227,172.17.135.228 &&  sudo systemctl start redpanda-tuner redpanda
```

For gsts2ship02
```
sudo rpk config bootstrap --id 202 --self 172.17.135.227 --ips 172.16.119.21,172.16.119.22,172.16.119.23,172.17.135.226,172.17.135.227,172.17.135.228 &&  sudo systemctl start redpanda-tuner redpanda
```

For gsts2ship03
```
sudo rpk config bootstrap --id 203 --self 172.17.135.228 --ips 172.16.119.21,172.16.119.22,172.16.119.23,172.17.135.226,172.17.135.227,172.17.135.228 &&  sudo systemctl start redpanda-tuner redpanda
```



## Tomcat

Find the following instructions to restart HA Proxy

```
sudo systemctl restart tomcat
```

## HA Proxy

Find the following instructions to restart HA Proxy

```
sudo systemctl restart haproxy
```


{{% children  %}}
