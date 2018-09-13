---
title: Use Draft with Azure Container Service and Azure Container Registry
description: Create an ACS Kubernetes cluster and an Azure Container Registry to create your first application in Azure with Draft.
services: container-service
author: squillace
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 09/14/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: c635a869506918ab7ee032df349eb307987c1284
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966117"
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="68429-103">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span><span class="sxs-lookup"><span data-stu-id="68429-103">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="68429-104">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span><span class="sxs-lookup"><span data-stu-id="68429-104">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="68429-105">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span><span class="sxs-lookup"><span data-stu-id="68429-105">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="68429-106">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span><span class="sxs-lookup"><span data-stu-id="68429-106">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="68429-107">This tutorial shows how to use ACS with Kubernetes and ACR to create a live but secure developer pipeline in Kubernetes using Draft, and how to use Azure DNS to expose that developer pipeline for others to see at a domain.</span><span class="sxs-lookup"><span data-stu-id="68429-107">This tutorial shows how to use ACS with Kubernetes and ACR to create a live but secure developer pipeline in Kubernetes using Draft, and how to use Azure DNS to expose that developer pipeline for others to see at a domain.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="68429-108">Create an Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="68429-108">Create an Azure Container Registry</span></span>
<span data-ttu-id="68429-109">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="68429-109">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="68429-110">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span><span class="sxs-lookup"><span data-stu-id="68429-110">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="68429-111">Create an ACR image registry using [az acr create](/cli/azure/acr#az-acr-create) and ensure that the `--admin-enabled` option is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="68429-111">Create an ACR image registry using [az acr create](/cli/azure/acr#az-acr-create) and ensure that the `--admin-enabled` option is set to `true`.</span></span>
      ```azurecli
      az acr create --resource-group draft --name draftacs --sku Basic
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="68429-112">Create an Azure Container Service with Kubernetes</span><span class="sxs-lookup"><span data-stu-id="68429-112">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="68429-113">Now you're ready to use [az acs create](/cli/azure/acs#az-acs-create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span><span class="sxs-lookup"><span data-stu-id="68429-113">Now you're ready to use [az acs create](/cli/azure/acs#az-acs-create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes --generate-ssh-keys
```

> [!NOTE]
> <span data-ttu-id="68429-114">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span><span class="sxs-lookup"><span data-stu-id="68429-114">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="68429-115">The output when successful looks similar to the following.</span><span class="sxs-lookup"><span data-stu-id="68429-115">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="68429-116">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span><span class="sxs-lookup"><span data-stu-id="68429-116">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="68429-117">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span><span class="sxs-lookup"><span data-stu-id="68429-117">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="68429-118">Install and configure draft</span><span class="sxs-lookup"><span data-stu-id="68429-118">Install and configure draft</span></span>


1. <span data-ttu-id="68429-119">Download draft for your environment at https://github.com/Azure/draft/releases and install into your PATH so that the command can be used.</span><span class="sxs-lookup"><span data-stu-id="68429-119">Download draft for your environment at https://github.com/Azure/draft/releases and install into your PATH so that the command can be used.</span></span>
2. <span data-ttu-id="68429-120">Download helm for your environment at https://github.com/kubernetes/helm/releases and [install it into your PATH so that the command can be used](https://github.com/kubernetes/helm/blob/master/docs/install.md#installing-the-helm-client).</span><span class="sxs-lookup"><span data-stu-id="68429-120">Download helm for your environment at https://github.com/kubernetes/helm/releases and [install it into your PATH so that the command can be used](https://github.com/kubernetes/helm/blob/master/docs/install.md#installing-the-helm-client).</span></span>
3. <span data-ttu-id="68429-121">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span><span class="sxs-lookup"><span data-stu-id="68429-121">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="68429-122">To configure Draft, you need:</span><span class="sxs-lookup"><span data-stu-id="68429-122">To configure Draft, you need:</span></span>
  - <span data-ttu-id="68429-123">your Azure Container Registry name (in this example, `draftacsdemo`)</span><span class="sxs-lookup"><span data-stu-id="68429-123">your Azure Container Registry name (in this example, `draftacsdemo`)</span></span>
  - <span data-ttu-id="68429-124">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="68429-124">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>

  <span data-ttu-id="68429-125">Call `draft init` and the configuration process prompts you for the values above; note that the URL format for the registry URL is the registry name (in this example, `draftacsdemo`) plus `.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="68429-125">Call `draft init` and the configuration process prompts you for the values above; note that the URL format for the registry URL is the registry name (in this example, `draftacsdemo`) plus `.azurecr.io`.</span></span> <span data-ttu-id="68429-126">Your username is the registry name on its own.</span><span class="sxs-lookup"><span data-stu-id="68429-126">Your username is the registry name on its own.</span></span> <span data-ttu-id="68429-127">The process looks something like the following the first time you run it.</span><span class="sxs-lookup"><span data-stu-id="68429-127">The process looks something like the following the first time you run it.</span></span>
 ```bash
    $ draft init
    Creating /home/ralph/.draft 
    Creating /home/ralph/.draft/plugins 
    Creating /home/ralph/.draft/packs 
    Creating pack go...
    Creating pack python...
    Creating pack ruby...
    Creating pack javascript...
    Creating pack gradle...
    Creating pack java...
    Creating pack php...
    Creating pack csharp...
    $DRAFT_HOME has been configured at /home/ralph/.draft.

    In order to configure Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io/myuser, quay.io/myuser, myregistry.azurecr.io): draftacsdemo.azurecr.io
    2. Enter your username: draftacsdemo
    3. Enter your password: 
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
```

<span data-ttu-id="68429-128">Now you're ready to deploy an application.</span><span class="sxs-lookup"><span data-stu-id="68429-128">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="68429-129">Build and deploy an application</span><span class="sxs-lookup"><span data-stu-id="68429-129">Build and deploy an application</span></span>

<span data-ttu-id="68429-130">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="68429-130">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="68429-131">Clone the repo and let's use the [Java example](https://github.com/Azure/draft/tree/master/examples/java).</span><span class="sxs-lookup"><span data-stu-id="68429-131">Clone the repo and let's use the [Java example](https://github.com/Azure/draft/tree/master/examples/java).</span></span> <span data-ttu-id="68429-132">Change into the examples/java directory, and type `draft create` to build the application.</span><span class="sxs-lookup"><span data-stu-id="68429-132">Change into the examples/java directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="68429-133">It should look like the following example.</span><span class="sxs-lookup"><span data-stu-id="68429-133">It should look like the following example.</span></span>
```bash
$ draft create
--> Draft detected the primary language as Java with 91.228814% certainty.
--> Ready to sail
```

<span data-ttu-id="68429-134">The output includes a Dockerfile and a Helm chart.</span><span class="sxs-lookup"><span data-stu-id="68429-134">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="68429-135">To build and deploy, you just type `draft up`.</span><span class="sxs-lookup"><span data-stu-id="68429-135">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="68429-136">The output is extensive, but should be like the following example.</span><span class="sxs-lookup"><span data-stu-id="68429-136">The output is extensive, but should be like the following example.</span></span>
```bash
$ draft up
Draft Up Started: 'handy-labradoodle'
handy-labradoodle: Building Docker Image: SUCCESS ⚓  (35.0232s)
handy-labradoodle: Pushing Docker Image: SUCCESS ⚓  (17.0062s)
handy-labradoodle: Releasing Application: SUCCESS ⚓  (3.8903s)
handy-labradoodle: Build ID: 01BT0ZJ87NWCD7BBPK4Y3BTTPB
```

## <a name="securely-view-your-application"></a><span data-ttu-id="68429-137">Securely view your application</span><span class="sxs-lookup"><span data-stu-id="68429-137">Securely view your application</span></span>

<span data-ttu-id="68429-138">Your container is now running in ACS.</span><span class="sxs-lookup"><span data-stu-id="68429-138">Your container is now running in ACS.</span></span> <span data-ttu-id="68429-139">To view it, use the `draft connect` command, which creates a secured connection to the cluster's IP with a specific port for your application so that you can view it locally.</span><span class="sxs-lookup"><span data-stu-id="68429-139">To view it, use the `draft connect` command, which creates a secured connection to the cluster's IP with a specific port for your application so that you can view it locally.</span></span> <span data-ttu-id="68429-140">If successful, look for the URL to connect to your app on the first line after the **SUCCESS** indicator.</span><span class="sxs-lookup"><span data-stu-id="68429-140">If successful, look for the URL to connect to your app on the first line after the **SUCCESS** indicator.</span></span>

> [!NOTE]
> <span data-ttu-id="68429-141">If you receive a message saying that no pods were ready, wait for a moment and retry, or you can watch the pods become ready with `kubectl get pods -w` and then retry when they do.</span><span class="sxs-lookup"><span data-stu-id="68429-141">If you receive a message saying that no pods were ready, wait for a moment and retry, or you can watch the pods become ready with `kubectl get pods -w` and then retry when they do.</span></span>

```bash
draft connect
Connecting to your app...SUCCESS...Connect to your app on localhost:46143
Starting log streaming...
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
== Spark has ignited ...
>> Listening on 0.0.0.0:4567
```

<span data-ttu-id="68429-142">In the preceding example, you could type `curl -s http://localhost:46143` to receive the reply, `Hello World, I'm Java!`.</span><span class="sxs-lookup"><span data-stu-id="68429-142">In the preceding example, you could type `curl -s http://localhost:46143` to receive the reply, `Hello World, I'm Java!`.</span></span> <span data-ttu-id="68429-143">When you CTRL+ or CMD+C (depending on your OS environment), the secure tunnel is torn down and you can continue iterating.</span><span class="sxs-lookup"><span data-stu-id="68429-143">When you CTRL+ or CMD+C (depending on your OS environment), the secure tunnel is torn down and you can continue iterating.</span></span>

## <a name="sharing-your-application-by-configuring-a-deployment-domain-with-azure-dns"></a><span data-ttu-id="68429-144">Sharing your application by configuring a deployment domain with Azure DNS</span><span class="sxs-lookup"><span data-stu-id="68429-144">Sharing your application by configuring a deployment domain with Azure DNS</span></span>

<span data-ttu-id="68429-145">You have already performed the developer iteration loop that Draft creates in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="68429-145">You have already performed the developer iteration loop that Draft creates in the preceding steps.</span></span> <span data-ttu-id="68429-146">However, you can share your application across the internet by:</span><span class="sxs-lookup"><span data-stu-id="68429-146">However, you can share your application across the internet by:</span></span>
1. <span data-ttu-id="68429-147">Installing an ingress in your ACS cluster (to provide a public IP address at which to display the app)</span><span class="sxs-lookup"><span data-stu-id="68429-147">Installing an ingress in your ACS cluster (to provide a public IP address at which to display the app)</span></span>
2. <span data-ttu-id="68429-148">Delegating your custom domain to Azure DNS and mapping your domain to the IP address ACS assigns to your ingress controller</span><span class="sxs-lookup"><span data-stu-id="68429-148">Delegating your custom domain to Azure DNS and mapping your domain to the IP address ACS assigns to your ingress controller</span></span>

### <a name="use-helm-to-install-the-ingress-controller"></a><span data-ttu-id="68429-149">Use helm to install the ingress controller.</span><span class="sxs-lookup"><span data-stu-id="68429-149">Use helm to install the ingress controller.</span></span>
<span data-ttu-id="68429-150">Use **helm** to search for and install `stable/traefik`, an ingress controller, to enable inbound requests for your builds.</span><span class="sxs-lookup"><span data-stu-id="68429-150">Use **helm** to search for and install `stable/traefik`, an ingress controller, to enable inbound requests for your builds.</span></span>
```bash
$ helm search traefik
NAME            VERSION DESCRIPTION
stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

$ helm install stable/traefik --name ingress
```
<span data-ttu-id="68429-151">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span><span class="sxs-lookup"><span data-stu-id="68429-151">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="68429-152">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span><span class="sxs-lookup"><span data-stu-id="68429-152">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

```bash
$ kubectl get svc -w
NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
kubernetes                    10.0.0.1       <none>          443/TCP                      7h
```

<span data-ttu-id="68429-153">In this case, the external IP for the deployment domain is `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="68429-153">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="68429-154">Now you can map your domain to that IP.</span><span class="sxs-lookup"><span data-stu-id="68429-154">Now you can map your domain to that IP.</span></span>

### <a name="map-the-ingress-ip-to-a-custom-subdomain"></a><span data-ttu-id="68429-155">Map the ingress IP to a custom subdomain</span><span class="sxs-lookup"><span data-stu-id="68429-155">Map the ingress IP to a custom subdomain</span></span>

<span data-ttu-id="68429-156">Draft creates a release for each Helm chart it creates -- each application you are working on.</span><span class="sxs-lookup"><span data-stu-id="68429-156">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="68429-157">Each one gets a generated name that is used by **draft** as a _subdomain_ on top of the root _deployment domain_ that you control.</span><span class="sxs-lookup"><span data-stu-id="68429-157">Each one gets a generated name that is used by **draft** as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="68429-158">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*.draft'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span><span class="sxs-lookup"><span data-stu-id="68429-158">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*.draft'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span> 

<span data-ttu-id="68429-159">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span><span class="sxs-lookup"><span data-stu-id="68429-159">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="68429-160">Create a resource group for your zone.</span><span class="sxs-lookup"><span data-stu-id="68429-160">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="68429-161">Create a DNS zone for your domain.</span><span class="sxs-lookup"><span data-stu-id="68429-161">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="68429-162">Use the [az network dns zone create](/cli/azure/network/dns/zone#az-network-dns-zone-create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span><span class="sxs-lookup"><span data-stu-id="68429-162">Use the [az network dns zone create](/cli/azure/network/dns/zone#az-network-dns-zone-create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="68429-163">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span><span class="sxs-lookup"><span data-stu-id="68429-163">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span> <span data-ttu-id="68429-164">The way you do this varies by domain provide; [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md) contains some of the details that you should know.</span><span class="sxs-lookup"><span data-stu-id="68429-164">The way you do this varies by domain provide; [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md) contains some of the details that you should know.</span></span> 
4. <span data-ttu-id="68429-165">Once your domain has been delegated to Azure DNS, create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span><span class="sxs-lookup"><span data-stu-id="68429-165">Once your domain has been delegated to Azure DNS, create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
  ```azurecli
  az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*.draft' -g squillace.io -z squillace.io
  ```
<span data-ttu-id="68429-166">The output looks something like:</span><span class="sxs-lookup"><span data-stu-id="68429-166">The output looks something like:</span></span>
  ```json
  {
    "arecords": [
      {
        "ipv4Address": "13.64.108.240"
      }
    ],
    "etag": "<guid>",
    "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
    "metadata": null,
    "name": "*.draft",
    "resourceGroup": "squillace.io",
    "ttl": 3600,
    "type": "Microsoft.Network/dnszones/A"
  }
  ```
5. <span data-ttu-id="68429-167">Reinstall **draft**</span><span class="sxs-lookup"><span data-stu-id="68429-167">Reinstall **draft**</span></span>

   1. <span data-ttu-id="68429-168">Remove **draftd** from the cluster by typing `helm delete --purge draft`.</span><span class="sxs-lookup"><span data-stu-id="68429-168">Remove **draftd** from the cluster by typing `helm delete --purge draft`.</span></span> 
   2. <span data-ttu-id="68429-169">Reinstall **draft** by using the same `draft-init` command, but with the `--ingress-enabled` option:</span><span class="sxs-lookup"><span data-stu-id="68429-169">Reinstall **draft** by using the same `draft-init` command, but with the `--ingress-enabled` option:</span></span>
    ```bash
    draft init --ingress-enabled
    ```
   <span data-ttu-id="68429-170">Respond to the prompts as you did the first time, above.</span><span class="sxs-lookup"><span data-stu-id="68429-170">Respond to the prompts as you did the first time, above.</span></span> <span data-ttu-id="68429-171">However, you have one more question to respond to, using the complete domain path that you configured with the Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="68429-171">However, you have one more question to respond to, using the complete domain path that you configured with the Azure DNS.</span></span>

6. <span data-ttu-id="68429-172">Enter your top-level domain for ingress (e.g. draft.example.com): draft.squillace.io</span><span class="sxs-lookup"><span data-stu-id="68429-172">Enter your top-level domain for ingress (e.g. draft.example.com): draft.squillace.io</span></span>
7. <span data-ttu-id="68429-173">When you call `draft up` this time, you will be able to see your application (or `curl` it) at the URL of the form `<appname>.draft.<domain>.<top-level-domain>`.</span><span class="sxs-lookup"><span data-stu-id="68429-173">When you call `draft up` this time, you will be able to see your application (or `curl` it) at the URL of the form `<appname>.draft.<domain>.<top-level-domain>`.</span></span> <span data-ttu-id="68429-174">In the case of this example, `http://handy-labradoodle.draft.squillace.io`.</span><span class="sxs-lookup"><span data-stu-id="68429-174">In the case of this example, `http://handy-labradoodle.draft.squillace.io`.</span></span> 
```bash
curl -s http://handy-labradoodle.draft.squillace.io
Hello World, I'm Java!
```


## <a name="next-steps"></a><span data-ttu-id="68429-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="68429-175">Next steps</span></span>

<span data-ttu-id="68429-176">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span><span class="sxs-lookup"><span data-stu-id="68429-176">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="68429-177">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span><span class="sxs-lookup"><span data-stu-id="68429-177">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






