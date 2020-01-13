Code author
-----------
Brian Rouse (@brouse12)  
Derek Grubis (@dgrubis)    
Harshit Gupta (@harshit21g)

# CS 6240 Final Project
The goal of this project was to train an ensemble of classification models that can determine whether an airplane flight will be delayed by weather conditions.  
The project required two phases of work:
1. Generate a suitable testing and training dataset by combining four datasets that describe flight, airport, weather observation, and weather station data.
2. Train and test a classification ensemble using this new dataset.


# Environment and Software Versions
Hadoop Version - 2.9.1  
Spark Version - 2.3.1 (without bundled hadoop)  
JDK 1.8  
Scala 2.11.12  
Maven  
AWS CLI (for EMR execution)  

JAVA_HOME=/usr/lib/jvm/java-8-oracle  
HADOOP_HOME=/home/user/tools/hadoop/hadoop-2.9.1  
SCALA_HOME=/home/user/tools/scala/scala-2.11.12  
SPARK_HOME=/home/user/tools/spark/spark-2.3.1-bin-without-hadoop  
YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop  
PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$SCALA_HOME/bin:$SPARK_HOME/bin  
SPARK_DIST_CLASSPATH=$(hadoop classpath)

# Input Files:
Weather Dataset: https://www7.ncdc.noaa.gov/CDO/cdoselect.cmd?datasetabbv=GSOD&countryabbv=&georegionabbv=
Flight and Airport Dataset: https://www.kaggle.com/usdot/flight-delays/version/1#flights.csv

# Build and Execution Steps
All of the build & execution commands are organized in the Makefile.
1) Add downloaded files to input folder.
2) Open command prompt.
3) Navigate to directory for the project you want to execute (thetajoin or classification).
4) Edit the Makefile to customize the environment at the top.
	Sufficient for standalone: hadoop.root, jar.name, local.input
	Other defaults acceptable for running standalone.
5) Standalone Hadoop:
	make switch-standalone		-- set standalone Hadoop environment (execute once)
	make local
6) Pseudo-Distributed Hadoop: (https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SingleCluster.html#Pseudo-Distributed_Operation)
	make switch-pseudo			-- set pseudo-clustered Hadoop environment (execute once)
	make pseudo					-- first execution
	make pseudoq				-- later executions since namenode and datanode already running 
7) AWS EMR Hadoop: (you must configure the emr.* config parameters at top of Makefile)
	make upload-input-aws		-- only before first execution
	make aws					-- check for successful execution with web interface (aws.amazon.com)
	download-output-aws			-- after successful execution & termination
