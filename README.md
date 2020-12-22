# ansible-playbooks
working ansible playbooks


ansible-playbook nginxinstall.yml

edit hosts parameter according to groupname

mysql8install.yml
---------------------

This will install mysql 8 on remote hosts configured on /etc/ansible/hosts file


[webservers] # group
web-host1 # hostfile

[webservers:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user='ansnode-1'  #remote host username
ansible_become='yes' 
ansible_become_pass='password' #remote host sudo password 
ansible_become_method='sudo'

content of /etc/ansible/host_vars/web-host1 

ansible_ssh_host: 192.168.1.8 #remote host ip 
ansible_ssh_port: 22
root_password: root #mysql root password will be set 

Need to create  /etc/ansible/group_vars/webservers file.No need to entry any values

run playbook from the location of yml file:

ansible-playbook mysql8install.yml

2.nginxgit.yml

must have static_site.cfg file on ansible server with below contents :

server {
        listen 80 default_server;
        listen [::]:80 default_server;
        root /var/www/html/webserver;
        server_name _;
        location / {
                try_files $uri $uri/ =404;
        }
}

This playbook will install nginx on remote host and will clone the repo in /var/www/html location

So if you check remotehost browser as localhost you can see the static html page.

