![users and ssh key](https://user-images.githubusercontent.com/72060000/109306122-b4037c00-780c-11eb-8a73-3cfdecb19f67.png)





Ansible: Create Users and Add SSH Key
=========
This play book create users and their ssh key's to remote machines. 
How to setup:
Shell = /bin/bash
Add the public key in "files" dir (username.pub)
In tasks/main.yml  specify that user should have the right to sudo or no

Distros tested
------------

Currently, this is only tested on Centos 7 as a client and server machine. It should theoretically work on Ubuntu or Debian based systems.


Role Variables
--------------

users:
  - username: user1
  - username: user2
  - username: user3
  - username: user4
  - username: user5
  
Example Playbook
------------
/*
  - name: Add users | create users, shell, home dirs
    user: name={{ item.username }} shell=/bin/bash createhome=yes comment='create with ansible'
    with_items: '{{users}}'

  - name: Setup | authorized key upload
    authorized_key: user={{ item.username }}
      key="{{ lookup('file', 'files/{{ item.username }}.pub') }}"
    with_items: '{{users}}'
    
    */

Usage
----------------

install ansible
create keys
add key's to the username.pub file

run command
ansible-playbook (-i inventory_file) user_ssh_deploy.yml

Author Information
------------------

Aaron Yildiztas
