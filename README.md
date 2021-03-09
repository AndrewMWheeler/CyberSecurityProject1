## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

CyberSecurityProject1/Images/NetworkDiagram

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the attached file may be used to install only certain pieces of it, such as Filebeat.

  - YAML/dvwa.yaml - for hosting DWVA Web Servers 
  - YAML/elk.yaml - for hosting an ELK Server to monitor DWVAs 
  	- YAML/filebeat.yaml - for installing filebeat on Web Servers 
  	- YAML/metricbeat.yaml - for installing metricbear on Web Servers 


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available in addition to restricting access to the network.
- The load balancer will insure availablitiy of the web application and allow for traffic to be sent between either of the redundant servers. 
- The jump box restricts access to the web servers and insures only authorized users can access the servers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

-Filebeat watches for log files/locations and collect log events. (Filebeat: Lightweight Log Analysis & Elasticsearch)
-Metricbeat records metrics and statistical data from the operating system and from services running on the server (Metricbeat: Lightweight Shipper for Metrics)

The configuration details of each machine may be found below.

| Name        | Function | IP Address | Operating System |
|-------------|----------|------------|------------------|
| Jump Box    | Gateway  | 10.0.0.4   | Linux            |
| Web 1       | DVWA     | 10.0.0.5   | Linux            |
| Web 2       | DVWA     | 10.0.0.6   | Linux            |
| ELK-Server  | ELK      | 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address for home workstation 

Machines within the network can only be accessed by SSH.
- The ELK server was only accessed through SSH from a personal at home workstation 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible    | Allowed IP Addresses           |
|----------|------------------------|--------------------------------|
| Jump Box | No                     | Personal IP                    |
| Web 1    | Yes with Load Balancer | Personal IP HTTP, Jump Box SSH |
| Web 2    | Yes with Load Balancer | Personal IP HTTP, Jump Box SSH |
| ELK      | No                     | Personal IP                    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The biggest advantage of using Ansible is the adility to deploy multiple machines at once without having to work on each instance indvidually 

The playbook implements the following tasks:

-Install Docker.io and pip3
-Increases VM memory
-Download and Configure elk docker container
-Sets Published Ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1 10.0.0.4
- Web 2 10.0.0.5

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat 

These Beats allow us to collect the following information from each machine:
- Filebeat watches for log files/locations and collect log events. (Filebeat: Lightweight Log Analysis & Elasticsearch)
- Metricbeat records metrics and statistical data from the operating system and from services running on the server (Metricbeat: Lightweight Shipper for Metrics)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.

### FAQs
- Which file is the playbook? YAML/dvwa.yaml, YAML/elk.yam, YAML/filebats.yaml, YAML/metricbeat.yaml
- Where do you copy it? /etc/ansible 
- Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts 
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? using the /etc/ansible/hosts file and the specific group in the yaml file 
- Which URL do you navigate to in order to check that the ELK server is running? http://(ELK-ServerIP):5601
