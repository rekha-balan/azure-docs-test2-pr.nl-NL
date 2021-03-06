---
title: Azure Container Service tutorial - Deploy Cluster
description: Azure Container Service tutorial - Deploy Cluster
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8403e5d8dd3bad07e412b08709dcb8c28201bcdf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870386"
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Deploy a Kubernetes cluster in Azure Container Service

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

Kubernetes provides a distributed platform for containerized applications. With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick. In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed. Steps completed include:

> [!div class="checklist"]
> * Deploying a Kubernetes ACS cluster
> * Installation of the Kubernetes CLI (kubectl)
> * Configuration of kubectl

In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Log Analytics is configured to monitor the Kubernetes cluster.

## <a name="before-you-begin"></a>Before you begin

In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance. If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Create Kubernetes cluster

Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command. 

The following example creates a cluster named `myK8sCluster` in a Resource Group named `myResourceGroup`. This Resource Group was created in the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md).

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8SCluster --generate-ssh-keys 
```

In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources. If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command. 

After several minutes, the deployment completes, and returns json formatted information about the ACS deployment.

## <a name="install-the-kubectl-cli"></a>Install the kubectl CLI

To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client. 

If you're using Azure CloudShell, kubectl is already installed. If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.

If running in Linux or macOS, you may need to run with sudo. On Windows, ensure your shell has been run as administrator.

```azurecli-interactive 
az acs kubernetes install-cli 
```

On Windows, the default installation is *c:\program files (x86)\kubectl.exe*. You may need to add this file to the Windows path. 

## <a name="connect-with-kubectl"></a>Connect with kubectl

To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group myResourceGroup --name myK8SCluster
```

To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.

```azurecli-interactive
kubectl get nodes
```

Output:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

At tutorial completion, you have an ACS Kubernetes cluster ready for workloads. In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.

## <a name="next-steps"></a>Next steps

In this tutorial, an Azure Container Service Kubernetes cluster was deployed. The following steps were completed:

> [!div class="checklist"]
> * Deployed a Kubernetes ACS cluster
> * Installed the Kubernetes CLI (kubectl)
> * Configured kubectl

Advance to the next tutorial to learn about running application on the cluster.

> [!div class="nextstepaction"]
> [Deploy application in Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
