# Backing Up SSM Data from the Docker Container

When SSM Server is run via Docker, its data are stored in the `ssm-data` container. To avoid data loss, you can extract the data and store outside of the container.

This example demonstrates how to back up SSM data on the computer where the Docker container is run and then how to restore them.

To back up the information from `ssm-data`, you need to create a local directory with essential sub folders and then run Docker commands to copy SSM related files into it.

1. Create a backup directory and make it the current working directory. In this example, we use *ssm-data-backup* as the directory name.

    ```
    $ mkdir ssm-data-backup; cd ssm-data-backup
    ```

2. Create the essential sub directories:

    ```
    $ mkdir -p opt/prometheus
    $ mkdir -p var/lib
    ```

Run the following commands as root or by using the **sudo** command

1. Stop the docker container:

    ```
    $ docker stop ssm-server
    ```

2. Copy data from the `ssm-data` container:

    ```
    $ docker cp ssm-data:/opt/prometheus/data opt/prometheus/
    $ docker cp ssm-data:/opt/consul-data opt/
    $ docker cp ssm-data:/var/lib/mysql var/lib/
    $ docker cp ssm-data:/var/lib/grafana var/lib/
    ```

Now, your SSM data are backed up and you can start SSM Server again:

```
$ docker start ssm-server
```
