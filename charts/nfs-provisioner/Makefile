
# https://github.com/kubernetes-incubator/external-storage/tree/master/nfs-client
nfs-provisioner:
	helm install nfs-provisioner stable/nfs-client-provisioner --set nfs.server=kubernetes --set nfs.path=/disk1 --set storageClass.name=nfs 
   # helm install nfs-provisioner stable/nfs-server-provisioner
   # helm delete nfs-provisioner

   ## Make this storage class the default
	kubectl patch storageclass nfs -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
	kubectl get storageclass
nfs-test:
	kubectl create -f deploy/test-claim.yaml -f deploy/test-pod.yaml
nfs-test-delete:
	kubectl delete -f deploy/test-pod.yaml -f deploy/test-claim.yaml