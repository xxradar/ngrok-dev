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
```
export NGROK_DOMAIN="key-skylark-full.ngrok-free.app"
```
```
kubectl apply -f - <<EOF
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: game-2048
spec:
  ingressClassName: ngrok
  rules:
    - host: $NGROK_DOMAIN
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: game-2048
                port:
                  number: 80
EOF
```

