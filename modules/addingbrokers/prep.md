# Preparation for adding brokers

If you want to add brokers to the MSK cluster, you *must* use the MSK tools (Console, CLI) to do this - do not do it directly by building brokers and updating ZK.  This will leave the cluster in an inconsistent state, and further operations on the cluster through MSK may remove the nodes you added manually.

As a general rule, don't touch Zookeeper.

Follow the instructions for the process you want to follow:

* [Adding brokers via the AWS Console](modules/addingbrokers/console.md)
* [Adding brokers via the Command Line Interface (CLI)](modules/addingbrokers/cli.md)