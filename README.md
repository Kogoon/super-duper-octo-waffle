# super-duper-octo-waffle
Final Project - kubernetes - Prometheus &amp; Grafana


### memo

 - 4 worker node?



### EKSCTL 

* Create Cluster
``` bash 
$ eksctl create cluster --name EKS-CLUSTER --region ap-northeast-2 --version 1.21 --vpc-public-subnets subnet-0e9e29515e373ce74,subnet-089ed26e00e4bb312 --without-nodegroup
```

* Create NodeGroup
``` bash
$ eksctl create nodegroup \
  --cluster EKS-CLUSTER \
  --region ap-northeast-2 \
  --name NODEGROUP \
  --node-type t2.micro \
  --nodes 4 \
  --nodes-min 4 \
  --nodes-max 8 \
  --ssh-access \
  --ssh-public-key my-key
```

* Delete Cluster 
``` bash
$ eksctl delete cluster EKS-CLUSTER --region ap-northeast-2
```