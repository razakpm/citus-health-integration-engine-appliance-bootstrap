# Welcome to the Citus Health Integration Engine (CHIE)

The CHIE helps connect Citus Health cloud servers with customers' Electronic Health Records (EHR), Revenue Cycle Management (RCM), and other systems behind private firewalls. It acts as a connection engine and gateway between Citus Health applications in the cloud and customers' local systems.

## Server software requirements

Ubuntu [18.04 LTS minimal](https://help.ubuntu.com/community/Installation/MinimalCD) server or similar Linux distribution on a virtual or physical machine is required. Unless you're an expert Linux admin with [Ansible](https://www.ansible.com/) skills, use the [64-bit Ubuntu 18.04 "Bionic Beaver" mini.iso](http://archive.ubuntu.com/ubuntu/dists/bionic/main/installer-amd64/current/images/netboot/mini.iso) netboot image or [64-bit Ubuntu 18.04 Server](https://www.ubuntu.com/download/server) image in case netboot will not work in your environment. The mini.io netboot creates the smallest footprint server so it's the most secure and requires minimal hardening for security.

Setup a Windows Hyper-V, VMware, VirtualBox, or other hypervisor VM:

* RAM: minimum 4096 megabytes, preferably **8192 megabytes**
* Storage: minimum 128 gigabytes, preferably **256 gigabytes**
* Network: **Accessible to the Internet** (both IPv4 and IPv6)
* Firewall Route: The publically accessible IP should point to this server, a Linux firewall is automatically managed by CHIE

## Setup the operating system

First, install Ubuntu 18.04.1 LTS or above *minimal server* on your preferred hypervisor. The smaller the footprint, the safer and more secure the system. You can use most of the defaults, but provide the following defaults when you are asked to make choices:

* Hostname: **chie**.
* Default User Full Name: **CHIE Admin**
* Default User Name: **chieadmin**
* Default User Password: **chieAdminDefault!**
* Disk Partitioning: **Guided - use entire disk**
* PAM Configuration: **Install security updates automatically**

## Prepare your CHIE appliance for our software

After installation is completed, log into the server as user **chieadmin**.

Install the following core utilities:

    sudo apt update
    sudo apt install openssh-server net-tools curl wget git -y

*Ask the Citus Health Customer Success Team for our PKI certificates and disable logins with just passwords.*

## Download the core software and prepare for CHIE containers

    sudo git clone --recurse https://github.com/CitusHealth/citus-health-integration-engine-appliance-public /etc/citus-health-integration-engine

## Setup your account-specific CHIE variables

The Citus Health Customer Success Team will supply you with a **chie.conf.yml** configuration file via secure e-mail or other mechanism.

Please place chie.conf.yml into /etc/citus-health-integration-engine/conf, which should then look something like this:

    > ls -al /etc/citus-health-integration-engine/conf
    drwxr-xr-x 2 root root 4096 Oct 16 10:39 .
    drwxr-xr-x 7 root root 4096 Oct 16 10:53 ..
    -rwxr-xr-x 1 root root  578 Oct 16 10:37 chie.conf.tmpl.yml
    -rwxr-xr-x 1 root root  563 Oct 16 10:54 chie.conf.yml

The **chie.conf.tmpl.yml** file is a template (sample), and the **chie.conf.yml** will be the file given to you by the Citus Health Customer Success Team.

## Setup the core software and prepare for CHIE containers

    cd /etc/citus-health-integration-engine 
    scripts/bootstrap.sh

After bootstrap.sh is complete, exit the shell and restart it.

Once you've logged in again as **chieadmin**, resume the setup:

    cd /etc/citus-health-integration-engine 
    scripts/setup-chie.sh

After setup is completed, reboot the server:

    sudo reboot

After reboot is completed, log into the server as user **chieadmin**.

## Getting started with CHIE

After all installation steps above are completed, log into the server as user **chieadmin**.

(more to come...)
