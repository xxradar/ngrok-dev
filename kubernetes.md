## Kubernetes ingress
Deploy as documented https://dashboard.ngrok.com/get-started/setup/kubernetes

```
kubectl apply -f https://raw.githubusercontent.com/xxradar/kubernetes_learning/master/nginx-deployment.yaml
```
```
kubectl apply -f https://raw.githubusercontent.com/xxradar/kubernetes_learning/master/nginx-expose-clusterip.yaml
```
```
export NGROK_DOMAIN="key-skylark-full.ngrok-free.app"
```
```
kubectl apply -f - <<EOF
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
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
                name: my-nginx-clusterip
                port:
                  number: 80
EOF
```

