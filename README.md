## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![docker ps image](https://github.com/drpeters83/ELK-Project/blob/main/Diagrams/Lab-diagram.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/drpeters83/ELK-Project/blob/main/Ansible/ELK-playbook.rtf
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure against malicious attacks, in addition to restricting access to a single point of entry to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network traffic and system logs.
- Filebeat will monir the log files and sent them to Elasticsearch and Logstash.
- Metricbeat records the metrics and statistics to an output you can specify. In this case we used Kibana to view all the data.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | Server   | 10.0.0.5   | Linux            |
| Web 2    | Server   | 10.0.0.6   | Linux            |
|ELK Server|ELK Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 24.8.88.199

Machines within the network can only be accessed by SSH port 22 via the Jumpbox.
- Jumpbox was able to access the ELK machine using 52.149.181.144.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box | Yes                 | 10.0.0.5 10.0.0.6 10.1.0.4 |





### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because ansible allowed for the automating of tasks on multiple servers and databases by writing scripts to carry out said tasks consistently and efficiently by running a single command.


The playbook implements the following tasks: By running the ansible-playbook ELK_playbook.yml
- Gathering facts
- Install docker.io
- Install pip3
- Install Docker python module
- Use more memory
- download and launch a docker elk container
- enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps image](https://github.com/drpeters83/ELK-Project/blob/main/Sudo%20docker%20ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Jumpbox 10.0.0.4
- Web 1 10.0.0.5
- Web 2 10.0.0.6


We have installed the following Beats on these machines:
- https://github.com/drpeters83/ELK-Project/blob/main/Ansible/Filebeat.rtf

These Beats allow us to collect the following information from each machine:
- Filebeat will log data collected from traffic on web 1 and web 2 and the output will be to the ELK server and viewed on Kibana. The data will show packets sent and received from users. For example, all data collected from Web 1 & 2 is logged on the ELK server and viewed using Kibana to examine why Web 1 is down or why traffic is hanging at Web 2.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to etc/filebeat/filebeat.yml.
- Update the filebeat.yml file to include 'Enable and Configure System Module' and 'filebeat setup' and 'start filebeat' commands. Run ansible-playbook filebeat-playbook.yml. You should see the following on the command line:

![docker ps image]<img width="891" alt="Running filebeat" src="https://user-images.githubusercontent.com/26662275/122965534-873c1d00-d345-11eb-98c6-1f544faff05b.png">



- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected. Click on module status and then check data. You should see the following on the screen:

![docker ps image]<img width="888" alt="Filebeat check data" src="https://user-images.githubusercontent.com/26662275/122965563-915e1b80-d345-11eb-9e9f-41d2339a493b.png">



