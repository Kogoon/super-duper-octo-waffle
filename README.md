# super-duper-octo-waffle
Final Project - kubernetes - Prometheus &amp; Grafana


### Kustomization usage

``` bash
kubectl apply -k <kustomization_directory>
```


### METRIC SERVER

``` bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.1/components.yaml
```


### EKSCTL 

* Create Cluster
``` bash 
$ eksctl create cluster --name EKS-CLUSTER --region ap-northeast-2 --version 1.21 --vpc-public-subnets subnet-05ad9b35153354dbc,subnet-0ab239ec58982fb8c --without-nodegroup
$ eksctl create cluster --name EKS-CLUSTER --region ap-northeast-2 --version 1.21 --without-nodegroup
```

* Create NodeGroup
``` bash
$ eksctl create nodegroup \
  --cluster EKS-CLUSTER \
  --region ap-northeast-2 \
  --name NODEGROUP \
  --node-type t3.small \
  --nodes 2 \
  --nodes-min 2 \
  --nodes-max 4 \
  --ssh-access \
  --ssh-public-key my-key \
  --managed
```

* Create Cluster & NodeGroup
```bash
$ eksctl create cluster --name MY-EKS-CLUSTER --version 1.21 --region ap-northeast-2 --nodegroup-name MY-NODEGROUP --node-type t3.medium --nodes 2 --nodes-min 2 --nodes-max 2 --ssh-access --ssh-public-key my-key --managed
```

* `--managed`   : 
* `--unmanaged` : 

* Delete NodeGroup
``` bash
eksctl delete nodegroup --cluster=MY-EKS-CLUSTER --name=MY-NODEGROUP
```

* Delete Cluster 
``` bash
$ eksctl delete cluster MY-EKS-CLUSTER --region ap-northeast-2
```

### Maximum number of pods (cpu/memory)
* t2.micro  = 4  (1/1)    $ 0.0144/h
* t3.micro  = 4  (2/1)    $ 0.0130/h
* t2.small  = 11 (1/2)    $ 0.0288/h
* t3.small  = 11 (2/2)    $ 0.0260/h -> 2022-08-24 실습 채택 -> Eviction
* t3.medium = 17 (2/4)    $ 0.0520/h -> 2022-08-24 실습 채택2 -> 2022-08-24 성공 -> 2022-08-25 2개 도전
* t3.large  = 35 (2/8)    $ 0.1040/h
* c4.large  = 29 (2/3.75) $ 0.1140/h 
* c4.xlarge = 58 (4/7.5)  $ 0.2270/h


## docker's exec
``` bash
kubectl exec --stdin --tty shell-demo -- /bin/bash
kubectl exec -i -t my-pod --container main-app -- /bin/bash
```

* nginx test
```
echo "Hello" > /usr/share/nginx/html/index.html
```


## K8S env
``` bash
kubectl exec my-nginx-3800858182-e9ihh -- printenv | grep SERVICE
```