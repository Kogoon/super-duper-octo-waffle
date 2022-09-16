## Argo CD

* [Guide](https://argo-cd.readthedocs.io/en/stable/getting_started/)


### QuickStart
~~~
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
~~~


### Access The Argo CD
#### Service Type Load Balancer
~~~
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
~~~

~~~
kubectl port-forward svc/argocd-server -n argocd 8080:443
~~~



### ArgoCD CLI Install
~~~
sudo curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo chmod +x /usr/local/bin/argocd
~~~


### Login using the CLI
> Initial Password
~~~
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
~~~


### ingress
~~~
apiVersion: getambassador.io/v2
kind: Mapping
metadata:
  name: argocd-server-ui
  namespace: argocd
spec:
  host: argocd.example.com
  prefix: /
  service: argocd-server:443
---
apiVersion: getambassador.io/v2
kind: Mapping
metadata:
  name: argocd-server-cli
  namespace: argocd
spec:
  # NOTE: the port must be ignored if you have strip_matching_host_port enabled on envoy
  host: argocd.example.com:443
  prefix: /
  service: argocd-server:80
  regex_headers:
    Content-Type: "^application/grpc.*$"
  grpc: true
~~~