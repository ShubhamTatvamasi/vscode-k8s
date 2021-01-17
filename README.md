# vscode-k8s

deploy vscode:
```
kubectl create deployment vscode --image=codercom/code-server
kubectl expose deployment vscode --port=8080 --name=vscode
```

get password:
```bash
kubectl exec deploy/vscode -- cat /home/coder/.config/code-server/config.yaml
```

delete everything:
```bash
kubectl delete deploy/vscode svc/vscode ing/vscode
```

create ingress value:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: vscode
spec:
  rules:
    - host: vscode.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: vscode
            servicePort: 8080
EOF
```
---

create pod
```bash
kubectl run vscode --image=codercom/code-server --restart=Never --port=8080 --expose -- --auth none

kubectl patch svc vscode \
  --patch='{"spec": {"type": "NodePort"}}'

kubectl patch svc vscode \
  --patch='{"spec": {"ports": [{"nodePort": 30100, "port": 8080}]}}'
```
