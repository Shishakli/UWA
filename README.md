## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Homework Week 13.drawio.png](https://github.com/Shishakli/UWA/blob/main/Diagrams/Homework%20Week%2013.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

- [DVWA Webserver playbook](https://github.com/Shishakli/UWA/blob/main/Ansible/DVWA.yml)
- [ELK Stack playbook](https://github.com/Shishakli/UWA/blob/main/Ansible/ELK-install.yml)
- [Filebeat Playbook](https://github.com/Shishakli/UWA/blob/main/Ansible/filebeat-playbook.yml)
- [Filebeat Configuration](https://github.com/Shishakli/UWA/blob/main/Ansible/filebeat-config.yml)
- [Metricbeat Playbook](https://github.com/Shishakli/UWA/blob/main/Ansible/metricbeat-playbook.yml)
- [Metricbeat Configuration](https://github.com/Shishakli/UWA/blob/main/Ansible/metricbeat-config.yml)

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
- Load balancers can protect a service against DDoS attacks
- A jump box can provide secure access to otherwise protected systems by ustilising a private/public key authentication

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat watches logfiles which aggregates the events and sends the aggregated data to kibana
- Metrixbeat watches system resource usage and sends the data to kibana

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.10.0.4  | Ubuntu 20.04     |
| Web-1     | Webserver         | 10.10.0.7    | Ubuntu 20.04     |
| Web-2    | Webserver         | 10.10.0.8  | Ubuntu 20.04     |
| ELKvm     |ELK Log Server     |10.20.0.4  | Ubuntu 20.04     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 103.100.28.211

Machines within the network can only be accessed by Jump Box.
- Jump Box, 10.10.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes              | 103.100.28.211    |
|Web Load Balancer | Yes                    | 103.100.28.211                     |
|ELK-vm|            Yes         |                   103.100.28.211   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible allows automated and consistently repeatable configuration of new services

The playbook implements the following tasks:
- Install Docker
- Install Python3_pip
- Docker Module with PIP
- Increase Memory
- Download and Launch ELK Container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/Shishakli/UWA/blob/main/Diagrams/dockerps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1, 10.10.0.7
- Web-2, 10.10.0.8

We have installed the following Beats on these machines:
- Filebeats and Metricbeats
- Web-1 and Web-2

These Beats allow us to collect the following information from each machine:
 - Filebeat:    web log events
 - Metricbeat:  System resource usage

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml
- Update the /etc/ansible/hosts file to include...

```
[webservers]
10.10.0.7 ansible_python_interpreter=/usr/bin/python3
10.10.0.8 ansible_python_interpreter=/usr/bin/python3

[elk]
10.20.0.4 ansible_python_interpreter=/usr/bin/python3
```

- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
