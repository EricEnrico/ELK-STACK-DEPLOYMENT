## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](Diagrams/NetworkDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Readme file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - filebeat-playbook.yml
  - pentest.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting dangerous traffic to the network.
- The Jumpbox gateway allows for server configuration from only one node on the network and prevents tampering from outside sources. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network  and system logs.
- Filebeat captures log information from DVWA server file systems and sends them to the ELK server for user analysis.
- 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| DVWA-VM  | Webserver| 10.1.0.5   | Linux            |
| DVWA-VM2 | Webserver| 10.1.0.6   | Linux            |
|ELK-SERVER| ELK-Stack| 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load balncer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 162.197.74.224

Machines within the network can only be accessed by SSH.
- : JumpBox Provisioner has access to ELK-SERVER through SSH. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 162.197.74.224       |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
this allows the System Admin the ability to quickly set up multiple machines quickly and easily. 
- 

The playbook implements the following tasks:
- Alerts ansible to make changes to the elkservers in the etc/ansible/hosts file
- Increases memory max to 262144 in order to ensure adequate VM for running elk stack
- Installs docker.io
- Installs python-pip module
- Installs docker python module
- Installs Docker container containing sebp/elk
  - Open ports needed to run elk server

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![DockerPS](Diagram/ElkstackAnsiblecomplete.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- : 10.1.0.5
- : 10.1.0.6

We have installed the following Beats on these machines:
- Filebeats onto DVWA-VM,DVWA-VM2

These Beats allow us to collect the following information from each machine:
- Filebeat collects log data from the DVWA servers file system, catalogs it, and sends it back to the ELK stack for analysis. 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to the docker container that has ansible installed.
    - Make sure to update filebeat.yml config file in order to allow access to Kibana and elastic stack. (Confirm IP addresses for elasticsearch (line 1106) and Kibana (line 1806).
- Update etc/ansible/hosts file to make sure webservers you want to install filebeat on are listed under the correct heading in hosts file.
- Update the ansible hosts file to include IP Addresses for DVWA-VM, DVWA-VM2
- Run the playbook, and navigate to http://40.71.19.187:5601/ to check that the installation worked as expected.





