# Reassign Partitions on an MSK Cluster

Your MSK cluster has grown, you've added new brokers.  But, new brokers will just sit there idle until you assign them some work.  This lab will show you how to accomplish this.  

You will need a text editor to keep notes.  For this section you will need:

* [Your Zookeeper connection string](/modules/commontasks/getzkinfo.md)
* To have completed an expansion of your MSK cluster using the [console](/modules/addingbrokers/console.md) or [cli](/modules/addingbrokers/cli.md)


## What are we doing?

Each broker is assigned a number of partitions - a partition is assigned to a broker at the creation time of the topic (which includes partition creation) and/or addition of partitions to a cluster.

We are going to use a [native kafka tool](https://cwiki.apache.org/confluence/display/KAFKA/Replication+tools#Replicationtools-4.ReassignPartitionsTool) to do this assignment.  The basic steps are:

* Generate a list of topics that you want to move 
  * This may be a subset of topics (topic1, topic2), or all your topics (if you want to rebalance the whole cluster)
  * Rebalancing a whole cluster may take a long time and will generate a lot of load on the cluster as data moves around - only do this if you know you need/want to

* Use `kafka-reassign-partitions` tool to generate a reassignment template

* If the reassignment plan looks good, we will execuate the template and start the reassignment
  * We can also edit the template to our liking to tweak the generated suggestions

* Finally, we can monitor the status of the reassignment as we wait for it to complete



## Reassign Partitions




## Additional Reading

* [Kafka cluster expansion and partition reassignment](https://kafka.apache.org/documentation/#basic_ops_cluster_expansion)