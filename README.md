[readme.txt](https://github.com/jrgoo267/First-Repsository/files/7139934/readme.txt)
# First-Repsository
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/jrgoo267/First-Repsository/blob/main/Diagrams/virtualnetwork_with_elk.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/jrgoo267/First-Repsository/tree/main/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting flooding of the network.
- Load balancers helps spread traffic throughout the servers, preventing DDoS attacks. The jump box allows the public to only be exposed to one server instead of all, creating less surface area for attack.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat is a lightweight shipper for forwarding and centralizing log data
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System |
|----------|----------- |------------|------------------|
| Jump Box | Gateway    | 10.0.0.10  | Linux            |
| WEB_1    | Web-server | 10.0.0.11  | Linux            |
| WEB_2    | web-server | 10.0.0.12  | Linux            |
| WEB_3    | web-server | 10.0.0.13  | Linux            |
| Elk_1    | ELK-stack  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal Home IP address

Machines within the network can only be accessed by ssh w/ key.
- The Jumpbox machine is the only machine allowed to access the Elk_1 webserver via port 5601

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | personal home IP     |
| Web_1-3  | no                  | 10.0.0.10            |
| Elk_1    | no                  | personal home IP     |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because if we need to add more virtual machines we can just run the ansible playbook and configure machines in seconds rather than configuring the VM piece by piece.

The playbook implements the following tasks:
- install docker.io
- install pip
- install python3-pip
- download and install docker elk container
- increase memory using systemctl
- download and launch docker container sebp/elk:761

The following screenshot displays the result of running “sudo docker ps” after successfully configuring the ELK instance.
 


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.11
- Web-2 10.0.0.12

We have installed the following Beats on these machines:
- FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:
- FileBeat collects system log data such as system events
- MetricBeat collect system data such as CPU usage  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat and metricbeat config file to local /etc/ansible.
- Update the config files to include Elk servers private IP
- Run the playbook, and navigate to http://[ELK-server-public-IP]:5601/app/kibana to check that the installation worked as expected.

- /etc/ansible/roles/filebeat-playbook.yml is the filebeat playbook. Copy it to /etc/ansible/roles/[playbook-name]

-/etc/ansible/files/metricbeat-playbook.yml is the metricbeat playbook. Copy it to /etc/ansible/files/[playbook-name]

- To make the Ansible playbook run on your specific machine, you will need to navigate to the /etc/ansible/hosts file and create yours groups using square brackets (for example I have [webservers] and [elk]) and replace private IP addresses with your own private machines IP. You will then need to update your respective playbooks with the groups you have created under the “hosts:” line so your playbook knows which machine to apply the playbook to

To make sure the ELK server is running properly you will need to navigate to http://[elk-machine-public-ip:5601]/app/kibana
