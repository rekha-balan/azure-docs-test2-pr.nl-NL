---
title: Add a Kubernetes Cluster to the Azure Stack Marketplace | Microsoft Docs
description: Learn how to add a Kubernetes Cluster to the Azure Stack Marketplace.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2018
ms.author: mabrigg
ms.reviewer: waltero
ms.openlocfilehash: 9287eb0925556d382410f95caf16a9ca478ca2da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968655"
---
# <a name="add-a-kubernetes-cluster-to-the-azure-stack-marketplace"></a><span data-ttu-id="f6842-103">Add a Kubernetes Cluster to the Azure Stack Marketplace</span><span class="sxs-lookup"><span data-stu-id="f6842-103">Add a Kubernetes Cluster to the Azure Stack Marketplace</span></span>

<span data-ttu-id="f6842-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="f6842-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

> [!note]  
> <span data-ttu-id="f6842-105">The AKS (Azure Kubernetes Service) Engine on Azure Stack is in private preview.</span><span class="sxs-lookup"><span data-stu-id="f6842-105">The AKS (Azure Kubernetes Service) Engine on Azure Stack is in private preview.</span></span> <span data-ttu-id="f6842-106">To request access to the Kubernetes Marketplace item needed to perform the instructions in this article, [submit a request to get access](https://aka.ms/azsk8).</span><span class="sxs-lookup"><span data-stu-id="f6842-106">To request access to the Kubernetes Marketplace item needed to perform the instructions in this article, [submit a request to get access](https://aka.ms/azsk8).</span></span>

<span data-ttu-id="f6842-107">You can offer a Kubernetes Cluster as a Marketplace item to your users.</span><span class="sxs-lookup"><span data-stu-id="f6842-107">You can offer a Kubernetes Cluster as a Marketplace item to your users.</span></span> <span data-ttu-id="f6842-108">Your users can deploy Kubernetes in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="f6842-108">Your users can deploy Kubernetes in a single, coordinated operation.</span></span>

<span data-ttu-id="f6842-109">The following article look at using an Azure Resource Manager template to deploy and provision the resources for a standalone Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="f6842-109">The following article look at using an Azure Resource Manager template to deploy and provision the resources for a standalone Kubernetes cluster.</span></span> <span data-ttu-id="f6842-110">Before you start, check your Azure Stack and global Azure tenant settings.</span><span class="sxs-lookup"><span data-stu-id="f6842-110">Before you start, check your Azure Stack and global Azure tenant settings.</span></span> <span data-ttu-id="f6842-111">Collect the required information about your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f6842-111">Collect the required information about your Azure Stack.</span></span> <span data-ttu-id="f6842-112">Add necessary resources to your tenant and to the Azure Stack Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f6842-112">Add necessary resources to your tenant and to the Azure Stack Marketplace.</span></span> <span data-ttu-id="f6842-113">The cluster depends on an Ubuntu server, custom script, and the Kubernetes Cluster items to be in the marketplace.</span><span class="sxs-lookup"><span data-stu-id="f6842-113">The cluster depends on an Ubuntu server, custom script, and the Kubernetes Cluster items to be in the marketplace.</span></span>

## <a name="create-a-plan-an-offer-and-a-subscription"></a><span data-ttu-id="f6842-114">Create a plan, an offer, and a subscription</span><span class="sxs-lookup"><span data-stu-id="f6842-114">Create a plan, an offer, and a subscription</span></span>

<span data-ttu-id="f6842-115">Create a plan, an offer, and a subscription for the Kubernetes Cluster Marketplace item.</span><span class="sxs-lookup"><span data-stu-id="f6842-115">Create a plan, an offer, and a subscription for the Kubernetes Cluster Marketplace item.</span></span> <span data-ttu-id="f6842-116">You can also use an existing plan and offer.</span><span class="sxs-lookup"><span data-stu-id="f6842-116">You can also use an existing plan and offer.</span></span>

1. <span data-ttu-id="f6842-117">Sign in to the [Administration portal.](https://adminportal.local.azurestack.external)</span><span class="sxs-lookup"><span data-stu-id="f6842-117">Sign in to the [Administration portal.](https://adminportal.local.azurestack.external)</span></span>

1. <span data-ttu-id="f6842-118">Create a plan as the base plan.</span><span class="sxs-lookup"><span data-stu-id="f6842-118">Create a plan as the base plan.</span></span> <span data-ttu-id="f6842-119">For instructions, see [Create a plan in Azure Stack](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="f6842-119">For instructions, see [Create a plan in Azure Stack](azure-stack-create-plan.md).</span></span>

1. <span data-ttu-id="f6842-120">Create an offer.</span><span class="sxs-lookup"><span data-stu-id="f6842-120">Create an offer.</span></span> <span data-ttu-id="f6842-121">For instructions, see [Create an offer in Azure Stack](azure-stack-create-offer.md).</span><span class="sxs-lookup"><span data-stu-id="f6842-121">For instructions, see [Create an offer in Azure Stack](azure-stack-create-offer.md).</span></span>

1. <span data-ttu-id="f6842-122">Select **Offers**, and find the offer you created.</span><span class="sxs-lookup"><span data-stu-id="f6842-122">Select **Offers**, and find the offer you created.</span></span>

1. <span data-ttu-id="f6842-123">Select **Overview** in the Offer blade.</span><span class="sxs-lookup"><span data-stu-id="f6842-123">Select **Overview** in the Offer blade.</span></span>

1. <span data-ttu-id="f6842-124">Select **Change state**.</span><span class="sxs-lookup"><span data-stu-id="f6842-124">Select **Change state**.</span></span> <span data-ttu-id="f6842-125">Select **Public**.</span><span class="sxs-lookup"><span data-stu-id="f6842-125">Select **Public**.</span></span>

1. <span data-ttu-id="f6842-126">Select **+ New** > **Offers and Plans** > **Subscription** to create a new subscription.</span><span class="sxs-lookup"><span data-stu-id="f6842-126">Select **+ New** > **Offers and Plans** > **Subscription** to create a new subscription.</span></span>

    <span data-ttu-id="f6842-127">a.</span><span class="sxs-lookup"><span data-stu-id="f6842-127">a.</span></span> <span data-ttu-id="f6842-128">Enter a **Display Name**.</span><span class="sxs-lookup"><span data-stu-id="f6842-128">Enter a **Display Name**.</span></span>

    <span data-ttu-id="f6842-129">b.</span><span class="sxs-lookup"><span data-stu-id="f6842-129">b.</span></span> <span data-ttu-id="f6842-130">Enter a **User**.</span><span class="sxs-lookup"><span data-stu-id="f6842-130">Enter a **User**.</span></span> <span data-ttu-id="f6842-131">Use the Azure AD account associated with your tenant.</span><span class="sxs-lookup"><span data-stu-id="f6842-131">Use the Azure AD account associated with your tenant.</span></span>

    <span data-ttu-id="f6842-132">c.</span><span class="sxs-lookup"><span data-stu-id="f6842-132">c.</span></span> <span data-ttu-id="f6842-133">**Provider Description**</span><span class="sxs-lookup"><span data-stu-id="f6842-133">**Provider Description**</span></span>

    <span data-ttu-id="f6842-134">d.</span><span class="sxs-lookup"><span data-stu-id="f6842-134">d.</span></span> <span data-ttu-id="f6842-135">Set the **Directory tenant** to the Azure AD tenant for your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f6842-135">Set the **Directory tenant** to the Azure AD tenant for your Azure Stack.</span></span> 

    <span data-ttu-id="f6842-136">e.</span><span class="sxs-lookup"><span data-stu-id="f6842-136">e.</span></span> <span data-ttu-id="f6842-137">Select **Offer**.</span><span class="sxs-lookup"><span data-stu-id="f6842-137">Select **Offer**.</span></span> <span data-ttu-id="f6842-138">Select the name of the offer that you created.</span><span class="sxs-lookup"><span data-stu-id="f6842-138">Select the name of the offer that you created.</span></span> <span data-ttu-id="f6842-139">Make note of the Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="f6842-139">Make note of the Subscription ID.</span></span>

## <a name="add-an-ubuntu-server-image"></a><span data-ttu-id="f6842-140">Add an Ubuntu server image</span><span class="sxs-lookup"><span data-stu-id="f6842-140">Add an Ubuntu server image</span></span>

<span data-ttu-id="f6842-141">Add the following Ubuntu Server image to the Marketplace:</span><span class="sxs-lookup"><span data-stu-id="f6842-141">Add the following Ubuntu Server image to the Marketplace:</span></span>

1. <span data-ttu-id="f6842-142">Sign in to the [Administration portal](https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="f6842-142">Sign in to the [Administration portal](https://adminportal.local.azurestack.external).</span></span>

1. <span data-ttu-id="f6842-143">Select **All services**, and then under the **ADMINISTRATION** category, select **Marketplace management**.</span><span class="sxs-lookup"><span data-stu-id="f6842-143">Select **All services**, and then under the **ADMINISTRATION** category, select **Marketplace management**.</span></span>

1. <span data-ttu-id="f6842-144">Select **+ Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6842-144">Select **+ Add from Azure**.</span></span>

1. <span data-ttu-id="f6842-145">Enter `UbuntuServer`.</span><span class="sxs-lookup"><span data-stu-id="f6842-145">Enter `UbuntuServer`.</span></span>

1. <span data-ttu-id="f6842-146">Select the server with the following profile:</span><span class="sxs-lookup"><span data-stu-id="f6842-146">Select the server with the following profile:</span></span>
    - <span data-ttu-id="f6842-147">**Publisher**: Canonical</span><span class="sxs-lookup"><span data-stu-id="f6842-147">**Publisher**: Canonical</span></span>
    - <span data-ttu-id="f6842-148">**Offer**: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f6842-148">**Offer**: UbuntuServer</span></span>
    - <span data-ttu-id="f6842-149">**SKU**: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="f6842-149">**SKU**: 16.04-LTS</span></span>
    - <span data-ttu-id="f6842-150">**Version**: 16.04.201802220</span><span class="sxs-lookup"><span data-stu-id="f6842-150">**Version**: 16.04.201802220</span></span>

    > [!Note]  
    > <span data-ttu-id="f6842-151">More than one version of Ubuntu Server 16.04 LTS may be listed.</span><span class="sxs-lookup"><span data-stu-id="f6842-151">More than one version of Ubuntu Server 16.04 LTS may be listed.</span></span> <span data-ttu-id="f6842-152">You will need to add the version that matches.</span><span class="sxs-lookup"><span data-stu-id="f6842-152">You will need to add the version that matches.</span></span> <span data-ttu-id="f6842-153">The Kubernetes Cluster requires the exact version of the item.</span><span class="sxs-lookup"><span data-stu-id="f6842-153">The Kubernetes Cluster requires the exact version of the item.</span></span>

1. <span data-ttu-id="f6842-154">Select **Download.**</span><span class="sxs-lookup"><span data-stu-id="f6842-154">Select **Download.**</span></span>

## <a name="add-a-custom-script-for-linux"></a><span data-ttu-id="f6842-155">Add a custom script for Linux</span><span class="sxs-lookup"><span data-stu-id="f6842-155">Add a custom script for Linux</span></span>

<span data-ttu-id="f6842-156">Add the Kubernetes Cluster from the Marketplace:</span><span class="sxs-lookup"><span data-stu-id="f6842-156">Add the Kubernetes Cluster from the Marketplace:</span></span>

1. <span data-ttu-id="f6842-157">Open the [Administration portal](https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="f6842-157">Open the [Administration portal](https://adminportal.local.azurestack.external).</span></span>

1. <span data-ttu-id="f6842-158">Select **ALL services** and then under the **ADMINISTRATION** category, select **Marketplace Management**.</span><span class="sxs-lookup"><span data-stu-id="f6842-158">Select **ALL services** and then under the **ADMINISTRATION** category, select **Marketplace Management**.</span></span>

1. <span data-ttu-id="f6842-159">Select **+ Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6842-159">Select **+ Add from Azure**.</span></span>

1. <span data-ttu-id="f6842-160">Enter `Custom Script for Linux`.</span><span class="sxs-lookup"><span data-stu-id="f6842-160">Enter `Custom Script for Linux`.</span></span>

1. <span data-ttu-id="f6842-161">Select the script with the following profile:</span><span class="sxs-lookup"><span data-stu-id="f6842-161">Select the script with the following profile:</span></span>
    - <span data-ttu-id="f6842-162">**Offer**: Custom Script for Linux 2.0</span><span class="sxs-lookup"><span data-stu-id="f6842-162">**Offer**: Custom Script for Linux 2.0</span></span>
    - <span data-ttu-id="f6842-163">**Version**: 2.0.3</span><span class="sxs-lookup"><span data-stu-id="f6842-163">**Version**: 2.0.3</span></span>
    - <span data-ttu-id="f6842-164">**Publisher**: Microsoft Corp</span><span class="sxs-lookup"><span data-stu-id="f6842-164">**Publisher**: Microsoft Corp</span></span>

    > [!Note]  
    > <span data-ttu-id="f6842-165">More than one version of Custom Script for Linux may be listed.</span><span class="sxs-lookup"><span data-stu-id="f6842-165">More than one version of Custom Script for Linux may be listed.</span></span> <span data-ttu-id="f6842-166">You will need to add the version that matches.</span><span class="sxs-lookup"><span data-stu-id="f6842-166">You will need to add the version that matches.</span></span> <span data-ttu-id="f6842-167">The Kubernetes Cluster requires the exact version of the item.</span><span class="sxs-lookup"><span data-stu-id="f6842-167">The Kubernetes Cluster requires the exact version of the item.</span></span>

1. <span data-ttu-id="f6842-168">Select **Download.**</span><span class="sxs-lookup"><span data-stu-id="f6842-168">Select **Download.**</span></span>


## <a name="add-the-kubernetes-cluster-to-the-marketplace"></a><span data-ttu-id="f6842-169">Add the Kubernetes Cluster to the marketplace</span><span class="sxs-lookup"><span data-stu-id="f6842-169">Add the Kubernetes Cluster to the marketplace</span></span>

1. <span data-ttu-id="f6842-170">Open the [Administration portal](https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="f6842-170">Open the [Administration portal](https://adminportal.local.azurestack.external).</span></span>

1. <span data-ttu-id="f6842-171">Select **A;; services** and then under the **ADMINISTRATION** category, select **Marketplace Management**.</span><span class="sxs-lookup"><span data-stu-id="f6842-171">Select **A;; services** and then under the **ADMINISTRATION** category, select **Marketplace Management**.</span></span>

1. <span data-ttu-id="f6842-172">Select **+ Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6842-172">Select **+ Add from Azure**.</span></span>

1. <span data-ttu-id="f6842-173">Enter `Kubernetes Cluster`.</span><span class="sxs-lookup"><span data-stu-id="f6842-173">Enter `Kubernetes Cluster`.</span></span>

1. <span data-ttu-id="f6842-174">Select `Kubernetes Cluster`.</span><span class="sxs-lookup"><span data-stu-id="f6842-174">Select `Kubernetes Cluster`.</span></span>

1. <span data-ttu-id="f6842-175">Select **Download.**</span><span class="sxs-lookup"><span data-stu-id="f6842-175">Select **Download.**</span></span>

    > [!note]  
    > <span data-ttu-id="f6842-176">It may take five minutes for the marketplace item to appear in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f6842-176">It may take five minutes for the marketplace item to appear in the Marketplace.</span></span>

    ![Kubernetes Cluster](user\media\azure-stack-solution-template-kubernetes-deploy\marketplaceitem.png)

## <a name="update-or-remove-the-kubernetes-cluster"></a><span data-ttu-id="f6842-178">Update or remove the Kubernetes Cluster</span><span class="sxs-lookup"><span data-stu-id="f6842-178">Update or remove the Kubernetes Cluster</span></span> 

<span data-ttu-id="f6842-179">When updating the Kubernetes Cluster item, you will need to remove the item that is in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f6842-179">When updating the Kubernetes Cluster item, you will need to remove the item that is in the Marketplace.</span></span> <span data-ttu-id="f6842-180">Then you can follow the instruction in this article to add the Kubernetes Cluster to the marketplace.</span><span class="sxs-lookup"><span data-stu-id="f6842-180">Then you can follow the instruction in this article to add the Kubernetes Cluster to the marketplace.</span></span>

<span data-ttu-id="f6842-181">To remove the Kubernetes Cluster item:</span><span class="sxs-lookup"><span data-stu-id="f6842-181">To remove the Kubernetes Cluster item:</span></span>

1. <span data-ttu-id="f6842-182">Note name of the current item, such as `Microsoft.AzureStackKubernetesCluster.0.1.0`</span><span class="sxs-lookup"><span data-stu-id="f6842-182">Note name of the current item, such as `Microsoft.AzureStackKubernetesCluster.0.1.0`</span></span>

1. <span data-ttu-id="f6842-183">Connect to Azure Stack with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6842-183">Connect to Azure Stack with PowerShell.</span></span>

1. <span data-ttu-id="f6842-184">Use the following PowerShell cmdlet to remove the item:</span><span class="sxs-lookup"><span data-stu-id="f6842-184">Use the following PowerShell cmdlet to remove the item:</span></span>

    ```PowerShell  
    $Itemname="Microsoft.AzureStackKubernetesCluster.0.1.0"

    Remove-AzsGalleryItem -Name $Itemname
    ```

## <a name="next-steps"></a><span data-ttu-id="f6842-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6842-185">Next steps</span></span>

[<span data-ttu-id="f6842-186">Deploy a Kubernetes Cluster to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f6842-186">Deploy a Kubernetes Cluster to Azure Stack</span></span>](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-solution-template-kubernetes-deploy)



[<span data-ttu-id="f6842-187">Overview of offering services in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f6842-187">Overview of offering services in Azure Stack</span></span>](azure-stack-offer-services-overview.md)