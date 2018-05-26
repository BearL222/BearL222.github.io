---
layout: post
title: HDFS and MapReduce
category: hadoop-hands-on
tags: [hadoop, mapreduce, hdfs]
---

## 1. What is HDFS
The Hadoop distributed file system

![hdfs](/public/blog-img/2018-5-20-HDFS-and-MapReduce/hdfs.jpg)

- **Name node** keeps track of the whole
- **Data node** stores data and file
	
#### Solutions for name node resilience:
- Back up metadata
- Secondary namenode
	
#### HDFS federation
	
#### HDFS high availability-zookeeper

## 2. install movielens dataset into HDFS using ambari UI

ambari port 8080 through http

## 3. install movielens dataset into HDFS using cmd line

- Hadoop fs -ls
- Hadoop fs -mkdir ml-100k
- Hadoop fs -copyFromLocal u.data // send data from local to Hadoop
- Hadoop fs // see all cmds

## 4. MapReduce
- 1. Mapper: Source data -> Key-value pair
- 2. Sort and groups the mapped data (shuffle and sort)
- 3. summary
![hdfs](/public/blog-img/2018-5-20-HDFS-and-MapReduce/mapreduce-summary.jpg)

## 5. MapReduce distributing process
- 1. What's happening
![hdfs](/public/blog-img/2018-5-20-HDFS-and-MapReduce/what-happening.jpg)
- 2. MapReduce written
![hdfs](/public/blog-img/2018-5-20-HDFS-and-MapReduce/mapreduce-written.jpg)

## 6. Break down movie ratings by rating score