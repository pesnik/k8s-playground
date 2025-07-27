create-cluster:
	kind create cluster --config=cluster-config.yml
deploy-nginx:
	kubectl create deployment nginx --image=nginx --port=80
start-service:
	kubectl create service nodeport nginx --tcp=80:80 --node-port=30000
