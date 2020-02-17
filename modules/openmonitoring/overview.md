# Openmonitoring Overview

Kafka emits a very large number of metrics via JMX, many of which can be useful for tuning the performance of your cluster, producers, and consumers.  However, at that large volume comes complexity with monitoring.  By default, MSK clusters come with Cloudwatch monitoring of your essential metrics, but if you want access to the full suite of metrics, you can now use Open Monitoring with Prometheus.  This feature enables you to scrape a Prometheus friendly API to gather all the JMX metrics and work with the data in the popular open source monitoring tool Prometheus.

[TODO: Insert diagram of how this works]

This workshop will walk you through setting up this system and getting essential monitoring in place.

---

## Resources

* [Open Monitoring with Prometheus](https://docs.aws.amazon.com/msk/latest/developerguide/monitoring.html#open-monitoring)
