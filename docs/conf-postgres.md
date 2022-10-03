# Configuring PostgreSQL for Monitoring

Monitoring PostgreSQL metrics with the [postgres_exporter](https://github.com/wrouesnel/postgres_exporter) is enabled by `ssm-admin add postgresql` command. The `postgresql` alias will set up `postgresql:metrics` and also `linux:metrics` on a host (for more information, see [Adding monitoring services](ssm-admin.md)).

`ssm-admin` supports passing PostgreSQL connection information via following flags:

| Flag         | Description         |
| ------------ | ------------------- |
| `--host`     | PostgreSQL host     |
| `--password` | PostgreSQL password |
| `--port`     | PostgreSQL port     |
| `--user`     | PostgreSQL user     |

An example command line would look like this:

```
ssm-admin add postgresql --host=localhost --password='secret' --port=5432 --user=ssm_user
```

!!! alert alert-info "Note"
    Capturing read and write time statistics is possible only if `track_io_timing` setting is enabled. This can be done either in configuration file or with the following query executed on the running system:

```
ALTER SYSTEM SET track_io_timing=ON;
SELECT pg_reload_conf();
```

## Supported versions of PostgreSQL

SSM follows [postgresql.org EOL policy](https://www.postgresql.org/support/versioning/), and thus supports monitoring PostgreSQL version 9.4 and up.  Older versions may work, but will not be supported.

### Setting Up the Required Permissions

We recommends that a PostgreSQL user be configured for `SUPERUSER` level access, in order to gather the maximum amount of data with a minimum amount of complexity. This can be done with the following command for the standalone PostgreSQL installation:

```
CREATE USER ssm_user WITH SUPERUSER ENCRYPTED PASSWORD 'secret';
```

!!! alert alert-info "Note"
    In case of monitoring a PostgreSQL database running on an Amazon RDS instance, the command should look as follows:

    ```
    CREATE USER ssm_user WITH rds_superuser ENCRYPTED PASSWORD 'secret';
    ```
