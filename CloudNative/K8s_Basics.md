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

```shell
# 查看所有资源
kubectl get all --no-headers # --no-headers不算header以免出错
kubectl get all --no-headers | wc -l
```

Pod-> Replicaset -> Deployment ->

Yaml: list, dict, list of dict

```shell
kubectl run - - help 
kubectl run nginx - -image=nginx

kubectl get pods
kubectl get po --watch # 有时候创建的时间太长，这个命令会创建完成后再显示
kubectl describe pod myapp-pod 

# 创建一个pod并且传递参数
kubectl run po nginx image=nginx -- --color green
kubectl run po my-app image=my-image --command python3 app.py --color green
# kubectl describe po my-app 可以查看参数

kubectl get pods -o wide

kubectl get nodes
kubectl delete pod podname

# 产生一个可运行的redis.yaml
kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml
# 然后可以运行: 
kubectl 

-f redis.yaml
# Change the image name: 1) kubectl edit 2) change redis.yaml and kubectl apply -f redis.yaml

# 更多例子
# Create an NGINX Pod
kubectl run nginx --image=nginx
# Generate POD Manifest YAML file (-o yaml). Don't actually create the pod(--dry-run)
kubectl run nginx --image=nginx --dry-run=client -o yaml

# Create the deployment
kubectl create deployment --image=nginx nginx
# Generate Deployment YAML file (-o yaml). Don't actually create the deployment(--dry-run)
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

# Generate Deployment YAML file (-o yaml). Don’t actually create the deployment(–dry-run) and save it to a file.
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

# Make necessary changes to the file (for example, adding more replicas) and then create the deployment.
kubectl create -f nginx-deployment.yaml
kubectl create --force -f nginx-deployment.yaml # 如果有pod，强行替代
# OR, In k8s version 1.19+, we can specify the --replicas option to create a deployment with 4 replicas.
kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
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

### Namespaces
```shell
# 查看单个ns下面的pods
kubectl get pods --namespace=example
kubectl get pods -n=example
# 查看所有ns的pods
kubectl get pods --all-namespaces
kubectl get pods -A
```

### Microservice Application
GKE, EKS, AKS

### 考试命令行熟悉
#### POD
Create an NGINX Pod
```shell
kubectl run nginx --image=nginx
```

Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)
```shell
kubectl run nginx --image=nginx --dry-run=client -o yaml
```


#### Deployment
Create a deployment
```shell
kubectl create deployment --image=nginx nginx
```

Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)
```shell
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
```


Generate Deployment with 4 Replicas
```shell
kubectl create deployment nginx --image=nginx --replicas=4
```

You can also scale a deployment using the kubectl scale command.
```shell
kubectl scale deployment nginx --replicas=4
```

Another way to do this is to save the YAML definition to a file and modify
```shell
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml
```

You can then update the YAML file with the replicas or any other field before creating the deployment.

#### Service
Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379
```shell
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
```
(This will automatically use the pod's labels as selectors)

Or
```shell
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 
```
(This will not use the pods labels as selectors, instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. So generate the file and modify the selectors before creating the service)

Expose pod port to service when creating pod 
```shell
kubectl run httpd --image=httpd:alpine --port=80 --expose=true
```


Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:
```shell
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
```
(This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.)

Or
```shell
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
```
(This will not use the pods labels as selectors)

Both the above commands have their own challenges. While one of it cannot accept a selector the other cannot accept a node port. I would recommend going with the kubectl expose command. If you need to specify a node port, generate a definition file using the same command and manually input the nodeport before creating the service.

#### Static Pods
```shell
# 找到kubelet配置文件的位置
ps -ef | grep /usr/bin/kubelet
ps -aux | grep kubelet

# 找到生成pod的yaml文件位置
grep -i staticpod /var/lib/kubelet/config.yaml

# Modify yaml 文件
```

#### ConfigMaps
```shell
# 从命令行生成cm
kubectl create cm webapp-config-map --from-literal=APP_COLOR=darkblue --from-literal=APP_OTHER=disregard
```
### SecretMaps
```shell
# 从命令行生成secret
kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
```
#### MultiContainer
```shell
kubectl -n my-namespace logs my-pod

kubectl logs orange -c init-myservice(container name)
```

## Core concepts
### Create a namespace called 'mynamespace' and a pod with image nginx called nginx on this namespace

<details><summary>show</summary>
<p>

```bash
kubectl create namespace mynamespace
kubectl run nginx --image=nginx --restart=Never -n mynamespace
```

</p>
</details>

### Create the pod that was just described using YAML

<details><summary>show</summary>
<p>

Easily generate YAML with:

```bash
kubectl run nginx --image=nginx --restart=Never --dry-run=client -n mynamespace -o yaml > pod.yaml
```

```bash
cat pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
  namespace: mynamespace
spec:
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
kubectl create -f pod.yaml
```

Alternatively, you can run in one line

```bash
kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml | kubectl create -n mynamespace -f -
```

</p>
</details>

### Create a busybox pod (using kubectl command) that runs the command "env". Run it and see the output

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox --command --restart=Never -it --rm -- env # -it will help in seeing the output, --rm will immediately delete the pod after it exits
# or, just run it without -it
kubectl run busybox --image=busybox --command --restart=Never -- env
# and then, check its logs
kubectl logs busybox
```

</p>
</details>

### Create a busybox pod (using YAML) that runs the command "env". Run it and see the output

<details><summary>show</summary>
<p>

```bash
# create a  YAML template with this command
kubectl run busybox --image=busybox --restart=Never --dry-run=client -o yaml --command -- env > envpod.yaml
# see it
cat envpod.yaml
```

```YAML
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: busybox
  name: busybox
spec:
  containers:
  - command:
    - env
    image: busybox
    name: busybox
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

```bash
# apply it and then see the logs
kubectl apply -f envpod.yaml
kubectl logs busybox
```

</p>
</details>

### Get the YAML for a new namespace called 'myns' without creating it

<details><summary>show</summary>
<p>

```bash
kubectl create namespace myns -o yaml --dry-run=client
```

</p>
</details>

### Get the YAML for a new ResourceQuota called 'myrq' with hard limits of 1 CPU, 1G memory and 2 pods without creating it

<details><summary>show</summary>
<p>

```bash
kubectl create quota myrq --hard=cpu=1,memory=1G,pods=2 --dry-run=client -o yaml
```

</p>
</details>

### Get pods on all namespaces

<details><summary>show</summary>
<p>

```bash
kubectl get po --all-namespaces
```
Alternatively 

```bash
kubectl get po -A
```
</p>
</details>

### Create a pod with image nginx called nginx and expose traffic on port 80

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --restart=Never --port=80
```

</p>
</details>

### Change pod's image to nginx:1.7.1. Observe that the container will be restarted as soon as the image gets pulled

<details><summary>show</summary>
<p>

*Note*: The `RESTARTS` column should contain 0 initially (ideally - it could be any number)

```bash
# kubectl set image POD/POD_NAME CONTAINER_NAME=IMAGE_NAME:TAG
kubectl set image pod/nginx nginx=nginx:1.7.1
kubectl describe po nginx # you will see an event 'Container will be killed and recreated'
kubectl get po nginx -w # watch it
```

*Note*: some time after changing the image, you should see that the value in the `RESTARTS` column has been increased by 1, because the container has been restarted, as stated in the events shown at the bottom of the `kubectl describe pod` command:

```
Events:
  Type    Reason     Age                  From               Message
  ----    ------     ----                 ----               -------
[...]
  Normal  Killing    100s                 kubelet, node3     Container pod1 definition changed, will be restarted
  Normal  Pulling    100s                 kubelet, node3     Pulling image "nginx:1.7.1"
  Normal  Pulled     41s                  kubelet, node3     Successfully pulled image "nginx:1.7.1"
  Normal  Created    36s (x2 over 9m43s)  kubelet, node3     Created container pod1
  Normal  Started    36s (x2 over 9m43s)  kubelet, node3     Started container pod1
```

*Note*: you can check pod's image by running

```bash
kubectl get po nginx -o jsonpath='{.spec.containers[].image}{"\n"}'
```

</p>
</details>

### Get nginx pod's ip created in previous step, use a temp busybox image to wget its '/'

<details><summary>show</summary>
<p>

```bash
kubectl get po -o wide # get the IP, will be something like '10.1.1.131'
# create a temp busybox pod
kubectl run busybox --image=busybox --rm -it --restart=Never -- wget -O- 10.1.1.131:80
```

Alternatively you can also try a more advanced option:

```bash
# Get IP of the nginx pod
NGINX_IP=$(kubectl get pod nginx -o jsonpath='{.status.podIP}')
# create a temp busybox pod
kubectl run busybox --image=busybox --env="NGINX_IP=$NGINX_IP" --rm -it --restart=Never -- sh -c 'wget -O- $NGINX_IP:80'
``` 

Or just in one line:

```bash
kubectl run busybox --image=busybox --rm -it --restart=Never -- wget -O- $(kubectl get pod nginx -o jsonpath='{.status.podIP}:{.spec.containers[0].ports[0].containerPort}')
```

</p>
</details>

### Get pod's YAML

<details><summary>show</summary>
<p>

```bash
kubectl get po nginx -o yaml
# or
kubectl get po nginx -oyaml
# or
kubectl get po nginx --output yaml
# or
kubectl get po nginx --output=yaml
```

</p>
</details>

### Get information about the pod, including details about potential issues (e.g. pod hasn't started)

<details><summary>show</summary>
<p>

```bash
kubectl describe po nginx
```

</p>
</details>

### Get pod logs

<details><summary>show</summary>
<p>

```bash
kubectl logs nginx
```

</p>
</details>

### If pod crashed and restarted, get logs about the previous instance

<details><summary>show</summary>
<p>

```bash
kubectl logs nginx -p
# or
kubectl logs nginx --previous
```

</p>
</details>

### Execute a simple shell on the nginx pod

<details><summary>show</summary>
<p>

```bash
kubectl exec -it nginx -- /bin/sh
```

</p>
</details>

### Create a busybox pod that echoes 'hello world' and then exits

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox -it --restart=Never -- echo 'hello world'
# or
kubectl run busybox --image=busybox -it --restart=Never -- /bin/sh -c 'echo hello world'
```

</p>
</details>

### Do the same, but have the pod deleted automatically when it's completed

<details><summary>show</summary>
<p>

```bash
kubectl run busybox --image=busybox -it --rm --restart=Never -- /bin/sh -c 'echo hello world'
kubectl get po # nowhere to be found :)
```

</p>
</details>

### Create an nginx pod and set an env value as 'var1=val1'. Check the env value existence within the pod

<details><summary>show</summary>
<p>

```bash
kubectl run nginx --image=nginx --restart=Never --env=var1=val1
# then
kubectl exec -it nginx -- env
# or
kubectl exec -it nginx -- sh -c 'echo $var1'
# or
kubectl describe po nginx | grep val1
# or
kubectl run nginx --restart=Never --image=nginx --env=var1=val1 -it --rm -- env
# or
kubectl run nginx --image nginx --restart=Never --env=var1=val1 -it --rm -- sh -c 'echo $var1'
```

</p>
</details>
