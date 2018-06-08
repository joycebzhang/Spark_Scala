1 Open a scala spark shell in local mode

[root@sandbox-hdp ~]# spark-shell local master
SPARK_MAJOR_VERSION is set to 2, using Spark2
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
18/06/08 11:15:30 WARN Utils: Service 'SparkUI' could not bind on port 4040. Attempting port 4041.
Spark context Web UI available at http://172.17.0.2:4041
Spark context available as 'sc' (master = local[*], app id = local-1528456530275).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.2.0.2.6.4.0-91
      /_/

Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_161)
Type in expressions to have them evaluated.
Type :help for more information.

2. Load the shakespare file from local /opt/spark/data
scala> val inputFile = sc.textFile("file///opt/spark/data")
inputFile: org.apache.spark.rdd.RDD[String] = file///opt/spark/data MapPartitionsRDD[1] at textFile at <console>:24
