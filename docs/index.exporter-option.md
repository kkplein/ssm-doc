# Exporters Overview

This is a list of exporters that Shattered Silicon Monitoring and Management uses to provides metrics from the supported systems. For each exporter, you may find information about the options that can be passed directly to the Prometheus.  when running **ssm-admin add**.

The exporter options are passed along with the monitoring service after two dashes (`--`).

```
$ ssm-admin add mongodb:metrics -- --mongodb.tls
```

* MongoDB Exporter (mongodb_exporter)
* MySQL Server Exporter (mysqld_exporter)
* Node Exporter (node_exporter)
* ProxySQL Server Exporter (proxysql_exporter)
* Amazon RDS Exporter (rds_exporter)
