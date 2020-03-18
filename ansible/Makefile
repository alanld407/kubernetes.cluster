
all : nfs drives
.PHONY : all
nfs:
	ansible-playbook -vvv -u root --private-key=~/.ssh/kubernetes playbooks/nfs_client_setup.yml

drives:
	ansible-playbook -u root --private-key=~/.ssh/kubernetes playbooks/drives_setup.yml


list:
	ansible-playbook --list-tasks -u root --private-key=~/.ssh/kubernetes playbooks/nfs_setup.yml
