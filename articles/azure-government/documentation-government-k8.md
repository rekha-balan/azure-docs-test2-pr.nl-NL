---
title: Deploy Kubernetes to Azure Government | Microsoft Docs
description: This article describes how to deploy Kubernetes to Azure Government using acs-engine.
services: azure-government
cloud: gov
documentationcenter: ''
author: gsacavdm
manager: pathuff
ms.assetid: 8f9a3700-b9ee-43b7-b64d-2e6c3b57d4c0
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 03/11/2018
ms.author: gsacavdm
ms.openlocfilehash: 32aab16b68e945fe2bbd4ecbb8875a5f63f3b8ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864931"
---
# <a name="kubernetes-on-azure-government"></a><span data-ttu-id="5ffc9-103">Kubernetes on Azure Government</span><span class="sxs-lookup"><span data-stu-id="5ffc9-103">Kubernetes on Azure Government</span></span>
<span data-ttu-id="5ffc9-104">This article describes how to deploy a Kubernetes cluster to Azure Government using acs-engine.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-104">This article describes how to deploy a Kubernetes cluster to Azure Government using acs-engine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ffc9-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ffc9-105">Prerequisites</span></span>
* <span data-ttu-id="5ffc9-106">Download [acs-engine](https://github.com/Azure/acs-engine/releases).</span><span class="sxs-lookup"><span data-stu-id="5ffc9-106">Download [acs-engine](https://github.com/Azure/acs-engine/releases).</span></span> <span data-ttu-id="5ffc9-107">Make sure you download **release v.0.14.0 or greater**, previous versions don't work properly with Azure Government.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-107">Make sure you download **release v.0.14.0 or greater**, previous versions don't work properly with Azure Government.</span></span>
* <span data-ttu-id="5ffc9-108">Download [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).</span><span class="sxs-lookup"><span data-stu-id="5ffc9-108">Download [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).</span></span>

## <a name="define-your-kubernetes-cluster-configuration"></a><span data-ttu-id="5ffc9-109">Define your Kubernetes cluster configuration</span><span class="sxs-lookup"><span data-stu-id="5ffc9-109">Define your Kubernetes cluster configuration</span></span>
1. <span data-ttu-id="5ffc9-110">Download the sample acs-engine `apimodel.json` [for Kubernetes 1.8](https://raw.githubusercontent.com/Azure/acs-engine/master/examples/kubernetes-releases/kubernetes1.8.json).</span><span class="sxs-lookup"><span data-stu-id="5ffc9-110">Download the sample acs-engine `apimodel.json` [for Kubernetes 1.8](https://raw.githubusercontent.com/Azure/acs-engine/master/examples/kubernetes-releases/kubernetes1.8.json).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ffc9-111">Only use Kubernetes version 1.8 or greater to if you intend to use Azure Files with Azure Government.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-111">Only use Kubernetes version 1.8 or greater to if you intend to use Azure Files with Azure Government.</span></span>
    >
    >

1. <span data-ttu-id="5ffc9-112">Modify the following values in your `apimodel.json` file:</span><span class="sxs-lookup"><span data-stu-id="5ffc9-112">Modify the following values in your `apimodel.json` file:</span></span>
    * <span data-ttu-id="5ffc9-113">`dnsPrefix`: The dns name you want for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-113">`dnsPrefix`: The dns name you want for the cluster.</span></span> <span data-ttu-id="5ffc9-114">For example, `contoso` will result in `https://contoso.usgovvirginia.cloudapp.usgovcloudapi.net`</span><span class="sxs-lookup"><span data-stu-id="5ffc9-114">For example, `contoso` will result in `https://contoso.usgovvirginia.cloudapp.usgovcloudapi.net`</span></span>
    * <span data-ttu-id="5ffc9-115">`keyData`: The public SSH key to SSH into the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-115">`keyData`: The public SSH key to SSH into the Kubernetes cluster.</span></span> <span data-ttu-id="5ffc9-116">See [How to create and use an SSH public and private key pair for Linux VMs in Azure](../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc9-116">See [How to create and use an SSH public and private key pair for Linux VMs in Azure](../virtual-machines/linux/mac-create-ssh-keys.md).</span></span>
    * <span data-ttu-id="5ffc9-117">`clientId` and `secret`: The client ID and secret for the Azure AD service principal that Kubernetes uses to communicate with Azure Government (for example, to create load balancers, request public IPs and access Azure storage).</span><span class="sxs-lookup"><span data-stu-id="5ffc9-117">`clientId` and `secret`: The client ID and secret for the Azure AD service principal that Kubernetes uses to communicate with Azure Government (for example, to create load balancers, request public IPs and access Azure storage).</span></span> 
    
        > [!NOTE]
        > <span data-ttu-id="5ffc9-118">Make sure this service principal is set up with the correct scope.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-118">Make sure this service principal is set up with the correct scope.</span></span> <span data-ttu-id="5ffc9-119">See [ACS-Engine: Service Principals](https://github.com/Azure/acs-engine/blob/master/docs/serviceprincipal.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc9-119">See [ACS-Engine: Service Principals](https://github.com/Azure/acs-engine/blob/master/docs/serviceprincipal.md).</span></span>
        >

## <a name="deploy-your-kubernetes-cluster-using-acs-engine"></a><span data-ttu-id="5ffc9-120">Deploy your Kubernetes cluster using acs-engine</span><span class="sxs-lookup"><span data-stu-id="5ffc9-120">Deploy your Kubernetes cluster using acs-engine</span></span>
1. <span data-ttu-id="5ffc9-121">Obtain your Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-121">Obtain your Subscription ID.</span></span> <span data-ttu-id="5ffc9-122">The subscription ID is available in the Azure portal, via Powershell and via the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="5ffc9-122">The subscription ID is available in the Azure portal, via Powershell and via the Azure CLI:</span></span>

    <span data-ttu-id="5ffc9-123">Via Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="5ffc9-123">Via Azure CLI:</span></span>

    ```bash
    az cloud set --n AzureUSGovernment
    az login
    az account list
    ```

1. <span data-ttu-id="5ffc9-124">Use acs-engine to deploy your template to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-124">Use acs-engine to deploy your template to Azure Government.</span></span> <span data-ttu-id="5ffc9-125">This operation takes up to 30 minutes for three nodes.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-125">This operation takes up to 30 minutes for three nodes.</span></span>

    ```bash
    acs-engine deploy --azure-env AzureUSGovernmentCloud --location usgovvirginia --subscription-id <YOUR_SUBSCRIPTION_ID> --api-model apimodel.json
    ```

## <a name="connect-to-your-kubernetes-cluster"></a><span data-ttu-id="5ffc9-126">Connect to your Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="5ffc9-126">Connect to your Kubernetes cluster</span></span>
1. <span data-ttu-id="5ffc9-127">Configure your kubectl context.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-127">Configure your kubectl context.</span></span> <span data-ttu-id="5ffc9-128">This configuration is per bash session.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-128">This configuration is per bash session.</span></span> <span data-ttu-id="5ffc9-129">You'll need to run this command for every session:</span><span class="sxs-lookup"><span data-stu-id="5ffc9-129">You'll need to run this command for every session:</span></span>

    ```bash
    export KUBECONFIG=$(pwd)/_output/<DNS-PREFIX>/kubeconfig/kubeconfig.usgovvirginia.json
    ```

    <span data-ttu-id="5ffc9-130">Alternatively, you can replace your kubectl config file for your configuration to persist across sessions.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-130">Alternatively, you can replace your kubectl config file for your configuration to persist across sessions.</span></span> 
    
    > [!WARNING]
    > <span data-ttu-id="5ffc9-131">Any existing configurations will be replaced.</span><span class="sxs-lookup"><span data-stu-id="5ffc9-131">Any existing configurations will be replaced.</span></span>
    >
    >

    ```bash
    cp $(pwd)/_output/<DNS-PREFIX>/kubeconfig/kubeconfig.usgovvirginia.json ~/.kube/config
    ```

1. <span data-ttu-id="5ffc9-132">Test your kubectl connectivity with the cluster</span><span class="sxs-lookup"><span data-stu-id="5ffc9-132">Test your kubectl connectivity with the cluster</span></span>

    ```bash
    kubectl get pods
    ```
1. <span data-ttu-id="5ffc9-133">(Optional) [Deploy a PHP Guestbook application with Redis in your Kubernetes cluster](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/)</span><span class="sxs-lookup"><span data-stu-id="5ffc9-133">(Optional) [Deploy a PHP Guestbook application with Redis in your Kubernetes cluster](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/)</span></span>

### <a name="references"></a><span data-ttu-id="5ffc9-134">References</span><span class="sxs-lookup"><span data-stu-id="5ffc9-134">References</span></span>
* [<span data-ttu-id="5ffc9-135">Microsoft Azure Container Service Engine - Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5ffc9-135">Microsoft Azure Container Service Engine - Kubernetes</span></span>](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md)
* [<span data-ttu-id="5ffc9-136">Configure Access to Multiple Clusters</span><span class="sxs-lookup"><span data-stu-id="5ffc9-136">Configure Access to Multiple Clusters</span></span>](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/#set-the-kubeconfig-environment-variable)

## <a name="next-steps"></a><span data-ttu-id="5ffc9-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ffc9-137">Next steps</span></span>

* <span data-ttu-id="5ffc9-138">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="5ffc9-138">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span></span>
* <span data-ttu-id="5ffc9-139">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span><span class="sxs-lookup"><span data-stu-id="5ffc9-139">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span></span>
* <span data-ttu-id="5ffc9-140">Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span><span class="sxs-lookup"><span data-stu-id="5ffc9-140">Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span></span>
