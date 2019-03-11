THIS IS A TECHNICAL DEMO BUILD OF ORBITALVM, EXPECT DRAGONS, BUGS AND EXPLOSIONS.

Introduction:
    OrbitalVM is the result of one hobbyist programmer who wanted more from their hypervisor. The goal of OrbitalVM is to give the user the freedom of choice when setting up and configuring their virtual machine host. OrbitalVM host machines are capable of having local or remote storage mounting options, GNU/Linux filesystem support (experimental) and ZFS support along with some of the standard conventions of modern hypervisors including live migrations.

Tooling:
    In order to give the administrator the right tools for the job, several packages have been pre-installed to provide functionality. 

    Based on: FreeBSD 12 amd64
    Included Packages:
        Xen 4.11
        Libvirt 5.0
        GlusterFS 3.11
        OpenVSwitch 2.10
        NUT 2.7

        ---And More---

    The combination of Xen and Libvirt allows for premade software to control an OrbitalVM hypervisor, however it should be known that most premade software(s) will not support OpenVSwitch.

Installation:
    Installation of OrbitalVM is fairly straight forward on a GNU/Linux or Unix-like operating system. Microsoft Windows users will need a Windows Disk Imaging tool to extract the disk image to a flash drive.
    
    REQUIRED: 16GB Flash Drive
    Note: The actual image size is 8GB, however because of differences between hardware and software using base10 and base2 numbers, most 8GB flash drives will not fit the OrbitalVM system image. Different image sizes may be made available later for increased software availability.
    
    After verifying the device name of your flash drive and downloading the image, run the following command to initialize the boot media.
    
        ` gunzip -dc orbitalvm.amd64.full.img.gz | sudo dd of=/dev/sdX bs=64k `
        
        Note: Replace '/dev/sdX' with the name of your flash drive.
        
    Note: The default password is ` password `
    
    After flashing your boot media and booting into your new system, the OpenVSwitch daemon will need to be initialized with a bridge device. The following command will add a bridge interface for clients to use.
    
        ` ovs-vsctl add-br bridge0 -- set bridge bridge0 datapath_type=netdev `
        (Thank you emaste@ at the FreeBSD Forums)
        
        Note: You will need to add a physical device for network access.
        ` ovs-vsctl add-port bridge0 eth0 `
        
    CURRENTLY: There is a helper init script called ovs-boot-setup in the ` /etc/local/rc.d ` directory. At the time of the technical preview of OrbitalVM this script doesn't execute at startup, this is NOT working as intended. 
    
    After logging in and changing the password or other config, you can save your configuration with the command.
        
        ` sh /root/save_cfg `
        
    Please note that if the administrator doesn't run the save config command and then reboots, all changes will be lost as OrbitalVM runs in memory. Any files saved to persistant media will be safe.
