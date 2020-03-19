
# https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/

create:
	echo 'Hello from Kubernetes storage' > /mnt/nfs/disk1/kubernetes/data

pv:
	kubectl apply -f pv-volume.yaml --validate=false
	kubectl apply -f pv-claim.yaml --validate=false
	kubectl apply -f pv-pod.yaml --validate=false

clean:
	kubectl delete pod task-pv-pod
	kubectl delete pvc task-pv-claim
	kubectl delete pv task-pv-volume

list:
	kubectl get pv task-pv-volume
	kubectl get pvc task-pv-claim
	kubectl get pod task-pv-pod

shell:
	kubectl exec -it task-pv-pod -- /bin/bash

install:
	##Run these in the shell
	apt update
	apt install curl
	curl http://localhost/