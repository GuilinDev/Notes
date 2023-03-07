pod
kubectl
Yaml: list, dict, list of dict

```shell
kubectl run - - help 
kubectl run nginx - -image=nginx

kubectl get pods
kubectl describe pod podname 

kubectl get pods -o wide

kubectl get nodes
kubectl delete pod podname

kubectl run redis —image=redis123 —dry-run=client -o yaml > redis.yaml, 产生一个可运行的redis.yaml
然后可以运行: kubectl create -f redis.yaml
Change the image name: 1) kubectl edit 2) change redis.yaml and kubectl apply -f redis.yaml
```
