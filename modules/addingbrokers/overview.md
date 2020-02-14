# Adding brokers to an MSK Cluster

While you did your [homework](https://amazonmsk.s3.amazonaws.com/MSK_Sizing_Pricing.xlsx) and followed [best practices](https://docs.aws.amazon.com/msk/latest/developerguide/bestpractices.html), your workload has grown and you need to make your MSK cluster bigger to support additional producers, consumers, retention, etc.

This module will walk you through the process of adding brokers to your cluster, both on the Console and using the CLI

After you are done adding brokers, you will need to rebalance the cluster to assign partitions and replicas to the new brokers, otherwise they will just sit there empty.

---
**TODO** Add before/after diagrams here

---

## Preparation

Before we expand the cluster, and in preparation for lab 2 (reassigning partitions) we are going to create a topic on the pre-resized cluster, so we can then reassign partitions after.

This is pretty straight forward if you've completed the other labs to this point.  We are going to create a topic with 10 partitions, 3 replicas.

`$ bin/kafka-topics.sh --zookeeper $ZK_STRING --topic test10 --partitions 10 --replication-factor 3`

Now you can move on expanding your cluster either via the [console](/modules/addingbrokers/console.md) or [CLI](/modules/addingbrokers/cli.md).


## Important Tidbits

* With MSK you can only scale in units that match your number of deployed AZs - if you deploy with 3 AZs, you can only scale up by 3 brokers at a time

* When you add brokers, they will be idle until you [assign partitions](/modules/addingbrokers/reassignparitions.md) to the new brokers

* Migrating partitions will take time while data is replicated to the new brokers, and *could* impact the performance of the cluster

  * ideally don't do this while under full load in production

* You are adding brokers to a cluster, so there will be an [additional cost](https://aws.amazon.com/msk/pricing/) to operate your MSK cluster based on your instance size


## A note and warning about Zookeeper

If you want to add brokers to the MSK cluster, you *must* use the MSK tools (Console, CLI) to do this - do not do it directly by building brokers and updating ZK.  This will leave the cluster in an inconsistent state, and further operations on the cluster through MSK may remove the nodes you added manually.

As a general rule, don't touch Zookeeper.  Nothing good will come of it.