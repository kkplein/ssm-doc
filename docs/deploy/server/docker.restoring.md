# Restoring the Backed Up Information to the SSM Data Container

If you have a backup copy of your `ssm-data` container, you can restore it into a Docker container. Start with renaming the existing SSM containers to prevent data loss, create a new `ssm-data` container, and finally copy the backed up information into the `ssm-data` container.

Run the following commands as root or by using the **sudo** command

1. Stop the running `ssm-server` container.

    ```
    $ docker stop ssm-server
    ```

2. Rename the `ssm-server` container to `ssm-server-backup`.

    ```
    $ docker rename ssm-server ssm-server-backup
    ```

3. Rename the `ssm-data` to `ssm-data-backup`

    ```
    $ docker rename ssm-data ssm-data-backup
    ```

4. Create a new `ssm-data` container

    ```
    $ docker create \
       -v /opt/prometheus/data \
       -v /opt/consul-data \
       -v /var/lib/mysql \
       -v /var/lib/grafana \
       --name ssm-data \
       shatteredsilicon/ssm-server:latest /bin/true
    ```

!!! alert alert-warning "Important"
    The last step creates a new `ssm-data` container based on the `shatteredsilicon/ssm-server:latest` image. If you do not intend to use the `latest` tag, specify the exact version instead, such as **8.6.1.17.5.2-1**. You can find all available versions of `ssm-server` images at [shatteredsilicon/ssm-server](https://hub.docker.com/r/shatteredsilicon/ssm-server/tags/).

Assuming that you have a backup copy of your `ssm-data`, created according to the procedure described in [Backing Up SSM Data from the Docker Container ](docker.backing-up.md), restore your data as follows:

1. Change the working directory to the directory that contains your `ssm-data` backup files.

    ```
    $ cd ~/ssm-data-backup
    ```

    !!! alert alert-info "Note"
        This example assumes that the backup directory is found in your home directory.

2. Copy data from your backup directory to the `ssm-data` container.

    ```
    $ docker cp opt/prometheus/data ssm-data:/opt/prometheus/
    $ docker cp opt/consul-data ssm-data:/opt/
    $ docker cp var/lib/mysql ssm-data:/var/lib/
    $ docker cp var/lib/grafana ssm-data:/var/lib/
    ```

3. Apply correct ownership to `ssm-data` files:

    ```
    $ docker run --rm --volumes-from ssm-data -it shatteredsilicon/ssm-server:latest chown -R ssm:ssm /opt/prometheus/data /opt/consul-data
    $ docker run --rm --volumes-from ssm-data -it shatteredsilicon/ssm-server:latest chown -R grafana:grafana /var/lib/grafana
    $ docker run --rm --volumes-from ssm-data -it shatteredsilicon/ssm-server:latest chown -R mysql:mysql /var/lib/mysql
    ```

4. Run (create and launch) a new `ssm-server` container:

    ```
    $ docker run -d \
       -p 80:80 \
       --volumes-from ssm-data \
       --name ssm-server \
       --restart always \
       shatteredsilicon/ssm-server:latest
    ```

To make sure that the new server is available run the **ssm-admin check-network** command from the computer where SSM Client is installed. Run this command as root or by using the **sudo** command.

```
$ ssm-admin check-network
```
