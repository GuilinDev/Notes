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

# 产生一个可运行的redis.yaml
kubectl run redis —image=redis123 —dry-run=client -o yaml > redis.yaml
# 然后可以运行: 
kubectl create -f redis.yaml
# Change the image name: 1) kubectl edit 2) change redis.yaml and kubectl apply -f redis.yaml
```

老 - Replication Controller - 为pod做LB和Scaling（单个node内部，以及多个nodes之间）
新 - Replica Set - spec下面多了个selector

创建replicaset-definition.yml
```shell
kubectl create -f replicaset-definition.yml

kubectl get replicaset

kubectl delelte replicaset myapp-replicaset # 会同时delete该replicaset的所有pods
```

创建replicaset-definition.yml后，例如如果想改变replicas的数量，可以run以下命令使之生效
```shell
kubectl replace -f replicaset-definition.yml
# 或者直接运行scale命令，此时文件会同时改变
kubectl scale --replicas=6 -f replicaset-definition.yml
# 或者接运行scale命令+replica set Name (此时配置文件不会改变，只是实际的pod数量变了)
kubectl scale --replicas=6 replicaset myapp-relicaset
```
