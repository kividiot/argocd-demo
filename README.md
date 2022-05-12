# Getting Started with ArgoCD
**Author/Maintainer:** Amil Khan

![ArgoCD](https://argo-cd.readthedocs.io/en/stable/assets/argocd-ui.gif)

## Background

After moving BisQue to full K8s, I started using ArgoCD for BisQue as our Continuous Deployment system and was immediately blown away by the ease of use. I was forced to be more organized and structured with my GitHub commits, which resulted in more stable releases. My previous experience with the Argo team was with Argo Workflows loved that too so now BisQue's entire module execution engine is powered by Argo Workflows.


## Choosing an Installation

ArgoCD offers two types of installation methods

  - **Quickstart** Mainly for trying out ArgoCD, small to large projects would see an immediate use case, in my opinion.
  - **Production HA** The route to go for production

---
**NOTE:** I am assuming you have `kubectl` installed and you know the location of your `KUBECONFIG` file.

  - [x] `kubectl` CLI Installed
  - [x] `KUBECONFIG` (default location is `~/.kube/config`).
---


### Quickstart

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Creates `argocd` namespace and installs Argo CD application.


#### Access UI 

**Option 1** Port-Forwarding

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
If you are using a remote machine, remember to set the `--address` flag.

_Example_

kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 128.112.93.8

**Option 2** Service Type Load Balancer

```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
