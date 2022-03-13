# Automated AZURE/ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project 1-S](https://user-images.githubusercontent.com/101228655/158072729-59b3aac7-b1ae-49a9-9272-d9dd2711f131.png)

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

| Name     | Publicly Accessible | Allowed IP Addresses        |
|----------|---------------------|-----------------------------|
| Jump Box | Yes                 | Public IP                   |
| WEB-1&2  | No                  | 10.0.0.4 – DVWA (Port 80)   |
| ELK      | No                  | 10.0.0.4 – Kibana(Port 5601)|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time when install packages or configuring a large number of servers.
- It is agentless: You do not need to install additional software on your server nodes. Makes installation clean while ensuring there are no conflicts with software.
- Playbooks are easy to read and edit: Written in YAML format, makes adding and editing configurations a simple task.
- Written in Python: One of the most popular programming languages and is familiar to engineers.

The playbook implements the following tasks:

- Install docker.io, python3-pip, python module:

![Docker](https://user-images.githubusercontent.com/101228655/158076518-a1025eca-1aeb-4c0d-8790-1fb092881e6c.JPG)

- Memory Requirements:

![Memory](https://user-images.githubusercontent.com/101228655/158076531-0273bc72-c5af-499c-a78e-330800aa7d77.JPG)

- Container image and published ports accessible through the network bridge:

![ports](https://user-images.githubusercontent.com/101228655/158076546-80c98f36-5d7c-4c0a-9c2b-5c5eb3273343.JPG)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk Server](https://user-images.githubusercontent.com/101228655/158076563-ca91a02f-0911-431b-9c68-23583ddaaf5f.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web Machines
  - Web-1 10.0.0.5
  - Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations specified, collects log events, and forwards them to Elasticsearch or Logstash.

![Filebeat](https://user-images.githubusercontent.com/101228655/158077435-f0798df0-4973-47b3-a5e8-4f05f77d30df.JPG)

- Metricbeat monitors servers by collecting metrics from the system and services running on the server.

![Metric](https://user-images.githubusercontent.com/101228655/158077450-2a58f6f4-b698-4531-9190-f4f37fdcdf79.JPG)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat/metricbeat config file to /etc/ansible/files.
- Update the config file to include public ip of elk server to include port for ELK APP webpage and ELK Listening Port to monitor Web Servers.
- Run the playbook with Web Machines running and navigate to Kibana – ([ELK Public IP:5601]/app/kibana) and go to System Logs Dashboard and  Docker Metrics to check that the installation worked as expected.

### Process for running filebeat:

##### Download instructions can be found on Kibana App Homepage, Add Log Data, System Logs, DEB Tab

- Configured hosts that will run filebeat. Hosts config file checks for listed hosts in host’s file and retrieves information against those hosts, then uses this information to make connection, login, and execute tasks on remote hosts.

![hosts config](https://user-images.githubusercontent.com/101228655/158081255-8cc0c621-a1ba-4aba-bf02-37c1351bc7d6.JPG)

- List hosts on which server filebeat and metricbeat will run

![Hosts](https://user-images.githubusercontent.com/101228655/158081518-3b9f8054-204d-4998-ab72-ce84fefcd509.JPG)

- Download using curl and install package (DEBIAN used in this instance)
  - curl -L downloads from the location and allows for redirects
  - curl -O saves data into a local file without having to use a path
  - dkpg is a package manager that can install, or build packages

![DownInstall](https://user-images.githubusercontent.com/101228655/158082318-cdd420f7-6454-469e-87f1-ad0764159bfd.JPG)

- Filebeat Configuration from Ansible Container to Webserver that opens ports 5601 and 9200 as well as other functions to gather data. 

[Filebeat Config File](https://github.com/GBeh1/AzureElkYamlGuide/blob/main/Ansible/Filebeat-Config.yml)

![copy](https://user-images.githubusercontent.com/101228655/158082715-b28fd84d-7310-45c0-b3c7-ecfa3213223d.JPG)

- Filebeat modules provide a way to process common log formats  They contain default configurations, Elasticsearch ingest pipeline definitions, and Kibana dashboards to implement and deploy a log monitoring solution.  You can modify configurations in modules.d/system.yml file.

- Filebeat setup command loads the Kibana dashboard.

- Service Filebeat start will start filebeat to begin monitoring.

- Enable service docker starts filebeat service when server starts.

![therest](https://user-images.githubusercontent.com/101228655/158083267-8e580e7f-1872-41e9-a5f0-7764db0f0104.JPG)

### Kibana File Beat Check

![finished](https://user-images.githubusercontent.com/101228655/158083911-8c94cd48-5691-4b91-8f97-2e803d721bf3.JPG)

![finished2](https://user-images.githubusercontent.com/101228655/158083931-4f759aea-f663-4215-a5cd-ccb47b3ba5cc.JPG)

