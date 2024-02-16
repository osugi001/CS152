# Lab 6

## Student information

* Full name: Owen Sugiarto
* E-mail: osugi001@ucr.edu
* UCR NetID: osugi001
* Student ID: 8632296300

## Answers

*Q1.) 
The stub code requires two command-line arguments: command, which specifies the operation to perform, and inputfile, which is the path to the dataset to be processed.




*Q2.)
case "avg-bytes-by-code" =>
// Define zero value for the aggregate (sum of bytes, count)
val zeroValue = (0L, 0L)

// Define seqOp to combine values within a partition
val seqOp = (accumulator: (Long, Long), element: (String, Long)) => (accumulator._1 + element._2, accumulator._2 + 1)

// Define combOp to merge values across partitions
val combOp = (accumulator1: (Long, Long), accumulator2: (Long, Long)) => (accumulator1._1 + accumulator2._1, accumulator1._2 + accumulator2._2)

// Use aggregateByKey to compute sum and count in one pass
val averages: RDD[(String, (Long, Long))] = loglinesByCodeAndBytes.aggregateByKey(zeroValue)(seqOp, combOp)
.mapValues { case (sum, count) => (sum, count) }

println(s"Average bytes per code for the file '$inputfile'")
println("Code,Avg(bytes)")
averages.collect().sortBy(_._1).foreach { case (code, (sum, count)) =>
println(s"$code,${sum.toDouble / count}")
}

*Explanation:
This code calculates the average bytes per response code in an RDD. It does so in one pass by using aggregateByKey with a zero value (tuple of 0s for sum and count), a seqOp to sum bytes and count occurrences within each partition, and a combOp to merge these sums and counts across partitions. Finally, it maps over these results to compute the average bytes for each code and prints them.


*Q3.)
The type of the attributes time and bytes this time will be strings. This is because without the inferSchema option enabled, Spark does not attempt to guess the data type of each column and defaults to treating them as strings.

*Q4.)option 2,

case "comparison" =>
  val filterTimestamp: Long = args(2).toLong
  println(s"Comparison of the number of lines per code before and after $filterTimestamp on file '$inputfile'")
  println("Code,CountBefore,CountAfter")

  val countsBefore = input.filter($"time" < filterTimestamp)
    .groupBy("response").count()
    .withColumnRenamed("count", "CountBefore")
  
  val countsAfter = input.filter($"time" >= filterTimestamp)
    .groupBy("response").count()
    .withColumnRenamed("count", "CountAfter")

  val comparedResults = countsBefore.join(countsAfter, "response", "outer")
    .select(coalesce(countsBefore("response"), countsAfter("response")).alias("response"), 
            coalesce(countsBefore("CountBefore"), lit(0)).alias("CountBefore"), 
            coalesce(countsAfter("CountAfter"), lit(0)).alias("CountAfter"))
    .orderBy("response")

  comparedResults.show()


I also had to add

import spark.implicits._

On top.


*explanation:
This code segment compares the number of log lines per response code before and after a specified timestamp in a Spark DataFrame. It first filters the data into two groups: countsBefore for entries before the timestamp and countsAfter for those on or after the timestamp. Each group is then aggregated by response code to count entries. The results are joined on the response code, ensuring no data is lost with an outer join, and zeros are filled in where counts are missing. Finally, it orders the results by response code and displays the comparison. The import spark.implicits._ enables the use of the $"columnName" syntax for easier DataFrame column referencing.


