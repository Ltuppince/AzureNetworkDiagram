# myAzureNetworkDiagram_Project1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Ltuppince/myAzureNetworkDiagram_Project1/tree/master/Diagrams

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk_playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

Elk_playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting excessive traffic to the network.

What aspect of security do load balancers protect?
Load Balancing plays an important role in security by distributing incoming network traffic across multiple backend servers to defend against distributed denial-of-service attacks (DDoS). 

What is the advantage of a jump box?
The jump box serves as the gateway and isolates access to a private network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system and system files.

What does Filebeat watch for?
Filebeat collects data about the file system.  It enables analysts to monitor files for suspicious activity.

What does Metricbeat record?
Machine metrics and services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function               | IP Address | Operation System |
|----------|------------------------|------------|------------------|
| Jump Box | Gateway                | 10.0.0.4   | Linux            |
| Web-1    | Display web content    | 10.0.0.7   | Linux            |
| Web-2    | Display web content    | 10.0.0.8   | Linux            |
| Web-3    | Display web content    | 10.0.0.9   | Linux            |
| Red-Elk  | Monitoring web servers | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 73.152.72.9

 Add whitelisted IP addresses
- 10.0.0.7 
- 10.0.0.8
- 10.0.0.9
- 10.1.0.4  

Machines within the network can only be accessed by SSH (port 22).
- Which machine did you allow to access your ELK VM? What was its IP address?
- Jump Box - 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Address |
|-----------|---------------------|--------------------|
| Jump Box  | Yes                 | 52.147.200.172     |
| Web-1     | No                  | 10.0.0.7           |
| Web-2     | No                  | 10.0.0.8           |
| Web-3     | No                  | 10.0.0.9           |
| Elk-Stack | Yes                 | 52.147.200.172     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_
Ansible is agentless. It does not require agents to be installed on remote systems in order to manage or configure the systems.  

The playbook implements the following tasks:
- Config Elk VM with Docket
- Increase Virtual Memory
- Install Docker
- Install pip3
- Install Docker Python module
- Download and launch a docker elk container
- Enables docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.10
- 10.0.0.11
- 10.0.0.12

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat helps to generate and organize log files to send the output to logstash and Elasticsearch.
- Metricbeat  collects metrics and statistics on the system, such as uptime, CPU usage and services running on the server and sends the output to Logstash and Elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the host file to /etc/ansible/files.
- Update the Ansible hosts file to include:
[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to Kibana with a public IP address to check that the installation worked as expected.


- YAML file is the playbook.  Where do you copy it? /etc/ansible/roles directory contains the ansible playbooks

- _Which file do you update to make Ansible run the playbook on a specific machine?
/etc/ansible/hosts

-_ How do I specify which machine to install the ELK server on versus which to install Filebeat on?
In order to use ansible to configure the ELK server you must add it to the list of machines ansible discover and connect to that is stored in the `hosts` text file.  When you run playbooks with Ansible, you specify which machine or group to run them on. This allows you to run certain playbooks on some machines, but not on others.

- _Which URL do you navigate to in order to check that the ELK server is running?
- kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

Connect to your jump box.
Use the command: 
$ ssh sysadmin@<jump box external IP>

Connect to the Ansible container in the box.
Use the following commands:
$ sudo docker container list -a
$ sudo docker start infallible_wozniak
$ sudo docker attach infallible_wozniak

Use the following command to run your playbook.
	~# ansible-playbook  /etc/ansible/roles/elk_playbook.yml

Use the following command to edit or update your playbook.
~# nano /etc/ansible/roles/elk_playbook.yml

