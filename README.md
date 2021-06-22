This example uses a simple maven based webapp project.

For build use : mvn clean package

<!--User story -->

Development Team

<!--push to SCM -->
GitHub

<!--CHECKOUT -->
JENKINS
MAVEN

<!-- PUBLISH -->
SONATYPE NEXUS

<!-- PULL LATEST BUILD ARTIFACT -->
ANSIBLE: open source automation tool for
1.  Provisioning
    - infrastructure provisioning: IAC (Terraform for data center; VPC, subnets, EC2, etc)

2.  Config managment 
    - applying OS patches
    - checking server 
    - installation of services

3.  Application deployment
---------------------------------
PLAYBOOKS - App deployment
- YAML format 
- instructs ansible on what needs to be executed 
- to do list for ansible
- Tasks are run sequentially

AGENTLESS: don't need to install on managed nodes
DECLARITIVE/Can Be Procedural
- Declare what you want and don't think about how to get there
- Playbooks=declarative; Tasks=procedural
- Idempotent - can execute an application multiple times without changing 

<!--ANSIBLE ADHOC COMMANDS -->
ansible [name-of-group] -m [module] -a [arguments] -i [inventory]

- m <modules> perform actual tasks

- a <argument> 

- i <inventory> required if not using default host file at /etc/ansible

# navigate to the /opt directory
cd /opt
# create the playbooks directory
mkdir playbooks
# change the ownership of the playbooks directory to ansibleadmin
sudo chown -R ansibleadmin:ansibleadmin playbooks/
# nav to the playbooks directory
cd playbooks
# create a file named hosts
vim hosts
:i
[tomcat]
# locate the private IP of the tomcat server created in aws and paste below
# do the same for docker
# file should read:

[tomcat]
172.20.10.135

[docker]
172.20.10.27
# :wq to save
