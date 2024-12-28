# ansiblepractice

# Ansible installation commands
> sudo apt-add-repository ppa:ansible/ansible <br>
> sudo apt update
> sudo apt install ansible

# Setting Up the Inventory File
> sudo nano /etc/ansible/hosts
 [servers]
server1 ansible_host=public_ip
server2 ansible_host=public_ip
server3 ansible_host=public_ip

[all:vars]
ansible_python_interpreter=/usr/bin/python3

# commands for ansible
ansible webservers -m user -a "name=web group=weblogic createhome=yes" -b : to create user and also attache to create group


ansible webservers -m group -a "name=weblogic state=present"  : to only create group by using ad-hoc command


ansible webservers -a "df -h"  to show disk space in worker node

ansible <group> -m apt -a "name=apache2 state=present"  : to install packages into workernodes
ansible <group  name> -m module name> -a "name=apache2 state=present"  : to install packages into workernodes

ansible <group> -m command -a " apt update -y"  to run commands in workernodes

[ansibel<grup> -m modulename -a "dest=/file name mode = 777 state = touch"  
ansibel<grup> -m file -a "dest=/file name mode = 777 state = touch"  ]: to create file in workernodes


ansibel<grup> -m file -a "dest=/<directoryname> mode = 777 state =directory"  : to create directory in workernodes
 ansible localhost -m file -a "dest=/opt/bmcdir mode=755 owner=<server name> group=<server name> state=directory"

ansible <group>  -m <modulename> (service) -a "name=<server name > (httpd) (apache2) state=started"  to start the services in workernodes

#  Run the job every 15 minutes
$ ansible <groupname> -m cron -a "name='daily-cron-all-servers' minute=*/15 
job='/path/to/minute-script.sh'"



# Run the job every four hours
$ ansible multi -s -m cron -a "name='daily-cron-all-servers' hour=4 
job='/path/to/hour-script.sh'"


# Enabling a Job to run at system reboot
$ ansible multi -s -m cron -a "name='daily-cron-all-servers' special_time=reboot 
job='/path/to/startup-script.sh'"


# Scheduling a Daily job
$ ansible <groupname> -m cron -a "name='daily-cron-all-servers' special_time=daily 
job='/path/to/daily-script.sh'"


# Scheduling a Weekly job
$ ansible <groupname> -m cron -a "name='daily-cron-all-servers' special_time=weekly 
job='/path/to/daily-script.sh'"

ansible <testserver> -m copy -a "src=~/Downloads/index.html dest=/var/www/html owner=apache group=apache mode=0644"  : to copy file from master to slave opt/bmcdiry
 


# playbook.yaml execution command
>ansible-playbook -i /etc/ansible/hosts playbook.yaml
