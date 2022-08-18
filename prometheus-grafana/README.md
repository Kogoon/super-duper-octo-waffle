## Prometheus & Grafana

* Namespace 생성
~~~
$kubectl create namespace monitoring
~~~

설치 순서(`kubectl apply -f`) - `prometheus-*` -> `kube-*` -> `grafana.yaml`

* `./prometheus-cluster-role.yaml`


* `./prometheus-config-map.yaml`


* `./prometheus-deployment.yaml`
   - `kube-state*`가 저장하고 있는 정보를 가져오는 기능
   
   
* `./prometheus-node-exporter.yaml`
   - (프로메테우스는 쿠버네티스만 관리하기 위한 도구는 아니다.) 
   - daemonset으로 구성되어 있음. 
   
* `./prometheus-svc.yaml`


* `./kube-state-cluster-role.yaml`


* `./kube-state-deployment.yaml`


* `./kube-state-svcaccount.yaml`


* `./kube-state-svc.yaml`


* `./grafana.yaml`
   - 마지막으로 `kubectl apply`


``` bash
kubectl get pods --all-namespaces
```