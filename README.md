# Ansible_installation_steps
Ansible is an open-source automation platform. It is very, very simple to set up and yet powerful. Ansible can help you with configuration management, application deployment, task automation.

# Pre-requisites
  1. An AWS EC2 instance (on Control node)
  
 # Installation steps:
   # on Amazon EC2 instance
   
 1. Install python and python-pip

        yum install python
        yum install python-pip

2. Install ansible using pip check for version

      pip install ansible
      
      ansible --version
      
3. Create a user called ansadmin (on Control node and Managed host)

      useradd ansadmin
      
      passwd ansadmin
      
 4.Below command grant sudo access to ansadmin user. But we strongly recommended using "visudo" command if you are aware vi or nano editor. (on Control node and Managed host)
 
       echo "ansadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
       
 5.Log in as a ansadmin user on master and generate ssh key (on Control node)

        ssh-keygen
        
 6.Copy keys onto all ansible managed hosts (on Control node)

        ssh-copy-id ansadmin@<target-server>
        
7. Ansible server used to create images and store on docker registry. Hence install docker, start docker services and add ansadmin to the docker group.

      yum install docker

      //start docker services 
      
      service docker start

      //add user to docker group 
      
      usermod -aG docker ansadmin
      
      
8. Create a directory /etc/ansible and create an inventory file called "hosts" add control node and managed hosts IP addresses to it.

# Validation test

    Run ansible command as ansadmin user it should be successful (Master)

    ansible all -m ping
