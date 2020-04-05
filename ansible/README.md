
Make sure to setup ssh keys on remote systems before deploying with ansible

Example:

ssh-copy-id root@kubernetes

ssh-copy-id root@worker-37ca16

ssh-copy-id root@worker-e21b7d

ssh-copy-id root@worker-e09a81

Add hosts to the local hosts file

Optionally edit the
```
/etc/ansible/hosts

kubernetes ansible_user=root
worker-37ca16 ansible_user=root
worker-e21b7d ansible_user=root
worker-e09a81 ansible_user=root
```
