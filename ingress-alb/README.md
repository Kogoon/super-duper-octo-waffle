## Helm

### Install 
~~~
helm install elastic elastic/elasticsearch -f es-value.yaml -n logging
~~~

~~~
helm install kibana elastic/kibana -f kibana-value.yaml -n logging
~~~

~~~
kubectl create namespace logging
kubectl apply -f fluent-bit-service-account.yaml
kubectl apply -f fluent-bit-role.yaml
kubectl apply -f fluent-bit-role-binding.yaml
kubectl apply -f output/elasticsearch/fluent-bit-configmap.yaml
kubectl apply -f output/elasticsearch/fluent-bit-ds.yaml
~~~

### Key Encoding
~~~
echo -n 'AWS_ACCESS_KEY_ID값' | base64
echo -n 'AWS_SECRET_ACCESS_KEY값' | base64
~~~

### OIDC 공급자
~~~
eksctl utils associate-iam-oidc-provider --cluster MY-EKS-CLUSTER --approve
~~~

### Policy
~~~
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.3.1/docs/install/iam_policy.json
aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document ./iam_policy.json
~~~

** ARN **

### iamserviceaccount
~~~
eksctl create iamserviceaccount \
 --cluster=MY-EKS-CLUSTER \
 --namespace=kube-system \
 --name=aws-load-balancer-controller \
 --attach-policy-arn=arn:aws:iam::709861978753:policy/AWSLoadBalancerControllerIAMPolicy \
 --override-existing-serviceaccounts \
 --approve
~~~

### Cert Manager
~~~
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.9.1/cert-manager.yaml
~~~

~~~
kubernetes.io/cluster/MY-EKS-CLUSTER-2 = shared 
kubernetes.io/role/internal-elb = 1 # internal
kubernetes.io/role/elb = 1  # internet-facing
~~~

### ALB Controller
~~~
wget https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.3/v2_4_3_full.yaml
~~~

~~~
    - --cluster-name=eks # Your cluster name
    - --ingress-class=alb   # ingress에 사용할 loadbalancer 정의 
    - --aws-vpc-id=vpc-0c78bbfadc749caab  # Your VPC ID
    - --aws-region=ap-northeast-2   # Your Region
~~~

~~~
kubectl apply -f v2_4_3_full.yaml
~~~

~~~
kubectl get deploy -n kube-system
kubectl get po -n kube-system
~~~

* ingress

~~~
kubectl apply -f ingress.yaml
~~~

### AWS
~~~
helm repo add eks https://aws.github.io/eks-charts
~~~

### Update 
~~~
helm repo update
~~~

#### Result 
~~~
[ec2-user@my-workspace workspace]$ helm repo add eks https://aws.github.io/eks-charts
"eks" has been added to your repositories
[ec2-user@my-workspace workspace]$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "eks" chart repository
...Successfully got an update from the "elastic" chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈Happy Helming!⎈
~~~

### ALB Controller 
~~~
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
 -n kube-system \
 --set clusterName=MY-EKS-CLUSTER-2 \
 --set serviceAccount.create=false \
 --set serviceAccount.name=aws-load-balancer-controller \
 --set image.repository=602401143452.dkr.ecr.ap-northeast-2.amazonaws.com/amazon/aws-load-balancer-controller \
 --set region=ap.northeast-2 \
 --set vpcid=vpc-01f60ca63c730c225
~~~

* check alb controller 
~~~
kubectl get deployment -n kube-system aws-load-balancer-controller
~~~

### Elastic Stack 
~~~
~~~

### Chart
~~~
~~~

### Delete
~~~
$ helm delete ~
~~~
