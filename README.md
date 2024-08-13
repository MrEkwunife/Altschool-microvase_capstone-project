<h3 text-align='center'> Microservices-Based Application Deployment on Kubernetes <h3>
This repository contains the Infrastructure as Code (IaaC) setup for deploying a microservices-based architecture application on Kubernetes. The application is based on the Socks Shop microservice application from [microservices repository](https://github.com/microservices-demo/microservices-demo.git).

<h2 text-align='center'> Setup Details <h2>
1. Provisioning Infrastructure
The infrastructure is provisioned on AWS using Amazon Elastic Kubernetes Service (EKS). The setup includes creating the necessary AWS resources for Kubernetes cluster provisioning.

2. Kubernetes Configuration
Kubernetes configuration files are provided in the infrastructure folder. These files define the Kubernetes resources required to deploy the microservices application. The configuration includes deployment manifests, service definitions, and any other necessary Kubernetes resources.

3. Continuous Integration and Continuous Deployment (CI/CD)
Continuous Integration and Continuous Deployment (CI/CD) pipelines are set up for automated testing, building, and deploying the application. The CI/CD pipeline utilizes GitOps principles and ArgoCD for managing deployments. The deployment workflow is triggered automatically upon changes to the repository.

<h4 text-align='center'> Prerequisites <h4>
To deploy the microservices application using this setup, ensure you have the following prerequisites installed:

1. AWS CLI
2. kubectl
3. Terraform
4. ArgoCD
5. GitOps action
6. 
![CI/CD with GitOps](/images/image-401-1024x421.png)


 <h4 text-align='center'> Directory Structure <h4>
infrastructure
|       |-- main.tf
|       |-- variables.tf
|       |-- terraform.tf
|       |-- LICENSE
|       |-- .terraform.lock.hcl
|       |-- .gitignore

|-- manifest-logging
|       |-- elasticsearch.yml
|       |-- elasticsearch.yml
|       |-- fluentd-cr.yml
|       |-- fluuentd.daemon.yml
|       |-- fluentd-sa.yaml
|       |-- kibana.yml

|-- manifest-monitoring
|       |-- monitoring-ns.yaml
|       |-- prometheus-sa.yaml
|       |-- prometheus-cr.yaml
|       |-- prometheus-crb.yaml
|       |-- prometheus-configmap.yaml
|       |-- prometheus-alertrules.yaml
|       |-- prometheus-dep.yaml
|       |-- prometheus-svc.yaml
|       |-- prometheus-exporter-disk-usage-ds.yaml
|       |-- kube-state-sa.yaml
|       |-- kube-state-cr.yaml
|       |-- kube-state-crb.yaml
|       |-- kube-state-dep.yaml
|       |-- kube-state-svc.yaml
|       |-- grafana-configmap.yaml
|       |-- grafana-dep.yaml
|       |-- grafana-svc.yaml
|       |-- grafana-import-dash-batch.yaml
|       |-- prometheus-node-exporter-sa.yaml
|       |-- prometheus-node-exporter-daemonset.yaml
|       |-- prometheus-node-exporter-svc.yaml

Getting Started
Follow these steps to deploy the microservices application:

Clone this repository:
```
git clone https://github.com/microservices-demo/microservices-demo.git
cd infrastructure
terraform init
terraform apply

```
The CLI output is given as:

![after terraform apply](/images/after_terraform_apply.PNG)

Then the Elastic Kubernetes Cluster (EKS) on the AWS console CLI is created:

![AWS console](/images/aws-console.PNG)

The kubectl nodes are obtained:

![get nodes](/images/kubectl_get_node.PNG)


Installing ArgoCD
```

 kubectl create namespace argocd
 kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
 
```

![installing ArgoCD](/images/installing_agroCD.PNG)

```
kubectl get pods -n argocd
 
```
![getting nodes](/images/kubectl_get_node.PNG)

Port forwarding to allow for the ArgoCD CLI

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
 
```

![port forwarding for Argo interface](/images/port_forwarding_forArgoCLI_display.PNG)


![AgroCLI interface](/images/agrocd-interface.PNG)


Signing into Argo CLI on powershell: This must be done on powershell while ran as an Administrator

![signing in ArgoCli](/images/signing_into_ArgoCli.PNG)


![argocli-login](/images/agrocd_logged-in.PNG)


Synchronizing the sock-shop on ArgoCLI

![sync_sock-shop](/images/sync_sock-shop.PNG)

![sync_sock-shop](/images/deployed_sockshop_on_argocd.PNG)

Deploying Sock-Shop

![connecting_pods](/images/connecting_pods.PNG)


![Deployed Sock-Shop](/images/deplpoyed_sock_app.PNG)

<h4 text-align='center'> Destroy the infrastructure using Terraform /<h4>

```
terraform destroy
 
```
