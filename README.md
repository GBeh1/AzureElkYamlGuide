# Automated AZURE/ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project 1-S](https://user-images.githubusercontent.com/101228655/158072729-59b3aac7-b1ae-49a9-9272-d9dd2711f131.png))

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, the configurations may be updated to reflect changes that support future ELK deployments.

[Ansible Playbooks and Configurations](https://github.com/GBeh1/AzureElkYamlGuide/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load Balancers help servers move data efficiently, optimizes the use of application delivery resources and prevents server overloads.  The conduct continuous health checks on servers to ensure they can handle requests. 

- As a security aspect, the ability to off-load defends against denial-   of-service (DDoS) attacks by shifting traffic from one server to another.
- The Jumpbox Server performs as a bridge for Virtual Machines (VM) connected to load-balancers, by connecting the public (IP) of the jumpbox to servers outside of the cloud.  

Integrating an ELK server allows users to monitor for CPU usage, memory usage, network traffic over routers and switches, and application performances.
- Filebeat monitors the log files or locations specified, collects log events, and forwards them to Elasticsearch or Logstash.  
- Metricbeat monitors servers by collecting metrics from the system and services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux-Ubuntu     |
| Web-1    |   DVWA   | 10.0.0.5   | Linux-Ubuntu     |
| Web-2    |   DVWA   | 10.0.0.6   | Linux-Ubuntu     |
| ELK      | ELK STACK| 10.1.0.4   | Linux-Ubuntu     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- #### When configuring your Azure to connect to jumpbox, your machines public ip will be used to connect via port 22.
- #### Web Machines within the network can only be accessed by the Jumpbox’s container SSH Key via port 22.
- #### ELK Machine can only be accessed via Jumpbox’s container’s SSH Key via port 22.

A summary of the access policies in place can be found in the table below.

Network Security Groups were set in place to allow public access to Jumpbox through username and ssh-key.  Jumpbox Container was given  access to Web1-2 and ELK machine and excludes all public access.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box | Yes                 | Public IP                  |
| WEB-1&2  | No                  | JumpBox Container 10.0.0.4 |
| ELK      | No                  | Jumpbox Container 10.0.0.4 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time when install packages or configuring a large number of servers.
- It is agentless: You do not need to install additional software on your server nodes. Makes installation clean while ensuring there are no conflicts with software.
- Playbooks are easy to read and edit: Written in YAML format, makes adding and editing configurations a simple task.
- Written in Python: One of the most popular programming languages and is familiar to engineers.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

