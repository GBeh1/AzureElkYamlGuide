This folder is reserved for Ansible Setup and Playbooks for Virtual Machine Configurations for Azure.

Files configured:

- ansible.cfg

- hosts.cfg

- configurewebvm.yml <> Configures Web Virtual Machines by using docker.  
		        Installs Docker.io
                        Installs Python3-pip
                        Installs Docker Python Module
			Downloads and Launches Docker Web Container
			Enables Docker Service

- ElkDocker.yml      <>	Configures Elk Virtual Machine by using docker.	
			Installs Docker.io
			Installs Python3-pip
			Installs Docker Python Module
			Download and Launches Docker Elk Container
			Enables Service Docker on Boot

- Filebeat.yml       <> Download and Installs Filebeat for ELK

- Metricbeat.yml     <> Download and Installs Metricbeat for Elk
