## 1. kube-bench 修复不安全项
参考文档：[依次点击：Tasks -> Run Jobs -> Running Automated Tasks with a CronJob](https://kubernetes.io/docs/reference/config-api/kubelet-config.v1beta1/)

```shell
kubectl config use-context KSCS00201

# 1. 切换到 Master 的 root 下
ssh master01
sudo -i

# sh kube-bench.sh # 模拟

# 2. 修改 api-server

# 3. 修改 kubelet

# 修复
# 检查 kubelet 配置文件位置。
systemctl status kubelet

# cat /etc/systemd/system/kubelet.service.d/10-kubeadm.conf 中也会看到 Environment="KUBELET_CONFIG_ARGS=--config=/var/lib/kubelet/config.yaml"。
# 所以去修改这个文件
# 修改之前，备份一下配置文件。
# 千万不要在/etc/kubernetes/下备份，可能会导致异常，可以备份到/tmp 目录下。
cp /var/lib/kubelet/config.yaml /tmp
vim /var/lib/kubelet/config.yaml

#修改
```

![](../images/certificates/cks/1-1.png)

```shell
# 可以使用这条命令查。可以不查的，直接按照考试题目里的要求做就行。
kube-bench
```
![](../images/certificates/cks/1-2.png)

## 2. Pod 指定 ServiceAccount
参考文档：[ServiceAccount](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

```shell
kubectl config use-context KSCH0030

# 1. 创建一个 ServiceAccount
vim qa-ns.yaml
# 根据参考文档修改如下
```
![](../images/certificates/cks/2-1.png)

```shell
kubectl apply -f qa-ns.yaml
kubectl get sa -n qa

# 2. 修改已存在的文件，创建一个 Pod使用该 ServiceAccount
vim /cks/sa/pod1.yaml
```
![](../images/certificates/cks/2-2.png)

```shell
kubectl apply -f /cks/sa/pod1.yaml
kubectl get pod -n qa

# 3. 删除没有使用的 ServiceAccount
# 查看所有sa
kubectl get sa -n qa
# 查看已经使用sa，例如default和backend-sa已经使用
kubectl get pod -n qa -o yaml | grep -i serviceAccountName
# 删除没有使用的sa
kubectl delete sa test01 -n qa
```

# 3. 默认的NetworkPolicy
参考文档：[NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

```shell
kubectl config use-context KSCS00101

# 可能是ingress或egress或both
vim /cks/net/p1.yaml
```
![](../images/certificates/cks/3-1.png)

```shell
kubectl apply -f /cks/net/p1.yaml

# 检查
kubectl describe networkpolicy denypolicy -n testing
```

# 4. RBAC - RoleBinding
参考文档：[RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterole)

```shell
kubectl config use-context KSCH00201

# 查看 ServiceAccount service-account-web 对应的 rolebindings role-1-binding
# 查看 rolebindings role-1-binding 对应的 role 为 role-1
kubectl describe rolebindings -n db

# 编辑 role-1 权限：
kubectl edit role role-1 -n db
```
![](../images/certificates/cks/4-1.png)

```shell
# 检查
kubectl describe role role-1 -n db

# 在 db 命名空间，创建名为 role-2 的 role，并且通过 rolebinding 绑定 service-account-web，只允许对 namespaces 做 delete 操作。
# 记住 --verb 是权限，可能考 delete 或者 update 等 --resource 是对象，可能考 namespaces 或者 persistentvolumeclaims 等。
kubectl create role role-2 --verb=delete --resource=namespaces -n db
kubectl create rolebinding role-2-binding --role=role-2 --serviceaccount=db:service-account-web -n db

# 检查
kubectl describe rolebindings -n db
```

# 5. 日志审计 log audit
参考文档：[Auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

```shell
kubectl config use-context KSCH00601

# 1. 切换到Master的root下
ssh master01
sudo -i

# 2. 配置审计策略
# 先备份配置文件
# 千万不要在/etc/kubernetes/下备份，可能会导致异常，可以备份到/tmp 目录下。
cp /etc/kubernetes/logpolicy/sample-policy.yaml /tmp
vim /etc/kubernetes/logpolicy/sample-policy.yaml
```
![](../images/certificates/cks/5-1.png)

```shell
# 3. 配置master节点的kube-apiserver.yaml
cp /etc/kubernetes/manifests/kube-apiserver.yaml /tmp
vim /etc/kubernetes/manifests/kube-apiserver.yaml

# 等待kube-apiserver自动重启，且恢复正常
# 配置完后保存，当 kube-apiserver.yaml 文件内容有变化时，kube-apiserver 会自动重启。
# 等待 2 分钟后，再检查
kubectl get pod -A
tail /var/log/kubernetes/audit-logs.txt

# (Optional)如果等了 3 分钟，kubectl get pod -A 还是报错，可以重启一下 kubelete 服务
systemctl daemon-reload
systemctl restart kubelet


# 退出 root，退回到 candidate@master01
exit
# 退出 master01，退回到 candidate@node01
exit

```

# 6. 创建Secret


# 7. Dockerfile 检测
