# odoo-argocd
scripts for ArgoCd to run k8s manifests on Google Cloud Platform  from repository
 https://github.com/kacpi52/odoo-gitops

### how to run it
kubectl apply -f applications/bm-staging.yaml

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

kubectl port-forward service/argocd-server -n argocd 8080:443