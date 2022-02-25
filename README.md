# What is it?

This repository contains the necessary yaml files to set up elasticsearch on kubernetes. There are 3 pods. Data, master and client. Yaml files are run via kubectl. Additionally elasticsearch supports authentication in this example.

Elasticsearch version: 7.17.0

## Setup

Pull the repository files:

```
git clone https://github.com/koraykutanoglu/kubernetes-elasticsearch
```

Go to directory:

```
cd kubernetes-elasticsearch
```

Go to directory:

```
cd elasticsearch
```

Create new a namespaces:

```
kubectl create namespaces logging
```

Run all yaml files in one go:

```
kubectl apply -f .
```

Generate a elasticsearch 9200 port sign user and password:

```
kubectl exec -it $(kubectl get pods -n logging | grep elasticsearch-client | sed -n 1p | awk '{print $1}') -n logging -- bin/elasticsearch-setup-passwords auto -b
```

Enter the password you obtained in the previous command here and store it as a secrets value in kubernetes.

```
kubectl create secret generic elasticsearch-pw-elastic -n logging --from-literal password=zxQlD3k6NHHK22rPIJK1
```
