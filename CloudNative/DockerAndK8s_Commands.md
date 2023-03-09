## Docker
熟悉image, container和registry

```shell
# 从registry 拉取镜像
docker pull nginx
docker pull lyzhang1999/hello-world-flask:latest

# 查看本地已经拉取的镜像
docker images

# 运行image，浏览器可查看 localhost:8000
docker run -d -p 8000:5000 hello-world-flask:latest

# 查看本地container列表
docker ps
# 进入container
docker exec -it c370825640b6 bash / docker exec -it c370825640b6 sh

# 停止container
docker stop docker containerID

# 制作本地image
docker build -t hello-world-flask .
# tag制作好的本地image(提交到registry，例如dockerhub时，需要的标签)
docker tag hello-world-flask guilindev/hello-world-flask
# 上传上述image到docker hub上
docker push guilindev/hello-world-flask

```

## Kubenetes
熟练 kubectl

Pod-> Replicaset -> Deployment ->

Yaml: list, dict, list of dict

```shell
kubectl run - - help 
kubectl run nginx - -image=nginx

kubectl get pods
kubectl describe pod myapp-pod 

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

创建replicaset-definition.yml (rs for relicaset)
```shell
kubectl create -f replicaset-definition.yml

kubectl get replicaset
kubectl get rs

kubectl describe replicaset rs-name

kubectl delelte replicaset myapp-replicaset # 会同时delete该replicaset的所有pods
```

创建replicaset-definition.yml后，例如如果想改变replicas的数量，可以run以下命令使之生效
```shell
kubectl replace -f replicaset-definition.yml
# 或者直接运行scale命令，此时文件会同时改变
kubectl scale --replicas=6 -f replicaset-definition.yml
# 或者接运行scale命令+replica set Name (此时配置文件会同时变，用kubectl edit rs rs-name查看)
kubectl scale --replicas=6 replicaset myapp-relicaset

kubectl get replicaset
kubectl describe replicaset myapp-replicaset

# 解释k8s的resources和fields的详细信息
kubectl explain rs

# 修改k8s自动生成的在内存中的配置文件，修改后无需apply，但如果需要替换掉坏掉的pods，需要删除坏的pods  kubectl delete pod new-replica-set-xkzg6 new-replica-set-hzlq8 new-replica-set-sftjd new-replica-set-9kdr2， 然后kubectl会自动重新生成新的pods
kubectl edit replicaset myapp-replicaset
```

设置了replicaset的replica数字以后，手动删除一个pod后，会自动生成same label的足额的pods数目；同样，如果想额外创建，则会自动terminating

```shell
# 创建一个deployment
kubectl create -f deployment-definition.yml

# check创建出啦的deployment
kubectl get deployments
kubectl describe deployment myapp-deployment
# deployment会自动create replicaset
kubectl get replicaset
# replicaset会自动创建pods
kubectl get pods

# 检查已经创建出来的所有objects，包括deployments， replicaset和pods
kubectl get all
```
