

# https://istio.io/docs/setup/getting-started/

istio-setup:
	curl -L https://istio.io/downloadIstio | sh -
	cd istio-1.5.2
	# Add the istioctl client to your path (Linux or macOS):
	export PATH=$PWD/bin:$PATH
	bin/istioctl manifest apply --set profile=demo
	kubectl label namespace default istio-injection=enabled

	## Deploy sampple application
	kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
	kubectl get services
	kubectl get pods
	# kubectl exec -it $(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}') -c ratings -- curl productpage:9080/productpage | grep -o "<title>.*</title>"
	kubectl exec -it `kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}' ` -c ratings -- curl productpage:9080/productpage | grep -o "<title>.*</title>"

	# Open the application to outside traffic
	kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
	kubectl get gateway

	#Set the ingress ports:

	set INGRESS_PORT=`kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}'`
	set SECURE_INGRESS_PORT=`kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].nodePort}'`

	# Set INGRESS_HOST:
	set INGRESS_HOST=`kubectl get po -l istio=ingressgateway -n istio-system -o jsonpath='{.items[0].status.hostIP}'`

	# Set GATEWAY_URL:
	set GATEWAY_URL=${INGRESS_HOST}:${INGRESS_PORT} 

	bin/istioctl dashboard kiali &
	kubectl -n istio-system get svc prometheus
	kubectl -n istio-system get svc grafana

	kubectl -n istio-system port-forward `kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}' ` 3000:3000 &

	http://localhost:3000/dashboard/db/istio-mesh-dashboard
	http://localhost:3000/dashboard/db/istio-service-dashboard
	http://localhost:3000/dashboard/db/istio-workload-dashboard

	## Send traffic through the mesh
	curl http://$GATEWAY_URL/productpage



istio-delete:
	istioctl manifest generate --set profile=demo | kubectl delete -f -

istio-test:
	kubectl create -f deploy/test-claim.yaml -f deploy/test-pod.yaml
istio-test-delete:
	kubectl delete -f deploy/test-pod.yaml -f deploy/test-claim.yaml