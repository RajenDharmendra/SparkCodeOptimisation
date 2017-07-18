# SparkCodeOptimisation
Tune  Apache Spark Jobs 

* Avoid groupByKey when performing an associative reductive operation. For example, rdd.groupByKey().mapValues(_.sum) will produce the same results as rdd.reduceByKey(_ + _). However, the former will transfer the entire dataset across the network, while the latter will compute local sums for each key in each partition and combine those local sums into larger sums after shuffling.


* Avoid reduceByKey When the input and output value types are different. For example, consider writing a transformation that finds all the unique strings corresponding to each key. One way would be to use map to transform each element into a Set and then combine the Sets with reduceByKey

* Avoid the flatMap-join-groupBy pattern. When two datasets are already grouped by key and you want to join them and keep them grouped, you can just use cogroup. That avoids all the overhead associated with unpacking and repacking the groups. 
