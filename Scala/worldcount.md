
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
scala> val inputFile = sc.textFile("/opt/spark/data")
inputFile: org.apache.spark.rdd.RDD[String] = /opt/spark/data MapPartitionsRDD[14] at textFile at <console>:24

#scala> val inputFile = sc.textFile("file///opt/spark/data")  // load from hdfs
#inputFile: org.apache.spark.rdd.RDD[String] = file///opt/spark/data MapPartitionsRDD[1] at textFile at <console>:24

scala> inputFile
res7: org.apache.spark.rdd.RDD[String] = /opt/spark/data MapPartitionsRDD[1] at textFile at <console>:24
3. Data Cleanup 
a. take out the empty line:
scala> val noemptyline = inputFile.filter(line => line.length >0 ).take(10)
noemptyline: Array[String] = Array(A MIDSUMMER-NIGHT'S DREAM, "Now , fair Hippolyta , our nuptial hour ", "Draws on apace : four happy days bring in ", "Another moon ; but O ! methinks how slow ", This old moon wanes ; she lingers my desires ,, "Like to a step dame , or a dowager ", Long withering out a young man's revenue ., Four days will quickly steep themselves in night ;, Four nights will quickly dream away the time ;, "And then the moon , like to a silver bow ")

b. take out the white space:
scala> val nospace = noemptyline.flatMap(line => line.split("\\W+"))
nospace: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[12] at flatMap at <console>:28

scala> nospace.take(50)
res16: Array[String] = Array(A, MIDSUMMER, NIGHT, S, DREAM, Now, fair, Hippolyta, our, nuptial, hour, Draws, on, apace, four, happy, days, bring, in, Another, moon, but, O, methinks, how, slow, This, old, moon, wanes, she, lingers, my, desires, Like, to, a, step, dame, or, a, dowager, Long, withering, out, a, young, man, s, revenue)

scala> val noempty = nospace.filter(word => word.length >0)
noempty: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[8] at filter at <console>:30

scala> noempty.take(5)
res5: Array[String] = Array(A, MIDSUMMER, NIGHT, S, DREAM)

