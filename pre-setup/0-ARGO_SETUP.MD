#Argo setup

** Read the instruction in README before executing the insturction**

**Install ARGO cd**

- kubectl create namespace argocd
- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

**Install ARGO CD Notification**

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj-labs/argocd-notifications/stable/manifests/install.yaml

**Expose ArgoCD**

- *Homelab/Katakoda - NodePort*
  - kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}' && kubectl get svc argocd-server -n argocd
  - kubectl port-forward svc/argocd-server -n argocd 8080:443 
  - kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
  - argocd login --insecure localhost:8080

- *Public Cloud platform, LoadBalancer based*
   - kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}' && kubectl get svc argocd-server -n argocd
   - kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
   - argocd login --insecure <IP_ADDRESS>

**Login and change ArgoCD password**
- Based on the type of service, the argocd is either exposed on NodePort and Localhost:8080 OR LoadBalancer
- Logon to the argocd portal or CLI using username as _admin_ and intial password is _the pod name of the argocd server_
- To change the password issue the command  _argocd account update-password_

**ARGO CLI on workstation to connect**
- VERSION=$(curl --silent "https://api.github.com/repos/argoproj/argo-cd/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/' | sed 's/[^"]*"\([^"]*\)".*/\1/')
- curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/$VERSION/argocd-linux-amd64
- chmod +x /usr/local/bin/argocd

**ARGO ROLLOUTS**

- kubectl create namespace argo-rollouts
- kubectl apply -n argo-rollouts -f https://raw.githubusercontent.com/argoproj/argo-rollouts/stable/manifests/install.yaml
