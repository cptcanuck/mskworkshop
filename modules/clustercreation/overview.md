# Overview

This module will step you through the creation of a custom configuration and an MSK Cluster, using both the Console and CLI.

## Custom Configuration
The custom configuration will enable us to provide special configuration to the cluster.  This can only be done at cluster creation time - it's not currently possible to modify these settings on a live cluster, so plan ahead and [review the available options](https://docs.aws.amazon.com/msk/latest/developerguide/msk-configuration-properties.html) to make sure you have what you need.

## Cluster
The cluster will be deployed into an existing VPC, with brokers deployed in 3 private subnets (one per AZ).  We will use `m5.large` nodes for this exercise.  If you are using an existing VPC, please ensure that there is a private subnet in each AZ for you to deploy in to.

When doing the CLI deploy, you will need to provide a number of inputs.  It's handy to have open a text editor of your choice to keep the details in.


## Architecture

![msk-arch](https://docs.aws.amazon.com/msk/latest/developerguide/images/msk-architecture-visio-reduced-size.png)

The diagram demonstrates the interaction between the following components:

* **Broker nodes** — When creating an Amazon MSK cluster, you specify how many broker nodes you want Amazon MSK to create in each Availability Zone. In the example cluster shown in this diagram, there's one broker per Availability Zone. Each Availability Zone has its own virtual private cloud (VPC) subnet.

* **ZooKeeper nodes** — Amazon MSK also creates the Apache ZooKeeper nodes for you. Apache ZooKeeper is an open-source server that enables highly reliable distributed coordination.

* **Producers, consumers, and topic creators** — Amazon MSK lets you use Apache Kafka data-plane operations to create topics and to produce and consume data.

* **AWS CLI** — You can use the AWS Command Line Interface (AWS CLI) or the APIs in the SDK to perform control-plane operations. For example, you can use the AWS CLI or the SDK to create or delete an Amazon MSK cluster, list all the clusters in an account, or view the properties of a cluster.