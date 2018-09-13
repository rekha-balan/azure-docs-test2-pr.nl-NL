---
title: Integrate with Azure-managed services using Open Service Broker for Azure (OSBA)
description: Integrate with Azure-managed services using Open Service Broker for Azure (OSBA)
services: container-service
author: sozercan
manager: jeconnoc
ms.service: container-service
ms.topic: overview
ms.date: 12/05/2017
ms.author: seozerca
ms.openlocfilehash: cebd98ec31ae6089c20952924c39ee240cb5d6a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869608"
---
# <a name="integrate-with-azure-managed-services-using-open-service-broker-for-azure-osba"></a><span data-ttu-id="e445b-103">Integrate with Azure-managed services using Open Service Broker for Azure (OSBA)</span><span class="sxs-lookup"><span data-stu-id="e445b-103">Integrate with Azure-managed services using Open Service Broker for Azure (OSBA)</span></span>

<span data-ttu-id="e445b-104">Together with the [Kubernetes Service Catalog][kubernetes-service-catalog], Open Service Broker for Azure (OSBA) allows developers to utilize Azure-managed services in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e445b-104">Together with the [Kubernetes Service Catalog][kubernetes-service-catalog], Open Service Broker for Azure (OSBA) allows developers to utilize Azure-managed services in Kubernetes.</span></span> <span data-ttu-id="e445b-105">This guide focuses on deploying Kubernetes Service Catalog, Open Service Broker for Azure (OSBA), and applications that use Azure-managed services using Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e445b-105">This guide focuses on deploying Kubernetes Service Catalog, Open Service Broker for Azure (OSBA), and applications that use Azure-managed services using Kubernetes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e445b-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e445b-106">Prerequisites</span></span>
* <span data-ttu-id="e445b-107">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e445b-107">An Azure subscription</span></span>

* <span data-ttu-id="e445b-108">Azure CLI: [install it locally][azure-cli-install], or use it in the [Azure Cloud Shell][azure-cloud-shell].</span><span class="sxs-lookup"><span data-stu-id="e445b-108">Azure CLI: [install it locally][azure-cli-install], or use it in the [Azure Cloud Shell][azure-cloud-shell].</span></span>

* <span data-ttu-id="e445b-109">Helm CLI 2.7+: [install it locally][helm-cli-install], or use it in the [Azure Cloud Shell][azure-cloud-shell].</span><span class="sxs-lookup"><span data-stu-id="e445b-109">Helm CLI 2.7+: [install it locally][helm-cli-install], or use it in the [Azure Cloud Shell][azure-cloud-shell].</span></span>

* <span data-ttu-id="e445b-110">Permissions to create a service principal with the Contributor role on your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e445b-110">Permissions to create a service principal with the Contributor role on your Azure subscription</span></span>

* <span data-ttu-id="e445b-111">An existing Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="e445b-111">An existing Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="e445b-112">If you need an AKS cluster, follow the [Create an AKS cluster][create-aks-cluster] quickstart.</span><span class="sxs-lookup"><span data-stu-id="e445b-112">If you need an AKS cluster, follow the [Create an AKS cluster][create-aks-cluster] quickstart.</span></span>

## <a name="install-service-catalog"></a><span data-ttu-id="e445b-113">Install Service Catalog</span><span class="sxs-lookup"><span data-stu-id="e445b-113">Install Service Catalog</span></span>

<span data-ttu-id="e445b-114">The first step is to install Service Catalog in your Kubernetes cluster using a Helm chart.</span><span class="sxs-lookup"><span data-stu-id="e445b-114">The first step is to install Service Catalog in your Kubernetes cluster using a Helm chart.</span></span> <span data-ttu-id="e445b-115">Upgrade your Tiller (Helm server) installation in your cluster with:</span><span class="sxs-lookup"><span data-stu-id="e445b-115">Upgrade your Tiller (Helm server) installation in your cluster with:</span></span>

```azurecli-interactive
helm init --upgrade
```

<span data-ttu-id="e445b-116">Now, add the Service Catalog chart to the Helm repository:</span><span class="sxs-lookup"><span data-stu-id="e445b-116">Now, add the Service Catalog chart to the Helm repository:</span></span>

```azurecli-interactive
helm repo add svc-cat https://svc-catalog-charts.storage.googleapis.com
```

<span data-ttu-id="e445b-117">Finally, install Service Catalog with the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="e445b-117">Finally, install Service Catalog with the Helm chart.</span></span> <span data-ttu-id="e445b-118">If your cluster is RBAC-enabled, run this command.</span><span class="sxs-lookup"><span data-stu-id="e445b-118">If your cluster is RBAC-enabled, run this command.</span></span>

```azurecli-interactive
helm install svc-cat/catalog --name catalog --namespace catalog --set controllerManager.healthcheck.enabled=false
```

<span data-ttu-id="e445b-119">If your cluster is not RBAC-enabled, run this command.</span><span class="sxs-lookup"><span data-stu-id="e445b-119">If your cluster is not RBAC-enabled, run this command.</span></span>

```azurecli-interactive
helm install svc-cat/catalog --name catalog --namespace catalog --set rbacEnable=false --set controllerManager.healthcheck.enabled=false
```

<span data-ttu-id="e445b-120">After the Helm chart has been run, verify that `servicecatalog` appears in the output of the following command:</span><span class="sxs-lookup"><span data-stu-id="e445b-120">After the Helm chart has been run, verify that `servicecatalog` appears in the output of the following command:</span></span>

```azurecli-interactive
kubectl get apiservice
```

<span data-ttu-id="e445b-121">For example, you should see output similar to the following (show here truncated):</span><span class="sxs-lookup"><span data-stu-id="e445b-121">For example, you should see output similar to the following (show here truncated):</span></span>

```
NAME                                 AGE
v1.                                  10m
v1.authentication.k8s.io             10m
...
v1beta1.servicecatalog.k8s.io        34s
v1beta1.storage.k8s.io               10
```

## <a name="install-open-service-broker-for-azure"></a><span data-ttu-id="e445b-122">Install Open Service Broker for Azure</span><span class="sxs-lookup"><span data-stu-id="e445b-122">Install Open Service Broker for Azure</span></span>

<span data-ttu-id="e445b-123">The next step is to install [Open Service Broker for Azure][open-service-broker-azure], which includes the catalog for the Azure-managed services.</span><span class="sxs-lookup"><span data-stu-id="e445b-123">The next step is to install [Open Service Broker for Azure][open-service-broker-azure], which includes the catalog for the Azure-managed services.</span></span> <span data-ttu-id="e445b-124">Examples of available Azure services are Azure Database for PostgreSQL, Azure Database for MySQL, and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e445b-124">Examples of available Azure services are Azure Database for PostgreSQL, Azure Database for MySQL, and Azure SQL Database.</span></span>

<span data-ttu-id="e445b-125">Start by adding the Open Service Broker for Azure Helm repository:</span><span class="sxs-lookup"><span data-stu-id="e445b-125">Start by adding the Open Service Broker for Azure Helm repository:</span></span>

```azurecli-interactive
helm repo add azure https://kubernetescharts.blob.core.windows.net/azure
```

<span data-ttu-id="e445b-126">Create a [Service Principal][create-service-principal] with the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="e445b-126">Create a [Service Principal][create-service-principal] with the following Azure CLI command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac
```

<span data-ttu-id="e445b-127">Output should be similar to the following.</span><span class="sxs-lookup"><span data-stu-id="e445b-127">Output should be similar to the following.</span></span> <span data-ttu-id="e445b-128">Take note of the `appId`, `password`, and `tenant` values, which you use in the next step.</span><span class="sxs-lookup"><span data-stu-id="e445b-128">Take note of the `appId`, `password`, and `tenant` values, which you use in the next step.</span></span>

```JSON
{
  "appId": "7248f250-0000-0000-0000-dbdeb8400d85",
  "displayName": "azure-cli-2017-10-15-02-20-15",
  "name": "http://azure-cli-2017-10-15-02-20-15",
  "password": "77851d2c-0000-0000-0000-cb3ebc97975a",
  "tenant": "72f988bf-0000-0000-0000-2d7cd011db47"
}
```

<span data-ttu-id="e445b-129">Set the following environment variables with the preceding values:</span><span class="sxs-lookup"><span data-stu-id="e445b-129">Set the following environment variables with the preceding values:</span></span>

```azurecli-interactive
AZURE_CLIENT_ID=<appId>
AZURE_CLIENT_SECRET=<password>
AZURE_TENANT_ID=<tenant>
```

<span data-ttu-id="e445b-130">Now, get your Azure subscription ID:</span><span class="sxs-lookup"><span data-stu-id="e445b-130">Now, get your Azure subscription ID:</span></span>

```azurecli-interactive
az account show --query id --output tsv
```

<span data-ttu-id="e445b-131">Again, set the following environment variable with the preceding value:</span><span class="sxs-lookup"><span data-stu-id="e445b-131">Again, set the following environment variable with the preceding value:</span></span>

```azurecli-interactive
AZURE_SUBSCRIPTION_ID=[your Azure subscription ID from above]
```

<span data-ttu-id="e445b-132">Now that you've populated these environment variables, execute the following command to install the Open Service Broker for Azure using the Helm chart:</span><span class="sxs-lookup"><span data-stu-id="e445b-132">Now that you've populated these environment variables, execute the following command to install the Open Service Broker for Azure using the Helm chart:</span></span>

```azurecli-interactive
helm install azure/open-service-broker-azure --name osba --namespace osba \
    --set azure.subscriptionId=$AZURE_SUBSCRIPTION_ID \
    --set azure.tenantId=$AZURE_TENANT_ID \
    --set azure.clientId=$AZURE_CLIENT_ID \
    --set azure.clientSecret=$AZURE_CLIENT_SECRET
```

<span data-ttu-id="e445b-133">Once the OSBA deployment is complete, install the [Service Catalog CLI][service-catalog-cli], an easy-to-use command-line interface for querying service brokers, service classes, service plans, and more.</span><span class="sxs-lookup"><span data-stu-id="e445b-133">Once the OSBA deployment is complete, install the [Service Catalog CLI][service-catalog-cli], an easy-to-use command-line interface for querying service brokers, service classes, service plans, and more.</span></span>

<span data-ttu-id="e445b-134">Execute the following commands to install the Service Catalog CLI binary:</span><span class="sxs-lookup"><span data-stu-id="e445b-134">Execute the following commands to install the Service Catalog CLI binary:</span></span>

```azurecli-interactive
curl -sLO https://servicecatalogcli.blob.core.windows.net/cli/latest/$(uname -s)/$(uname -m)/svcat
chmod +x ./svcat
```

<span data-ttu-id="e445b-135">Now, list installed service brokers:</span><span class="sxs-lookup"><span data-stu-id="e445b-135">Now, list installed service brokers:</span></span>

```azurecli-interactive
./svcat get brokers
```

<span data-ttu-id="e445b-136">You should see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="e445b-136">You should see output similar to the following:</span></span>

```
  NAME                               URL                                STATUS
+------+--------------------------------------------------------------+--------+
  osba   http://osba-open-service-broker-azure.osba.svc.cluster.local   Ready
```

<span data-ttu-id="e445b-137">Next, list the available service classes.</span><span class="sxs-lookup"><span data-stu-id="e445b-137">Next, list the available service classes.</span></span> <span data-ttu-id="e445b-138">The displayed service classes are the available Azure-managed services that can be provisioned through Open Service Broker for Azure.</span><span class="sxs-lookup"><span data-stu-id="e445b-138">The displayed service classes are the available Azure-managed services that can be provisioned through Open Service Broker for Azure.</span></span>

```azurecli-interactive
./svcat get classes
```

<span data-ttu-id="e445b-139">Finally, list all available service plans.</span><span class="sxs-lookup"><span data-stu-id="e445b-139">Finally, list all available service plans.</span></span> <span data-ttu-id="e445b-140">Service plans are the service tiers for the Azure-managed services.</span><span class="sxs-lookup"><span data-stu-id="e445b-140">Service plans are the service tiers for the Azure-managed services.</span></span> <span data-ttu-id="e445b-141">For example, for Azure Database for MySQL, plans range from `basic50` for Basic tier with 50 Database Transaction Units (DTUs), to `standard800` for Standard tier with 800 DTUs.</span><span class="sxs-lookup"><span data-stu-id="e445b-141">For example, for Azure Database for MySQL, plans range from `basic50` for Basic tier with 50 Database Transaction Units (DTUs), to `standard800` for Standard tier with 800 DTUs.</span></span>

```azurecli-interactive
./svcat get plans
```

## <a name="install-wordpress-from-helm-chart-using-azure-database-for-mysql"></a><span data-ttu-id="e445b-142">Install WordPress from Helm chart using Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="e445b-142">Install WordPress from Helm chart using Azure Database for MySQL</span></span>

<span data-ttu-id="e445b-143">In this step, you use Helm to install an updated Helm chart for WordPress.</span><span class="sxs-lookup"><span data-stu-id="e445b-143">In this step, you use Helm to install an updated Helm chart for WordPress.</span></span> <span data-ttu-id="e445b-144">The chart provisions an external Azure Database for MySQL instance that WordPress can use.</span><span class="sxs-lookup"><span data-stu-id="e445b-144">The chart provisions an external Azure Database for MySQL instance that WordPress can use.</span></span> <span data-ttu-id="e445b-145">This process can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="e445b-145">This process can take a few minutes.</span></span>

```azurecli-interactive
helm install azure/wordpress --name wordpress --namespace wordpress --set resources.requests.cpu=0
```

<span data-ttu-id="e445b-146">In order to verify the installation has provisioned the right resources, list the installed service instances and bindings:</span><span class="sxs-lookup"><span data-stu-id="e445b-146">In order to verify the installation has provisioned the right resources, list the installed service instances and bindings:</span></span>

```azurecli-interactive
./svcat get instances -n wordpress
./svcat get bindings -n wordpress
```

<span data-ttu-id="e445b-147">List installed secrets:</span><span class="sxs-lookup"><span data-stu-id="e445b-147">List installed secrets:</span></span>

```azurecli-interactive
kubectl get secrets -n wordpress -o yaml
```

## <a name="next-steps"></a><span data-ttu-id="e445b-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="e445b-148">Next steps</span></span>

<span data-ttu-id="e445b-149">By following this article, you deployed Service Catalog to an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="e445b-149">By following this article, you deployed Service Catalog to an Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="e445b-150">You used Open Service Broker for Azure to deploy a WordPress installation that uses Azure-managed services, in this case Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="e445b-150">You used Open Service Broker for Azure to deploy a WordPress installation that uses Azure-managed services, in this case Azure Database for MySQL.</span></span>

<span data-ttu-id="e445b-151">Refer to the [Azure/helm-charts][helm-charts] repository to access other updated OSBA-based Helm charts.</span><span class="sxs-lookup"><span data-stu-id="e445b-151">Refer to the [Azure/helm-charts][helm-charts] repository to access other updated OSBA-based Helm charts.</span></span> <span data-ttu-id="e445b-152">If you're interested in creating your own charts that work with OSBA, refer to [Creating a New Chart][helm-create-new-chart].</span><span class="sxs-lookup"><span data-stu-id="e445b-152">If you're interested in creating your own charts that work with OSBA, refer to [Creating a New Chart][helm-create-new-chart].</span></span>

<!-- LINKS - external -->
[helm-charts]: https://github.com/Azure/helm-charts
[helm-cli-install]: kubernetes-helm.md#install-helm-cli
[helm-create-new-chart]: https://github.com/Azure/helm-charts#creating-a-new-chart
[kubernetes-service-catalog]: https://github.com/kubernetes-incubator/service-catalog
[open-service-broker-azure]: https://github.com/Azure/open-service-broker-azure
[service-catalog-cli]: https://github.com/Azure/service-catalog-cli

<!-- LINKS - internal -->
[azure-cli-install]: /cli/azure/install-azure-cli
[azure-cloud-shell]: ../cloud-shell/overview.md
[create-aks-cluster]: ./kubernetes-walkthrough.md
[create-service-principal]: ./kubernetes-service-principal.md
