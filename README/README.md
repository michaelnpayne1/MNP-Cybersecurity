## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/Users/mrffib/MNP-Cybersecurity/README/Images/diagram_topology.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - /Users/mrffib/MNP-Cybersecurity/Ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting access to the network.
- Load balancers protect against DDos attacks, as they filter traffic through its configured pools. The main advantage of a jumpbox is that everything is contained and maintained in one central location (the jumpbox vm).

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- Filebeat monitors log files.
- Metricbeat records stats and metrics of the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function     | IP Address | Operating System |
|----------|--------------|------------|------------------|
| Jump Box | Gateway      | 10.0.0.7   | Linux            |
| Web-1    | Monitored VM | 10.0.0.8   | Linux            |
| Web-2    | Monitored VM | 10.0.0.9   | Linux            |
| Elk      | Elk Suite    | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 168.62.40.123

Machines within the network can only be accessed by Red-Team-NSG
- Elk was allowed on my Web 1 and Web 2 servers. Elk IP is 10.1.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 10.0.0.8 10.0.0.9    |
| Ansible  | No                  | 10.0.0.7             |
| HTTP     | Yes                 | 10.0.0.8 10.0.0.9    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because tasks are numerous and often have to be updated to their latest states.
- Ansible's main advantage is that it is free to use/implement.

The playbook implements the following tasks:
- Install docker.io: installs the latest version of Docker.
- Install python3-pip: installs the latest version of the python programming language.
- Install Docker module: controls the state of Docker.
- Increase virtual memory: allows more memory to be used due to numerous tasks being implemented.
- Use more memory: allows Elk to be run.
- Download & launch Elk: downloads and launches the latest version of Elk.
- Enable docker on boot: enables Elk to start when computer is booted.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

/Users/mrffib/MNP-Cybersecurity/README/Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8
- 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to collect and view logs on our servers. These logs include instances of sudo, log-ins, ssh, etc. The data is presented in graphs. 
- Metricbeat allows us to collect stats and metrics of web traffic on our servers. 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to Ansible.
- Update the hosts file to include the IP address of your ELK VM.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana.  to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
    - install-elk.yml
    - copy to Web 1 and Web 2
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
    - update the hosts file to include ip addresses of Web VMs.
    - You have to update the roles file to allow Filebeat to be configured. 
- _Which URL do you navigate to in order to check that the ELK server is running?
    - http://[your.ELK-VM.External.IP]:5601/app/kibana. 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
-Run playbook:
  - ansible-playbook install-elk.yml
