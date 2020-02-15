# Creating an MSK Cluster using the Console

Creating and MSK cluster is quick and easy using the Console.  A few steps and you're off!

**Note** that it can take some time to get the cluster up and running (15+ minutes).


1. Sign into the AWS Console in the account you want to create your cluster in

1. Browse to [the MSK create cluster wizzard](https://console.aws.amazon.com/msk/home?region=us-east-1#/cluster/create) to start the creation

1. Enter the cluster name - "MSK Workshop Cluster"
1. Select the version of Kafka you want to run on the cluster (ie: 2.3.1)
1. Select 'Use a custom configuration supporting Apache Kafka x.y.z' (based on version selected above)
1. Select the custom configuration you created in the [prep step](/modules/clustercreation/prep.md) from the drop down (WorkstopMSKConfig)