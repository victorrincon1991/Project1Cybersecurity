## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](/Image/diagram_filename.png/)

These files have been tested and used to generate a live ELK deployment on Azure.


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network. The load balancer ensures that work to process inccoming traffic will be shared by both vulnerable web servers. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider Access controls will ensure that only authorized users will be able to connect in the first place.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network, as well as watch system metrics, such as: CPU usage; attempted SSH logins; sudo escalation failures.

The configuration details of each machine may be found below.

| Name      | Function     | IP Address | Operating System |
|-----------|--------------|------------|------------------|
| Jump Box  | Gateway      | 10.0.0.1   | Linux            |
| WEB-1     |Web Server    | 10.0.0.5   | Linux            |
| WEB-2     |Web Server    | 10.0.0.6   | Linux            |
| DVWA-VM2  |Backup Server | 10.0.0.7   | Linux            |
|ELK        |Monitoring    | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box machine machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:40.88.125.174

Machines within the network can only be accessed by each other. WEB-1, WEB-2, DVWA-VM2 VMs send traffic to the ELK server.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 40.88.125.174        |
| Web-1    | No                  | 10.0.0.0/16          |
| Web-2    | No                  | 10.0.0.0/16          |
| DVWA-VM2 | No                  | 10.0.0.0/16          |
| ELK      | No                  | 10.1.0.0/16          |

### Elk Configuration

The ELK VM uses Docker to download and manage an ELK container that exposes an Elastic Stack instance. Rather than configure ELK manually, we opted to develop a reusable Ansible Playbook to accomplish the task. The playbook implements the following tasks:

Installs docker.io: the Docker engine, used for running containers
Installs python3-pip: Package used to install Python software
Installs docker module: Python client for Docker
Increases the virtual memory of the target VM in order to run the ELK container
Downloads and launches the Docker container called sebp/elk:761
Configures the container to start with the following port mappings
5601:5601
9200:9200
5044:5044

https://github.com/victorrincon1991/Project1Cybersecurity/blob/main/Image/4.PNG

https://github.com/victorrincon1991/Project1Cybersecurity/blob/main/Image/5.PNG


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1    10.0.0.5
Web-2    10.0.0.6
DVWA-VM2 10.0.0.7


We have installed the following Beats on these machines:

Filebeat
Metricbeat
Packetbeat

These Beats allow us to collect the following information from each machine:

Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs.
Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.
Packetbeat collects packets that pass through the NIC, similar to Wireshark. We use it to generate a trace of all activity that takes place on the network, in case later forensic analysis should be warranted.
The playbooks below install Filebeat and Metricbeat on the target hosts.

https://github.com/victorrincon1991/Project1Cybersecurity/blob/main/Scripts/Filebeat/Installation-Filebeat.yml

https://github.com/victorrincon1991/Project1Cybersecurity/blob/main/Scripts/Meticbeat/Installation-Metricbeat.yml


### Using the Playbook
In order to use the playbooks, you will need to have an Ansible control node already configured. We use the Jump Box for this purpose.

First we must SSH into the Jump Box and locate, start, and attach to our Ansible container.

$ ssh RedAdmin@40.88.125.174

$ sudo docker ps

$ sudo docker list -a

$ sudo docker start nice_moore

$ sudo docker attach nice_moore

The easiest way to copy the playbooks is to use Git:

$ cd /etc/ansible

$ mkdir files

https://github.com/victorrincon1991/Project1Cybersecurity/blob/main/Image/6.PNG

### Playbooks and Hosts file into /etc/ansible

$ cp Automated-ELK-Stack-Deployment/resources/* .

$ cp Automated-ELK-Stack-Deployment/resources/* ./files

This copies the playbook files to the correct place.

Next, you must create a hosts file to specify which VMs to run each playbook on. Run the commands below:

$ cd /etc/ansible

$ cat > hosts <<EOF

[webservers]

10.0.0.5

10.0.0.6

10.0.0.7

[elk]

10.1.0.4

EOF

After this, run the commands below to run the playbooks:

$ cd /etc/ansible/files

$ ansible-playbook install_elk.yml elk

$ ansible-playbook install_filebeat.yml webservers

$ ansible-playbook install_metricbeat.yml webservers

https://github.com/victorrincon1991/Project1Cybersecurity/blob/main/Image/3.PNG




