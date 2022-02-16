## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below:

![NetworkDiagram](https://user-images.githubusercontent.com/99365720/153497900-453d44be-7c24-480e-83ef-07ad874bae6a.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. 

Alternatively, select portions of the **YAML** file may be used to install only certain pieces of it, such as Filebeat.

- [ELK-Install.yml](https://github.com/MartinaBialek/CyberBootcamp-UofO-Project-1/blob/ab7475d51289cb04ee9b21ba2ed2c981a5d687f6/Ansible/install-elk.yml)
- [Filebeat-playbook.yml](https://github.com/MartinaBialek/CyberBootcamp-UofO-Project-1/blob/9b6c661e16864902b8fa4cbec37bf6c0acb713e8/Ansible/filebeat-playbook.yml)
- [Metricbeat-playbook.yml](https://github.com/MartinaBialek/CyberBootcamp-UofO-Project-1/blob/9b6c661e16864902b8fa4cbec37bf6c0acb713e8/Ansible/metricbeat-playbook.yml)
 
**This document contains the following details:**

- Description of the Topology
- Access Policies
- ELK Configuration
- Target Machines and Beats
- Using a Playbook

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the _D*mn Vulnerable Web Application_.
Load balancing ensures that the application will be highly **available**, in addition to restricting **in-bound access** to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?

- The off-loading function of a **load balancer** defends an organization against distributed denial-of-service (DDoS) attacks. A **jump box** ensures that your network has continous support this is also a more doable solution when a user either has no direct office or data center access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **jump box** and system **network**.

- **Filebeat** monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

- **Metricbeat** takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. 

**The configuration details of each machine may be found below:**

| Name     | Function | IP Address | Operating System|
|----------|----------|------------|-----------------|
| Jump Box | Gateway  | 10.0.0.5   |  Linux          |
| Web-1    |Web Server| 10.0.0.6   |  Linux          |
| Web-2    |Web Server| 10.0.0.7   |  Linux          |
| Web-3    |Web Server| 10.0.0.8   |  Linux          |
| ELK-VM   |Web Server| 10.1.0.7   |  Linux          |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 

Only the **jump box provisioner** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- **5061 Kibana Port**

Machines within the network can only be accessed by the **jump box provisioner**.

**Which machine did you allow to access your ELK VM? What was its IP address?**
- IP Address of the Azadmin/Sysadmin machine
- IP Address: 50.45.135.213

**The configuration details of each machine may be found below.**

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |    No               | 50.45.135.213        |
|  Web-1   |    No               | 10.0.0.6             |
|  Web-2   |    No               | 10.0.0.7             |
|  Web-3   |    No               | 10.0.0.8             |
| ELK-VM   |    No               | 10.1.0.7             |  

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous in the following ways:

- **Flexible/Customizable:** You can create a customizable environment regardless of where it is deployed.  
- **Free:** Operates as an open-source tool.
- **Accessible:** You do not neet to install any additional software for Ansible to perform its tasks. 
- **Powerful:** Ansible allows you to model highly complex IT workflows.

**The playbook implements the following tasks:** 

- Configure Elk VM with Docker
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Download and launch a docker ELK container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


**docker-ps-output.png**

![docker-ps-output](https://user-images.githubusercontent.com/99365720/153778045-32e1f45e-0ef1-4a36-8b02-b1f8438fb4c8.png)




### Target Machines & Beats

This ELK server is configured to monitor the following machines: 

- Private IPs of Web-1, Web-2, Web-3

| Name     |    IP Addresses     |
|----------|---------------------|
|  Web-1   | 10.0.0.6            |
|  Web-2   | 10.0.0.7            |
|  Web-3   | 10.0.0.8            |


We have installed the following Beats on these machines:

-**Microbeat**: which is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. 

**Also successfully installed:**
- Microbeat
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine in the following ways:

- **Filebeat** - monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- **Metricbeat** - takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

### Using the Playbook

Playbooks for [Filebeat](https://github.com/MartinaBialek/CyberBootcamp-UofO-Project-1/blob/0042ece19b85cb12278a9cf4ff4aad3faac4eb5a/Ansible/filebeat-playbook.yml) and [Metricbeat](https://github.com/MartinaBialek/CyberBootcamp-UofO-Project-1/blob/0042ece19b85cb12278a9cf4ff4aad3faac4eb5a/Ansible/metricbeat-playbook.yml) are can be also found here.

- You can edit the **filebeat.config** and **metricbeat.config** files to specify which hosts the playbook would run on.

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 


SSH into the control node and follow the steps below to access Filebeat playbook:
 
1. Copy the **playbook** file to the **Ansible** directory.

   ```cd /etc/ansible```
   
   ```mkdir files```
   
   ```curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.0.0-amd64.deb```

2. Update the **hosts** file to include webserver and ELK VM.

  ```cd /etc/ansible```
  
   ```nano hosts```
   
   ```[webservers]```
   
   ```10.0.0.6```  
   
   ```10.0.0.7```  
   
   ```10.0.0.8```
   
   ```[ELK]```
   
   ```10.1.0.7```
   
3. **Create** playbook:
   ```nano Playbook-name.yml```

4. **Run** the playbook:
   ```ansible-playbook Playbook-name.yml```
   
- This indicates that the installation was successful:   
![filebeat-system-module](https://user-images.githubusercontent.com/99365720/153778056-8b7129c2-69bf-48a6-acb1-479f85da650e.png)

- The playbook is Install-elk.yml and copy it to /etc/ansible.
- In the ansible.cfg file add the elk_vm ip address to monitor under the [webservers] to monitor it and place the elk ip address under [elk] which indicates that the destination where the elk has to be installed on.
- Navigate to kibana to check that the installation worked as expected: http://[Elk-Serve-IP]:5601/app/kibana
