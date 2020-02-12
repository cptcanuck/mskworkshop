# Adding brokers to an MSK Cluster

While you did your [homework](https://amazonmsk.s3.amazonaws.com/MSK_Sizing_Pricing.xlsx) and followed [best practices](https://docs.aws.amazon.com/msk/latest/developerguide/bestpractices.html), your workload has grown and you need to make your MSK cluster bigger to support additional producers, consumers, retention, etc.

This module will walk you through the process of adding brokers to your cluster, both on the Console and using the CLI

After you are done adding brokers, you will need to rebalance the cluster to assign partitions and replicas to the new brokers, otherwise they will just sit there empty.

Some important things to note:

* With MSK you can only scale in units that match your number of deployed AZs - if you deploy with 3 AZs, you can only scale up by 3 brokers at a time

* When you add brokers, they will be idle until you [assign partitions](/modules/addingbrokers/reassignparitions.md) to the new brokers
* Migrating partitions will take time while data is replicated to the new brokers, and *could* impact the performance of the cluster
  * ideally don't do this while under full load in production

* You are adding brokers to a cluster, so there will be an [additional cost](https://aws.amazon.com/msk/pricing/) to operate your MSK cluster based on your instance size