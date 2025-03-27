# dify-chart

这是一个根据 `Dify` 开源工程 `docker` 目录下 `docker-compose.yaml` 文件和 `.env` 文件，转换成的 `Helm YAML` 部署脚本，完成了 `Dify` 高可用部署的基础结构，可以在这基础上修改更复杂的部署结构。

## Kubernetes

本例中，依赖 `Docker` 和 `minikube` 最为演示服务，确保你安装了它们。

## 服务依赖

本例中，`Dify` 的依赖，如：DB、Redis、Weaviate，都改了外联，但不涉及这些服务的高可用部署，需要可以参考它们的官网部署高可用集群。

一开始，可以参考工程中的 `demo-dependent-docker.txt` 文件中的命令建立这些服务的单例，也可以部署高可用集群后，修改 `values.yaml` 中的相关配置。

## 部署工程

执行下列命令部署：

```
git clone https://github.com/flower-trees/dify-chart.git
cd dify-chart
helm install dify ./ --namespace dify
kubectl get pods -n dify
```

确保服务都已正常启动

```
dify-api-5c446f5dbf-r674x            1/1     Running   0               103m
dify-api-5c446f5dbf-rxjw4            1/1     Running   0               103m
dify-plugin-daemon-667b754cf-755zg   1/1     Running   0               70m
dify-plugin-daemon-667b754cf-sl7zm   1/1     Running   1 (3h54m ago)   20h
dify-sandbox-9769bb9ff-dxcnm         1/1     Running   0               70m
dify-sandbox-9769bb9ff-ml5lc         1/1     Running   1 (3h54m ago)   5h6m
dify-ssrf-proxy-b966c4bfb-m4c6q      1/1     Running   0               70m
dify-ssrf-proxy-b966c4bfb-ptbbh      1/1     Running   1 (3h54m ago)   5h6m
dify-web-5d844944df-nq7d9            1/1     Running   0               145m
dify-web-5d844944df-qrrdn            1/1     Running   0               70m
dify-worker-7d9f77566-gxdjn          1/1     Running   0               91m
dify-worker-7d9f77566-pcmcq          1/1     Running   0               91m
```

## 访问

确保你的 `Kubernetes` 服务外部可以访问，如果是 `minikube`，可以使用 `minikube tunnel`。

在 `/etc/hosts` 中配置域名 `127.0.0.1 dify.local`

访问链接：`http://dify.local/install`

## 配置修改

本例中，基本兼容 `Dify` 中 `.env` 文件配置，可以参考 `Dify` 文档进行升级。



