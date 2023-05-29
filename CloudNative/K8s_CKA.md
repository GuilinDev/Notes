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
```bash
# Task:
# 在现有的namespacemy-app中创建一个名为allow-port-from-namespace的新NetworkPolicy。确保新的NetworkPolicy允许namespaceecho中的Pods连接到namespacemy-app中的Pods的9000端口。进一步确保新的NetworkPolicy：不允许对没有在监听端口9000的Pods的访问, 不允许非来自namespaceecho中的Pods的访问
# 双重否定就是肯定，所以最后两句话的意思就是：仅允许端口为9000的pod方法。仅允许echo命名空间中的pod访问

# 考点： NetworkPolicy的创建

kubectl config use-context k8s

# 参考： https://kubernetes.io/docs/concepts/services-networking/network-policies/

# 查看所有ns标签的label
kubectl get ns --show-labels



```

