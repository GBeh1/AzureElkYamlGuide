### This folder is used for various linux commands that have helped in the creation of this project.

#### ssh-keygen 
- Secure Socket Shell Tool for creating new authentication key pairs for SSH.  Key pairs are used for automatic logins, single sign-on, and authenticating hosts. rsa - default key file - is based on the difficulty of factoring large numbers.

#### ssh username#ipaddress
- Opens terminal on remote machine from client machine through TCP port 22 or other specified port.
  
#### curl
- "Client URL" used to transfer data to and from a server.  Talks to server by specifying the location and the data you want to send.

#### dpkg
- Tool to install, build, remove and manage Debian packages.

#### apt
- Utility for installing, updating, removing, and managing deb packages on Ubuntu.

#### pip
- package installer for python, can use it to install packages from python.

#### docker
- Automates the deployment of applications inside Linux Containers, and provides the capability to package an application with its runtime dependencies into a container.
  - docke pull [image_maker]/[image_name] - pulls a docker image by its digest.
  - docker run - creates and runs new container
  - docker container ls - list containers pulled
  - docker start (container name) - starts container
  - docker attach (container name) - attaches local standard input, output, and error streams to a running container.
  - docker ps - shows running containers

#### systemctl
- Used to control and manage systemd and services. Contains libraries, daemons, and utilities you can use to manage services in the Linux system.

#### ansible
- Used to run any commands or run any scripts in the remote target machine, or execute commands on a remote note.  The command module is used to run simple Linux commands on a remote node or server, which is part of the host group or standalone server mentioned in the host group.
  - ansible-playbook - executes defined tasks on the targeted host from a human readible mapping block called YAML
  - ansible (host) ping -m - ansible ping module to test connection between ansible and hosts
