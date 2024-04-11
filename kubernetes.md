## Kubernetes ingress
Deploy as documented https://dashboard.ngrok.com/get-started/setup/kubernetes

```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Service
metadata:
	name: game-2048
spec:
	ports:
		- name: http
			port: 80
			targetPort: 80
	selector:
		app: game-2048
---
apiVersion: apps/v1
kind: Deployment
metadata:
	name: game-2048
spec:
	replicas: 1
	selector:
		matchLabels:
			app: game-2048
	template:
		metadata:
			labels:
				app: game-2048
		spec:
			containers:
				- name: backend
					image: alexwhen/docker-2048
					ports:
						- name: http
							containerPort: 80
EOF
```
