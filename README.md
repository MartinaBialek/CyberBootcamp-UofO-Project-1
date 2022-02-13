## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![NetworkDiagram](https://user-images.githubusercontent.com/99365720/153497900-453d44be-7c24-480e-83ef-07ad874bae6a.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **YAML** file may be used to install only certain pieces of it, such as Filebeat.

[ELK-Install.yml] (https://github.com/MartinaBialek/CyberBootcamp-UofO-Project-1/blob/ab7475d51289cb04ee9b21ba2ed2c981a5d687f6/Ansible/install-elk.yml)
 
 This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
- Target Machines and Beats
- Using a Playbook

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly **available**, in addition to restricting **in-bound access** to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box?_

- The off-loading function of a **load balancer** defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **jump box** and system **network**.

- **Filebeat** monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

- **Metricbeat** takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. 

The configuration details of each machine may be found below:

| Name     | Function | IP Address | Operating System|
|----------|----------|------------|-----------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux           |
| Web-1    |Web Server| 10.0.0.6   |  Linux          |
| Web-2    |Web Server| 10.0.0.7   |  Linux          |
| Web-3    |Web Server| 10.0.0.8   |  Linux          |
| ELK-VM   |Web Server| 10.1.0.7   |  Linux          |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 

Only the **jump box provisioner** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- **5061 Kibana Port**

Machines within the network can only be accessed by the **jump box provisioner**.

- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?
- My IP Address: 50.45.135.213

A summary of the access policies in place can be found in the table below:

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |    Yes              | 50.45.135.213        |
|  Web-1   |    No               | 10.0.0.6             |
|  Web-2   |    No               | 10.0.0.7             |
|  Web-3   |    No               | 10.0.0.8             |
| ELK-VM   |    No               | 10.1.0.7             |  

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- _TODO: What is the main advantage of automating configuration with Ansible?
- 
- Flexible/Customizable: You can create a customizable environment regardless of where it is deployed.  
- Free: Operates as an open-source tool.
- Accessible: You do not neet to install any additional software for Ansible to perform its tasks. 
- Powerful: Ansible allows you to model highly complex IT workflows.

The playbook implements the following tasks:

- Configure Elk VM with Docker
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Download and launch a docker ELK container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- This ELK server is configured to monitor the following machines: -Private IPs of Web-1, Web-2, Web-3

| Name     |    IP Addresses     |
|----------|---------------------|
|  Web-1   | 10.0.0.6            |
|  Web-2   | 10.0.0.7            |
|  Web-3   | 10.0.0.8            |


We have installed the following Beats on these machines:

-**Microbeat**: is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

-Specify which Beats you successfully installed:
- Microbeat
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- **Filebeat** - collects data about the file system
- **Metricbeat** - collects machine metrics, such as uptime


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:

- Copy the **playbook** file to the **Ansible** directory.

- Update the **hosts** file to include webserver and ELK VM.

- Run the playbook, and navigate to **Kibana** to check that the installation worked as expected.


_TODO: Answer the following questions to fill in the blanks:_

- _Which file is the playbook? Where do you copy it?_
- 
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- 
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
