## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagram/project-13.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? What is the advantage of a jump box? Load Balancing plays an important security role as computing moves evermore to the cloud. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. The advantage of a jump box is to give access to the user from a single node that can be secured and monitored and also serves as an additional layer of protection.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
- What does Filebeat watch for?_ Data about the file system
- What does Metricbeat record?_ Machine metrics such as uptime/downtime and usage

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Client   | 10.0.0.5   | Linux            |
| Web-2    | Client   | 10.0.0.6   | Linux            |
| Web-3    | Client   | 10.0.0.7   | Linux            |
| ELK-Server|Gateway  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses:13.92.139.174

Machines within the network can only be accessed by ssh from the Jump-Box VM
- Which machine did you allow to access your ELK VM? What was its IP address? The Jump-Box can access the ELK-Server with it private IP 10.0.0.4:22 because there is a peering between the two virtual network.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump Box  | Yes                 | 10.0.0.4 10.0.0.30   |
|Elk Server| No                  | 10.1.0.0/24          |
|Web-1     | No                  | 10.0.0.5/24
|Web-2     | No                  | 10.0.0.6/24
|Web-3     | No                  | 10.0.0.7/24
|/Images/SSHAccess|              |                      |
| /Images/Jump-Box-ip|           |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? Single point of configuration, management and provisioning.

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
i)install docker
ii) install pip3
iii) install docker python module
iv) Download and lunch docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance. /Images/install ELK Playbook

Images/docker ps

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring: Web-1 10.0.0.5 Web-2 10.0.0.6 Web-3 10.0.0.7 ELK-Server 10.1.0.4

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed: Filebeat and Metricbeat were installed successfully

These Beats allow us to collect the following information from each machine:
-In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

- Filebeat monitors the log files or location that you specify, collect log events and forwards them either to Elasticsearch or Logstach
- Metricbeat records the metric and statistics such as up time that it collect and ships them to the output that being specify, such as Elasticsearch or Logstach.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the Playbook file to /etc/Ansible
- Update the hosts file to include the VM's client IP addresses 10.0.0.5 - 10.0.0.7
Ansible_python_interpreter=/urs/bin/python3
- Run the playbook, and navigate to 10.0..0.5 and curl localhost/setup.php  to check that the installation worked as expected.

- Which file is the playbook? Where do you copy it? Ansible-playbook.yml /etc/ansible
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? It is updated on the hosts files, when add the hosts name elk into the webservers group followd by the IP address for the ELK-SERVER 10.1.0.4 /ansible/hosts-file.txt
- _Which URL do you navigate to in order to check that the ELK server is running? Public IP address of the ELK-server on port 5601 (13.92.139.174:5601)

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
ansible-playbook your-playbook.yml *.yml nano hosts, nano ansible.cfg nano *.yml
