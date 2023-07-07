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

## 5. 限制CPU和内存 - 2

## 6. 运行旧版应用程序

## 7. 金丝雀发布

## 8. 配置Deployment安全上下文

## 9. 创建Deployment并指定环境变量

## 10. RBAC授权

## 11. ConfigMap

## 12. Secret

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
