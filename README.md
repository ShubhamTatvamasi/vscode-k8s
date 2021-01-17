# vscode-k8s

```bash
kubectl run vscode --image=codercom/code-server --restart=Never --port=8080 --expose -- --auth none

kubectl patch svc vscode \
  --patch='{"spec": {"type": "NodePort"}}'

kubectl patch svc vscode \
  --patch='{"spec": {"ports": [{"nodePort": 30100, "port": 8080}]}}'
```


```bash
date +%s%N | md5sum | awk '{print $1}'
```
