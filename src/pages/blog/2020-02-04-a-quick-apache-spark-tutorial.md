---
templateKey: blog-post
title: A quick Apache Spark tutorial
date: 2020-02-04T06:52:42.380Z
description: >-
  This post would guide you through a basic setup of Apache Spark on your local
  machine (using a Virtual Machine) and run some commands to test. 

  Follow this tutorial for a quick setup and have fun exploring the intricacies
  of Spark.
featuredpost: true
featuredimage: /img/1200px-Apache_Spark_Logo.svg.png
tags:
  - Scala
  - Apache Spark
  - Hadoop
  - Big Data Processing
---
## Using Spark on your local machine

I prefer using the VirtualBox VM. You can download it here :  

<https://www.virtualbox.org/>

Download the Cloudera Quickstart VM :   

<https://www.cloudera.com/downloads/quickstart_vms/5-10.html>

The recommended system requirements for running Cloudera VM are:

| CDH and Cloudera Manager Version | RAM Required by VM |
| -------------------------------- | ------------------ |
| CDH 5 (default)                  | 4+ GB              |
| Cloudera Express                 | 8+ GB              |
| Cloudera Enterprise (trial)      | 12+ GB             |

Most of the modules needed for the following Spark snippets is already installed in the VM (Hadoop-HDFS, Spark, Spark shells for Scala and Python, etc.).

## Try Hadoop Commands

Try out the Hadoop HDFS commands in your Hadoop environment: 

A great reference: 

<http://hadoop.apache.org/docs/r2.6.0/hadoop-project-dist/hadoop-common/FileSystemShell.html>

Open a terminal window and type these commands at the Linux command line - you shouldn't see any errors:

```
hdfs dfs -ls /            -- View the contents of the top-level directory in HDFS
hdfs dfs -ls              -- View the contents of your user directory (likely empty)
hdfs dfs -mkdir myNewDir  -- Create a new directory named ‘myNewDir’ in your user directory
hdfs dfs -ls              -- Verify that you now have a directory called ‘myNewDir’
hdfs dfs -rm -r myNewDir  -- Remove directory ‘myNewDir’
hdfs dfs -ls              -- Verify that you successfully removed ‘myNewDir’
```

```
hdfs dfs -mkdir funny_input                           -- Create a new directory
hdfs dfs -put cs_fun.txt funny_input                  -- Put your file into HDFS
hdfs dfs -cat funny_input/cs_fun.txt                  -- Output the contents of your HDFS file
cat cs_fun.txt                                        -- Output the contents of your local file



-- Get the file from HDFS and store it locally into new_copy_from_hdfs.txt: 
hdfs dfs -get funny_input/cs_fun.txt new_copy_from_hdfs.txt

cat new_copy_from_hdfs.txt -- View the new local version of the file 
diff cs_fun.txt new_copy_from_hdfs.txt -- The two files should be the same
```

## Start Spark REPL

Verify that the Spark REPL (shell) is working in your virtual environment.

In the already open terminal window type the following command to start the Spark shell - you shouldn't see any errors (warnings can be ignored):

```
$ spark-shell     — Start the Scala version of the Spark REPL
```

... After some output from the shell, you should see a scala> prompt ...

Type the following commands and take a screenshot to show that your Spark environment is working. Upload the screenshot to NYU Classes:

```
scala> :help                            -- In the Spark shell, try the help command
scala> sc[TAB]                          -- View the commands available in the Spark Context (sc)
scala> sc.version                       -- View the version of Spark that is running in the shell
scala> val myConstant: Int = 2016
scala> myConstant
scala> my[TAB]
scala> myConstant.[TAB]
scala> myConstant.to[TAB]
scala> myConstant.toFloat
scala> myConstant                       -- Note that myConstant has not changed; it’s still an Int
scala> myConstant.toFloat.toInt
scala> val myString = myConstant        -- Note the type inferred for myString
scala> :type val myString2 = myConstant -- Use the :type command to view the type that is inferred for myString2
```

## Some Resources

1. **“MapReduce: Simplified Data Processing on Large Clusters”, Dean and Ghemawat, OSDI 2004.** 

   <http://static.usenix.org/event/osdi04/tech/full_papers/dean/dean.pdf> 

   *Describes how the MapReduce paradigm was implemented by Google. This work was the inspiration for Hadoop MapReduce (Hadoop’s open source implementation of the MapReduce paradigm).*
2. “**The Google File System”, by Ghemawat, Gobioff, and Leung.** 

   [http://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf](<1. http://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf>) 

   *Read sections 1 and 2 at least. You will notice a difference in terminology when compared with HDFS; GFS was the inspiration for the open source Hadoop Distributed File System, HDFS.*
