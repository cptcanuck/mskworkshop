# Adding brokers to MSK via the AWS Console

1. Log in to the console for the account with the cluster you want to modify

1. Open the Amazon MSK Console - https://console.aws.amazon.com/msk/

![img](/_media/modules/addingbrokers/mskconsoleclick.png)

3. Choose the MSK cluster you want to modify and click on the name

![img](/_media/modules/addingbrokers/mskclickcluster.png)

4. Scroll to the **Brokers** section and select **Edit**

![img](/_media/modules/addingbrokers/mskclusteredit.png)

5. Enter the total number of brokers you want to have *in each availability zone* and select **Save Changes**

![img](/_media/modules/addingbrokers/mskeditbrokernum.png)

Notice that you will be notified about the total number of Kafka brokers when the change is complete - ensure this is what you want

6. You will be returned to the Cluster overview page to wait

Notice that there is a status bar at the top which indicates there is a cluster update in process (Updating the number of brokers per AZ)
![img](/_media/modules/addingbrokers/mskupdatebar.png)


Also note that the *Status* of the cluster is **Updating**

![img](/_media/modules/addingbrokers/mskstatusupdating.png)

The expansion operation will take some time (10+ minutes) so be patient, and you can go ahead with reading more about how to [reassign partitions](/modules/addingbrokers/reassignpartitions.md) while you wait.

7. When the change is done and the cluster is expanded, you will see a green bar in the console letting you MSK has successfully updated the number of brokers

![img](/_media/modules/addingbrokers/mskdonechange.png)

8. You can now [reassign partitions](/modules/addingbrokers/reassignpartitions.md) to the new brokers.



## Reference Documentation

* [Expanding an MSK Cluster - Official AWS Documentation](https://docs.aws.amazon.com/msk/latest/developerguide/bestpractices.html)
* [Expanding a Kafka cluster - official Kafka Documentation](https://kafka.apache.org/documentation/#basic_ops_cluster_expansion)