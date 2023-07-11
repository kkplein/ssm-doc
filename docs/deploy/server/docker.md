# Running SSM Server via Docker

Docker images of SSM Server are stored at the [shatteredsilicon/ssm-server](https://hub.docker.com/r/shatteredsilicon/ssm-server/tags/) public repository. The host must be able to run Docker 1.12.6 or later, and have network access.

SSM needs roughly 1GB of storage for each monitored database node with data retention set to one week. Minimum memory is 2 GB for one monitored database node, but it is not linear when you add more nodes.  For example, data from 20 nodes should be easily handled with 16 GB.

Make sure that the firewall and routing rules of the host do not constrain the Docker container. For more information, see [How to troubleshoot communication issues between SSM Client and SSM Server?](../../faq.md#how-to-troubleshoot-communication-issues-between-ssm-client-and-ssm-server).

For more information about using Docker, see the [Docker Docs](https://docs.docker.com).

!!! important
    By default, [retention](../../glossary.terminology.md#data-retention) is set to 30 days for Metrics Monitor and to 8 days for SSM Query Analytics.  Also consider [disabling table statistics](../../faq.md#what-are-common-performance-considerations), which can greatly decrease Prometheus database size.


* [Setting Up a Docker Container for SSM Server](docker.setting-up.md)
* [Updating SSM Server Using Docker](docker.upgrading.md)
* [Backing Up SSM Data from the Docker Container](docker.backing-up.md)
* [Restoring the Backed Up Information to the SSM Data Container](docker.restoring.md)
