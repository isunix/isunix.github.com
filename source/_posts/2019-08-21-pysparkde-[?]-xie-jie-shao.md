---
layout: post
title: "PySpark的一些介绍"
date: 2019-08-21 08:00:24 +0800
comments: true
categories: Data&ML&AI	
---

1. ##### 一些概念

   - Spark, PySpark, Spark SQL, SparkML
   - Jobs, Stages, Task, Driver, Worker
   - RDD, DataFrames, DataSets
   - SparkSession

2. ##### RDD

   1. two ways to create an RDD in PySpark

      ```python
      data = sc.parallelize([('Amber', 22), ('Albert', 12), ('Amber', 9)])
      ```

      ```python
      data_from_file = sc.textFile('/data/PySpark_Data/VS14MORT.txt.gz', 4)
      ```

      

   2. RDDs are *schema-less* data structures  Thus, parallelizing a dataset is perfectly fine with Spark when using RDDs:

   2. ```python
      # parallelize a rdd
      data_heterogenous = sc.parallelize([ 
        ('Ferrari', 'fast'),
      	{'Porsche': 100000}, 
        ['Spain','visited', 4504]
      ]).collect()
      
      # access element
      data_heterogenous[1]['Porsche']
      ```

   

   3. Transformations
      1. .map(...)

      2. .filter(...)  

      3. .flatMap(...) 

      4. .distinct(...)

      5. .sample(...)

      6. .leftOuterJoin(...)

      7. .repartition(...)

         

   4. Actions
      1. .take(...)
      2. .reduce(...)
      3. .reduceByKey(...)
      4. .count()
      5. .collect()
      6. .saveAsTextFile(...)
      7. .foreach(...)

      

3. ##### DataFrames

   1. specify the schema

      ```python
      from pyspark.sql.types import *
      
      # Generate our own CSV data 
      #   This way we don't have to access the file system yet.
      stringCSVRDD = sc.parallelize([(123, 'Katie', 19, 'brown'), (234, 'Michael', 22, 'green'), (345, 'Simone', 23, 'blue')])
      
      # The schema is encoded in a string, using StructType we define the schema using various pyspark.sql.types
      schemaString = "id name age eyeColor"
      schema = StructType([
          StructField("id", LongType(), True),    
          StructField("name", StringType(), True),
          StructField("age", LongType(), True),
          StructField("eyeColor", StringType(), True)
      ])
      
      # Apply the schema to the RDD and Create DataFrame
      swimmers = spark.createDataFrame(stringCSVRDD, schema)
      
      # Creates a temporary view using the DataFrame
      swimmers.createOrReplaceTempView("swimmers")
      ```

   2. DataFrame Query

      ```python
      # Set File Paths
      flightPerfFilePath = "/databricks-datasets/flights/departuredelays.csv"
      airportsFilePath = "/databricks-datasets/flights/airport-codes-na.txt"
      
      # Obtain Airports dataset
      airports = spark.read.csv(airportsFilePath, header='true', inferSchema='true', sep='\t')
      airports.createOrReplaceTempView("airports")
      
      # Obtain Departure Delays dataset
      flightPerf = spark.read.csv(flightPerfFilePath, header='true')
      flightPerf.createOrReplaceTempView("FlightPerformance")
      
      # Cache the Departure Delays dataset 
      flightPerf.cache()
      
      # Query Sum of Flight Delays by City and Origin Code (for Washington State)
      spark.sql("select a.City, f.origin, sum(f.delay) as Delays from FlightPerformance f join airports a on a.IATA = f.origin where a.State = 'WA' group by a.City, f.origin order by sum(f.delay) desc").show()
      ```

      

4. Prepare Data

   1. create data frame

      ```python
      df = spark.createDataFrame([
      (1, 144.5, 5.9, 33, 'M'), (2, 167.2, 5.4, 45, 'M'), (3, 124.1, 5.2, 23, 'F'), (4, 144.5, 5.9, 33, 'M'), (5, 133.2, 5.7, 54, 'F'), (3, 124.1, 5.2, 23, 'F'), (5, 129.2, 5.3, 42, 'M'), ], ['id', 'weight', 'height',
      'age', 'gender'])
      ```

   2. get basic description

      ```python
      print('Count of rows: {0}'.format(df.count()))
      print('Count of distinct rows: {0}'.format(df.distinct().count()))
      df = df.dropDuplicates()
      df = df.dropDuplicates(subset=[c for c in df.columns if c != 'id'])
      df.show()
      ```

   4. To calculate the total and distinct number of IDs in one step we can use the `.agg(...)` method.

      ```python
      import pyspark.sql.functions as fn
      
      df.agg(
          fn.count('id').alias('count'),
          fn.countDistinct('id').alias('distinct')
      ).show()
      
      # Give each row a unique ID.
      df.withColumn('new_id', fn.monotonically_increasing_id()).show()
      ```

   5. missing observations

      ```python
      df_miss = spark.createDataFrame([
              (1, 143.5, 5.6, 28,   'M',  100000),
              (2, 167.2, 5.4, 45,   'M',  None),
              (3, None , 5.2, None, None, None),
              (4, 144.5, 5.9, 33,   'M',  None),
              (5, 133.2, 5.7, 54,   'F',  None),
              (6, 124.1, 5.2, None, 'F',  None),
              (7, 129.2, 5.3, 42,   'M',  76000),
          ], ['id', 'weight', 'height', 'age', 'gender', 'income'])
      
      # To find the number of missing observations per row
      df_miss.rdd.map(
          lambda row: (row['id'], sum([c == None for c in row]))
      ).collect()
      
      # see what values are missing
      df_miss.where('id == 3').show()
      
      # get the percentage of missing observations we see in each column
      df_miss.agg(*[
          (1 - (fn.count(c) / fn.count('*'))).alias(c + '_missing')
          for c in df_miss.columns
      ]).show()
      
      # drop the 'income' feature as most of its values are missing
      df_miss_no_income = df_miss.select([c for c in df_miss.columns if c != 'income'])
      df_miss_no_income.show()
      
      # impute
      means = df_miss_no_income.agg(
          *[fn.mean(c).alias(c) for c in df_miss_no_income.columns if c != 'gender']
      ).toPandas().to_dict('records')[0]
      
      means['gender'] = 'missing'
      
      df_miss_no_income.fillna(means).show()
      
      # Descriptive statistics
      import pyspark.sql.types as typ
      fraud = sc.textFile('ccFraud.csv.gz')
      header = fraud.first()
      
      fraud = fraud \
          .filter(lambda row: row != header) \
          .map(lambda row: [int(elem) for elem in row.split(',')])
          
      fields = [
          *[
              typ.StructField(h[1:-1], typ.IntegerType(), True)
              for h in header.split(',')
          ]
      ]
      
      schema = typ.StructType(fields)
      
      fraud_df = spark.createDataFrame(fraud, schema)
      fraud_df.printSchema()
      fraud_df.groupby('gender').count().show()
      
      numerical = ['balance', 'numTrans', 'numIntlTrans']
      desc = fraud_df.describe(numerical)
      desc.show()
      
      fraud_df.agg({'balance': 'skewness'}).show()
      
      # find Correlations
      fraud_df.corr('balance', 'numTrans')
      
      # to create a correlations matrix 
      n_numerical = len(numerical)
      
      corr = []
      
      for i in range(0, n_numerical):
          temp = [None] * i
          
          for j in range(i, n_numerical):
              temp.append(fraud_df.corr(numerical[i], numerical[j]))
          corr.append(temp)
          
      corr
      ```

      