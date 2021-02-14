## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/apettit512/automating-elk-configuration/blob/main/Images/network_diagram.png "Network Diagram")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.


The configuration details of each machine may be found below.

| Name                 | Function  | IP Address | Operating System |
|----------------------|-----------|------------|------------------|
| Jump-Box-Provisioner | Gateway   | 10.0.0.5   | Linux            |
| Web-1                | Webserver | 10.0.0.6   | Linux            |
| Web-2                | Webserver | 10.0.0.7   | Linux            |
| ELK-machine          | ELK stack | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the local host's IP address.

Machines within the network can only be accessed via SSH from Jump-Box-Provisioner (10.0.0.5).

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box Provisioner | Yes                 | Local host IP        |
| Web-1                | No                  | 10.0.0.5             |
| Web-2                | No                  | 10.0.0.5             |
| ELK-machine          | No                  | 10.0.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time and resources by allowing ELK stack instances to be spun up and torn down as needed. Additionally, if an update needs to be performed, it can be configured in the playbook and automatically update any instance included in the hosts list.

The playbook implements the following tasks:
- Install Docker
- Increase virtual memory sufficient for ELK machine and make sure it is increased upon reboot of VM
- Download and install ELK container
- Enable service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/apettit512/automating-elk-configuration/blob/main/Images/ELK_configuration_success.png "ELK success")

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.6)
- Web-2 (10.0.0.7)

I have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about system logs and any changes to the file system on the target machine. 
- Metricbeat collects data about system metrics on the target machine, such as uptime, CPU, and connections.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to `/etc/ansible/roles/`.
- Update the hosts file to include the group of machines that you want to install ELK on (elk is used in the playbook).
- Run the playbook, and navigate to `[localhostIP]:5601` to check that the installation worked as expected.
