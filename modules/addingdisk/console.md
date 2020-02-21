# Adding more disk space to your MSK cluster

1. Open the Amazon MSK console at https://console.aws.amazon.com/msk/.

1. Choose the MSK cluster for which you want to update broker storage.

1. In the Storage section, choose Edit.

1. Specify the storage volume you want - for the workshop, add 100mb of storage.

**Note** that you can only increase the amount of storage, you can't decrease it.

1. Choose Save changes.

The change will be applied in the background, with no interuption to cluster operations.



# Resources

* [Scaling up broker storage](https://docs.aws.amazon.com/msk/latest/developerguide/msk-update-storage.html)