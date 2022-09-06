## Helm

### Install 
~~~
helm install elastic elastic/elasticsearch -f es-value.yaml -n logging
~~~

~~~
helm install kibana elastic/kibana -f kibana-value.yaml -n logging
~~~

~~~
fluent-bit-service-account.yaml
fluent-bit-role.yaml
fluent-bit-role-binding.yaml
fluent-bit-configmap.yaml
fluent-bit-ds.yaml
~~~

### Version 

### Update 

### Elastic Stack 

### Chart

### Delete
~~~
$ helm delete ~
~~~
