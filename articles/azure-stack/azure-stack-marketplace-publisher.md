---
title: Use the Marketplace toolkit to create and publish marketplace items | Microsoft Docs
description: Learn how to quickly create marketplace items with the publishing Toolkit
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: brenduns
ms.reviewer: jeffgo
ms.openlocfilehash: d404fc60d99379bbdc02d75ed9630ca39e9fd797
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856531"
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="a9f0d-103">Add marketplace items using publishing tool</span><span class="sxs-lookup"><span data-stu-id="a9f0d-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="a9f0d-104">Adding your content to the [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available to you and your tenants for deployment.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-104">Adding your content to the [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available to you and your tenants for deployment.</span></span>  <span data-ttu-id="a9f0d-105">The Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-105">The Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="a9f0d-106">You can also use the Marketplace Toolkit to publish .azpkg files, either created with the tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-106">You can also use the Marketplace Toolkit to publish .azpkg files, either created with the tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="a9f0d-107">This topic guides you through downloading the tool, creating a marketplace item based on a VM template, and then publishing that item to the Azure Stack Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-107">This topic guides you through downloading the tool, creating a marketplace item based on a VM template, and then publishing that item to the Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="a9f0d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9f0d-108">Prerequisites</span></span>
 - <span data-ttu-id="a9f0d-109">You must run the toolkit on the Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from the machine where you run the tool.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-109">You must run the toolkit on the Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from the machine where you run the tool.</span></span>

 - <span data-ttu-id="a9f0d-110">Download the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-110">Download the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="a9f0d-111">Download the [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span><span class="sxs-lookup"><span data-stu-id="a9f0d-111">Download the [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="a9f0d-112">Publishing to the marketplace requires icons and a thumbnail file.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-112">Publishing to the marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="a9f0d-113">You can use your own, or save the [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-113">You can use your own, or save the [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-the-tool"></a><span data-ttu-id="a9f0d-114">Download the tool</span><span class="sxs-lookup"><span data-stu-id="a9f0d-114">Download the tool</span></span>
<span data-ttu-id="a9f0d-115">The Marketplace Toolkit can be [downloaded from the Azure Stack Tools repo](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="a9f0d-115">The Marketplace Toolkit can be [downloaded from the Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="a9f0d-116">Create marketplace items</span><span class="sxs-lookup"><span data-stu-id="a9f0d-116">Create marketplace items</span></span>
<span data-ttu-id="a9f0d-117">In this section, you use the Marketplace Toolkit to create a marketplace item package in .azpkg format.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-117">In this section, you use the Marketplace Toolkit to create a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="a9f0d-118">Provide marketplace information with wizard</span><span class="sxs-lookup"><span data-stu-id="a9f0d-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="a9f0d-119">Run the Marketplace Toolkit from a PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="a9f0d-119">Run the Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="a9f0d-120">Click the **Solution** tab.  This screen accepts information about your marketplace item.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-120">Click the **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="a9f0d-121">Enter information about your item as you want it to appear in the marketplace.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-121">Enter information about your item as you want it to appear in the marketplace.</span></span>  <span data-ttu-id="a9f0d-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) to prepopulate the form.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) to prepopulate the form.</span></span>  
    
    ![screenshot of Marketplace Toolkit first screen](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="a9f0d-124">Click **Browse** and select an image file for each icon and screenshot field.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="a9f0d-125">You can use your own icons, or the sample icons in the [support files](azure-stack-marketplace-publisher.md#support-files) section.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-125">You can use your own icons, or the sample icons in the [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="a9f0d-126">Once all fields are populated, select "Preview Solution" for a preview of the solution within the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-126">Once all fields are populated, select "Preview Solution" for a preview of the solution within the Marketplace.</span></span>  <span data-ttu-id="a9f0d-127">You can revise and edit the text, images, and screenshot before clicking **Next**.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-127">You can revise and edit the text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="a9f0d-128">Import template and create package</span><span class="sxs-lookup"><span data-stu-id="a9f0d-128">Import template and create package</span></span>
<span data-ttu-id="a9f0d-129">In this section, you import the template and work with input for your solution.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-129">In this section, you import the template and work with input for your solution.</span></span>

1.  <span data-ttu-id="a9f0d-130">Click **Browse** and select the *azuredeploy.json* from the 101-Simple-Windows-VM folder in the downloaded templates.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-130">Click **Browse** and select the *azuredeploy.json* from the 101-Simple-Windows-VM folder in the downloaded templates.</span></span>

    ![screenshot of Marketplace Toolkit second screen](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="a9f0d-132">The Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in the template.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-132">The Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in the template.</span></span>  <span data-ttu-id="a9f0d-133">You can add additional steps and move inputs between steps.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="a9f0d-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="a9f0d-135">Specify the path to AzureGalleryPackager.exe.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-135">Specify the path to AzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="a9f0d-136">Click **Create** and the Marketplace Toolkit packages your solution into an .azpkg file.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-136">Click **Create** and the Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="a9f0d-137">Once complete, the wizard displays the path to your solution file and give you the option to continue publishing your package to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-137">Once complete, the wizard displays the path to your solution file and give you the option to continue publishing your package to Azure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="a9f0d-138">Publish marketplace items</span><span class="sxs-lookup"><span data-stu-id="a9f0d-138">Publish marketplace items</span></span>
<span data-ttu-id="a9f0d-139">In this section, you publish the marketplace item to your Azure Stack Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-139">In this section, you publish the marketplace item to your Azure Stack Marketplace.</span></span>

![screenshot of Marketplace Toolkit first screen](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="a9f0d-141">The wizard requires information to publish your solution:</span><span class="sxs-lookup"><span data-stu-id="a9f0d-141">The wizard requires information to publish your solution:</span></span>
    
    |<span data-ttu-id="a9f0d-142">Field</span><span class="sxs-lookup"><span data-stu-id="a9f0d-142">Field</span></span>|<span data-ttu-id="a9f0d-143">Description</span><span class="sxs-lookup"><span data-stu-id="a9f0d-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="a9f0d-144">Service Admin Name</span><span class="sxs-lookup"><span data-stu-id="a9f0d-144">Service Admin Name</span></span> | <span data-ttu-id="a9f0d-145">Service Administrator account.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-145">Service Administrator account.</span></span>  <span data-ttu-id="a9f0d-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="a9f0d-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="a9f0d-147">Password</span><span class="sxs-lookup"><span data-stu-id="a9f0d-147">Password</span></span> | <span data-ttu-id="a9f0d-148">Password for Service Administrator account.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="a9f0d-149">API Endpoint</span><span class="sxs-lookup"><span data-stu-id="a9f0d-149">API Endpoint</span></span> | <span data-ttu-id="a9f0d-150">Azure Stack Azure Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="a9f0d-151">Example: management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="a9f0d-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="a9f0d-152">Click **Publish** and the publishing log is displayed.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-152">Click **Publish** and the publishing log is displayed.</span></span>
3.  <span data-ttu-id="a9f0d-153">You are now able to deploy your published item via the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-153">You are now able to deploy your published item via the Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="a9f0d-154">Use a parameters file</span><span class="sxs-lookup"><span data-stu-id="a9f0d-154">Use a parameters file</span></span>
<span data-ttu-id="a9f0d-155">You can also use a parameters file to complete the marketplace item information.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-155">You can also use a parameters file to complete the marketplace item information.</span></span>  

<span data-ttu-id="a9f0d-156">The Marketplace Toolkit includes a *solution.parameters.ps1* you can use to create your own parameters file.</span><span class="sxs-lookup"><span data-stu-id="a9f0d-156">The Marketplace Toolkit includes a *solution.parameters.ps1* you can use to create your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="a9f0d-157">Support files</span><span class="sxs-lookup"><span data-stu-id="a9f0d-157">Support files</span></span>
| <span data-ttu-id="a9f0d-158">Description</span><span class="sxs-lookup"><span data-stu-id="a9f0d-158">Description</span></span> | <span data-ttu-id="a9f0d-159">Sample</span><span class="sxs-lookup"><span data-stu-id="a9f0d-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="a9f0d-160">40x40 .png icon</span><span class="sxs-lookup"><span data-stu-id="a9f0d-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="a9f0d-161">90x90 .png icon</span><span class="sxs-lookup"><span data-stu-id="a9f0d-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="a9f0d-162">115x115 .png icon</span><span class="sxs-lookup"><span data-stu-id="a9f0d-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="a9f0d-163">255x115 .png icon</span><span class="sxs-lookup"><span data-stu-id="a9f0d-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="a9f0d-164">533x324 .png thumbnail</span><span class="sxs-lookup"><span data-stu-id="a9f0d-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


