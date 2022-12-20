## Terraform 配置语法
配置文件： .tf
支持两种模式： HCL 和 JSON （以下均用HCL）

### Provider
Terraform通过provider管理基础设施，使用provider与与供应商API进行交互。每个provider都包含相关的资源(resources)和数据源(data sources)。

providers: (https://www.terraform.io/docs/providers)[https://www.terraform.io/docs/providers]

### Resource
Resource来自Provider，是Terraform中最重要的元素。每个资源块描述一个或多个基础对象，例如网络、计算实例或更高级别的组件，例如DNS记录。

资源名称必须以字母或下划线开头，并且只能包含字母、数字、下划线和连字符。
