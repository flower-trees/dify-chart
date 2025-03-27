
# dify-chart

This is a Helm YAML deployment script converted from the `docker-compose.yaml` and `.env` files under the `docker` directory of the open-source `Dify` project. It sets up the basic infrastructure for a high-availability deployment of `Dify`, and can be further customized to support more complex deployment architectures.

## Kubernetes

In this example, `Docker` and `minikube` are used as demonstration environments. Make sure both are installed on your system.

## Service Dependencies

In this example, Dify's dependencies such as the database, Redis, and Weaviate are externally connected. However, high availability deployment for these services is not included. You may refer to their official documentation to set up high-availability clusters.

Initially, you can use the commands listed in the `demo-dependent-docker.txt` file to deploy single instances of these services, or configure a high-availability cluster and update the relevant settings in the `values.yaml` file.

## Deploying the Project

Run the following commands to deploy:

```
git clone https://github.com/flower-trees/dify-chart.git
cd dify-chart
helm install dify ./ --namespace dify
kubectl get pods -n dify
```

Ensure that all services are running properly:

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

## Access

Ensure your Kubernetes services are accessible externally. If you're using `minikube`, you can enable access using:

```
minikube tunnel
```

Add the following entry to your `/etc/hosts` file:

```
127.0.0.1 dify.local
```

Then visit the installation page:

```
http://dify.local/install
```

## Configuration Modifications

This example is largely compatible with the configuration found in Dify’s `.env` file. Refer to the official Dify documentation for further customization and upgrades.
