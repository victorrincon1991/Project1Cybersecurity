## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

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
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

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

![](Image/4.PNG)

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
