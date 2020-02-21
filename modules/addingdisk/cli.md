# Adding disk space to an MSK cluster using the CLI

As a prerequisite for this, you will need to have:

* [Your cluster ARN](/modules/commontasks/getclusterarn.md) - this will be `<cluster ARN>` below
* [Your Command Line/aws cli configurated](/modules/commontasks/setupawscli.md)

You will also need to know what size you want the disks to be - you will provide the new value, not an increment to grow by.  You can get the current value with:

        $ aws kafka describe-cluster --cluster-arn <cluster ARN> --output json | grep VolumeSize
                    "VolumeSize": 2000

This value will be `<New Volume size>` below


---

1. Get your Current-cluster-version, which is a hash that identifies your config

        $ aws kafka describe-cluster <ClusterARN>  --output json | grep CurrentVersion
        "CurrentVersion": "K3AEGXETSR30VB",

Grab this value (minus the quotes) for the next command.  This value will be `<Current-Cluster-Version>` below

2. Expand the disk volume size

        $ aws kafka update-broker-storage --cluster-arn <ClusterArn> --current-version <Current-Cluster-Version> --target-broker-ebs-volume-info '{"KafkaBrokerNodeId": "All", "VolumeSizeGB": < New volume size >}' 

This will return a JSON object that contains an ARN for the action that's taking place.  Copy this for the next step.

3. Monitor the progress of the change

        $ aws kafka describe-cluster-operation --cluster-operation-arn "<cluster operations ARN>"

This will give you an output similar to this:

    $ aws kafka describe-cluster-operation --cluster-operation-arn "<cluster ARN>"
    {
        "ClusterOperationInfo": {
            "ClientRequestId": "390aaa23-579a-49b7-bb33-e5f39f68ecd1",
            "ClusterArn": "arn:aws:kafka:us-east-1:1553xyz16955788:cluster/ToddTest2/c2209be6-9efd-4cd8-9602-60e6220fd84c-6",
            "CreationTime": "2020-02-21T20:31:52.872Z",
            "OperationArn": "arn:aws:kafka:us-east-1:xyz:cluster-operation/ToddTest2/c2209be6-9efd-4cd8-9602-60e6220fd84c-6/8ce20ff9-6617-4139-a49f-e19c9175d4b4",
            "OperationState": "UPDATE_IN_PROGRESS",
            "OperationType": "UPDATE_BROKER_EBS_VOLUME",
            "SourceClusterInfo": {
                "BrokerEBSVolumeInfo": [
                    {
                        "KafkaBrokerNodeId": "All",
                        "VolumeSizeGB": 2000
                    }
                ]
            },
            "TargetClusterInfo": {
                "BrokerEBSVolumeInfo": [
                    {
                        "KafkaBrokerNodeId": "All",
                        "VolumeSizeGB": 2500
                    }
                ]
            }
        }
    }


You can see the config you've pushed to the cluster to be implemented, as well as the `OperationState` - it will say `UPDATE_IN_PROGRESS` until it's done, when it will change to "UPDATE_COMPLETE"


# Resources

* [Scaling up broker storage using the AWS CLI](https://docs.aws.amazon.com/msk/latest/developerguide/msk-update-storage.html)
