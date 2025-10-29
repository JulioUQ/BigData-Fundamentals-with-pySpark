
There's been a lot of buzz about Big Data over the past few years, and it's finally become mainstream for many companies. But what is this Big Data? This course covers the fundamentals of Big Data via PySpark. Spark is a "lightning fast cluster computing" framework for Big Data. It provides a general data processing platform engine and lets you run programs up to 100x faster in memory, or 10x faster on disk, than Hadoop. You’ll use PySpark, a Python package for Spark programming and its powerful, higher-level libraries such as SparkSQL, MLlib (for machine learning), etc. You will explore the works of William Shakespeare, analyze Fifa 2018 data and perform clustering on genomic datasets. At the end of this course, you will have gained an in-depth understanding of PySpark and its application to general Big Data analysis.
# What is BigData?

Big data is a term used to refer to the sudy and applications of data sets that are too complex for traditional data-procssing software.

# The 3 V's of BigData

Volume: 
- Size of the data
- Different souces and formats
- Speed of the data
	
Variety
Velocity

# Big data concepts and Terminology

Clustered computing: Collection of resources of multiple machines
Parallel computing: Simultaneous computation on single computer.
Distributed computing: Collection of nodes (networked computers) that run in parallel.
Batch processing: Breaking the job into small pieces and running them on individual machines.
Real-time processing: Inmediate processing of data.

# Big Data processing systems

Hadoop/MapReduce: Scalable and fault tolerant framework written in Java
- Open Source
- Batch processing

Apache Spak: General purpose and ligthnign fast cluster computing system
- Open Source
- Both batch and real-time processing

> Note: ApacheSpark is nowadays preferred over Hadoop/MapReduce


# Feautres of Apache Spark framework

Distributed cluster ocmputing framework
Efficient in-memory ocmputtaions for large data sets.
Lightning fast dta processinf framework
Provides support for Java, Scala, Python, R and SQL.

# Apache Spark Components

SparkSQL
MLlib (MachineLearning)
GrapthX
SparkStreaming
RDD API ApacheSpark Core

# Spark modes of deployment

Local mode: Single machine such as your laptop
- Local mode convenient for testing, debugging and demostration.
Cluster mode: Set of pre-defined machines
- Good for production
Workflow: Local -> clusters
No code change neccesary

---

# PySpark: Spark with python

## Overview of PySpark

Apache Spark is written in Scala
To support Python with Spark, Apache Spark Community released PySpark
Similar computation speed and power as Scala
PySpark API's are similar to Pandas and Scikit-learn

## What is Spark shell?

Interactive environment for runnign Spark jobs
Helpful for fast interactive prototyping
Spark shells allow interacting with data on disk or in memory
Three different Spark shells:
- Spark-shell for Scala
- PySpark-shell for Python
- SparkR for R

## PySpark shell

PySpark shell is the Python-based command line tool
PySpark shell allows data scientists interface with Spark data structures
PySpark shell support connecting to a cluster


## Understanding SparkContext

SparkContext is an entry point into the world of Spark
An entry point is a way of connecting to Spark cluster
An entry point is like a key to the house
PySpark has a default SparkContext called `sc`


## Inspecting Spark Context

Version: To retrieve SparkContext version `sc.version`
Python Version: To retrieve Python version of SparkContext `sc.pythonVer`
Master: URL of the cluster or local string to run in local mode of SparkContext `sc.master`

## Loading data in PySpark

SparkContext's `parallelize()` metod
- `rdd = sc.parallelize([1,2,3,4,5])`
SparkContext's `textFile()` method
- `rdd2 = sc.textFile("test.txt")`

# Use of Lambda functions in python - filter()

## What are anonymous functions in Python?

Lambda functions are anonymous functions in Python
Very powerful and used in Python. Quite efficient with `map()` and `filter()`
Lambda functions create functions to be called later similar to `def`
It returns the functions without any name (i.e. anonymous)
Inline a function definition or to defer execution of a code

## Lambda function syntax

The general form of lambda function is 
`lambda argument: expression`
Example of lambda function
```python
double = lambda x: x*2
print(double(3)
```

## Difference between def vs lambda functions

Python code illustrate cube of a number

```python
def cube(x):
	return x**3
	
g = lambda x: x**3

print(g(10))
print(cube(10))
```

No return statement of lambda
Can put lambda function anywhere

## Use of lambda function in Python - map()


`map()` applies a function to all items in the input list
General systax of map() `map(function, list)`
Example map()
```python
items = [1,2,3,4]
list(map(lambda x: x + 2, items))
```

## Use of lambda function in Python - filter()


filter()` function takes a function and a list and returns a new list which the function evaluates as true
General systax of filter() `filter(function, list)`
Example map()
```python
items = [1,2,3,4]
list(map(filter x: x%2 != 0, items))
```


# Abstracting Data with RDDs

## What are RDD's?

Resilient Distributed Datasets
- Resilient: Ability to withstand failures
- Distributed: Spanning across multiple machines
- Datasets: Collection of partitioned data e.g, Arrays, Tables, Tuples etc.,

![[Pasted image 20251021111646.png|500]]


## Creating RDD's How to do it?

Parallelizing an existing colleciton of objects
External datasets:
- Files HDFS
- Objects in Amazon S3 buckets
- lines ina text file
From existing RDDs

## Parallelized collection (parallelizing)
parallelize() for creating RDDs from python lists
```python
numRDD = sc.parallelize([1,2,3,4])
helloRDD = sc.parallelize("Hello world")
type(helloRDD)
```
## From external datasets

textFile() for creating RDDs from external datasets

```python
fileRDD = SC.textFile("README.md")
type(fileRDD)
```
## Understanding Partitioning in PySpark

A partition is a logical division of a large distributed data set
parallelize() method
```python
numRDD = sc.parallelize(rango(10), minPartitions = 6)
```
textFile() method

```python
fileRDD = SC.textFile("README.md", minPartitions = 6)
type(fileRDD)
```
The number of partitions in an RDD can be found by using `getNumPartitions()` method


# Basic RDD Transformations and Actions

Transformrations create new RDDs, while Actions perform computtiaon on the RDDs.
Basic RDD Transformations are: map(), filter(), flatMap() and union().

![[Pasted image 20251021113943.png]]

- **map() Transformation**

map() transformation applies a function to all element in the RDD
```python
RDD = sc.parallelize([1,2,3,4])
RDD_map = RDD.map(lambda x: x*x)
```

-  **filter() Transformation**

Filter trnsformation returns a new RDD with only the elemens that pass the condition
```python
RDD = sc.parallelize([1,2,3,4])
RDD_filter = RDD.filter(lambda x: x>2)
```

- **flatMap() Transformation**

flatMap() transformation return multiples values for each element in the original RDD
```python
RDD = sc.parallelize(["Hello world", "How are you])
RDD_flatmap = RDD.flatMap(lambda x: x.split(" "))
```

- **union() Transformation**

```python
inputRDD = sc.textFile("logs.txt")
errorRDD = inputRDD.filter(lambda x: "error" in x.split(" "))
warningsRDD = inputRDD.filter(lambda x: "warnings" in x.split(" "))
combinedRDD = errorRDD.union(warningsRDD)
```

## RDD Actions

They are operations that return a value after running a computation on the RDD
Basic RDD Actions are:

- **collect()**: return all the elements of the data set as an array
```python
RDD_map.collect()
```
- **take(N)**: returns an array with the first N elements of the datset.
```python
RDD_map.take(2)
```
- first() -> similar to take(1)
```python
RDD_map.first()
```
- **count()**: return the number of elements in the RDD
```python
RDD_map.count()
```

# Pair RDDs in PySpark

## Introduction to pair RDDs in PySpark

Real life datasets are usually key/value pairs
Each row is a key and maps to one or more values
Pais RDD is a special data structure to work with this kind of datasets
Pais RDD: Key is the identifier and value is the data

## Creating pair RDDs

Two common ways to create pair RDDs
- From a list of key-value tuple
- From a regular RDD
Get the data into key/value form for paired RDD

```python
my_tuple =[('Sam', 23), ('Mary', 34), ('Peter', 25)]
pairRDD_tuple = sc.parallelize(my_tuple)

my_tuple =[('Sam', 23), ('Mary', 34), ('Peter', 25)]
regularRDD = sc.parallelize(mylist)
pairRDD_RDD = regularRDD.map(lambda s: (s.split(' ')[0], s.split(' ')[1]))
```

## Transformations on pair RDDs

All regular transformations work on pair RDD
Have to pass functions that operate on key value pairs rather than on indivual elements
Examples of paired RDD Transformations:

- reduceByKey() transformation combines values with the same key
	- It runs parallel operations for each key in the dataset
	- It is a transformation and not action

```python
regularRDD = sc.parallelize([('Messi', 23), ('Ronaldo', 34), ('Neymar', 22), ('Messi', 24)]
pairRDD_reducebykey = regularRDD.reduceByKey(lambda x, y: x + y)
pairRDD_reducebykey.collect()
```

- sortByKey() operation orders pair RDD by key.
	- It returns an RDD sorted by key in ascending or descending order.

```python
pairRDD_reducebykey_rev = pairRDD_reducebykey.map(lambda x: (x[1], x[0]))
pairRDD_reducebykey_rev.sortByKey(ascending=False).collect()
```
- groupByKey() groups all the values with the same key in the pair RDD
```python
airports = [('US', 'JFK'), ('UK', 'LHR'), ('FR', 'CDG'), ('US', 'SFO')]
regularRDD = sc.parallelize(airports)
pairRDD_group = regularRDD.groupByKey().collect()

for cont, air in pairRDD_group:
	print(cont, list(air))
```

- join() transformation joins the two pair RDDs based on their key
- ```python
  RDD1 = sc.parallelize([('Messi', 34), ('Ronaldo', 32), ('Neymar', 24)])
  RDD2 = sc.parallelize([('Messi', 100), ('Ronaldo', 80), ('Neymar', 120)])
  
  RDD1.join(RDD2).collect()
  ```


---

# Exercises to practise

## Understanding SparkContext

A SparkContext represents the entry point to Spark functionality. It's like a key to your car. When we run any Spark application, a driver program starts, which has the main function and your SparkContext gets initiated here. PySpark automatically creates a SparkContext for you in the PySpark shell (so you don't have to create it by yourself) and is exposed via a variable sc.

In this simple exercise, you'll find out the attributes of the SparkContext in your PySpark shell which you'll be using for the rest of the course.

- Print the version of SparkContext in the PySpark shell.
```python
# Print the version of SparkContext
print("The version of Spark Context in the PySpark shell is", sc.version)
```
- Print the Python version of SparkContext in the PySpark shell.
```python
# Print the Python version of SparkContext
print("The Python version of Spark Context in the PySpark shell is", sc.pythonVer)
```
- What is the master of SparkContext in the PySpark shell?
```python
# Print the master of SparkContext
print("The master of Spark Context in the PySpark shell is", sc.master)
```

## Interactive Use of PySpark

Spark comes with an interactive Python shell in which PySpark is already installed. PySpark shell is useful for basic testing and debugging and is quite powerful. The easiest way to demonstrate the power of PySpark’s shell is with an exercise. In this exercise, you'll load a simple list containing numbers ranging from 1 to 100 in the PySpark shell.

The most important thing to understand here is that we are not creating any SparkContext object because PySpark automatically creates the SparkContext object named sc in the PySpark shell.

- Create a Python list named numb containing the numbers 1 to 100.
```python
# Create a Python list of numbers from 1 to 100 
numb = range(1, 100)
```
- Load the list into Spark using Spark Context's parallelize method and assign it to a variable spark_data.
```python
# Load the list into PySpark  
spark_data = sc.parallelize(numb)
```

## Loading data in PySpark shell

In PySpark, we express our computation through operations on distributed collections that are automatically parallelized across the cluster. In the previous exercise, you have seen an example of loading a list as parallelized collections and in this exercise, you'll load the data from a local file in PySpark shell.

Remember, you already have a SparkContext sc and file_path variable (which is the path to the README.md file) available in your workspace.

- Load a local text file README.md in PySpark shell.

```python
# Load a local file into PySpark shell
lines = sc.textFile(file_path)
```

## Use of lambda() with map()

The map() function in Python returns a list of the results after applying the given function to each item of a given iterable (list, tuple etc.). The general syntax of map() function is map(fun, iter). We can also use lambda functions with map(). Refer to slide 5 of video 1.7 for general help of map() function with lambda().

In this exercise, you'll be using lambda function inside the map() built-in function to square all numbers in the list.

- Print my_list which is available in your environment.
```python
# Print my_list in the console
print("Input list is", my_list)
```
- Square each item in my_list using map() and lambda().
 ```python
 # Square all numbers in my_list
squared_list_lambda = list(map(lambda x: x**2, my_list))
 ```
- Print the result of map function.
 ```python
 # Print the result of the map function
print("The squared numbers are", squared_list_lambda)
 ```

## Use of lambda() with filter()

Another function that is used extensively in Python is the filter() function. The filter() function in Python takes in a function and a list as arguments. Similar to the map(), filter() can be used with lambda function. Refer to slide 6 of video 1.7 for general help of the filter() function with lambda().

In this exercise, you'll be using lambda() function inside the filter() built-in function to find all the numbers divisible by 10 in the list.

- Print my_list2 which is available in your environment.
```python
# Print my_list2 in the console
print("Input list is:", my_list2)
```
- Filter the numbers divisible by 10 from my_list2 using filter() and lambda().
 ```python
# Filter numbers divisible by 10
filtered_list = list(filter(lambda x: (x%10 == 0), my_list2))
 ```
- Print the numbers divisible by 10 from my_list2.
 ```python
# Print the numbers divisible by 10
print("Numbers divisible by 10 are:", filtered_list)
 ```

## RDDs from Parallelized collections

Resilient Distributed Dataset (RDD) is the basic abstraction in Spark. It is an immutable distributed collection of objects. Since RDD is a fundamental and backbone data type in Spark, it is important that you understand how to create it. In this exercise, you'll create your first RDD in PySpark from a collection of words.

Remember, you already have a SparkContext sc available in your workspace.

- Create a RDD named RDD from a Python list of words.
 ```python
# Create an RDD from a list of words
RDD = sc.parallelize(["Spark", "is", "a", "framework", "for", "Big Data processing"])
 ```
- Confirm the object created is RDD.
 ```python
# Print out the type of the created object
print("The type of RDD is", type(RDD))
 ```

## RDDs from External Datasets

PySpark can easily create RDDs from files that are stored in external storage devices, such as HDFS (Hadoop Distributed File System), Amazon S3 buckets, etc. However, the most common method of creating RDD's is from files stored in your local file system. This method takes a file path and reads it as a collection of lines. In this exercise, you'll create an RDD from the file path (file_path) with the file name README.md which is already available in your workspace.

Remember, you already have a SparkContext sc available in your workspace.

- Print the file_path in the PySpark shell.
 ```python
# Print the file_path
print("The file_path is", file_path)
 ```
- Create a RDD named fileRDD from a file_path.
 ```python
# Create a fileRDD from file_path
fileRDD = sc.textFile(file_path)
 ```
- Print the type of the fileRDD created.
 ```python
# Check the type of fileRDD
print("The file type of fileRDD is", type(fileRDD))
 ```

## Partitions in your data

SparkContext's textFile() method takes an optional second argument called minPartitions for specifying the minimum number of partitions. In this exercise, you'll create a RDD named fileRDD_part with 5 partitions and then compare that with fileRDD that you created in the previous exercise. Refer to the "Understanding Partition" slide in video 2.1 to know the methods for creating and getting the number of partitions in a RDD.

Remember, you already have a SparkContext sc, file_path and fileRDD available in your workspace.

- Find the number of partitions that support fileRDD RDD.
 ```python
# Check the number of partitions in fileRDD
print("Number of partitions in fileRDD is", fileRDD.getNumPartitions())
 ```
- Create an RDD named fileRDD_part from the file path but create 5 partitions.
 ```python
# Create a fileRDD_part from file_path with 5 partitions
fileRDD_part = sc.textFile(file_path, minPartitions = 5)
 ```
- Confirm the number of partitions in the new fileRDD_part RDD.
 ```python
# Check the number of partitions in fileRDD_part
print("Number of partitions in fileRDD_part is", fileRDD_part.getNumPartitions())
 ```

## Map and Collect

The main method with which you can manipulate data in PySpark is using map(). The map() transformation takes in a function and applies it to each element in the RDD. It can be used to do any number of things, from fetching the website associated with each URL in our collection to just squaring the numbers. In this simple exercise, you'll use map() transformation to cube each number of the numbRDD RDD that you've created earlier. Next, you'll store all the elements in a variable and finally print the output.

Remember, you already have a SparkContext sc, and numbRDD available in your workspace.

- Create map() transformation that cubes all of the numbers in numbRDD.
```python
# Create map() transformation to cube numbers
cubedRDD = numbRDD.map(lambda x: x**3)
 ```
- Collect the results in a numbers_all variable.
```python
# Collect the results
numbers_all = cubedRDD.collect()
 ```
- Print the output from numbers_all variable.
```python
# Print the numbers from numbers_all
for numb in numbers_all:
	print(numb)
 ```

## Filter and Count

The RDD transformation filter() returns a new RDD containing only the elements that satisfy a particular function. It is useful for filtering large datasets based on a keyword. For this exercise, you'll filter out lines containing keyword Spark from fileRDD RDD which consists of lines of text from the README.md file. Next, you'll count the total number of lines containing the keyword Spark and finally print the first 4 lines of the filtered RDD.

Remember, you already have a SparkContext sc, file_path, and fileRDD available in your workspace.

- Create filter() transformation to select the lines containing the keyword Spark.
```python
# Filter the fileRDD to select lines with Spark keyword
fileRDD_filter = fileRDD.filter(lambda line: 'Spark' in line)
 ```
- How many lines in fileRDD_filter contain the keyword Spark?
```python
# How many lines are there in fileRDD?
print("The total number of lines with the keyword Spark is", fileRDD_filter.count())
 ```
- Print the first four lines of the resulting RDD.
```python
# Print the first four lines of fileRDD
for line in fileRDD_filter.take(4):
  print(line)
 ```
## ReduceBykey and Collect

One of the most popular pair RDD transformations is `reduceByKey()` which operates on key, value (k,v) pairs and merges the values for each key. In this exercise, you'll first create a pair RDD from a list of tuples, then combine the values with the same key and finally print out the result.

Remember, you already have a SparkContext `sc` available in your workspace.

- Create a pair RDD named `Rdd` with tuples `(1,2)`,`(3,4)`,`(3,6)`,`(4,5)`.
```python
# Create PairRDD Rdd with key value pairs
Rdd = sc.parallelize([(1,2), (3,4),(3,6), (4,5)])
 ```
- Transform the `Rdd` with `reduceByKey()` into a pair RDD `Rdd_Reduced` by adding the values with the same key.
```python
# Apply reduceByKey() operation on Rdd
Rdd_Reduced = Rdd.reduceByKey(lambda x, y: x + y)
 ```
- Collect the contents of pair RDD `Rdd_Reduced` and iterate to print the output.
```python
# Iterate over the result and print the output
for num in Rdd_Reduced.collect(): 
  print("Key {} has {} Counts".format(num[0], num[1]))
 ```
## SortByKey and Collect

Many times it is useful to sort the pair RDD based on the key (for example word count which you'll see later in the chapter). In this exercise, you'll sort the pair RDD `Rdd_Reduced` that you created in the previous exercise into descending order and print the final output.

Remember, you already have a SparkContext `sc` and `Rdd_Reduced` available in your workspace.

- Sort the `Rdd_Reduced` RDD using the key in descending order.
```python
# Iterate over the result and print the output
for num in Rdd_Reduced.collect(): 
  print("Key {} has {} Counts".format(num[0], num[1]))
 ```
- Collect the contents and iterate to print the output.
```python
# Iterate over the result and print the output
for num in Rdd_Reduced.collect(): 
  print("Key {} has {} Counts".format(num[0], num[1]))
 ```