# Installing the SSM Client Package on Red Hat and CentOS

If you are running an RPM-based Linux distribution, use the **yum** package
manager to install SSM Client from the official Shattered Silicon software repository.

Shattered Silicon provides `.rpm` packages for 64-bit versions
of Red Hat Enterprise Linux 6 (Santiago) and 7 (Maipo),
including its derivatives that claim full binary compatibility,
such as, CentOS, Oracle Linux, Amazon Linux AMI, and so on.

!!! alert alert-info "Note"
    SSM Client should work on other RPM-based distributions,
but it is tested only on RHEL and CentOS versions 6 and 7.

To install the SSM Client package, complete the following procedure. Run the following commands as root or by using the **sudo** command:


1. Install the `ssm-release` package to setup the official Shattered Silicon software repository:

```
$ rpm -i https://dl.shatteredsilicon.net/ssm/8/ssm-release-1.0-1.el8.noarch.rpm
```

2. Install the `ssm-client` package:

```
$ yum install ssm-client
```

!!! alert alert-info "Note"
    You can also go to the [SSM download page](https://dl.shatteredsilicon.net/ssm/8/), download the appropriate version of SSM client for your GNU/Linux distribution.
