
all : cluster drives nfs
.PHONY : all

## Add host name to the hosts file first
## /etc/ansible/hosts
.PHONY : cluster
cluster:
	ansible-playbook -i hosts -u root --private-key=~/.ssh/kubernetes playbooks/server_setup.yaml
	ansible-playbook ${DEBUG} -i hosts -u root --private-key=~/.ssh/kubernetes playbooks/client_setup.yaml

nfs:
	ansible-playbook ${DEBUG} -i hosts -u root --private-key=~/.ssh/kubernetes playbooks/nfs_client_setup.yml

drives:
	ansible-playbook -u root --private-key=~/.ssh/kubernetes playbooks/drives_setup.yml


list:
	ansible-playbook --list-tasks -u root --private-key=~/.ssh/kubernetes playbooks/nfs_client_setup.yml
