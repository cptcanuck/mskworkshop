# Creating an MSK Cluster using the Console

Creating and MSK cluster is quick and easy using the Console.  A few steps and you're off!

**Note** that it can take some time to get the cluster up and running (15+ minutes).


1. Sign into the AWS Console in the account you want to create your cluster in

1. Browse to [the MSK create cluster wizzard](https://console.aws.amazon.com/msk/home?region=us-east-1#/cluster/create) to start the creation

1. Enter the cluster name - "MSKWorkshopCluster"
1. Select the version of Kafka you want to run on the cluster (ex: 2.3.1)

## Configuration Section
1. Select 'Use a custom configuration supporting Apache Kafka x.y.z' (based on version selected above)
1. Select the custom configuration you created in the [prep step](/modules/clustercreation/prep.md) from the drop down (WorkstopMSKConfig)

## Networking Section

1. Select the VPC you want to deploy your cluster in (GET FROM CFN TEMPLATE)

1. Select the number of availability zones you want to deploy in to (3)
1. Select `us-east-1a` for the first Availability Zone (AZ), then the subnet (MSKLabSubnet1 GET FROM CFN)
1. Select 'us-east-1b' for the second AZ, and the appropriate subnet
1. Select 'us-east-1c' for the third AZ, and the appropriate subnet

## Brokers

1. Select `kafka.m5.large` as the Broker Instance Type

1. Enter `1` for the number of brokers per AZ

## Tags

1. Under key enter `Name` and in value `MSKLabCluster`

## Storage

1. Enter 1000 GiB (default size)

## Encryption

**Tip**: You cannot enable encryption on an already created cluster, nor can you turn it off on a cluster configured with encryption, so plan your use carefully to avoid rebuilding to change these settings.

1. Select 'Enable Encryption within the cluster'

    Note that this can [impact the performance](https://docs.aws.amazon.com/msk/latest/developerguide/msk-encryption.html) of the cluster in production.  If you don't need this level of encryption consider leaving it off.

1. Select `Both TLS encrypted and plaintext traffic allowed`.  This will enable 2 different service ports on the cluster (9092 and 9094).  You will be able to communicate in both an encrypted and unencrypted manner - choose based on your data needs.  For this workshop we will experiment with both, but you should choose what fits your production environment best.  

1. Select `Use AWS managed CMK`.  This means Amazon will manage the encryption key for you.

## Authentication

1. Leave `Enable TLS client authentication` blank.  This feature as will be explored in other labs.

## Monitoring

There are 2 types of monitoring available for MSK - Cloudwatch monitoring which is available in 3 flavours (Basic, Enhanced broker-level, Enhanced topic-level), as well as the Open Monitoring with Prometheus.  We will use both.

1. Select `Enhanced topic-level monitoring`.  This will enable collection of metrics from each broker at the topic level.  This generates more metrics and incurs additional costs, but will also let you troubleshoot and understand your traffic better.

1. Select `Enable open monitoring with Prometheus`

## Advanced Settings

In advanced settings, you can customize the security groups assocated with your cluster.  In the prep step, we created a security group called **MSK Service** and we will attach that as well.

1. Select `Customize Settings`, then in the drop down box select the `MSKWorkshopKafkaService` security group

## And off we go!

Click **Create Cluster** - voila!  Your cluster is being built.


---
# References

* [MSK Encryption](https://docs.aws.amazon.com/msk/latest/developerguide/msk-encryption.html)

