## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/ACJones73/USyd-Elk/blob/main/Diagrams/Activity%20Week%2013.drawio

These files have been tested and used to generate a live ELK deployment on Azure. Install-Elk.yml can be used to either recreate the entire deployment pictured above. Alternatively, the filebeat-playbook.yml file may be used to install Filebeat and metricbeat-playbook will install Metricbeat.

  - Install-Elk.yml
  - metricbeat-playbook.yml
  - filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as Apache.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.7   | Linux            |
| Web-1    | Web Server | 10.0.0.8   | Linux            |
| Web-2    | Web Server | 10.0.0.9   | Linux            |
| Web-3    | Web Server | 10.0.0.10  | Linux            |
| Elk-1    | Web Server | 10.1.0.4   | Linux  

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk-1 machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 118.211.22.6

Machines within the network can only be accessed by Jump-Box.
- The Jump-Box machine with IP 10.0.0.07

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |          No         |  118.211.22.6        |
| Web-1    |          No         |  10.0.0.7            |
| Web-2    |          No         |  10.0.0.7            |
| Web-3    |          No         |  10.0.0.7            | 
| Elk-1    |          Yes        |  10.0.0.7            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- it allows for multiple machines to be configured at the same time.

The playbook implements the following tasks:
- Downloads the docker module 
- Installs the Docker module
- Increases virtual memory to vm.max_map_count=262144
- Sets the Docker to use the extra memory
- Downloads and launches a Docker Elk container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

azadmin@ELK-1:~$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                  PORTS                                                                              NAMES
05d9afae0287        sebp/elk:761        "/usr/local/bin/star…"   11 days ago         Up Less than a second   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.8
10.0.0.9
10.0.0.10

We have installed the following Beats on these machines:
Filebeat
MetricBeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors for and collects system log events from the OS. Metricbeat monitors metrics from the individual services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Install-Elk.yml file to /etc/ansible on your jump box
- Update the Ansible Hosts file, First uncomment the [webservers] header line then add the python line: ansible_python_interpreter=/usr/bin/python3 besides each IP needed.
- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana. to check that the installation worked as expected.
