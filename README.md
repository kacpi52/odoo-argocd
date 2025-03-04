# odoo-argocd
scripts for ArgoCd to run k8s manifests on Google Cloud Platform  from repository

 https://github.com/kacpi52/odoo-gitops

### how to run it
##### install ArgoCD on your cluster

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```
##### then check the installation 

```
kubectl get all -n argocd
```

##### then apply odoo app configuration 

```
kubectl apply -f applications/odoo-main.yml
```

##### then you need to get ArgoCD admin password

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

##### and forward port to your localhost:8080

```
kubectl port-forward service/argocd-server -n argocd 8080:443
```

##### then you can reach ArgoCD gui
![ArgoCD gui](images/argocd_odoo.jpg)

### dont forget to cleanup

```
kubectl delete -f applications/odoo-main.yml
kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```

#### Section Notes and Resources
This project contains open source Odoo app image (https://github.com/odoo/odoo). 