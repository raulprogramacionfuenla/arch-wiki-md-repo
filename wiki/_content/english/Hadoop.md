Related articles

*   [Apache spark](/index.php/Apache_spark "Apache spark")

[Apache Hadoop](https://hadoop.apache.org) is a framework for running applications on large cluster built of commodity hardware. The Hadoop framework transparently provides applications both reliability and data motion. Hadoop implements a computational paradigm named Map/Reduce, where the application is divided into many small fragments of work, each of which may be executed or re-executed on any node in the cluster. In addition, it provides a distributed file system (HDFS) that stores data on the compute nodes, providing very high aggregate bandwidth across the cluster. Both MapReduce and the Hadoop Distributed File System are designed so that node failures are automatically handled by the framework.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Single Node Setup](#Single_Node_Setup)
    *   [3.1 Standalone Operation](#Standalone_Operation)
    *   [3.2 Pseudo-Distributed Operation](#Pseudo-Distributed_Operation)
        *   [3.2.1 Set up passphraseless ssh](#Set_up_passphraseless_ssh)
        *   [3.2.2 Execution](#Execution)

## Installation

[Install](/index.php/Install "Install") the [hadoop](https://aur.archlinux.org/packages/hadoop/) package.

## Configuration

By default, hadoop is already configured for pseudo-distributed operation. Some environment variables are set in `/etc/profile.d/hadoop.sh` with different values than traditional hadoop.

| ENV | Value | Description | Permission |
| HADOOP_CONF_DIR | `/etc/hadoop` | Where configuration files are stored. | Read |
| HADOOP_LOG_DIR | `/tmp/hadoop/log` | Where log files are stored. | Read and Write |
| HADOOP_SLAVES | `/etc/hadoop/slaves` | File naming remote slave hosts. | Read |
| HADOOP_PID_DIR | `/tmp/hadoop/run` | Where pid files are stored. | Read and Write |

You also should set up the following files correctly.

```
/etc/hosts
/etc/hostname 
/etc/locale.conf

```

You need to tell hadoop your JAVA_HOME in `/etc/hadoop/hadoop-env.sh` because it doesn't assume the location where it's installed to in Arch Linux by itself:

 `/etc/hadoop/hadoop-env.sh`  `export JAVA_HOME=/usr/lib/jvm/java-8-openjdk/` 

Check installation with:

```
hadoop version

```

If you get warning message "WARNING: HADOOP_SLAVES has been replaced by HADOOP_WORKERS. Using value of HADOOP_SLAVES." Then replace `export HADOOP_SLAVES=/etc/hadoop/slaves` in `/etc/profile.d/hadoop.sh` with:

```
export HADOOP_WORKERS=/etc/hadoop/workers

```

## Single Node Setup

**Note:** This section is based on the [Hadoop Official Documentation](http://hadoop.apache.org/docs/stable/)

### Standalone Operation

By default, Hadoop is configured to run in a non-distributed mode, as a single Java process. This is useful for debugging.

The following example copies the unpacked conf directory to use as input and then finds and displays every match of the given regular expression. Output is written to the given output directory.

```
$ HADOOP_CONF_DIR=/usr/lib/hadoop/orig_etc/hadoop/
$ mkdir input
$ cp /etc/hadoop/*.xml input
$ hadoop jar /usr/lib/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.0.0.jar grep input output 'dfs[a-z.]+'
$ cat output/*

```

### Pseudo-Distributed Operation

Hadoop can also be run on a single-node in a pseudo-distributed mode where each Hadoop daemon runs in a separate Java process.

By default, Hadoop will run as the user root. You can change the user in `/etc/conf.d/hadoop`:

```
HADOOP_USERNAME="<your user name>"

```

#### Set up passphraseless ssh

Make sure you have [sshd](/index.php/Sshd "Sshd") [enabled](/index.php/Enabled "Enabled"). Now check that you can connect to localhost without a passphrase:

```
$ ssh localhost

```

If you cannot ssh to localhost without a passphrase, execute the following commands:

```
$ ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys

```

Also make sure this line is commented in `/etc/ssh/sshd_config`

 `/etc/ssh/sshd_config`  `#AuthorizedKeysFile .ssh/authorized_keys` 

#### Execution

Format a new distributed-filesystem:

```
$ hadoop namenode -format

```

Edit `/etc/hadoop/core-site.xml` and add below configuration:

```
 <configuration>
   <property>
     <name>fs.defaultFS</name>
     <value>hdfs://localhost:9000</value>
   </property>
 </configuration>

```

Start the hadoop namenode:

```
$ hadoop namenode

```

You may access the web GUI via [http://localhost:9870/](http://localhost:9870/)

[Start](/index.php/Start "Start") the following hadoop systemd units: `hadoop-datanode`, `hadoop-jobtracker`, `hadoop-namenode`, `hadoop-secondarynamenode`, `hadoop-tasktracker`.

The hadoop daemon log output is written to the `${HADOOP_LOG_DIR}` directory (defaults to `/var/log/hadoop`).

Browse the web interface for the NameNode and the JobTracker; by default they are available at:

*   NameNode - [http://localhost:50070/](http://localhost:50070/)
*   JobTracker - [http://localhost:50030/](http://localhost:50030/)

Copy the input files into the distributed filesystem:

```
$ hadoop fs -put /etc/hadoop input

```

Run some of the examples provided:

```
$ hadoop jar /usr/lib/hadoop-2.7.3/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep input output 'dfs[a-z.]+'

```

Examine the output files:

Copy the output files from the distributed filesystem to the local filesystem and examine them:

```
$ hadoop fs -get output output
$ cat output/*

```

or

View the output files on the distributed filesystem:

```
$ hadoop fs -cat output/*

```

When you're done, [stop](/index.php/Stop "Stop") the daemons `hadoop-datanode`, `hadoop-jobtracker`, `hadoop-namenode`, `hadoop-secondarynamenode`, `hadoop-tasktracker`.