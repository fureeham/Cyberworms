# Cyberworms
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/75343261/119215004-ce11cb00-ba98-11eb-88cd-eea37c21cbcd.png)

(GitHub-Cyberworms/Cyberworms-main/Diagrams/Cloud Security HW Network Diagram.draw.io)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

 	 -Filebeat-playbook.yml
 	 -Metricbeat-playbook.yml
	 -WebVM-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
-Load balancers protect systems from DDoS attacks by shifting attack traffic. They ensure that the application remains available while providing 
an additional layer of protection. The advantage of a jumpbox is that the availability of access given to the user from a single node that can be secured and monitored, simplifying 
routing logic.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
    	-Filebeat monitors the log files and collects data about any changes in the file system. 
 	-Metricbeat collects the metrics and sends them to the specifies output. 

The configuration details of each machine may be found below.

| Name     | Function   | IP Address             | Operating System |
|----------|------------|------------------------|------------------|
| Jump Box | Gateway    | 10.0.0.4/168.62.221.64 | Linux            |
| Web VM 1 | VM         | 10.0.0.7               | Linux            |
| Web VM 2 | VM         | 10.0.0.8               | Linux            |
| Web VM 3 | VM         | 10.0.0.10              | Linux            |
| Elk VM   | Monitoring | 10.1.0.4/40.121.44.128 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 -172.58.236.61 (Local Workstation's Public IP)

Machines within the network can only be accessed by the Jump Box machine.
 -The ELK VM can only be accessed via ssh from the local machine's public IP address (172.58.236.61) and the Jump Box (168.62.221.64).

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible     | Allowed IP Address                 |
|----------|-------------------------|------------------------------------|
| Jump Box | No                      | Workstations Public IP             |
| Web VM 1 | Yes (via Load Balancer) | 138.91.165.238                     |
| Web VM 2 | Yes (via Load Balancer) | 138.91.165.238                     |
| Web VM 3 | Yes (via Load Balancer) | 138.91.165.238                                 |
| Elk VM   | No                      | Workstations Public IP/Jump Box IP |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
 	-Ansible is a popular IT automation tool that can manage and automate tasks into multiple servers from a single deployment (via playbook).
The deployment is simple plain English  that is used in Ansible called YAML which stands for “YAML Ain’t Markup Language.” 


The playbook implements the following tasks:
-Install docker.io
-Install python-pip
-Install docker python module
-Download and launch a docker elk stack

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
     -Web VM with Docker (10.0.0.7)
     -Web VM with Docker (10.0.0.8)
     -Web VM with Docker (10.0.0.10 )

We have installed the following Beats on these machines:
     -Metricbeat
     -Filebeat

These Beats allow us to collect the following information from each machine:
     -Filebeat generates and collects log files to forward them to Logstatsh and Elasticsearch. It logs any modifications that have been made to the file system.  
     -Metricbeat collects and provides information such as metrics from services and operating systems running on a server. This data is then sent to Elasticsearch/Logstash (user specified).

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the roles file to /etc/ansible/roles
- Update the hosts file to include the webserver IP's and ELKServer IP
- Run the playbook, and navigate to http://[ELKServer_Public_IP]:5601/app/kibana to check that the installation worked as expected.
