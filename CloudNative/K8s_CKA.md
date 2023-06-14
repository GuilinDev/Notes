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

## Application Lifecycle Management

## Cluster Maintaince

## Security

## Storage

## Networking

## Others


## Questions
### 1. Role-based Access Control (RBAC)
```bash
# Task:为部署流水线创建一个新的ClusterRole并将其绑定到范围为特定的namespace 的特定ServiceAccount。
# Task:
# 创建一个名为deployment-clusterrole且仅允许创建以下资源类型的新ClusterRole：
# Deployment, StatefulSet, DaemonSet
#
# 在现有的namespace app-team1中, 创建一个名为cicd-token的新ServiceAccount。
# 限于namespace app-team1中，将新的ClusterRole deployment-clusterrole绑定到新的ServiceAccount cicd-token上。

# 考点：对RBAC的理解，直接看-h，不用查文档
kubectl create clusterrole -h
kubectl create rolebinding -h

# switch to k8s context
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
kubectl label ns my-namespace purpose=production,env=dev

# 编写一个NetworkPolicy的yaml文件，从上面官网copy过来，然后修改

kubectl apply -f network-policy.yaml

# 验证 (optional)
kubectl describe neworkpolicy -n my-app

```

#### 4. Expose Service
参考文档： [依次点击Concepts→Workloads→Workload Resources→Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
```bash
kubectl config use-context k8s



```

#### 5. 创建Ingress
```shell
kubectl config use-context k8s

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
```shell
kubectl config use-context k8s

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
```

#### 10. 创建PV
```shell
kubectl config use-context k8s

```

#### 11. 创建PVC
```shell
kubectl config use-context k8s

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

# 修改官方文档的yaml
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
