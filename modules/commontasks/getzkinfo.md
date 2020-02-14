# Get your MSK Zookeeper Connection String

There will be times when you need your [Zookeeper](https://docs.aws.amazon.com/console/msk/zookeeper/documentation) connection string such as using various kafka utilities.  This string will be a list of hostnames and ports that the application will use to connect to Zookeeper and gather required data.  

It is **strongly** reccomended you do not modify or reuse the provided Zookeeper servers in any way.  The connection provided is for applications to gather data about the cluster.  Modifying the contents of Zookeeper directly can cause cluster failure and data loss.

## Using the AWS Console

1. Open the MSK console at https://console.aws.amazon.com/msk/

1. Click on the name of the cluster you want the details for

![mskclusterclick](_media/modules/commontasks/mskclickcluster.png)

3. Click on **View client information** in the **Cluster summary** section

![buttonhighlight](_media/modules/commontasks/mskviewclientinfobutton.png)

4. Click the **copy** button in the **ZooKeeper connect** section

![copyhighlight](_media/modules/commontasks/mskzookeeperdata.png)

## Using the AWS CLI

1. [Get your ClusterARN](/modules/commontasks/getclusterarn.md)

1. Use the CLI to describe the cluster with the ARN provided:

`aws kafka describe-cluster --cluster-arn arn:aws:kafka:us-east-1:xyz:cluster/MSKCluster/0546f493-019f-475a-9903-272f0371ce19-6 --output json | jq ".ClusterInfo.ZookeeperConnectString"`

`z-3.mskcluster.xyz.c6.kafka.us-east-1.amazonaws.com:2181,z-1.mskcluster.xyz.c6.kafka.us-east-1.amazonaws.com:2181,z-2.mskcluster.xyz.c6.kafka.us-east-1.amazonaws.com:2181"`

**Tip**

If you're working on the command line, and to save yourself some work, put your ZooKeeper connection string into an envrionment variable:

`$ export ZK_CONNECT="zkhost1:2181,zkhost2:2181,zkhost3:2181"`

Then you can refer to the variable in later commands:

`$ bin/kafka-topcs.sh --zookeeper $ZK_CONNECT --list`

