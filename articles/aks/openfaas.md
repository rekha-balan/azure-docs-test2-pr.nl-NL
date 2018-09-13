---
title: Use OpenFaaS with Azure Kubernetes Service (AKS)
description: Deploy and use OpenFaaS with Azure Kubernetes Service (AKS)
services: container-service
author: justindavies
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 03/05/2018
ms.author: juda
ms.custom: mvc
ms.openlocfilehash: b5484233c7d3d32e51098baad8c22ec51df8f0d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869693"
---
# <a name="using-openfaas-on-aks"></a><span data-ttu-id="7a38e-103">Using OpenFaaS on AKS</span><span class="sxs-lookup"><span data-stu-id="7a38e-103">Using OpenFaaS on AKS</span></span>

<span data-ttu-id="7a38e-104">[OpenFaaS][open-faas] is a framework for building Serverless functions on top of containers.</span><span class="sxs-lookup"><span data-stu-id="7a38e-104">[OpenFaaS][open-faas] is a framework for building Serverless functions on top of containers.</span></span> <span data-ttu-id="7a38e-105">As an Open Source project, it has gained large-scale adoption within the community.</span><span class="sxs-lookup"><span data-stu-id="7a38e-105">As an Open Source project, it has gained large-scale adoption within the community.</span></span> <span data-ttu-id="7a38e-106">This document details installing and using OpenFaas on an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="7a38e-106">This document details installing and using OpenFaas on an Azure Kubernetes Service (AKS) cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a38e-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a38e-107">Prerequisites</span></span>

<span data-ttu-id="7a38e-108">In order to complete the steps within this article, you need the following.</span><span class="sxs-lookup"><span data-stu-id="7a38e-108">In order to complete the steps within this article, you need the following.</span></span>

* <span data-ttu-id="7a38e-109">Basic understanding of Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7a38e-109">Basic understanding of Kubernetes.</span></span>
* <span data-ttu-id="7a38e-110">An Azure Kubernetes Service (AKS) cluster and AKS credentials configured on your development system.</span><span class="sxs-lookup"><span data-stu-id="7a38e-110">An Azure Kubernetes Service (AKS) cluster and AKS credentials configured on your development system.</span></span>
* <span data-ttu-id="7a38e-111">Azure CLI installed on your development system.</span><span class="sxs-lookup"><span data-stu-id="7a38e-111">Azure CLI installed on your development system.</span></span>
* <span data-ttu-id="7a38e-112">Git command-line tools installed on your system.</span><span class="sxs-lookup"><span data-stu-id="7a38e-112">Git command-line tools installed on your system.</span></span>

## <a name="get-openfaas"></a><span data-ttu-id="7a38e-113">Get OpenFaaS</span><span class="sxs-lookup"><span data-stu-id="7a38e-113">Get OpenFaaS</span></span>

<span data-ttu-id="7a38e-114">Clone the OpenFaaS project repository to your development system.</span><span class="sxs-lookup"><span data-stu-id="7a38e-114">Clone the OpenFaaS project repository to your development system.</span></span>

```azurecli-interactive
git clone https://github.com/openfaas/faas-netes
```

<span data-ttu-id="7a38e-115">Change into the directory of the cloned repository.</span><span class="sxs-lookup"><span data-stu-id="7a38e-115">Change into the directory of the cloned repository.</span></span>

```azurecli-interactive
cd faas-netes
```

## <a name="deploy-openfaas"></a><span data-ttu-id="7a38e-116">Deploy OpenFaaS</span><span class="sxs-lookup"><span data-stu-id="7a38e-116">Deploy OpenFaaS</span></span>

<span data-ttu-id="7a38e-117">As a good practice, OpenFaaS and OpenFaaS functions should be stored in their own Kubernetes namespace.</span><span class="sxs-lookup"><span data-stu-id="7a38e-117">As a good practice, OpenFaaS and OpenFaaS functions should be stored in their own Kubernetes namespace.</span></span>

<span data-ttu-id="7a38e-118">Create a namespace for the OpenFaaS system.</span><span class="sxs-lookup"><span data-stu-id="7a38e-118">Create a namespace for the OpenFaaS system.</span></span>

```azurecli-interactive
kubectl create namespace openfaas
```

<span data-ttu-id="7a38e-119">Create a second namespace for OpenFaaS functions.</span><span class="sxs-lookup"><span data-stu-id="7a38e-119">Create a second namespace for OpenFaaS functions.</span></span>

```azurecli-interactive
kubectl create namespace openfaas-fn
```

<span data-ttu-id="7a38e-120">A Helm chart for OpenFaaS is included in the cloned repository.</span><span class="sxs-lookup"><span data-stu-id="7a38e-120">A Helm chart for OpenFaaS is included in the cloned repository.</span></span> <span data-ttu-id="7a38e-121">Use this chart to deploy OpenFaaS into your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="7a38e-121">Use this chart to deploy OpenFaaS into your AKS cluster.</span></span>

```azurecli-interactive
helm install --namespace openfaas -n openfaas \
  --set functionNamespace=openfaas-fn, \
  --set serviceType=LoadBalancer, \
  --set rbac=false chart/openfaas/
```

<span data-ttu-id="7a38e-122">Output:</span><span class="sxs-lookup"><span data-stu-id="7a38e-122">Output:</span></span>

```
NAME:   openfaas
LAST DEPLOYED: Wed Feb 28 08:26:11 2018
NAMESPACE: openfaas
STATUS: DEPLOYED

RESOURCES:
==> v1/ConfigMap
NAME                 DATA  AGE
prometheus-config    2     20s
alertmanager-config  1     20s

{snip}

NOTES:
To verify that openfaas has started, run:

  kubectl --namespace=openfaas get deployments -l "release=openfaas, app=openfaas"
```

<span data-ttu-id="7a38e-123">A public IP address is created for accessing the OpenFaaS gateway.</span><span class="sxs-lookup"><span data-stu-id="7a38e-123">A public IP address is created for accessing the OpenFaaS gateway.</span></span> <span data-ttu-id="7a38e-124">To retrieve this IP address, use the [kubectl get service][kubectl-get] command.</span><span class="sxs-lookup"><span data-stu-id="7a38e-124">To retrieve this IP address, use the [kubectl get service][kubectl-get] command.</span></span> <span data-ttu-id="7a38e-125">It may take a minute for the IP address to be assigned to the service.</span><span class="sxs-lookup"><span data-stu-id="7a38e-125">It may take a minute for the IP address to be assigned to the service.</span></span>

```console
kubectl get service -l component=gateway --namespace openfaas
```

<span data-ttu-id="7a38e-126">Output.</span><span class="sxs-lookup"><span data-stu-id="7a38e-126">Output.</span></span>

```console
NAME               TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)          AGE
gateway            ClusterIP      10.0.156.194   <none>         8080/TCP         7m
gateway-external   LoadBalancer   10.0.28.18     52.186.64.52   8080:30800/TCP   7m
```

<span data-ttu-id="7a38e-127">To test the OpenFaaS system, browse to the external IP address on port 8080, `http://52.186.64.52:8080` in this example.</span><span class="sxs-lookup"><span data-stu-id="7a38e-127">To test the OpenFaaS system, browse to the external IP address on port 8080, `http://52.186.64.52:8080` in this example.</span></span>

![OpenFaaS UI](media/container-service-serverless/openfaas.png)

<span data-ttu-id="7a38e-129">Finally, install the OpenFaaS CLI.</span><span class="sxs-lookup"><span data-stu-id="7a38e-129">Finally, install the OpenFaaS CLI.</span></span> <span data-ttu-id="7a38e-130">This example used brew, see the [OpenFaaS CLI documentation][open-faas-cli] for more options.</span><span class="sxs-lookup"><span data-stu-id="7a38e-130">This example used brew, see the [OpenFaaS CLI documentation][open-faas-cli] for more options.</span></span>

```console
brew install faas-cli
```

## <a name="create-first-function"></a><span data-ttu-id="7a38e-131">Create first function</span><span class="sxs-lookup"><span data-stu-id="7a38e-131">Create first function</span></span>

<span data-ttu-id="7a38e-132">Now that OpenFaaS is operational, create a function using the OpenFaas portal.</span><span class="sxs-lookup"><span data-stu-id="7a38e-132">Now that OpenFaaS is operational, create a function using the OpenFaas portal.</span></span>

<span data-ttu-id="7a38e-133">Click on **Deploy New Function** and search for **Figlet**.</span><span class="sxs-lookup"><span data-stu-id="7a38e-133">Click on **Deploy New Function** and search for **Figlet**.</span></span> <span data-ttu-id="7a38e-134">Select the Figlet function, and click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="7a38e-134">Select the Figlet function, and click **Deploy**.</span></span>

![Figlet](media/container-service-serverless/figlet.png)

<span data-ttu-id="7a38e-136">Use curl to invoke the function.</span><span class="sxs-lookup"><span data-stu-id="7a38e-136">Use curl to invoke the function.</span></span> <span data-ttu-id="7a38e-137">Replace the IP address in the following example with that of your OpenFaas gateway.</span><span class="sxs-lookup"><span data-stu-id="7a38e-137">Replace the IP address in the following example with that of your OpenFaas gateway.</span></span>

```azurecli-interactive
curl -X POST http://52.186.64.52:8080/function/figlet -d "Hello Azure"
```

<span data-ttu-id="7a38e-138">Output:</span><span class="sxs-lookup"><span data-stu-id="7a38e-138">Output:</span></span>

```console
 _   _      _ _            _
| | | | ___| | | ___      / \    _____   _ _ __ ___
| |_| |/ _ \ | |/ _ \    / _ \  |_  / | | | '__/ _ \
|  _  |  __/ | | (_) |  / ___ \  / /| |_| | | |  __/
|_| |_|\___|_|_|\___/  /_/   \_\/___|\__,_|_|  \___|

```

## <a name="create-second-function"></a><span data-ttu-id="7a38e-139">Create second function</span><span class="sxs-lookup"><span data-stu-id="7a38e-139">Create second function</span></span>

<span data-ttu-id="7a38e-140">Now create a second function.</span><span class="sxs-lookup"><span data-stu-id="7a38e-140">Now create a second function.</span></span> <span data-ttu-id="7a38e-141">This example will be deployed using the OpenFaaS CLI and includes a custom container image and retrieving data from a Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a38e-141">This example will be deployed using the OpenFaaS CLI and includes a custom container image and retrieving data from a Cosmos DB.</span></span> <span data-ttu-id="7a38e-142">Several items need to be configured before creating the function.</span><span class="sxs-lookup"><span data-stu-id="7a38e-142">Several items need to be configured before creating the function.</span></span>

<span data-ttu-id="7a38e-143">First, create a new resource group for the Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a38e-143">First, create a new resource group for the Cosmos DB.</span></span>

```azurecli-interactive
az group create --name serverless-backing --location eastus
```

<span data-ttu-id="7a38e-144">Deploy a CosmosDB instance of kind `MongoDB`.</span><span class="sxs-lookup"><span data-stu-id="7a38e-144">Deploy a CosmosDB instance of kind `MongoDB`.</span></span> <span data-ttu-id="7a38e-145">The instance needs a unique name, update `openfaas-cosmos` to something unique to your environment.</span><span class="sxs-lookup"><span data-stu-id="7a38e-145">The instance needs a unique name, update `openfaas-cosmos` to something unique to your environment.</span></span>

```azurecli-interactive
az cosmosdb create --resource-group serverless-backing --name openfaas-cosmos --kind MongoDB
```

<span data-ttu-id="7a38e-146">Get the Cosmos database connection string and store it in a variable.</span><span class="sxs-lookup"><span data-stu-id="7a38e-146">Get the Cosmos database connection string and store it in a variable.</span></span>

<span data-ttu-id="7a38e-147">Update the value for the `--resource-group` argument to the name of your resource group, and the `--name` argument to the name of your Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a38e-147">Update the value for the `--resource-group` argument to the name of your resource group, and the `--name` argument to the name of your Cosmos DB.</span></span>

```azurecli-interactive
COSMOS=$(az cosmosdb list-connection-strings \
  --resource-group serverless-backing \
  --name openfaas-cosmos \
  --query connectionStrings[0].connectionString \
  --output tsv)
```

<span data-ttu-id="7a38e-148">Now populate the Cosmos DB with test data.</span><span class="sxs-lookup"><span data-stu-id="7a38e-148">Now populate the Cosmos DB with test data.</span></span> <span data-ttu-id="7a38e-149">Create a file named `plans.json` and copy in the following json.</span><span class="sxs-lookup"><span data-stu-id="7a38e-149">Create a file named `plans.json` and copy in the following json.</span></span>

```json
{
    "name" : "two_person",
    "friendlyName" : "Two Person Plan",
    "portionSize" : "1-2 Person",
    "mealsPerWeek" : "3 Unique meals per week",
    "price" : 72,
    "description" : "Our basic plan, delivering 3 meals per week, which will feed 1-2 people.",
    "__v" : 0
}
```

<span data-ttu-id="7a38e-150">Use the *mongoimport* tool to load the CosmosDB instance with data.</span><span class="sxs-lookup"><span data-stu-id="7a38e-150">Use the *mongoimport* tool to load the CosmosDB instance with data.</span></span>

<span data-ttu-id="7a38e-151">If needed, install the MongoDB tools.</span><span class="sxs-lookup"><span data-stu-id="7a38e-151">If needed, install the MongoDB tools.</span></span> <span data-ttu-id="7a38e-152">The following example installs these tools using brew, see the [MongoDB documentation][install-mongo] for other options.</span><span class="sxs-lookup"><span data-stu-id="7a38e-152">The following example installs these tools using brew, see the [MongoDB documentation][install-mongo] for other options.</span></span>

```azurecli-interactive
brew install mongodb
```

<span data-ttu-id="7a38e-153">Load the data into the database.</span><span class="sxs-lookup"><span data-stu-id="7a38e-153">Load the data into the database.</span></span>

```azurecli-interactive
mongoimport --uri=$COSMOS -c plans < plans.json
```

<span data-ttu-id="7a38e-154">Output:</span><span class="sxs-lookup"><span data-stu-id="7a38e-154">Output:</span></span>

```console
2018-02-19T14:42:14.313+0000    connected to: localhost
2018-02-19T14:42:14.918+0000    imported 1 document
```

<span data-ttu-id="7a38e-155">Run the following command to create the function.</span><span class="sxs-lookup"><span data-stu-id="7a38e-155">Run the following command to create the function.</span></span> <span data-ttu-id="7a38e-156">Update the value of the `-g` argument with your OpenFaaS gateway address.</span><span class="sxs-lookup"><span data-stu-id="7a38e-156">Update the value of the `-g` argument with your OpenFaaS gateway address.</span></span>

```azurecli-interctive
faas-cli deploy -g http://52.186.64.52:8080 --image=shanepeckham/openfaascosmos --name=cosmos-query --env=NODE_ENV=$COSMOS
```

<span data-ttu-id="7a38e-157">Once deployed, you should see your newly created OpenFaaS endpoint for the function.</span><span class="sxs-lookup"><span data-stu-id="7a38e-157">Once deployed, you should see your newly created OpenFaaS endpoint for the function.</span></span>

```console
Deployed. 202 Accepted.
URL: http://52.186.64.52:8080/function/cosmos-query
```

<span data-ttu-id="7a38e-158">Test the function using curl.</span><span class="sxs-lookup"><span data-stu-id="7a38e-158">Test the function using curl.</span></span> <span data-ttu-id="7a38e-159">Update the IP address with the OpenFaaS gateway address.</span><span class="sxs-lookup"><span data-stu-id="7a38e-159">Update the IP address with the OpenFaaS gateway address.</span></span>

```console
curl -s http://52.186.64.52:8080/function/cosmos-query
```

<span data-ttu-id="7a38e-160">Output:</span><span class="sxs-lookup"><span data-stu-id="7a38e-160">Output:</span></span>

```json
[{"ID":"","Name":"two_person","FriendlyName":"","PortionSize":"","MealsPerWeek":"","Price":72,"Description":"Our basic plan, delivering 3 meals per week, which will feed 1-2 people."}]
```

<span data-ttu-id="7a38e-161">You can also test the function within the OpenFaaS UI.</span><span class="sxs-lookup"><span data-stu-id="7a38e-161">You can also test the function within the OpenFaaS UI.</span></span>

![alt text](media/container-service-serverless/OpenFaaSUI.png)

## <a name="next-steps"></a><span data-ttu-id="7a38e-163">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7a38e-163">Next Steps</span></span>

<span data-ttu-id="7a38e-164">The default deployment of OpenFaas needs to be locked down for both OpenFaaS Gateway and Functions.</span><span class="sxs-lookup"><span data-stu-id="7a38e-164">The default deployment of OpenFaas needs to be locked down for both OpenFaaS Gateway and Functions.</span></span> <span data-ttu-id="7a38e-165">[Alex Ellis' Blog post](https://blog.alexellis.io/lock-down-openfaas/) has more details on secure configuration options.</span><span class="sxs-lookup"><span data-stu-id="7a38e-165">[Alex Ellis' Blog post](https://blog.alexellis.io/lock-down-openfaas/) has more details on secure configuration options.</span></span>

<!-- LINKS - external -->
[install-mongo]: https://docs.mongodb.com/manual/installation/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[open-faas]: https://www.openfaas.com/
[open-faas-cli]: https://github.com/openfaas/faas-cli
