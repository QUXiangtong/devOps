Lab3
ansible/inventories/setup.yml
# Project inventory grouping production hosts
all:
  vars:
    ansible_user: admin  # default user for SSH
    ansible_ssh_private_key_file: /Users/tong/Desktop/devOps/id_rsa
  children:
    prod:
      hosts:
        xiangtong.qu.takima.cloud:

Base Commands

ansible all -i inventories/setup.yml -m ping


ansible all -i inventories/setup.yml -m setup -a "filter=ansible_distribution*"


ansible all -i inventories/setup.yml -m apt -a "name=apache2 state=present" --become


ansible all -i inventories/setup.yml -m apt -a "name=apache2 state=absent" --become
