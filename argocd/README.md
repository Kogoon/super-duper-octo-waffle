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