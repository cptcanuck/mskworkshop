# Adding disk space to our MSK cluster

As you use your MSK cluster, you will start to retain data and see the data volume usage grow (see [cloudwatch monitoring](/modules/cloudwatchmonitoring/overview.md) for more details).  This is normal as the cluster will retain data for as long as you've configured it to be kept.

But what happens when the cluster keeps growing, and you've looked at your growth and retention and realize, you're going to need more storage?  Never fear, storage can be scaled **up** in your MSK cluster.  It's a quick, painless, online operation that will quickly add more capacity to your cluster.

Some notes to consider:

* While there is a default retention set for your cluster, you can also set retention on a per topic basis.  If you have some topics you only need short retention on, go ahead and lower it on a per topic basis to save some space.

* Kafka does not handle running out of disk space well.  Brokers will safely shut down and will not restart until there is enough disk space to safely start again.  

* We **strongly** urge you to setup Cloudwatch alarms (or other monitoring) that will warn you when your cluster or brokers are getting low on disk space.  A little monitoring can save you downtime.

* You can only expand the disk on the brokers the same amount on every broker.  This means if you have one broker that is filling up and you want to add more space, you will be adding space to every node.

* As you grow your disk capacity, there will be additional charges for the additional storage.