# Installing SSM Client on Debian or Ubuntu

Shattered Silicon provides `.deb` packages for 64-bit versions of the following
distributions:


* Debian 8 (jessie) and later


* Ubuntu 14.04 LTS (Trusty Tahr) and later


!!! alert alert-info "Note"
    SSM Client should work on other DEB-based distributions, but it is tested only on the platforms listed above.

To install the SSM Client package, complete the following procedure. Run the following commands as root or by using the **sudo** command:

1. Go to the [SSM download page](https://dl.shatteredsilicon.net/ssm/9/), download the appropriate version of SSM client for your GNU/Linux distribution

```
$ curl -O https://dl.shatteredsilicon.net/ssm/9/DEBS/ssm-client_9.4.1-0_amd64.deb
```

2. Install the SSM Client package:

```
$ dpkg -i ssm-client_9.4.1-0_amd64.deb
```
