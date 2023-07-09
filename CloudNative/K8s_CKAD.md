## Core Concepts

## Configuration

## Multi-container Pods

## Obervability

## POD Design

## Services and Networking

## State Persistance

## Others

## 1. CronJob - 1
参考文档1：[依次点击：Tasks -> Run Jobs -> Running Automated Tasks with a CronJob](https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/)\

参考文档2：[依次点击：Concepts -> Workloads -> Workload Resources -> Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)

```shell
kubectl config use-context k8s

# 1. 创建 CronJob
vim cronjob-1.yaml
```
![](../images/certificates/ckad/1.png)
```shell
# 创建 CronJob
kubectl apply -f cronjob-1.yaml
# 检查 CronJob
kubectl get cronjob

# 2. 手动触发 CronJob
kubectl create job ppi-test --from=cronjob/ppi
# 查看这个 job
kubectl get jobs
```
## 2. CronJob - 2
参考文档1：[依次点击：Tasks -> Run Jobs -> Running Automated Tasks with a CronJob](https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/)\

参考文档2：[依次点击：Concepts -> Workloads -> Workload Resources -> Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)

```shell
kubectl config use-context k8s

# 按照题目要求，修改 yaml 文件
vim /ckad/CKAD00016/periodic.yam
```
![](../images/certificates/ckad/2.png)
```shell
# 创建 Cronjob
kubectl apply -f /ckad/CKAD00016/periodic.yaml
# 检查 Cronjob 和 job，确保至少有一个 hello-****的 job（创建后，需要等一分钟，才会执行）
kubectl get cronjobs hello
kubectl get jobs
```

## 3. Dockerfile
```shell
# kubectl config use-context k8s

docker -h

# 1. 构建镜像
cd /ckad/DF/
sudo docker build -t centos:8.2 . # 切换到 Dockerfile 文件所在的目录做，注意命令最后还有一个小数点，表示当前目录

# 检查镜像
sudo docker images | grep centos | grep 8.2

# 2. 导出新镜像 centos:8.2，并保存到/ckad/DF/centos-8.2.tar
sudo docker save centos:8.2 > /ckad/DF/centos-8.2.tar

# 检查存储的镜像
ll /ckad/DF/centos-8.2.tar
```

## 4. 限制CPU和内存 - 1
参考文档：[依次点击：Concepts -> Configuration -> Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

```shell
kubectl config use-context k8s

vim nginx-resources.yaml
```
![](../images/certificates/ckad/4.png)
```shell
kubectl apply -f nginx-resources.yaml
``

## 5. 限制CPU和内存 - 2
参考文档：[依次点击：Concepts -> Configuration -> Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

```shell
kubectl config use-context k8s

# 先查看 namespace haddock 的 LimitRange 详情（这个查询命令，要背过）
kubectl describe ns haddock
# 或者使用下面两条命令查看详情
kubectl -n haddock get limitrange
kubectl -n haddock get limitrange xxxxxxxxx -o yaml
# 可见 namespace haddock 设置的最大内存为 40Mi，一半就是 20Mi。（注意，是看 Max，不是看 Min。)

# 方法 1：直接在线修改
kubectl -n haddock edit deployments.apps nosql
```
![](../images/certificates/ckad/5-1.png)
```shell
# 检查一下，确保修改成功了。
kubectl -n haddock describe deployment nosql

# 方法 2：使用 yaml 文件，重新创建

# 修改 Deployment nosql 的内存限制，先删除原来的。
# 备份一下文件，防止改错了。
cp /ckad/chief-cardinal/nosql.yaml nosql.yaml-bak
# 删除原先的 deployment
kubectl delete -f /ckad/chief-cardinal/nosql.yaml
# 或者
kubectl -n haddock delete deployments.apps nosql
vim /ckad/chief-cardinal/nosql.yaml
```
![](../images/certificates/ckad/5-2.png)
```shell
# 重新创建
kubectl apply -f /ckad/chief-cardinal/nosql.yaml
# 检查一下，确保修改成功了。
kubectl -n haddock describe deployment nosql

```

## 6. 运行旧版应用程序
```shell
kubectl config use-context k8s

kubectl explain deployment.spec
kubectl explain deployment.spec.selector

vim /ckad/credible-mite/www.yaml
```
![](../images/certificates/ckad/6.png)
```shell
# 创建
kubectl apply -f /ckad/credible-mite/www.yaml
# 检查
kubectl -n garfish get all
```

## 7. Canary金丝雀发布
```shell
kubectl config use-context k8s

kubectl scale -h

cp /ckad/goshawk/current-chipmunk-deployment.yaml bak.yaml
vim /ckad/goshawk/current-chipmunk-deployment.yam
```
![](../images/certificates/ckad/7.png)
```shell
kubectl apply -f /ckad/goshawk/current-chipmunk-deployment.yaml
# 总共 10 个 Pod，将 60%流量给当前版本 Pod，就是 current-chipmunk-deployment 扩容至 6 个 pod
kubectl scale deployment current-chipmunk-deployment --replicas=6 -n goshawk
# 将 40%流量给金丝雀版本 Pod，就是 canary-chipmunk-deployment 扩容至 4 个 pod
kubectl scale deployment canary-chipmunk-deployment --replicas=4 -n goshawk
# 注意，如果考试时，有可能考将 20%流量给金丝雀版本 Pod，那就是原先为 8 个，金丝雀为 2 个，要变通。

# 检查
kubectl get pod -n goshawk
```

## 8. 配置Container安全上下文
参考文档：[依次点击：Tasks -> Configure Pods and Contaienrs -> Configure a Security Context for a Pod or Container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

```shell
kubectl config use-context k8s

kubectl edit deployment broker-deployment -n quetzal
```
![](../images/certificates/ckad/8.png)


## 9. 创建Deployment并指定环境变量
参考文档(Optional)：[依次点击：Concepts -> Tasks -> Inject Data Into Applications -> Define Environment Variables for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)

```shell
kubectl config use-context k8s

# 下面命令背过，如果不会，就使用 kubectl -h 来帮助。
kubectl create deployment api --image=nginx:1.16 --replicas=6 -n ckad00014 --dry-run=client -o yaml > api.yaml

vim api.yaml
# 在 containers:里的 image:和 name:下添加
```
![](../images/certificates/ckad/9.png)
```shell
kubectl apply -f api.yaml
```

## 10. RBAC授权
参考文档(Optional)：[依次点击：Reference -> API Access Control -> Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

```shell
kubectl config use-context k8s

# 1、通过 logs 打印错误日志
kubectl -n gorilla get pod
kubectl -n gorilla logs honeybee-deployment-***
# 2
# 检查现有的 serviceaccount
kubectl -n gorilla get sa
# 查看 rolebinding 和 role 的绑定
kubectl -n gorilla get rolebinding
# 通过 rolebinding，查看 role 和 serviceaccount 的绑定
kubectl -n gorilla describe rolebinding
# 检查 role，寻找有 get 或 list 权限的 role
kubectl -n gorilla describe role
# 通过上面的一系列操作，检查发现，gorilla-role 符合题目的要求，它对应的 serviceaccount 是 gorilla-sa

# 3、设置 honeybee-deployment 的 serviceaccount
# （in exam，其实就是跟题目里的 namespace 相同的那个 sa 是正确的。对应这道模拟题，就是 gorilla-sa 是正确的）
kubectl -n gorilla set serviceaccount deployments honeybee-deployment gorilla-sa

# 等 2 分钟，会自动生成一个新 pod，再次检查，不报错了
kubectl -n gorilla logs honeybee-deployment-***
```

## 11. ConfigMap
参考文档：[依次点击：Concepts -> Configuration -> ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)

```shell
kubectl config use-context k8s

kubectl create configmap some-config --from-literal=key3=value4

vim nginx-configmap.yaml

#添加如下内容
apiVersion: v1
kind: Pod
metadata:
  name: nginx-configmap
spec:
  containers:
  - name: nginx-configmap
    image: nginx:stable
    volumeMounts:
    - name: config
      mountPath: "/some/path"
  volumes:
  - name: config
    configMap:
    name: some-config


kubectl apply -f nginx-configmap.yaml

# 检查
kubectl exec -it nginx-configmap -- /bin/bash
cat /some/path/key3
```

## 12. Secret
参考文档：[依次点击：Concepts -> Configuration -> Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

```shell
kubectl config use-context k8s

kubectl create secret generic another-secret --from-literal=key1=value2

vim nginx-secret.yaml
```
![](../images/certificates/ckad/12.png)
```shell
kubectl apply -f nginx-secret.yaml
```

## 13. Pod健康检查 livelinessProbe

## 14. Pod健康检查 readinessProbe

## 15. 升级与回滚

## 16. Deployment使用ServiceAccount

## 17. 更新Deployment并暴露Service

## 18. NetworkPolicy

## 19. Ingress排错 - 1

## 20. Ingress排错 - 2

## 21. Service、ConfigMap、Sidecar

## 22. Deployment修改镜像

## 23. 获取使用CPU最高的Pod

## 24. PV/PVC

## 25. Pod多容器 - sidecar

## 扩展
### 1. 资源配额 Quota
### 2. SecurityContext
### 3. Secret private Key
### 4. Jobs
