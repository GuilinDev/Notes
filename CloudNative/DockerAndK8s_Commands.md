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

# 修改k8s自动生成的在内存中的配置文件，修改后无需apply，但如果需要替换掉坏掉的pods，需要删除坏的pods  
kubectl delete pod new-replica-set-xkzg6 new-replica-set-hzlq8 new-replica-set-sftjd new-replica-set-9kdr2
#然后kubectl会自动重新生成新的pods

# 直接编辑rs配置文件
kubectl edit replicaset myapp-replicaset
```

设置了replicaset的replica数字以后，手动删除一个pod后，会自动生成same label的足额的pods数目；同样，如果想额外创建，则会自动terminating

```shell
# 创建一个deployment
kubectl create -f deployment-definition.yml
kubectl create -f deployment-definition.yml --record # 记录已经发生的变化

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

```shell
# 从头新建一个deployment的yaml
kubectl create deployment --help
kubectl create deployment-name --image=image-name --replicas=3
kubectl get deploy

# 同时check多个部署单位
kubectl get pods, deploy, svc, rs
```

Update and Rollback:

When first crates a deployment, it triggers a **roolout**, a new rollout creates a new revision. When application is updated, new rollout is triggered and new deployment revision is created. 
```shell
# check the status of rollout
kubectl rollout status deployment/myapp-deployment
# check revisions and history of deployment
kubectl rollout history deployment/myapp-deployment
```

Two deployment strategies: 1）(Default)Rolling update: 逐个替换，service不会down，2）Recreate: 全部destroy后再spin up新的版本

```shell
# 1）更新版本号方法1: 直接修改配置yml中spec下pod的image的版本号，然后应用
kubectl apply -f deployment-definition.yml
# 2）更新版本号方法2: set命令 (会产生新的definition文件)
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
kubectl set image deployment myapp-deployment nginx=nginx:1.9.1 --record
# 例子
kubectl set image deployment(整个deployment)/frontend(具体deployment的名字，/可用空格) simple-webapp(pod中container的名字)=kodekloud/webapp-color:v2(需要替换的版本号)

# 查看具体deployment的strategy (strategyType)是rolling update还是recreate
kubectl describe deployment myapp-deployment
# 更换deployment的strategy，一种方法是修改原始的yaml然后apply，另一种是以下(原始yaml文件不变)：
kubectl edit deployment myapp-deployment # 修改后不用做任何apply

```

Upgrade： # ReplicaSet总是会重新创建的

Rollback (把前一个版本的replicaset的回滚)：
```shell
kubectl rollout undo deployment/myapp-deployment
# 检查rs的名字
kubectl get replicaset

# rollout相关的命令
kubectl rollout status
kubectl rollout hisotry
kubectl rollout undo
kubectl rollout pause
kubectl rollout resume

# 例如，查看rollout的历史修改各版本，以及各自信息
kubectl rollout history deployment.apps/myapp-deployment
```

### K8s Network 101
* 同一个node下，default部署pods的最大数量是110；
* 同一个node下，Each pod has its own ip;
* 同一个node下Pods之间不直接交流(up down不方便，而通过internal network)
* 而在K8s的cluster中，不同pods(无论pods在不在同一个node)之间的交流，K8s需要我们自己配置，使用现有的解决方案（CNI Provider）例如Calico，flannel，cilium，NSX等等，确保不同pods之间各自的IP能被别的pods访问，作为pods之间的routing用；

### Services
K8s services enable communication btw components within/outside the application

TargetPort (backend port for container/pod to be exposed) -> port(on K8s Service) -> NodePort (range from 30000 to 32767), only port is required in yaml file, if not set targetPort, then targetPort will be same as port, it not set nodePort, it will auto set a free port btw 30000 and 32767.

```shell
kubectl get service
kubectl get svc
# 查看k8s集群下的service的各种状态，包括labels，nodePorts等
kubectl describe svc myServiceName
# 创建一个service
kubectl create -f service-definition.yaml
```
Pods通常带有labels，这些labels通常作为Service的selectors（如果service的selector昱pods的labels不同，则service无法access pods）

### Microservice Application

