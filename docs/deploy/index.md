# Deploying Shattered Silicon Monitoring

SSM is designed to be scalable for various environments.  If you have just one MySQL or MongoDB server, you can install and run both server and clients on one database host.

It is more typical to have several MySQL and MongoDB server instances distributed over different hosts. In this case, you need to install the client package on each database host that you want to monitor. In this scenario, the  server is set up on a dedicated monitoring host.

In this chapter

[TOC]

## Installing SSM Server

To install and set up the SSM Server, use one of the following options:

* [Running SSM Server via Docker](server/docker.md)

!!! important
    On each computer where SSM Client is installed, the [following ports](../glossary.terminology.md#ports) must be open. These are default ports that you can change when adding the respective monitoring service with the `ssm-admin add` command.

    !!! seealso "See also"
        Improving security
        : [Security Features in Shattered Silicon Monitoring](../security.md)

### Verifying SSM Server

In your browser, go to the server by its IP address. If you run your server as a virtual appliance or by using an Amazon machine image, you will need to setup the user name, password and your public key if you intend to connect to the server by using ssh. This step is not needed if you run SSM Server using Docker.

In the given example, you would need to direct your browser to *http://192.168.100.1*. Since you have not added any monitoring services yet, the site will not show any data.

You can also check if SSM Server is available requesting the /ping URL as in the following example:

```
$ curl http://192.168.100.1/ping
{'version': '8.7.1.17.5.2'}
```

## Installing Clients

SSM Client is a package of agents and exporters installed on a database host that you want to monitor. Before installing the SSM Client package on each database host that you intend to monitor, make sure that your SSM Server host is accessible.

For example, you can run the **ping** command passing the IP address of the computer that SSM Server is running on. For example:

```
$ ping 192.168.100.1
```

You will need to have root access on the database host where you will be installing SSM Client (either logged in as a user with root privileges or be able to run commands with **sudo**).

### Supported platforms

SSM Client should run on any modern Linux 64-bit distribution, however Shattered Silicon provides SSM Client packages for automatic installation from software repositories only on the most popular Linux distributions:

* [DEB packages for Debian based distributions such as Ubuntu](#installing-ssm-client-on-debian-or-ubuntu)
* [RPM packages for Red Hat based distributions such as CentOS](#installing-the-ssm-client-package-on-red-hat-and-centos)

It is recommended that you install your  client by using the software repository for your system. If this option does not work for you, Shattered Silicon provides downloadable SSM Client packages from the [Download Shattered Silicon Monitoring](https://dl.shatteredsilicon.net/ssm/8/) page.

In addition to DEB and RPM packages, this site also offers:

* Generic tarballs that you can extract and run the included `install` script.
* Source code tarball to build your SSM client from source.

**WARNING**: You should not install agents on database servers that have the same host name, because host names are used by SSM Server to identify collected data.

### Storage requirements

Minimum **100** MB of storage is required for installing the SSM Client package. With a good constant connection to SSM Server, additional storage is not required. However, the client needs to store any collected data that it is not able to send over immediately, so additional storage may be required if connection is unstable or throughput is too low.

### Installing SSM Client on Debian or Ubuntu

Shattered Silicon provides `.deb` packages for 64-bit versions of the following distributions:

* Debian 8 (jessie)
* Debian 9 (stretch)
* Ubuntu 14.04 LTS (Trusty Tahr)
* Ubuntu 16.04 LTS (Xenial Xerus)
* Ubuntu 16.10 (Yakkety Yak)
* Ubuntu 17.10 (Artful Aardvark)
* Ubuntu 18.04 (Bionic Beaver)

!!! alert alert-info "Note"
    SSM Client should work on other DEB-based distributions, but it is tested only on the platforms listed above.

To install the SSM Client package, complete the following procedure. Run the following commands as root or by using the **sudo** command:

1. Go to [SSM download page](https://dl.shatteredsilicon.net/ssm/8/), download the appropriate version of SSM client for your GNU/Linux distribution:

    ```
    $ curl -O https://dl.shatteredsilicon.net/ssm/8/DEBS/ssm-client_8.7.1.17.5.2-1_amd64.deb
    ```

2. Install the SSM Client package:

    ```
    $ dpkg -i ssm-client_8.7.1.17.5.2-1_amd64.deb
    ```

### Installing the SSM Client Package on Red Hat and CentOS

If you are running an RPM-based Linux distribution, use the **yum** package manager to install SSM Client from the official Shattered Silicon software repository.

Shattered Silicon provides `.rpm` packages for 64-bit versions of Red Hat Enterprise Linux 6 (Santiago) and 7 (Maipo), including its derivatives that claim full binary compatibility, such as, CentOS, Oracle Linux, Amazon Linux AMI, and so on.

!!! alert alert-info "Note"
    SSM Client should work on other RPM-based distributions, but it is tested only on RHEL 8.

To install the SSM Client package, complete the following procedure. Run the following commands as root or by using the **sudo** command:

1. Install the `ssm-release` package to setup the official Shattered Silicon software repository:

    ```
    $ rpm -i https://dl.shatteredsilicon.net/ssm/9/ssm-release-1.1-1.el9.noarch.rpm
    ```

2. Install the `ssm-client` package:

    ```
    $ yum install ssm-client
    ```

    !!! alert alert-info "Note"
        You can also go to the [SSM download page](https://dl.shatteredsilicon.net/ssm/8/), download the appropriate version of SSM client for your GNU/Linux distribution.

## Connecting SSM Clients to the SSM Server

With your server and clients set up, you must configure each SSM Client and specify which SSM Server it should send its data to.

To connect a SSM Client, enter the IP address of the SSM Server as the value of the `--server` parameter to the **ssm-admin config** command.

Run this command as root or by using the **sudo** command

```
$ ssm-admin config --server 192.168.100.1:8080
```

For example, if your SSM Server is running on 192.168.100.1, and you have installed SSM Client on a machine with IP 192.168.200.1, run the following in the terminal of your client. Run the following commands as root or by using the **sudo** command:

```
$ ssm-admin config --server 192.168.100.1
OK, SSM server is alive.

SSM Server      | 192.168.100.1
Client Name     | ubuntu-amd641
Client Address  | 192.168.200.1
```

If you change the default port **80** when running SSM Server, specify the new port number after the IP address of SSM Server. For example:

```
$ ssm-admin config --server 192.168.100.1:8080
```

## Collecting Data from SSM Clients on SSM Server

To start collecting data on each SSM Client connected to a server, run the **ssm-admin add** command along with the name of the selected monitoring service.

Run the following commands as root or by using the **sudo** command.

Enable general system metrics, MySQL metrics, MySQL query analytics:

```
$ ssm-admin add mysql
```

Enable general system metrics, MongoDB metrics, and MongoDB query analytics:

```
$ ssm-admin add mongodb
```

Enable ProxySQL performance metrics:

```
$ ssm-admin add proxysql:metrics [NAME] [OPTIONS]
```

To see what is being monitored, run **ssm-admin list**. For example, if you enable
general OS and MongoDB metrics monitoring, the output should be similar to the
following:

```
$ ssm-admin list

...

SSM Server      | 192.168.100.1
Client Name     | ubuntu-amd64
Client Address  | 192.168.200.1
Service manager | linux-systemd

---------------- ----------- ----------- -------- ---------------- --------
SERVICE TYPE     NAME        LOCAL PORT  RUNNING  DATA SOURCE      OPTIONS
---------------- ----------- ----------- -------- ---------------- --------
linux:metrics    mongo-main  42000       YES      -
mongodb:metrics  mongo-main  42003       YES      localhost:27017
```

## Obtaining Diagnostics Data for Support

SSM Server is able to generate a set of files for enhanced diagnostics, which can be examined and/or shared with Shattered Silicon Support to solve an issue faster.

Collected data are provided by the `logs.zip` service, and cover the following subjects:

* Prometheus targets
* Consul nodes, QAN API instances
* Amazon RDS and Aurora instances
* Version
* Server configuration
* Shattered Silicon Toolkit commands

You can retrieve collected data from your SSM Server in a single zip archive using this URL:

```
https://<address-of-your-ssm-server>/managed/logs.zip
```

## Updating

When changing to a new version of SSM, you update the SSM Server and each SSM Client separately.

### Updating the SSM Server

See [Updating SSM Server Using Docker](server/docker.upgrading.md)

### Updating a SSM Client

When a newer version of SSM Client becomes available, you can update to it from  the Shattered Silicon software repositories:

Debian or Ubuntu

```
$ sudo apt-get update && sudo apt-get install ssm-client
```

Red Hat or CentOS

```
$ yum update ssm-client
```

If you installed your SSM client manually, remove it and then download and install a newer version.

## Uninstalling SSM Components

Each SSM Client and the SSM Server are removed separately. First, remove all monitored services by using the **ssm-admin remove** command (see [Removing monitoring services](../ssm-admin.md#removing-monitoring-services)). Then you can remove each SSM Client and the SSM Server.

### Removing the SSM Client

Remove all monitored instances as described in Removing monitoring services. Then, uninstall the **ssm-admin** package. The exact procedure of removing the SSM Client depends on the method of installation.

Run the following commands as root or by using the **sudo** command

Using YUM

```
$ yum remove ssm-client
```

Using APT

```
$ apt-get remove ssm-client
```

Manually installed RPM package

```
$ rpm -e ssm-client
```

Manually installed DEB package

```
$ dpkg -r ssm-client
```

Using the generic SSM Client tarball.

**cd** into the directory where you extracted the tarball contents. Then, run the `uninstall` script:

```
$ ./uninstall
```

### Removing the SSM Server

If you run your SSM Server using Docker, stop the container as follows:

```
$ docker stop ssm-server && docker rm ssm-server
```

To discard all collected data (if you do not plan to use SSM Server in the future), remove the `ssm-data` container:

```
$ docker rm ssm-data
```
