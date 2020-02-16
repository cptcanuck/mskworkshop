# Creating an MSK Cluster using the CLI

## Prep

In order to create a cluster on using the CLI, we will need to gather a bunch of information so we can build the cluster definition.

### Subnets

We need to get the subnets to deploy the brokers in to.  For that, we need to know the VPC ID for the lab.  

1. Use the cli to get a list of VPCs in your account

`aws ec2 describe-vpcs --output table`

1. Look in the table for the VPC you're using for the exercise.  If you created a new VPC as per the [prep](/modules/clustercreation/prep.md) step, then you want the VPC called "AWSKafkaTutorialVPC".  If you are using the VPC created as part of the workshop event, it will be named "MMVPC"

1. Copy the VPCid (example: vpc-001ed0757f999e2b5) to your notepad

1. Use the cli to get a list of subnets in that VPC:

`aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-001ed0757fbb9e2b5" --output table | egrep "Name|AvailabilityZone|SubnetId"`

This will list the subnets in the selected VPC, then grab only the AZ, SubnetID, and Name, making it easier for you to grab the SubnetIds for the 3 private subnets in 3 different AZs.  Add these to your notepad for later use.

Example:

    [ec2-user@ip-10-0-0-245 ~]$ aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-XYZ" --output table | egrep "Name|AvailabilityZone|SubnetId"
    ||  AvailabilityZone                       |  us-east-1c                                                                                    
    ||  AvailabilityZoneId                     |  use1-az6                                                                                     
    ||  SubnetId                               |  subnet-05e9ee503739783a4                                                                      
    |||  Name                         |  MMPrivateSubnetThree                                                                                  
    ||  AvailabilityZone                       |  us-east-1a                                                                                    
    ||  AvailabilityZoneId                     |  use1-az2                                                                                      
    ||  SubnetId                               |  subnet-054990841567825d4               
    |||  Name                         |  MMPrivateSubnetOne                                                       

## Create the cluster definition file

To complete this step, you need the following

  * Private SubnetID us-east-1a (from previous step)
  * Private SubnetID us-east-1b (from previous step)
  * Private SubnetID us-east-1c (from previous step)
  * Securitygroup ID for the SG "MSKWorkshopKafkaService" (from [preparation](/modules/clustercreation/prep.md) stage)
  * Cluster configuration ARN (from [preparation](/modules/clustercreation/prep.md) stage)

You will now combine the data above into a cluster definition file (`clusterinfo.json`).  It will look something like this, where you will replace the values with the values from above:

Example of a complete file:

    {
        "BrokerNodeGroupInfo": {
            "BrokerAZDistribution": "DEFAULT",
            "InstanceType": "kafka.m5.large",
            "ClientSubnets": [
                "subnet-05e9ee503739783a4", "subnet-054990841567825d4", "subnet-07af438a99fe7f508"
            ],
            "SecurityGroups": [
                "sg-008cf48ee78b732ef"
            ]
        },
        "ClusterName": "MSKWorkshopCluster",
        "ConfigurationInfo": {
            "Arn": "arn:aws:kafka:us-east-1:xyz:configuration/WorkshopMSKConfig/2d99aad1-a420-4f62-83c1-0e2473aea998-6",
            "Revision": 1
        },
        "EncryptionInfo": {
            "EncryptionAtRest": {
                "DataVolumeKMSKeyId": ""
            },
            "EncryptionInTransit": {
                "InCluster": true,
                "ClientBroker": "TLS_PLAINTEXT"
            }
        },
        "EnhancedMonitoring": "PER_TOPIC_PER_BROKER",
        "KafkaVersion": "2.3.1",
        "NumberOfBrokerNodes": 3,
        "OpenMonitoring": {
            "Prometheus": {
                "JmxExporter": {
                    "EnabledInBroker": true
                },
                "NodeExporter": {
                    "EnabledInBroker": true
                }
            }
        }
    }

## Create the cluster

We can now use the command line tool and the cluster definition to create the cluster:

`aws kafka create-cluster --cli-input-json file://clusterinfo.json`