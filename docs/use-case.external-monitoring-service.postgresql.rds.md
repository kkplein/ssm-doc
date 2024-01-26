# Use case: Monitoring a PostgreSQL database running on an Amazon RDS instance

As of version 1.14.0 SSM supports PostgreSQL [out-of-the-box](conf-postgres.md).

This example demonstrates how to start monitoring a PostgreSQL host which is installed on an Amazon RDS instance.

!!! alert alert-warning "Important"
    This use case is limited to demonstrating the essential part of using external monitoring services of SSM and should be treated as an example. As such, it does not demonstrate how to use the security features of Amazon RDS or of the Prometheus exporter being used.

## Set Up the PostgreSQL Exporter

First, you need to enable an exporter for PostgreSQL on the computer where you have installed the SSM Client package with the `ssm-admin add` command:

```
ssm-admin add postgresql --host=172.17.0.2 --password=ABC123 --user=ssm_user
```

More information on enabling and configuring PostgreSQL exporter can be found in the [detailed instructions](conf-postgres.md).

## Check Settings of Your Amazon RDS Instance

Your Amazon RDS instance where you have installed PostgreSQL must be allowed to communicate outside of the VPC hosting the DB instance. Select *Yes* in the Public accessibility field.

## Add monitoring service for PostgreSQL

To make the metrics from your Amazon RDS instance available to SSM, you need to run **ssm-admin add** command as follows:

Run this command as root or by using the **sudo** command

```
ssm-admin add postgresql --host=172.17.0.1 --password=ABC123 --port=5432 --user=ssm_user postgresql_rds01
```

The last parameter gives a distinct name to your host. If you do not specify a custom instance name, the name of the host where you run **ssm-admin add** is used automatically. The command adds the given PostgreSQL instance to both system and metrics monitoring, and confirms that now monitoring the given system and the PostgreSQL metrics on it. Also **ssm-admin list** command can be used further to
see more details:

```
$ ssm-admin list
ssm-admin 1.8.0

SSM Server      | 127.0.0.1
Client Name     | ssm
Client Address  | 172.17.0.1
Service Manager | linux-systemd

...

Job name  Scrape interval  Scrape timeout  Metrics path  Scheme  Target           Labels                       Health
postgres  1m0s             10s             /metrics      http    172.17.0.1:9187  instance="postgresql_rds01"  DOWN
```

## Viewing PostgreSQL Metrics in SSM

Now, open Metrics Monitor in your browser and select the [PostgreSQL Overview dashboard](dashboard.postgres-overview.md) either using the Dashboard Dropdown or the PostgreSQL group of the navigation menu:
