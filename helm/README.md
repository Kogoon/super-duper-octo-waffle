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

### Update 

### Elastic Stack 

### Chart

### Delete
~~~
$ helm delete ~
~~~
