# Ansible
Ansible config file default location: /etc/ansible.ansible.cfg
/opt/ansible-web.cfg has the highest priority

# Set env variable
ANSIBLE_GATHERING=explicit

# View all configs
ansible-config list
ansible-config view - This shows the active config file
ansible-config dymp - This shows current settings

# Inventory Files
ansible_host=server1.com - this specifies the dns or Ip of the server
ansible_connection=ssh/winrm - This specifies how to conect to a host. SSH for linux, winrm for windows
ansible_user=root/admin -  This specifies the user
ansible_ssh_pass=Password - Specifies the password for ssh connection. Best practice is to set up ssh passwordless auth between servers

# Inventory file sample
web1 ansible_host=<dns/ipadd> ansible_connection=ssh/winrm 

# Variables
vars:
    var_name: value

{{ var_name }}

Can also make use of a host variable file
var1: value
var2: value

if varibale is starting a sentence use quotes - '{{ var_name }}'

variable types:
    number
    boolean
    list
    dictionary

Grouping variables
    [web_servers]
    web1
    web2
    web3

    [webservers:vars]
    var_name=value
variables defined on the host level take precednce over group variables and playbook variables take precedence over host. Varibale passed in the cmd line takes the highest variables

# Variable scope
    Host
    Play
    Global

# Magic Variables
 Used to retrieve variables that were defined on other hosts
    '{{hostvars['web2'].variable_name }}'
 group_names : shows what groups a host is part of 
 inventory_hostname

# Register a result/output
register: result

# Ansible facts
    system specific info
    Auto ran by ansible to gather facts
    all facts are stored in a variable called ansible_fact
    disable by
        gather_facts: no

# Ansible playbook
run ans ansible playbook
ansible-playbook <playbook_name>
run ansible in check mode
    ansible-playbook <playbook_name> --check
    makes sure ansible does what its intended to do

run ansible in diff mode
    ansible-playbook <playbook_name> --diff
    show the difference between and after playbook runs

# Ansible lint
catches style related issues
