

##NOTE: This does not work with helm 3.xxx

# https://istio.io/docs/setup/install/helm/

istio-setup:
	# helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.5.2/charts/

	# Create a namespace for the istio-system components
	kubectl create namespace istio-system

	# Install all the Istio Custom Resource Definitions (CRDs) using kubectl apply:
	# $ helm template install/kubernetes/helm/istio-init --name istio-init --namespace istio-system | kubectl apply -f -
	helm template istio-init install/kubernetes/helm/istio-init --namespace istio-system | kubectl apply -f -

	# Wait for all Istio CRDs to be created:
	kubectl -n istio-system wait --for=condition=complete job --all

istio-provisioner:
	helm install istio-provisioner stable/istio-client-provisioner --set istio.server=kubernetes --set istio.path=/disk1 --set storageClass.name=istio 
	# helm install istio-provisioner stable/istio-client-provisioner --set istio.server=kubernetes --set istio.path=/disk1 --set storageClass.name=managed-istio-storage 
   # helm install istio-provisioner stable/istio-server-provisioner
   # helm delete istio-provisioner
   ## Make this storage class the default
	kubectl patch storageclass istio -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
	kubectl get storageclass

istio-test:
	kubectl create -f deploy/test-claim.yaml -f deploy/test-pod.yaml
istio-test-delete:
	kubectl delete -f deploy/test-pod.yaml -f deploy/test-claim.yaml