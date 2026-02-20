🔹 1. Basic Ansible Commands (Daily Essentials)
✅ Check Ansible Version
ansible --version

✅ Ping All Hosts (Connectivity Test)
ansible all -m ping

Ping specific group:

ansible webservers -m ping

✅ Run Ad-hoc Command (Execute Shell Command)

ansible all -a "uptime"

Using shell module:

ansible all -m shell -a "df -h"

✅ Run Command as Sudo

ansible all -b -a "yum update -y"

-b = become (sudo)

✅ Check Inventory

ansible-inventory --list

Check specific host:

ansible-inventory --host <hostname>


✅ Gather Facts

ansible all -m setup
----------------------------------------------------------------------------------------------------
🔹 2. Working with Playbooks (Very Common in Daily Work)
✅ Run a Playbook
ansible-playbook site.yml

With specific inventory:

ansible-playbook -i inventory.ini site.yml

✅ Check Playbook Syntax

ansible-playbook site.yml --syntax-check

✅ Dry Run (Check Mode)
ansible-playbook site.yml --check

✅ Show Differences (When Files Change)
ansible-playbook site.yml --diff

✅ Run Specific Tags
ansible-playbook site.yml --tags "install"

Skip tags:

ansible-playbook site.yml --skip-tags "config"
✅ Limit to Specific Hosts
ansible-playbook site.yml --limit webservers

🔹 3. File & Package Management Commands (Daily Use)
✅ Copy File
ansible all -m copy -a "src=/tmp/file.txt dest=/tmp/file.txt"
✅ Install Package (RHEL/CentOS)
ansible all -m yum -a "name=httpd state=present"
✅ Install Package (Ubuntu/Debian)
ansible all -m apt -a "name=nginx state=present update_cache=yes"
✅ Start/Enable Service
ansible all -m service -a "name=nginx state=started enabled=yes"
🔹 4. Intermediate Commands
✅ Use Different User
ansible all -u ec2-user -a "whoami"
✅ Ask for SSH Password
ansible all -k -m ping
✅ Ask for Sudo Password
ansible all -K -a "systemctl restart nginx"
✅ Run in Parallel (Increase Forks)
ansible all -f 20 -a "uptime"
✅ Use Extra Variables
ansible-playbook site.yml -e "env=prod version=1.2"

From file:

ansible-playbook site.yml -e @vars.yml
🔹 5. Advanced Ansible Commands (Production Level)

✅ Run Playbook Step-by-Step
ansible-playbook site.yml --step

✅ Start at Specific Task
ansible-playbook site.yml --start-at-task="Install Nginx"

✅ Debug Variables
ansible all -m debug -a "var=ansible_hostname"

✅ Vault (Encrypt Secrets)

Encrypt file:

ansible-vault encrypt secrets.yml

Edit encrypted file:

ansible-vault edit secrets.yml

Run playbook with vault:

ansible-playbook site.yml --ask-vault-pass
✅ Dynamic Inventory Script
ansible-inventory -i aws_ec2.yml --graph
✅ Run Only Failed Hosts
ansible-playbook site.yml --limit @site.retry

🔹 7. Real-Life Daily Use Examples

🔥 Restart Nginx on Web Servers
ansible webservers -b -m service -a "name=nginx state=restarted"

🔥 Check Disk Usage on All Servers
ansible all -a "df -h"

🔥 Deploy Application
ansible-playbook deploy.yml --limit appservers