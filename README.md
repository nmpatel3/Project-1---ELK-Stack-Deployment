## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml_TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.

 - Load balancing protects the availability component of the C.I.A. triad by making sure that one server is not overloaded with requests and is distributing the data load effectively across other servers on the network.
- The importance of having the Jump-Box-Provisioner machine is to be able to automatically change the configuration of devices in the network using a single provisioner command.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name        | Function  | IP Address | Operating System |
|-------------|-----------|------------|------------------|
| Jump Box    | Gateway   | 10.1.0.4   | Linux            |
| Web-1       | Web Server| 10.1.0.6   | Linux            |
| Web-2       | Web Server| 10.1.0.7   | Linux            |
| ELK-VM-1    | Monitoring| 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- (My personal IP Address)

Machines within the network can only be accessed by Jump-Box-Provisioner.
- The Jumpbox Provisioner connects via SSH to the Webservers and the ELK Server. The Web Server machines send logs to the ELK Server to be forwarded for indexing. Jump-Box-Provisioner's public IP address - 20.37.244.69

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses       |
|----------------------|---------------------|----------------------------|
| Jump-Box-Provisioner | Yes                 | 10.1.0.4, 20.37.244.69     |
| Web-1                | No                  | 10.1.0.6                   |
| Web-2                | No                  | 10.1.0.7                   |
| ELK                  | No                  | 10.2.0.4, 52.172.232.170   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantae of an automated configuration with Ansible is you can rerun the install as many times as needed with the same result, as it remove the margin of human error. This would be helpful when setting up multiple computers with the same indended setup.

The playbook implements the following tasks:
- Install docker
- Install Python-pip
- Install the docker python module
- Increase the virtual Memory
- Download and launch the elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.1.0.6)
- Web-2 (10.1.0.7)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat
	- Allows you to collect data that is specified to certain log files or locations on the machine. It then can take these logs and put them in Logstash and/or Elasticsearch.
- Metricbeat 
	- Collects system metrics, such as CPU usage, RAM usage, and network load from each machine. It is used to monitor system performance and to identify abnormal behavior patterns across the network that could indicate an attack has occured.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Filebeat

	- Replace The IP address with the ELK server private IP address in the filebeat-configuration.yml and save the file to 	/etc/ansible/filebeat-config.yml.
	- Update the /etc/ansible/hosts file to include the IP addresses of webservers on which the filebeat is installed.
	- Run the playbook, and navigate to http://http://20.204.18.152:5601/app/kibana to check that the installation worked as expected.

- Metricbeat

	- Replace The IP address with the ELK server private IP address in the metric-configuration.yml and save the file to 	/etc/ansible/metric-config.yml.
	- Update the /etc/ansible/hosts file to include the IP addresses of webservers on which the filebeat is installed.
	- Run the playbook, and navigate to http://http://20.204.18.152:5601/app/kibana to check that the installation worked as expected.

- Answer the following questions to fill in the blanks:_

- Which file is the playbook? Where do you copy it?
	- Copy install-elk.yml file to /etc/ansible/
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
	- You have to update the ansible hosts file to specifiy which VMs to run each playbook on. Your machine's IP address must be under "webservers" if installing Filebeat, or under "elk" if installing the ELK stack.
- Which URL do you navigate to in order to check that the ELK server is running?
	- To check that the ELK server is running input <ELK SERVER IP Address>:5601 into the browser.



