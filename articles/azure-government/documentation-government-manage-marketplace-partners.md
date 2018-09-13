---
title: Azure Marketplace for Azure Government partners | Microsoft Docs
description: This article provides a comparison of features and guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: tsingh
manager: asimm
ms.assetid: 7790d3c5-d0fa-4662-b4f0-a174cb7d6c9f
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 11/14/2016
ms.author: zakramer;tsingh;divacc
ms.openlocfilehash: ca93c6c77704d4e7dac0294dcef9195060cb687e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564353"
---
# <a name="azure-marketplace-for-azure-government"></a><span data-ttu-id="28177-103">Azure Marketplace for Azure Government</span><span class="sxs-lookup"><span data-stu-id="28177-103">Azure Marketplace for Azure Government</span></span>
<span data-ttu-id="28177-104">If you're an Azure Government partner who's interested in publishing offerings to the Azure Marketplace, find the details in this article.</span><span class="sxs-lookup"><span data-stu-id="28177-104">If you're an Azure Government partner who's interested in publishing offerings to the Azure Marketplace, find the details in this article.</span></span>

<span data-ttu-id="28177-105">Currently BYOL VM Images and Solution Templates are supported in Azure Government Marketplace.</span><span class="sxs-lookup"><span data-stu-id="28177-105">Currently BYOL VM Images and Solution Templates are supported in Azure Government Marketplace.</span></span> <span data-ttu-id="28177-106">As a best practice, Solution Templates should be reviewed prior to publishing to Azure Government to ensure it will function on both Azure Public and Azure Government Clouds.</span><span class="sxs-lookup"><span data-stu-id="28177-106">As a best practice, Solution Templates should be reviewed prior to publishing to Azure Government to ensure it will function on both Azure Public and Azure Government Clouds.</span></span> <span data-ttu-id="28177-107">If you are only publishing a VM Image you can proceed to the publishing steps further below.</span><span class="sxs-lookup"><span data-stu-id="28177-107">If you are only publishing a VM Image you can proceed to the publishing steps further below.</span></span>

## <a name="pre-publishing-validation-for-solution-templates"></a><span data-ttu-id="28177-108">Pre-Publishing Validation for Solution Templates</span><span class="sxs-lookup"><span data-stu-id="28177-108">Pre-Publishing Validation for Solution Templates</span></span>

<span data-ttu-id="28177-109">Before you publish your solution template to Azure Government, we recommend checking a couple of common best practice areas to ensure your Template will work in both Azure Public Cloud and Azure Government.</span><span class="sxs-lookup"><span data-stu-id="28177-109">Before you publish your solution template to Azure Government, we recommend checking a couple of common best practice areas to ensure your Template will work in both Azure Public Cloud and Azure Government.</span></span>

1.  <span data-ttu-id="28177-110">Verify endpoints are not hard coded into your solution Template for Azure Public Cloud.</span><span class="sxs-lookup"><span data-stu-id="28177-110">Verify endpoints are not hard coded into your solution Template for Azure Public Cloud.</span></span> <span data-ttu-id="28177-111">These won't be valid for any other Azure Environments.</span><span class="sxs-lookup"><span data-stu-id="28177-111">These won't be valid for any other Azure Environments.</span></span> <span data-ttu-id="28177-112">Instead modify the Solution template to request an API call to pull the valid end point:</span><span class="sxs-lookup"><span data-stu-id="28177-112">Instead modify the Solution template to request an API call to pull the valid end point:</span></span>  

  <span data-ttu-id="28177-113">Example:</span><span class="sxs-lookup"><span data-stu-id="28177-113">Example:</span></span>

  <span data-ttu-id="28177-114">Incorrect VHD uri (hard coded) "uri": "[concat('https://', variables('storageAccountName'), '.blob.core.windows.net/',  '/osdisk.vhd')]",</span><span class="sxs-lookup"><span data-stu-id="28177-114">Incorrect VHD uri (hard coded) "uri": "[concat('https://', variables('storageAccountName'), '.blob.core.windows.net/',  '/osdisk.vhd')]",</span></span>

  <span data-ttu-id="28177-115">Correct VHD uri (referenced)</span><span class="sxs-lookup"><span data-stu-id="28177-115">Correct VHD uri (referenced)</span></span>

  <span data-ttu-id="28177-116">"uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'osdisk.vhd')]",</span><span class="sxs-lookup"><span data-stu-id="28177-116">"uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'osdisk.vhd')]",</span></span>

  <span data-ttu-id="28177-117">The corrected syntax will ensure the template will work on any cloud (Gov, Public Azure, AzureStack, China, etc)</span><span class="sxs-lookup"><span data-stu-id="28177-117">The corrected syntax will ensure the template will work on any cloud (Gov, Public Azure, AzureStack, China, etc)</span></span>

2.  <span data-ttu-id="28177-118">Verify that resources used in your solution template are available in the Sovereign Cloud you are publishing to.</span><span class="sxs-lookup"><span data-stu-id="28177-118">Verify that resources used in your solution template are available in the Sovereign Cloud you are publishing to.</span></span>
<span data-ttu-id="28177-119">RPs in Azure & API version</span><span class="sxs-lookup"><span data-stu-id="28177-119">RPs in Azure & API version</span></span>

    <span data-ttu-id="28177-120">Identify availability Azure Government using Resource Explorer in the portal:</span><span class="sxs-lookup"><span data-stu-id="28177-120">Identify availability Azure Government using Resource Explorer in the portal:</span></span>

  1.    <span data-ttu-id="28177-121">Log into Azure Government Portal</span><span class="sxs-lookup"><span data-stu-id="28177-121">Log into Azure Government Portal</span></span>
  2.    <span data-ttu-id="28177-122">Launch Resource Explorer, following steps listed here https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-supported-services#supported-regions</span><span class="sxs-lookup"><span data-stu-id="28177-122">Launch Resource Explorer, following steps listed here https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-supported-services#supported-regions</span></span>

  <span data-ttu-id="28177-123">Most commonly used extensions; Availability in Fairfax</span><span class="sxs-lookup"><span data-stu-id="28177-123">Most commonly used extensions; Availability in Fairfax</span></span>  

  | <span data-ttu-id="28177-124">Publisher/Type</span><span class="sxs-lookup"><span data-stu-id="28177-124">Publisher/Type</span></span> | <span data-ttu-id="28177-125">Available Versions in Fairfax</span><span class="sxs-lookup"><span data-stu-id="28177-125">Available Versions in Fairfax</span></span> |
  | --- | --- |
  | <span data-ttu-id="28177-126">Microsoft.OSTCExtensions/CustomScriptForLinux</span><span class="sxs-lookup"><span data-stu-id="28177-126">Microsoft.OSTCExtensions/CustomScriptForLinux</span></span> | <span data-ttu-id="28177-127">1; 1.1; 1.2.2.0; 1.3.0.2; 1.4.1.0; 1.5.2.0</span><span class="sxs-lookup"><span data-stu-id="28177-127">1; 1.1; 1.2.2.0; 1.3.0.2; 1.4.1.0; 1.5.2.0</span></span> |
  | <span data-ttu-id="28177-128">Microsoft.Compute/CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="28177-128">Microsoft.Compute/CustomScriptExtension</span></span> | <span data-ttu-id="28177-129">1.2; 1.3; 1.4; 1.7; 1.8</span><span class="sxs-lookup"><span data-stu-id="28177-129">1.2; 1.3; 1.4; 1.7; 1.8</span></span> |
  | <span data-ttu-id="28177-130">Microsoft.Azure.Extensions/DockerExtension</span><span class="sxs-lookup"><span data-stu-id="28177-130">Microsoft.Azure.Extensions/DockerExtension</span></span> | <span data-ttu-id="28177-131">Not Available</span><span class="sxs-lookup"><span data-stu-id="28177-131">Not Available</span></span> |
  | <span data-ttu-id="28177-132">Microsoft.Azure.Extensions/CustomScript</span><span class="sxs-lookup"><span data-stu-id="28177-132">Microsoft.Azure.Extensions/CustomScript</span></span> | <span data-ttu-id="28177-133">2.0.2</span><span class="sxs-lookup"><span data-stu-id="28177-133">2.0.2</span></span> |
  | <span data-ttu-id="28177-134">Microsoft.OSTCExtensions/LinuxDiagnostic</span><span class="sxs-lookup"><span data-stu-id="28177-134">Microsoft.OSTCExtensions/LinuxDiagnostic</span></span> | <span data-ttu-id="28177-135">2.0.9005; 2.1.9005; 2.2.9005; 2.3.9011</span><span class="sxs-lookup"><span data-stu-id="28177-135">2.0.9005; 2.1.9005; 2.2.9005; 2.3.9011</span></span> |
  | <span data-ttu-id="28177-136">Microsoft.Powershell/DSC</span><span class="sxs-lookup"><span data-stu-id="28177-136">Microsoft.Powershell/DSC</span></span> | <span data-ttu-id="28177-137">2.19.0.0</span><span class="sxs-lookup"><span data-stu-id="28177-137">2.19.0.0</span></span> |

> [!NOTE]
> <span data-ttu-id="28177-138">If you put locations in for a list of allowed values, you will need to periodically update it as new regions are added.</span><span class="sxs-lookup"><span data-stu-id="28177-138">If you put locations in for a list of allowed values, you will need to periodically update it as new regions are added.</span></span>  


## <a name="publishing"></a><span data-ttu-id="28177-139">Publishing</span><span class="sxs-lookup"><span data-stu-id="28177-139">Publishing</span></span>
> [!NOTE]
> <span data-ttu-id="28177-140">If you are not an existing Azure Certified Marketplace partner, complete the steps that show how to [publish and manage an offer](../marketplace-publishing/marketplace-publishing-getting-started.md) before proceeding.</span><span class="sxs-lookup"><span data-stu-id="28177-140">If you are not an existing Azure Certified Marketplace partner, complete the steps that show how to [publish and manage an offer](../marketplace-publishing/marketplace-publishing-getting-started.md) before proceeding.</span></span>
>
>

### <a name="step-1"></a><span data-ttu-id="28177-141">Step 1</span><span class="sxs-lookup"><span data-stu-id="28177-141">Step 1</span></span>
<span data-ttu-id="28177-142">Sign in to [Azure Publishing](https://publish.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="28177-142">Sign in to [Azure Publishing](https://publish.windowsazure.com).</span></span>

### <a name="step-2"></a><span data-ttu-id="28177-143">Step 2</span><span class="sxs-lookup"><span data-stu-id="28177-143">Step 2</span></span>
<span data-ttu-id="28177-144">Click the offer that you want to publish.</span><span class="sxs-lookup"><span data-stu-id="28177-144">Click the offer that you want to publish.</span></span>

### <a name="step-3"></a><span data-ttu-id="28177-145">Step 3</span><span class="sxs-lookup"><span data-stu-id="28177-145">Step 3</span></span>
<span data-ttu-id="28177-146">Click **SKUS**, and select the **Azure Government Cloud** box.</span><span class="sxs-lookup"><span data-stu-id="28177-146">Click **SKUS**, and select the **Azure Government Cloud** box.</span></span>

> [!NOTE]
> <span data-ttu-id="28177-147">Only Bring Your Own License (BYOL) SKUs are supported.</span><span class="sxs-lookup"><span data-stu-id="28177-147">Only Bring Your Own License (BYOL) SKUs are supported.</span></span>  <span data-ttu-id="28177-148">This option is not available for Pay-as-You-Go (PayG) SKUs.</span><span class="sxs-lookup"><span data-stu-id="28177-148">This option is not available for Pay-as-You-Go (PayG) SKUs.</span></span>
>
>

![Offer page where the SKUS and Azure Government Cloud options are located](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-1.png)

### <a name="step-4"></a><span data-ttu-id="28177-150">Step 4</span><span class="sxs-lookup"><span data-stu-id="28177-150">Step 4</span></span>
<span data-ttu-id="28177-151">Click the **+ Add Certification** link to add links to any certifications for your offer.</span><span class="sxs-lookup"><span data-stu-id="28177-151">Click the **+ Add Certification** link to add links to any certifications for your offer.</span></span>

![Offer page with Add Certification link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-2.png)

### <a name="step-5"></a><span data-ttu-id="28177-153">Step 5</span><span class="sxs-lookup"><span data-stu-id="28177-153">Step 5</span></span>
<span data-ttu-id="28177-154">To test your image in the publishing portal, request a [trial account](https://azuregov.microsoft.com/trial/azuregovtrial) for Microsoft Azure Government.</span><span class="sxs-lookup"><span data-stu-id="28177-154">To test your image in the publishing portal, request a [trial account](https://azuregov.microsoft.com/trial/azuregovtrial) for Microsoft Azure Government.</span></span>

<span data-ttu-id="28177-155">Your eligibility as a partner who serves US federal, state, local, or tribal entities is verified, and confirmation will be provided via email.</span><span class="sxs-lookup"><span data-stu-id="28177-155">Your eligibility as a partner who serves US federal, state, local, or tribal entities is verified, and confirmation will be provided via email.</span></span>  <span data-ttu-id="28177-156">Your trial account will be available in three to five business days.</span><span class="sxs-lookup"><span data-stu-id="28177-156">Your trial account will be available in three to five business days.</span></span>

### <a name="step-6"></a><span data-ttu-id="28177-157">Step 6</span><span class="sxs-lookup"><span data-stu-id="28177-157">Step 6</span></span>
<span data-ttu-id="28177-158">Click **Publish**, and click **Push to Staging**.</span><span class="sxs-lookup"><span data-stu-id="28177-158">Click **Publish**, and click **Push to Staging**.</span></span>

![Publish and Push to Staging options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-3.png)

<span data-ttu-id="28177-160">You're prompted to enter a whitelisted subscription that has access to the staged offer.</span><span class="sxs-lookup"><span data-stu-id="28177-160">You're prompted to enter a whitelisted subscription that has access to the staged offer.</span></span> <span data-ttu-id="28177-161">Enter the subscription ID from your newly acquired Azure Government trial account.</span><span class="sxs-lookup"><span data-stu-id="28177-161">Enter the subscription ID from your newly acquired Azure Government trial account.</span></span>

![Prompt where you specify the subscription IDs that can access the offer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-4.png)

### <a name="step-7"></a><span data-ttu-id="28177-163">Step 7</span><span class="sxs-lookup"><span data-stu-id="28177-163">Step 7</span></span>
<span data-ttu-id="28177-164">After the offer is successfully staged, you can test your image by signing in to the [Azure portal](https://portal.azure.us) by using your Azure Government trial account.</span><span class="sxs-lookup"><span data-stu-id="28177-164">After the offer is successfully staged, you can test your image by signing in to the [Azure portal](https://portal.azure.us) by using your Azure Government trial account.</span></span>

### <a name="step-8"></a><span data-ttu-id="28177-165">Step 8</span><span class="sxs-lookup"><span data-stu-id="28177-165">Step 8</span></span>
<span data-ttu-id="28177-166">After you have validated your image by using the trial subscription, you can make the offer available live by clicking **Publish** and requesting approval to go to production.</span><span class="sxs-lookup"><span data-stu-id="28177-166">After you have validated your image by using the trial subscription, you can make the offer available live by clicking **Publish** and requesting approval to go to production.</span></span>

![Request approval to go to production command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-government/media/government-manage-marketplace-partner-5.png)

## <a name="next-steps"></a><span data-ttu-id="28177-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="28177-168">Next steps</span></span>
<span data-ttu-id="28177-169">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span><span class="sxs-lookup"><span data-stu-id="28177-169">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span></span>





