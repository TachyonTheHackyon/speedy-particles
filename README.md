## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 (Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the elkdeployment.yml file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unwanted users to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logfiles and system metrics.

The configuration details of each machine may be found below.

| Name          | Function           | IP Address   | Operating System |
|---------------|--------------------|--------------|------------------|
| Jump Box      | Gateway            | 10.0.0.4     | Linux            |
| Web-1         | Server             | 10.0.0.5     | Linux            |
| Web-2         | Server             | 10.0.0.6     | Linux            |
| Web-3         | Server             | 10.0.0.8     | Linux            |
| Load Balancer | Traffic Management | 20.191.94.90 |                  |
| Elk Sever     | Traffic Monitor    | 10.1.0.4     | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the load balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Localhost IP

Machines within the network can only be accessed by the Jump Box via SSH on port 22.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses | Method of Connection |
|---------------|---------------------|----------------------|----------------------|
| Jump Box      | No                  | Localhost IP         | SSH                  |
| Web-1         | No                  | 10.0.0.4             | SSH                  |
| Web-2         | No                  | 10.0.0.4             | SSH                  |
| Web-3         | No                  | 10.0.0.4             | SSH                  |
| Load Balancer | No                  | Localhost IP         | HTTP                 |
| Elk Sever     | No                  | 10.0.0.4 / Local IP  | SSH / HTTP port 5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Configurations can be completed for multiple machines instantaneously, and easily updated.

The elk installation playbook implements the following tasks:
- Download and isntall docker image, python-pip3_
- Increase virtual memory via vm.max_map_count
- Download/launch elk container and open ports 5601, 9200, 5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

 (/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.8

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Filebeat collects data on system logs within the target system and relays any changes to the ELK stack
- Metricbeat: Metricbeat collects system metric data for any given target system(s) and relays them to the ELK stack

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the YML file to /etc/ansible/roles (if you do not have this folder please make it).
- Update the hosts file to include a section for [webservers] with each of their individual ip followed by ansible_python_interpreter=/usr/bin/python3 as well as an [elk] section with the elk server IP and ansible_python_interpreter=/usr/bin/python3
- Make sure to adjust the filebeat-config.yml to such that line 1106 reads 'hosts: ["<elkseverIP>:9200"]' and line 1805 reads 'host: "<elkserverIP>:5601". Do the same for metricbeat-config.yml
- Run the playbook, and navigate to http://<elkseverip>:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
