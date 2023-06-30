## Core Concepts
#### Docker & containerD
containerD command line tools: ctr, nerdctl, crictl

#### ETCD Beginner
etcdctl

#### Kube-API server
1. Authenticate  User
2. Validate Request
3. Retrieve Data
4. Update ETCD (Kube-API server是唯一与ECTD直接打交道的component)
5. Scheduler
6. Kubelet

#### Kube Controller Manager

## Scheduling

## Logging & Monitoring

```shell
kubectl top node --sort-by='cpu'
kubectl top pod --no-headers

kubectl logs my-web-pod

```

## Application Lifecycle Management

## Cluster Maintaince

## Security

三种certificates，1）server certificate, configured on servers; 2) root certificate, configured on CA servers; 3) client certificates, configured on clients;

```shell
# 以text方式查看server和etcd证书信息
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text
openssl x509 -in /etc/kubernetes/pki/ca.crt -text
openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text
```

```shell
# 提取certificate文件中的证书信息
cat akshay.csr | base64 -w 0

# 查看已创建csr request
kubectl get csr
# 批准或拒绝一个csr
kubectl certificate approve akshay
kubectl certificate deny agent-smith
# 查看某个csr的yaml
kubectl get csr agent-smith -o yaml
```

```shell
# 查看当前config
kubectl config --kubeconfig=/root/my-kube-config current-context
```

```shell
# 用can-i检查权限
kubectl auth can-i create deployments
kubectl auth can-i create deployments --as dev-user
kubectl auth can-i delete nodes
kubectl auth can-i delete nodes --as sta-user

# 检查当前用的何种authorization mode，检查--authorization-mode=Node
kubectl describe pod kube-apiserver-controlplane -n kube-system
```

```shell
# Create a role, or with yaml
kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods
# Create a rolebinding, or with yaml
kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user

# clusterrole and clusterrolebinding are similar
```

1.24版本后需要自己在serviceaccount里面创建secret和token
```shell
kubectl create secret docker-registry my-secret --docker-server=DOCKER_REGISTRY_SERVER
--docker-username=DOCKER_USER --docker-password=DOCKER_PASSWORD --docker-email=DOCKER_EMAIL
```

## Storage

## Networking
```shell
ip link
ip addr
ip route
cat /proc/sys/net/ipv4/ip_forward

dig

ip netns
```

```shell
# 查看container runtime
ps -aux | grep -i kubelet | grep --color container-runtime-endpoint
```

## Others

```shell
# For controlplane failture
service kubelet status
kubectl logs kube-api-server -n kube-system
sudo journalctl -u kube-apiserver

# For work node failture

```


## Questions
### 1. Role-based Access Control (RBAC)
```bash
kubectl config use-context k8s

# 解题：
kubectl create clusterrole deployment-clusterrole --verb=create --resource=deployments,statefulsets,daemonsets
kubectl -n app-team1 create serviceaccount cicd-token

# 如果题目说了“限于namespace app-team1中”，创建rolebinding；如果没说，则创建clusterrolebinding
# option 1，创建rolebinding，只给一个namespace授权permission
kubectl -n app-team1 create rolebinding cicd-token-rolebinding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cicd-token
# option 2，创建clusterrolebinding，给cluster中所有namespace授权permission
kubectl -n app-team1 create clusterrolebinding cicd-token-clusterrolebinding --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cicd-token

# 验证 (optional)
kubectl -n app-team1 describe rolebinding cicd-token-rolebinding
kubectl -n app-team1 describe clusterrolebinding cicd-token-clusterrolebinding
```

### 2. Check Pod's CPU
```bash
# Task:
# 通过pod labelname=cpu-loader，找到运行时占用大量CPU 的pod，
# 并将占用CPU 最高的pod 名称写入文件/opt/KUTR000401/KUTR00401.txt（已存在）。

# 考点：对kubectl top pod --| 的理解，直接看-h，不用查文档
kubectl top pod -h

# switch to k8s context
kubectl config use-context k8s

# 解题：
# 通过-A查询所有namespace下的pod名称，由高到低排序
kubectl top pod -l name=cpu-loader --sort-by=cpu -A

# 将上一步找到的第一个，也就是cpu占用最多的pod的name写入/opt/KUTR000401/KUTR00401.txt中
echo "上一步查出来的Pod Name" > /opt/KUTR000401/KUTR00401.txt

# 验证 (optional)
cat /opt/KUTR000401/KUTR00401.txt
```

### 3. Network Policy
参考文档：[依次点击Concepts→Services, Load Balancing, and Networking →Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
```bash
# Task:
# 在现有的namespacemy-app中创建一个名为allow-port-from-namespace的新NetworkPolicy。确保新的NetworkPolicy允许namespaceecho中的Pods连接到namespacemy-app中的Pods的9000端口。进一步确保新的NetworkPolicy：不允许对没有在监听端口9000的Pods的访问, 不允许非来自namespaceecho中的Pods的访问
# 双重否定就是肯定，所以最后两句话的意思就是：仅允许端口为9000的pod方法。仅允许echo命名空间中的pod访问

# 考点： NetworkPolicy的创建

kubectl config use-context k8s

# 查看所有ns标签的label
kubectl get ns --show-labels

# 如果没有标签，手动打一个
kubectl label ns echo project=echo
```
  

# 编写一个NetworkPolicy的yaml文件，从上面官网copy过来，然后如下修改
![](../images/certificates/3.png)

```bash
kubectl apply -f network-policy.yaml

# 验证 (optional)
kubectl describe neworkpolicy -n my-app

```

#### 4. Expose Service
参考文档： [依次点击Concepts→Workloads→Workload Resources→Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
```bash
kubectl config use-context k8s

# 检查deployment信息，并记下SELECTOR的Lable标签，这里是app=front-end
kubectl get deployment front-end -o wide

# 参考官方文档， 按需edit上面的deployment
kubectl edit deployment front-end

# ...
spec:
  containers:
  -image: vicuu/nginx:hello
    imagePullPolicy: IfNotPresent
    name: nginx # 找到此位置。下文会简单说明一下yaml文件的格式，不懂yaml格式的，往下看。
    ports:                  #添加这4行
    -name: http
      containerPort: 80
      protocol: TCP
      
# ...      
      
# 暴露对应端口
# 注意考试中需要创建的是NodePort，还是ClusterIP。如果是ClusterIP，则应为--type=ClusterIP
# --port是service的端口号，--target-port是deployment里pod的容器的端口号。
kubectl expose deployment front-end --type=NodePort --port=80 --target-port=80--name=front-end-svc

# 暴露服务后，检查一下service的selector标签是否正确，这个要与deployment的selector标签一致的。
kubectl get svc front-end-svc -o wide
kubectl get deployment front-end -o wide

# 如果kubectl expose暴露服务后，发现service的selector标签是空的<none>，或者不是deployment的, 则需要编辑service，手动添加标签
kubectl edit svc front-end-svc
# 在ports这一小段下面添加selector标签
selector:
  app: front-end      
# 注意yaml里是写冒号，而不是等号，不是app=front-end。确保service的selector标签与deployment的selector标签一致。

# 最后curl检查
kubectl get pod,svc -o wide
curl 所在的node的ip或主机名:30938
curl svc的ip地址:80
# （注意，只能curl通svc的80端口，但是无法ping通的。）考试时，如果curl不通，简单排错后也不通，就不要过于纠结，继续往下做题即可。
```

#### 5. 创建Ingress
参考文档： [依次点击Concepts→Services, Load Balancing, and Networking→Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
```shell
kubectl config use-context k8s

# 从上面官网copy一个ingress的yaml文件，然后修改如下
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  labels:
    app.kubernetes.io/component: controller
  name: nginx-example # 考试时，默认是没有ingressClassName的，所以我们要先手动建一个ingressClassName，命名就为nginx-example吧
  annotations:ingressclass.kubernetes.io/is-default-class: "true"
spec:controller: k8s.io/ingress-nginx
--- # 因为是不同文件，所以这3个---，必须要写，不能省略
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ping
  namespace: ing-internal
  annotations:
nginx.ingress.kubernetes.io/rewrite-target: / # 因为考试环境有多套，不清楚具体抽中的是哪套。在1.26的考试里，先写上这行，如果apply时报错需要指定域名，则注释这行再apply，就成功了。spec:
  ingressClassName: nginx-example#这里调用上面新建的ingressClassName为nginx-example
  rules:
  -http:paths:-path: /hello
    pathType: Prefix
    backend:service:
      name:hello
      port:
        number: 5678
```

创建好Ingress的yaml后，执行如下命令

```shell
kubectl apply -f ingress.yaml

# 检查，利用curl，通过get ingress 查看ingress的内外IP，然后通过提供的curl 测试ingress 是否正确
# 做完题后，略等3分钟，再检查，否则可能还没获取IP地址。或者可以先去做别的题，等都做完了，再回来检查这道题，一下，记得回来检查时，先使用kubectl config use-context k8s切换到此集群。
kubectl get ingress -n ing-internal # 查看ingress的内外IP
curl 拿到的ID/hello # 测试ingress 是否正确
```

#### 6. 扩容deployment副本数量
```shell
kubectl config use-context k8s

# 先检查一下现有的pod数量（可不检查
kubectl get deployments presentation -o wide
kubectl get pod -l app=presentation

# 扩容
kubectl scale deployments presentation --replicas=4

```

#### 7. 调度pod到指定节点
参考文档：[依次点击Tasks→Configure Pods and Containers→Assign Pods to Nodes](https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/)
```shell
kubectl config use-context k8s

# 先检查一下是否有这个pod，一般是没有创建的，所以需要自己创建
kubectl get pod -A | grep nginx-kusc00401

# 确保node有这个labels，考试时，检查一下就行，应该已经提前设置好了labels
kubectl get nodes --show-labels | grep 'disk=ssd'
# 如果node没有这个labels，可以手动添加
kubectl label nodes node01 disk=ssd

# 创建pod yaml，set paste，防止yaml文件空格错序
apiVersion: v1
kind: Pod
metadata:
  name: nginx-kusc00401
spec:
  containers:
  -name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent       #这句的意思是，如果此image已经有了，则不重新下载。考试时写不写这个都是可以的。
  nodeSelector:
    disk: ssd

# 创建pod
kubectl apply -f pod-disk-ssd.yaml

# 检查
kubectl get po nginx-kusc00401 -o wide
```

#### 8. 查看可用节点数量
```shell
kubectl config use-context k8s

# grep -i是忽略大小写，grep -v是排除在外，grep -c是统计查出来的条数。
kubectl describe nodes | grep -i Taint | grep -vc NoSchedule
echo "查出来的数字" > /opt/KUSC00402/kusc00402.txt

# 检查
cat /opt/KUSC00402/kusc00402.txt
```

#### 9. 创建多容器的pod
```shell
kubectl config use-context k8s

vim pod-kucc.yaml
# 注意:set paste，防止yaml文件空格错序
apiVersion: v1
kind: Pod
  metadata:
  name: kucc8
spec:
  containers:
  -name:nginx
    image: nginx
    imagePullPolicy: IfNotPresent#这句的意思是，如果此image已经有了，则不重新下载。考试时写不写都可以。但模拟环境里推荐写，pod启动快。
  -name: consul
    image: consul
    imagePullPolicy: IfNotPresent

# 创建pod
kubectl apply -f pod-kucc.yaml

# 检查
kubectl get po kucc8
```

#### 10. 创建PV
参考文档：[依次点击Tasks→Configure Pods and Containers→Configure a Pod to Use a PersistentVolume for Storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
```shell
kubectl config use-context hk8s

# 直接从官方复制合适的案例，修改参数，然后设置hostPath 为/srv/app-config 即可。
vim pv.yaml
#注意: set paste，防止yaml文件空格错序
apiVersion: v1
kind: PersistentVolume
metadata:
  name: app-config
  #labels:#不需要写
    #type: local
spec:
  capacity:
    storage: 1Gi
  accessModes:
    -ReadWriteMany #注意，考试时的访问模式可能有ReadWriteMany和ReadOnlyMany和ReadWriteOnce，根据题目要求写。
  hostPath:path: "/srv/app-config"

# 创建pv
kubectl apply -f pv.yaml

# 检查
kubectl get pv
# 在检查结果里，ACCESS MODES那一列中，RWX是ReadWriteMany，RWO是ReadWriteOnce。
```

#### 11. 创建PVC
参考文档：[依次点击Tasks→Configure Pods and Containers→Configure a Pod to Use a PersistentVolume for Storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
```shell
```shell
kubectl config use-context ok8s

# 根据官方文档复制一个PVC配置，修改参数，不确定的地方就是用kubectl 的explain 帮助。
vim pvc.yaml
#注意:set paste，防止yaml文件空格错序

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-volume #pvc名字
spec:
  storageClassName: csi-hostpath-sc
  accessModes:
    -ReadWriteOnce #注意，考试时的访问模式可能有ReadWriteMany和ReadOnlyMany和ReadWriteOnce，根据题目要求写。
  resources:
    requests:
      storage: 10Mi

# 创建pvc
kubectl apply -f pvc.yaml

# 检查
kubectl get pvc

vim pvc-pod.yaml
# 注意:set paste，防止yaml文件空格错序

apiVersion: v1
kind: Pod
metadata:
  name: web-server
spec:
  volumes:
    -name: task-pv-storage # 这个name要和下面volumeMounts的name一样。
      persistentVolumeClaim:
        claimName:pv-volume #这个要使用上面创建的pvc名字
  containers:
    -name: nginx
      image: nginx:1.16
      volumeMounts:
        -mountPath: "/usr/share/nginx/html"
        name: task-pv-storage # 这个name要和上面的volumes的name一样。

# 创建pod
kubectl apply -f pvc-pod.yaml

# 检查
kubectl get po web-server

# 更改大小，并记录过程。
# 将storage: 10Mi改为storage: 70Mi   （模拟环境里会报错，下面有解释。）
# 注意是修改上面的spec:里面的storage:
kubectl edit pvc pv-volume --record
# 模拟环境是nfs存储，操作时，会有报错忽略即可。考试时用的动态存储，不会报错的。
```

#### 12. 查看pod日志
```shell
kubectl config use-context k8s

kubectl logs foo| grep "RLIMIT_NOFILE"> /opt/KUTR00101/foo

#检查
cat /opt/KUTR00101/foo
```

#### 13. 使用sidecar代理容器日志
参考文档：[依次点击Concepts→Cluster Administration→LoggingArchitecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/)
```shell
kubectl config use-context k8s

# 通过kubectl get pod -o yaml 的方法备份原始pod 信息，删除旧的pod 11-factor-appcopy 一份新yaml 文件，添加一个名称为sidecar 的容器新建emptyDir 的卷，确保两个容器都挂载了/var/log 目录新建含有sidecar 的pod，并通过kubectl logs 验证

# 导出这个pod的yaml文件
kubectl get pod 11-factor-appcopy -o yaml > varlog.yaml
# 备份yaml文件，防止改错了时回退。
cp varlog.yaml varlog.yaml.bak

# 修改varlog.yaml文件
vim varlog.yaml

# 根据官方文档拷贝需要的信息，在《下面是运行两个边车容器的Pod 的配置文件》里。
spec:
。。。。。。
    volumeMounts:#在原配置文件，灰色的这段后面添加
    -mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-4l6w8
      readOnly: true
    -name: varlog # 新加内容
      mountPath: /var/log # 新加内容
  -name: sidecar #新加内容，注意name 别写错了
    image:busybox # 新加内容
    args: [/bin/sh, -c, 'tail -n+1 -f /var/log/11-factor-app.log'] # 新加内容，注意文件名别写错了。另外是用逗号分隔的，而题目里是空格。
    volumeMounts: # 新加内容
    -name: varlog #新加内容
      mountPath: /var/log # 新加内容
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
。。。。。。
  volumes: # 在原配置文件，灰色的这段后面添加。
  -name: kube-api-access-kcjc2
    projected:defaultMode: 420
    sources:
    -serviceAccountToken:
      expirationSeconds: 3607
      path: token
    -configMap:
      items:
      -key: ca.crt
        path: ca.crt
      name: kube-root-ca.crt
    -downwardAPI:
      items:
      -fieldRef:
        apiVersion: v1
        fieldPath: metadata.namespace
      path: namespace
  -name: varlog # 新加内容，注意找好位置。
    emptyDir: {} # 新加内容

# 删除原先的pod，大于需要等2分钟
kubectl delete pod 11-factor-appcopy
# 检查一下是否删除了
kubectl get pod 11-factor-appcopy
# 新建这个pod
kubectl apply -f varlog.yaml

# 检查
kubectl logs 11-factor-app sidecar
```

#### 14. 升级集群
```shell
kubectl config use-context mk8s

kubectl get nodes
kubectl cordon master01
kubectl drain master01 --ignore-daemonsets

# ssh到master01，切换为root
ssh master01
sudo -i

# 升级
apt-get update
apt-get show kubeadm | grep Version
apt-get install -y kubeadm=1.27.1-00

# 检查升级后的版本
kubeadm version

# 验证升级计划
kubeadm upgrade plan
# 排除etcd，升级其他的，提示时，输入y
kubeadm upgrade apply v1.27.1 --etcd-upgrade=false

# 升级kubelet
apt-get install -y kubelet=1.27.1-00
kubelet --version

# 升级kubectl
apt-get install -y kubectl=1.27.1-00
kubectl version

#退出root，退回到candidate@master01
exit
#退出master01，退回到candidate@node01
exit

# 恢复master01调度
kubectl uncordon master01

# 检查master01的状态是否Ready
kubectl get nodes
```

#### 15. 备份还原etcd
```shell
# 这步不需做 kubectl config use-context k8s

# 备份
# 如果不使用export ETCDCTL_API=3，而使用ETCDCTL_API=3，则下面每条etcdctl命令前都要加ETCDCTL_API=3。
# 如果执行时，提示permission denied，则是权限不够，命令最前面加sudo即可
export ETCDCTL_API=3
etcdctl --endpoints=https://11.0.1.111:2379--cacert="/opt/KUIN00601/ca.crt" --cert="/opt/KUIN00601/etcd-client.crt" --key="/opt/KUIN00601/etcd-client.key" snapshot save /var/lib/backup/etcd-snapshot.db

# 检查（optional）
etcdctl snapshot status /var/lib/backup/etcd-snapshot.db -wtable

# 还原
sudo ETCDCTL_API=3etcdctl --endpoints=https://11.0.1.111:2379--cacert="/opt/KUIN00601/ca.crt" --cert="/opt/KUIN00601/etcd-client.crt" --key="/opt/KUIN00601/etcd-client.key" snapshot restore /data/backup/etcd-snapshot-previous.db

```

#### 16. 排查集群中的故障节点
```shell
kubectl config use-context wk8s

# 检查哪个node有问题
kubectl get nodes

ssh node02
sudo -i

# 查看kubelet日志，会发现没有启动
systemctl status kubelet

# 启动kubelet并设置为开机服务
systemctl start kubelet
systemctl enable kubelet

# 退出root，返回cadidate@node02
exit
# 退出node02，返回candidate@node01
exit
```

#### 17. 节点维护
```shell
kubectl config use-context ek8s

kubectl get nodes

kubectl cordon node02
kubect get nodes

kubectl drain node02 --ignore-daemonsets
# 加上 --delete-emptydir-data --force 强制将node上的pod删除
```
