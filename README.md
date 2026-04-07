# go-simple-webserver

## Prerequisites

### Install Argo CD in k8s

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Install Argo CD Argo Rollouts

```bash
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://raw.githubusercontent.com/argoproj/argo-rollouts/stable/manifests/install.yaml
```

## Login with Argo CD

To interact with Argo CD we need to forward the port of the argocd-server service to localhost:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Get the password and login with the CLI:
```bash
password=$(kubectl get secret argocd-initial-admin-secret -n argocd   -o jsonpath="{.data.password}" | base64 -d && echo)
argocd login localhost:8080 --username admin --password $password
```

## Argo UI Guideline

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

To login use the following credentials: `admin/<password>`

`<password>` can be retrieved from `kubectl get secret argocd-initial-admin-secret -n argocd   -o jsonpath="{.data.password}" | base64 -d && echo`

## Create app
