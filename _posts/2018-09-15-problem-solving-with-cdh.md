---
layout: post
title: Problem solving with CDH
categories: bigdata
tags: bigdata hadoop cdh
---

Here are some problems I met during my internship on bigdata. I list them here for future reference.  

## CDH
Q: heartbeat from agent fails  
A: change: 
```
vim /etc/cloudera-scm-agent/config.ini
server_host=srv15
```

Q: host in bad health, cm server guid updated expected received  
A:  
1. guid is wrong, delete /var/lib/cloudera-scm-agent/cm_guid no each nod  
2. restart the agent: service cloudera-scm-agent restart  
3. Run the Host inspector?

reference:  
[https://community.cloudera.com/t5/Cloudera-Manager-Installation/Error-CM-Server-guid-updated-CDH-5-9-0/m-p/47221](https://community.cloudera.com/t5/Cloudera-Manager-Installation/Error-CM-Server-guid-updated-CDH-5-9-0/m-p/47221)  
[https://community.cloudera.com/t5/Cloudera-Manager-Installation/CM-CDH-5-14-mirror-issue/td-p/64396](https://community.cloudera.com/t5/Cloudera-Manager-Installation/CM-CDH-5-14-mirror-issue/td-p/64396)

Q: CDH log path  
A: agent log: tail -300 /var/log/cloudera-scm-agent/cloudera-scm-agent.log

Q:  ```Permission denied: user=cloudera, access=WRITE, inode="/user":hdfs:supergroup:drwxr-xr-x```
A: change in CM, HDFS, configuration, advanced, safety  

```
<property>
	<name>dfs.permissions.enabled</name>
	<value>false</value>
</property>
```

Q: format hdfs  
A: hdfs namenode -format
then delete datanode's dir

Q: VERSION (permission denied)  
A: chmod 777 to /dfs/nn

Q: try connection to server several times  
A: fail to start yarn, start it (resource manager)

Q: mapred permission denied  
A: In CM, uncheck HDFS permissions (always do it)

Q: out of physical memory limit  
A: yarn -> nodemanager  

```
<property>
	<name>yarn.nodemanager.pmem-check-enabled</name>
	<value>false</value>
</property>
```

Q: namenode fails to format/hdfs start fails/datanode fails to start
A: clean namenode/datanode directory

Q: volume fail  
A: check if mounted disk is ok. If not, re-mount it. Then restart node

Q: namenode is in safe mode  
A: ```hadoop dfsadmin -safemode leave```

Q: yarn-site.xml fail  

```assert 0, "Get workers from yarn-site.xml page failed, reason:%s\nplease set \`hibench.masters.hostnames\` and \`hibench.slaves.hostnames\` manually" % e
AssertionError: Get workers from yarn-site.xml page failed, reason:[Errno 2] No such file or directory: '/opt/cloudera/parcels/CDH-5.15.0-1.cdh5.15.0.p0.21/lib/hadoop/etc/hadoop/yarn-site.xml'
```
yarn not started  
A: yarn should be on the same server with namenode

Q: hdfs canary problem  
A: wait for a while, it may disappear

Q: terasort run breaks brings down a disk  
A: change ```hibench.conf```, parallel = 120

Q: missing blocks  
A: restart all services

Q: CM add hive service, use mysql, unable to connect to database  
A: use a proper version of jdbc

Q: CM add hive service, use mysql, wrong username/pwd  
A:  

```
create user 'hive'@'srv15' identified by 'intel123'; 
GRANT ALL PRIVILEGES ON *.* TO 'hive'@'%' IDENTIFIED BY 'intel123' WITH GRANT OPTION; FLUSH PRIVILEGES;
```

Q: src parcel not exist  
A: restart agent service

Q: srvx out of contact  
A: use_tls problem: ```vim /etc/cloudera-scm-agent/config.ini```

## Hadoop
Q: hive
```Unable to instantiate org.apache.hadoop.hive.ql.metadata.SessionHiveMetaStoreClient```
A: ```start hive metastore server
hive --service metastore &```

## Linux
Q: srv7 ssh fail  
A: change authority of /etc/ssh
```chmod xxx /etc/ssh/*```
then see files in other srv

Q: time  
A: ```date +%T -s "09:21:30"```

Q: When installing maven, mvn spark= scala= ...
A: leave out some model number, use package instead of packagemv

Q: srv11 enters emergency mode  
A: fail to mount disk, change in /etc/fstab

Q: read only file system because wrong configuration in /etc/fstab  
A: ```mount -o remount,rw /```

## MySQL
Q: ```mysql service starting failed,  InnoDB: The innodb_system data file 'ibdata1' must be writable;```  
A: 

```
sudo chown -R mysql /var/lib/mysql
sudo chgrp -R mysql /var/lib/mysql
```

Q: drop database with content  
A: ```DROP DATABASE IF EXISTS db_name CASCADE;```