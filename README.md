# SREK8gitops

** This repo is the IaC which deploys SRE tools and applications for Chaos engineering and self healing demo**
**Pre-requisite**
* K8s Cluster
* Ingress router [for DevOps application ngix router will be used]
* DNS address to point traffic via istio-ingress and nginx-ingress

**Installation instruction** 
1. All source files for installation listed in "pre-setup" directory.
2. Install argocd, argorollout and cli using the commands listed in 0-argo_setup.txt.
3. Configure the DNS to access the argocd over the internet.
4. Using kubectl command create namespaces.
5. login to argocd using cli and also logon to argocd UI.
6. run the file 2-istio-setup.yaml  to deploy istio configuration 
7. Frist sync istio-init helm chart first. Up on successful completion, sync the istio-config helm later.
8. execute the file 3-devopstools-setup.yaml to deploy jenkins,sonarqube and harbor to devopstools namespace
9. CI pipeline can build containers and push it to docker repository
10. Deploy argo example application to experience the gitops using argocd using 4-argoapps-demo.yaml
11. Deploy istio example application to experience the gitops using argocd using 5-istioapps-demo.yaml
