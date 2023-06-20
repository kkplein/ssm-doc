# VirtualBox Using the GUI

The following procedure describes how to run the SSM Server appliance using the graphical user interface of VirtualBox:

1. Download the OVA. The latest version is available at the [Downloads](https://dl.shatteredsilicon.net/ssm/) site.

2. Import the appliance. For this, open the File menu and click Import Appliance and specify the path to the OVA and click Continue. Then, select Reinitialize the MAC address of all network cards and click Import.

3. Configure network settings to make the appliance accessible from other hosts in your network.

    !!! alert alert-info "Note"
        All database hosts must be in the same network as *SSM Server*, so do not set the network adapter to NAT.

    If you are running the appliance on a host with properly configured network settings, select Bridged Adapter in the Network section of the appliance settings.

4. Start the SSM Server appliance and set the root password (required on the first login).

    If it was assigned an IP address on the network by DHCP, the URL for accessing SSM will be printed in the console window.
