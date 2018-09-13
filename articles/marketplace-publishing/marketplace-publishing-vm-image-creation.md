---
title: Creating a virtual machine image for the Azure Marketplace | Microsoft Docs
description: Detailed instructions on how to create a virtual machine image for the Azure Marketplace for others to purchase.
services: Azure Marketplace
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: bf2ba6d31c170715a52b84439276c45665293c35
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790756"
---
# <a name="guide-to-create-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="c5183-103">Guide to create a virtual machine image for the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="c5183-103">Guide to create a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="c5183-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c5183-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span></span> <span data-ttu-id="c5183-105">Your VHDs are the foundation of your SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-105">Your VHDs are the foundation of your SKU.</span></span> <span data-ttu-id="c5183-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="c5183-107">This article covers both scenarios.</span><span class="sxs-lookup"><span data-stu-id="c5183-107">This article covers both scenarios.</span></span> <span data-ttu-id="c5183-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span><span class="sxs-lookup"><span data-stu-id="c5183-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="c5183-109">1. Define Offers and SKUs</span><span class="sxs-lookup"><span data-stu-id="c5183-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="c5183-110">In this section, you learn to define the offers and their associated SKUs.</span><span class="sxs-lookup"><span data-stu-id="c5183-110">In this section, you learn to define the offers and their associated SKUs.</span></span>

<span data-ttu-id="c5183-111">An offer is a "parent" to all of its SKUs.</span><span class="sxs-lookup"><span data-stu-id="c5183-111">An offer is a "parent" to all of its SKUs.</span></span> <span data-ttu-id="c5183-112">You can have multiple offers.</span><span class="sxs-lookup"><span data-stu-id="c5183-112">You can have multiple offers.</span></span> <span data-ttu-id="c5183-113">How you decide to structure your offers is up to you.</span><span class="sxs-lookup"><span data-stu-id="c5183-113">How you decide to structure your offers is up to you.</span></span> <span data-ttu-id="c5183-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span><span class="sxs-lookup"><span data-stu-id="c5183-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="c5183-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span><span class="sxs-lookup"><span data-stu-id="c5183-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span></span>

* <span data-ttu-id="c5183-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="c5183-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="c5183-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="c5183-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="c5183-118">A SKU is the commercial name for a VM image.</span><span class="sxs-lookup"><span data-stu-id="c5183-118">A SKU is the commercial name for a VM image.</span></span> <span data-ttu-id="c5183-119">A VM image contains one operating system disk and zero or more data disks.</span><span class="sxs-lookup"><span data-stu-id="c5183-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="c5183-120">It is essentially the complete storage profile for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c5183-120">It is essentially the complete storage profile for a virtual machine.</span></span> <span data-ttu-id="c5183-121">One VHD is needed per disk.</span><span class="sxs-lookup"><span data-stu-id="c5183-121">One VHD is needed per disk.</span></span> <span data-ttu-id="c5183-122">Even blank data disks require a VHD to be created.</span><span class="sxs-lookup"><span data-stu-id="c5183-122">Even blank data disks require a VHD to be created.</span></span>

<span data-ttu-id="c5183-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span></span> <span data-ttu-id="c5183-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span><span class="sxs-lookup"><span data-stu-id="c5183-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5183-125">**Do not change disk count in a new image version.**</span><span class="sxs-lookup"><span data-stu-id="c5183-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="c5183-126">If you must reconfigure Data disks in the image, define a new SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-126">If you must reconfigure Data disks in the image, define a new SKU.</span></span> <span data-ttu-id="c5183-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span><span class="sxs-lookup"><span data-stu-id="c5183-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="c5183-128">1.1 Add an offer</span><span class="sxs-lookup"><span data-stu-id="c5183-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="c5183-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span><span class="sxs-lookup"><span data-stu-id="c5183-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="c5183-130">Select the **Virtual Machines** tab of the Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-130">Select the **Virtual Machines** tab of the Publishing Portal.</span></span> <span data-ttu-id="c5183-131">In the prompted entry field, enter your offer name.</span><span class="sxs-lookup"><span data-stu-id="c5183-131">In the prompted entry field, enter your offer name.</span></span> <span data-ttu-id="c5183-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c5183-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span></span>
3. <span data-ttu-id="c5183-133">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5183-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="c5183-134">1.2 Define a SKU</span><span class="sxs-lookup"><span data-stu-id="c5183-134">1.2 Define a SKU</span></span>
<span data-ttu-id="c5183-135">After you have added an offer, you need to define and identify your SKUs.</span><span class="sxs-lookup"><span data-stu-id="c5183-135">After you have added an offer, you need to define and identify your SKUs.</span></span> <span data-ttu-id="c5183-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span><span class="sxs-lookup"><span data-stu-id="c5183-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="c5183-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span><span class="sxs-lookup"><span data-stu-id="c5183-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="c5183-138">**Add a SKU.**</span><span class="sxs-lookup"><span data-stu-id="c5183-138">**Add a SKU.**</span></span> <span data-ttu-id="c5183-139">The SKU requires an identifier, which is used in the URL.</span><span class="sxs-lookup"><span data-stu-id="c5183-139">The SKU requires an identifier, which is used in the URL.</span></span> <span data-ttu-id="c5183-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span><span class="sxs-lookup"><span data-stu-id="c5183-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c5183-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c5183-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="c5183-142">**Add a summary description for your SKU.**</span><span class="sxs-lookup"><span data-stu-id="c5183-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="c5183-143">Summary descriptions are visible to customers, so you should make them easily readable.</span><span class="sxs-lookup"><span data-stu-id="c5183-143">Summary descriptions are visible to customers, so you should make them easily readable.</span></span> <span data-ttu-id="c5183-144">This information does not need to be locked until the "Push to Staging" phase.</span><span class="sxs-lookup"><span data-stu-id="c5183-144">This information does not need to be locked until the "Push to Staging" phase.</span></span> <span data-ttu-id="c5183-145">Until then, you are free to edit it.</span><span class="sxs-lookup"><span data-stu-id="c5183-145">Until then, you are free to edit it.</span></span>
3. <span data-ttu-id="c5183-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c5183-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="c5183-147">2. Create an Azure-compatible VHD (Linux-based)</span><span class="sxs-lookup"><span data-stu-id="c5183-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="c5183-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c5183-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span></span> <span data-ttu-id="c5183-149">For a step-by-step walkthrough, refer to the following documentation: [Create a custom Linux VM image](../virtual-machines/linux/create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5183-149">For a step-by-step walkthrough, refer to the following documentation: [Create a custom Linux VM image](../virtual-machines/linux/create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="c5183-150">3. Create an Azure-compatible VHD (Windows-based)</span><span class="sxs-lookup"><span data-stu-id="c5183-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="c5183-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c5183-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-the-correct-base-vhds"></a><span data-ttu-id="c5183-152">3.1 Ensure that you are using the correct base VHDs</span><span class="sxs-lookup"><span data-stu-id="c5183-152">3.1 Ensure that you are using the correct base VHDs</span></span>
<span data-ttu-id="c5183-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c5183-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="c5183-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="c5183-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="c5183-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="c5183-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="c5183-156">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="c5183-156">SQL Server 2014</span></span> 
* <span data-ttu-id="c5183-157">SQL Server 2012 SP2</span><span class="sxs-lookup"><span data-stu-id="c5183-157">SQL Server 2012 SP2</span></span> 

<span data-ttu-id="c5183-158">These links can also be found in the Publishing Portal under the SKU page.</span><span class="sxs-lookup"><span data-stu-id="c5183-158">These links can also be found in the Publishing Portal under the SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="c5183-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span><span class="sxs-lookup"><span data-stu-id="c5183-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="c5183-160">3.2 Create your Windows-based VM</span><span class="sxs-lookup"><span data-stu-id="c5183-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="c5183-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="c5183-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="c5183-162">The following is an overview of the process:</span><span class="sxs-lookup"><span data-stu-id="c5183-162">The following is an overview of the process:</span></span>

1. <span data-ttu-id="c5183-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c5183-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![drawing][img-acom-1]
2. <span data-ttu-id="c5183-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="c5183-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span></span>
3. <span data-ttu-id="c5183-166">Follow the prompts to create a VM by using the base image you have selected.</span><span class="sxs-lookup"><span data-stu-id="c5183-166">Follow the prompts to create a VM by using the base image you have selected.</span></span> <span data-ttu-id="c5183-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span><span class="sxs-lookup"><span data-stu-id="c5183-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span></span>

    ![drawing][img-portal-vm-create]
4. <span data-ttu-id="c5183-169">Select the size of the VM to deploy:</span><span class="sxs-lookup"><span data-stu-id="c5183-169">Select the size of the VM to deploy:</span></span>

    <span data-ttu-id="c5183-170">a.</span><span class="sxs-lookup"><span data-stu-id="c5183-170">a.</span></span>    <span data-ttu-id="c5183-171">If you plan to develop the VHD on-premises, the size does not matter.</span><span class="sxs-lookup"><span data-stu-id="c5183-171">If you plan to develop the VHD on-premises, the size does not matter.</span></span> <span data-ttu-id="c5183-172">Consider using one of the smaller VMs.</span><span class="sxs-lookup"><span data-stu-id="c5183-172">Consider using one of the smaller VMs.</span></span>

    <span data-ttu-id="c5183-173">b.</span><span class="sxs-lookup"><span data-stu-id="c5183-173">b.</span></span>    <span data-ttu-id="c5183-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span><span class="sxs-lookup"><span data-stu-id="c5183-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span></span>

    <span data-ttu-id="c5183-175">c.</span><span class="sxs-lookup"><span data-stu-id="c5183-175">c.</span></span>    <span data-ttu-id="c5183-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span></span> <span data-ttu-id="c5183-177">It will provide the three recommended sizes provided by the publisher.</span><span class="sxs-lookup"><span data-stu-id="c5183-177">It will provide the three recommended sizes provided by the publisher.</span></span> <span data-ttu-id="c5183-178">(In this case, the publisher is Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="c5183-178">(In this case, the publisher is Microsoft.)</span></span>

    ![drawing][img-portal-vm-size]
5. <span data-ttu-id="c5183-180">Set properties:</span><span class="sxs-lookup"><span data-stu-id="c5183-180">Set properties:</span></span>

    <span data-ttu-id="c5183-181">a.</span><span class="sxs-lookup"><span data-stu-id="c5183-181">a.</span></span>    <span data-ttu-id="c5183-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="c5183-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="c5183-183">b.</span><span class="sxs-lookup"><span data-stu-id="c5183-183">b.</span></span>    <span data-ttu-id="c5183-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span><span class="sxs-lookup"><span data-stu-id="c5183-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span></span>

    <span data-ttu-id="c5183-185">c.</span><span class="sxs-lookup"><span data-stu-id="c5183-185">c.</span></span>    <span data-ttu-id="c5183-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span><span class="sxs-lookup"><span data-stu-id="c5183-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span></span>
6. <span data-ttu-id="c5183-187">Select the **Location** for deployment:</span><span class="sxs-lookup"><span data-stu-id="c5183-187">Select the **Location** for deployment:</span></span>

    <span data-ttu-id="c5183-188">a.</span><span class="sxs-lookup"><span data-stu-id="c5183-188">a.</span></span>    <span data-ttu-id="c5183-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span><span class="sxs-lookup"><span data-stu-id="c5183-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span></span>

    <span data-ttu-id="c5183-190">b.</span><span class="sxs-lookup"><span data-stu-id="c5183-190">b.</span></span>    <span data-ttu-id="c5183-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span><span class="sxs-lookup"><span data-stu-id="c5183-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span></span> <span data-ttu-id="c5183-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span><span class="sxs-lookup"><span data-stu-id="c5183-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![drawing][img-portal-vm-location]
7. <span data-ttu-id="c5183-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5183-194">Click **Create**.</span></span> <span data-ttu-id="c5183-195">The VM starts to deploy.</span><span class="sxs-lookup"><span data-stu-id="c5183-195">The VM starts to deploy.</span></span> <span data-ttu-id="c5183-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-the-cloud"></a><span data-ttu-id="c5183-197">3.3 Develop your VHD in the cloud</span><span class="sxs-lookup"><span data-stu-id="c5183-197">3.3 Develop your VHD in the cloud</span></span>
<span data-ttu-id="c5183-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="c5183-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="c5183-199">You connect to RDP with the user name and password specified during provisioning.</span><span class="sxs-lookup"><span data-stu-id="c5183-199">You connect to RDP with the user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5183-200">**Do not use discs managed.**</span><span class="sxs-lookup"><span data-stu-id="c5183-200">**Do not use discs managed.**</span></span> <span data-ttu-id="c5183-201">The virtual machine used to develop the VHD to the cloud must not be based on disks managed as it currently does not support the creation of an image from them.</span><span class="sxs-lookup"><span data-stu-id="c5183-201">The virtual machine used to develop the VHD to the cloud must not be based on disks managed as it currently does not support the creation of an image from them.</span></span>
> <span data-ttu-id="c5183-202">Creating the virtual machine in the optional feature change the default for disks managed.</span><span class="sxs-lookup"><span data-stu-id="c5183-202">Creating the virtual machine in the optional feature change the default for disks managed.</span></span>

> <span data-ttu-id="c5183-203">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="c5183-203">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="c5183-204">Downloading your VHD is not necessary if you are developing in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c5183-204">Downloading your VHD is not necessary if you are developing in the cloud.</span></span>
>
>

<span data-ttu-id="c5183-205">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="c5183-205">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="c5183-206">Select **All services** > **VMs**.</span><span class="sxs-lookup"><span data-stu-id="c5183-206">Select **All services** > **VMs**.</span></span>
2. <span data-ttu-id="c5183-207">The Virtual machines blade opens.</span><span class="sxs-lookup"><span data-stu-id="c5183-207">The Virtual machines blade opens.</span></span> <span data-ttu-id="c5183-208">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span><span class="sxs-lookup"><span data-stu-id="c5183-208">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span></span>
3. <span data-ttu-id="c5183-209">A blade opens that describes the selected VM.</span><span class="sxs-lookup"><span data-stu-id="c5183-209">A blade opens that describes the selected VM.</span></span> <span data-ttu-id="c5183-210">At the top, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c5183-210">At the top, click **Connect**.</span></span>
4. <span data-ttu-id="c5183-211">You are prompted to enter the user name and password that you specified during provisioning.</span><span class="sxs-lookup"><span data-stu-id="c5183-211">You are prompted to enter the user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="c5183-212">**Connect via RDP using PowerShell**</span><span class="sxs-lookup"><span data-stu-id="c5183-212">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="c5183-213">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span><span class="sxs-lookup"><span data-stu-id="c5183-213">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="c5183-214">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span><span class="sxs-lookup"><span data-stu-id="c5183-214">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span></span> <span data-ttu-id="c5183-215">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span><span class="sxs-lookup"><span data-stu-id="c5183-215">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="c5183-216">In the Microsoft Azure portal, select **All services** > **VMs**.</span><span class="sxs-lookup"><span data-stu-id="c5183-216">In the Microsoft Azure portal, select **All services** > **VMs**.</span></span>
2. <span data-ttu-id="c5183-217">The Virtual machines blade opens.</span><span class="sxs-lookup"><span data-stu-id="c5183-217">The Virtual machines blade opens.</span></span> <span data-ttu-id="c5183-218">Select the VM that you deployed.</span><span class="sxs-lookup"><span data-stu-id="c5183-218">Select the VM that you deployed.</span></span>
3. <span data-ttu-id="c5183-219">A blade opens that describes the selected VM.</span><span class="sxs-lookup"><span data-stu-id="c5183-219">A blade opens that describes the selected VM.</span></span>
4. <span data-ttu-id="c5183-220">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="c5183-220">Click **Properties**.</span></span>
5. <span data-ttu-id="c5183-221">The first portion of the domain name is the service name.</span><span class="sxs-lookup"><span data-stu-id="c5183-221">The first portion of the domain name is the service name.</span></span> <span data-ttu-id="c5183-222">The host name is the VM name.</span><span class="sxs-lookup"><span data-stu-id="c5183-222">The host name is the VM name.</span></span>

    ![drawing][img-portal-vm-rdp]
6. <span data-ttu-id="c5183-224">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span><span class="sxs-lookup"><span data-stu-id="c5183-224">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="c5183-225">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5183-225">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="c5183-226">**Configure a VM and create your SKU**</span><span class="sxs-lookup"><span data-stu-id="c5183-226">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="c5183-227">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-227">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span></span> <span data-ttu-id="c5183-228">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5183-228">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-the-correct-vhd-size"></a><span data-ttu-id="c5183-229">3.4 Choose the correct VHD size</span><span class="sxs-lookup"><span data-stu-id="c5183-229">3.4 Choose the correct VHD size</span></span>
<span data-ttu-id="c5183-230">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span><span class="sxs-lookup"><span data-stu-id="c5183-230">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="c5183-231">If the physical size is less than 128 GB, the VHD should be sparse.</span><span class="sxs-lookup"><span data-stu-id="c5183-231">If the physical size is less than 128 GB, the VHD should be sparse.</span></span> <span data-ttu-id="c5183-232">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span><span class="sxs-lookup"><span data-stu-id="c5183-232">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span></span>  

<span data-ttu-id="c5183-233">Data disks can be as large as 1 TB.</span><span class="sxs-lookup"><span data-stu-id="c5183-233">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="c5183-234">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span><span class="sxs-lookup"><span data-stu-id="c5183-234">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span></span> <span data-ttu-id="c5183-235">Data disk VHDs should be created as a fixed-format VHD.</span><span class="sxs-lookup"><span data-stu-id="c5183-235">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="c5183-236">They should also be sparse.</span><span class="sxs-lookup"><span data-stu-id="c5183-236">They should also be sparse.</span></span> <span data-ttu-id="c5183-237">Data disks can be empty or contain data.</span><span class="sxs-lookup"><span data-stu-id="c5183-237">Data disks can be empty or contain data.</span></span>

### <a name="35-install-the-latest-windows-patches"></a><span data-ttu-id="c5183-238">3.5 Install the latest Windows patches</span><span class="sxs-lookup"><span data-stu-id="c5183-238">3.5 Install the latest Windows patches</span></span>
<span data-ttu-id="c5183-239">The base images contain the latest patches up to their published date.</span><span class="sxs-lookup"><span data-stu-id="c5183-239">The base images contain the latest patches up to their published date.</span></span> <span data-ttu-id="c5183-240">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span><span class="sxs-lookup"><span data-stu-id="c5183-240">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="c5183-241">3.6 Perform additional configuration and schedule tasks as necessary</span><span class="sxs-lookup"><span data-stu-id="c5183-241">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="c5183-242">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span><span class="sxs-lookup"><span data-stu-id="c5183-242">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span></span>

* <span data-ttu-id="c5183-243">It is a best practice to have the task delete itself upon successful execution.</span><span class="sxs-lookup"><span data-stu-id="c5183-243">It is a best practice to have the task delete itself upon successful execution.</span></span>
* <span data-ttu-id="c5183-244">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span><span class="sxs-lookup"><span data-stu-id="c5183-244">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span></span> <span data-ttu-id="c5183-245">Drive C is the operating system disk, and drive D is the temporary local disk.</span><span class="sxs-lookup"><span data-stu-id="c5183-245">Drive C is the operating system disk, and drive D is the temporary local disk.</span></span>

### <a name="37-generalize-the-image"></a><span data-ttu-id="c5183-246">3.7 Generalize the image</span><span class="sxs-lookup"><span data-stu-id="c5183-246">3.7 Generalize the image</span></span>
<span data-ttu-id="c5183-247">All images in the Azure Marketplace must be reusable in a generic fashion.</span><span class="sxs-lookup"><span data-stu-id="c5183-247">All images in the Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="c5183-248">In other words, the operating system VHD must be generalized:</span><span class="sxs-lookup"><span data-stu-id="c5183-248">In other words, the operating system VHD must be generalized:</span></span>

* <span data-ttu-id="c5183-249">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span><span class="sxs-lookup"><span data-stu-id="c5183-249">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span></span>
* <span data-ttu-id="c5183-250">You can run the following command from the directory %windir%\System32\Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c5183-250">You can run the following command from the directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="c5183-251">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5183-251">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="c5183-252">4. Deploy a VM from your VHDs</span><span class="sxs-lookup"><span data-stu-id="c5183-252">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="c5183-253">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span><span class="sxs-lookup"><span data-stu-id="c5183-253">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="c5183-254">Then you can test that image.</span><span class="sxs-lookup"><span data-stu-id="c5183-254">Then you can test that image.</span></span> <span data-ttu-id="c5183-255">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span><span class="sxs-lookup"><span data-stu-id="c5183-255">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span></span>

<span data-ttu-id="c5183-256">To learn more about VM images, review the following blog posts:</span><span class="sxs-lookup"><span data-stu-id="c5183-256">To learn more about VM images, review the following blog posts:</span></span>

* [<span data-ttu-id="c5183-257">VM Image</span><span class="sxs-lookup"><span data-stu-id="c5183-257">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="c5183-258">VM Image PowerShell How To</span><span class="sxs-lookup"><span data-stu-id="c5183-258">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="c5183-259">About VM images in Azure</span><span class="sxs-lookup"><span data-stu-id="c5183-259">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-the-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="c5183-260">Set up the necessary tools, PowerShell and Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5183-260">Set up the necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="c5183-261">How to setup PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5183-261">How to setup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="c5183-262">How to setup Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5183-262">How to setup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="c5183-263">4.1 Create a user VM image</span><span class="sxs-lookup"><span data-stu-id="c5183-263">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="c5183-264">Capture VM</span><span class="sxs-lookup"><span data-stu-id="c5183-264">Capture VM</span></span>
<span data-ttu-id="c5183-265">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c5183-265">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="c5183-266">API</span><span class="sxs-lookup"><span data-stu-id="c5183-266">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="c5183-267">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5183-267">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c5183-268">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5183-268">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="c5183-269">Generalize Image</span><span class="sxs-lookup"><span data-stu-id="c5183-269">Generalize Image</span></span>
<span data-ttu-id="c5183-270">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c5183-270">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="c5183-271">API</span><span class="sxs-lookup"><span data-stu-id="c5183-271">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="c5183-272">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5183-272">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c5183-273">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5183-273">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="c5183-274">4.2 Deploy a VM from a user VM image</span><span class="sxs-lookup"><span data-stu-id="c5183-274">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="c5183-275">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5183-275">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="c5183-276">**Deploy a VM from the current Azure portal**</span><span class="sxs-lookup"><span data-stu-id="c5183-276">**Deploy a VM from the current Azure portal**</span></span>

1. <span data-ttu-id="c5183-277">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span><span class="sxs-lookup"><span data-stu-id="c5183-277">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

2. <span data-ttu-id="c5183-278">Go to **My images**, and then select the VM image from which to deploy a VM:</span><span class="sxs-lookup"><span data-stu-id="c5183-278">Go to **My images**, and then select the VM image from which to deploy a VM:</span></span>

   1. <span data-ttu-id="c5183-279">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span><span class="sxs-lookup"><span data-stu-id="c5183-279">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="c5183-280">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span><span class="sxs-lookup"><span data-stu-id="c5183-280">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span></span> <span data-ttu-id="c5183-281">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span><span class="sxs-lookup"><span data-stu-id="c5183-281">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span></span>

      ![drawing][img-manage-vm-select]
3. <span data-ttu-id="c5183-283">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span><span class="sxs-lookup"><span data-stu-id="c5183-283">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="c5183-284">**Deploy a VM from PowerShell**</span><span class="sxs-lookup"><span data-stu-id="c5183-284">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="c5183-285">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5183-285">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="c5183-286">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span><span class="sxs-lookup"><span data-stu-id="c5183-286">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="c5183-287">5. Obtain certification for your VM image</span><span class="sxs-lookup"><span data-stu-id="c5183-287">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="c5183-288">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span><span class="sxs-lookup"><span data-stu-id="c5183-288">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span></span>

<span data-ttu-id="c5183-289">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span><span class="sxs-lookup"><span data-stu-id="c5183-289">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-the-certification-test-tool-for-azure-certified"></a><span data-ttu-id="c5183-290">5.1 Download and run the Certification Test Tool for Azure Certified</span><span class="sxs-lookup"><span data-stu-id="c5183-290">5.1 Download and run the Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="c5183-291">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c5183-291">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="c5183-292">It will verify that the guidance and requirements about preparing your VHD have been met.</span><span class="sxs-lookup"><span data-stu-id="c5183-292">It will verify that the guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="c5183-293">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span><span class="sxs-lookup"><span data-stu-id="c5183-293">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="c5183-294">The certification tool can be used with both Windows and Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="c5183-294">The certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="c5183-295">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span><span class="sxs-lookup"><span data-stu-id="c5183-295">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="c5183-296">First, download the certification tool at the [Microsoft download site][link-msft-download].</span><span class="sxs-lookup"><span data-stu-id="c5183-296">First, download the certification tool at the [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="c5183-297">Open the certification tool, and then click the **Start New Test** button.</span><span class="sxs-lookup"><span data-stu-id="c5183-297">Open the certification tool, and then click the **Start New Test** button.</span></span>
3. <span data-ttu-id="c5183-298">From the **Test Information** screen, enter a name for the test run.</span><span class="sxs-lookup"><span data-stu-id="c5183-298">From the **Test Information** screen, enter a name for the test run.</span></span>
4. <span data-ttu-id="c5183-299">Choose whether your VM is on Linux or Windows.</span><span class="sxs-lookup"><span data-stu-id="c5183-299">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="c5183-300">Depending on which you choose, select the subsequent options.</span><span class="sxs-lookup"><span data-stu-id="c5183-300">Depending on which you choose, select the subsequent options.</span></span>

### <a name="connect-the-certification-tool-to-a-linux-vm-image"></a><span data-ttu-id="c5183-301">**Connect the certification tool to a Linux VM image**</span><span class="sxs-lookup"><span data-stu-id="c5183-301">**Connect the certification tool to a Linux VM image**</span></span>
1. <span data-ttu-id="c5183-302">Select the SSH authentication mode: password or key file.</span><span class="sxs-lookup"><span data-stu-id="c5183-302">Select the SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="c5183-303">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span><span class="sxs-lookup"><span data-stu-id="c5183-303">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="c5183-304">If using key file authentication, enter the DNS name, user name, and private key location.</span><span class="sxs-lookup"><span data-stu-id="c5183-304">If using key file authentication, enter the DNS name, user name, and private key location.</span></span>

   ![Password authentication of Linux VM Image][img-cert-vm-pswd-lnx]

   ![Key file authentication of Linux VM Image][img-cert-vm-key-lnx]

### <a name="connect-the-certification-tool-to-a-windows-based-vm-image"></a><span data-ttu-id="c5183-307">**Connect the certification tool to a Windows-based VM image**</span><span class="sxs-lookup"><span data-stu-id="c5183-307">**Connect the certification tool to a Windows-based VM image**</span></span>
1. <span data-ttu-id="c5183-308">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="c5183-308">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="c5183-309">Enter the user name and password.</span><span class="sxs-lookup"><span data-stu-id="c5183-309">Enter the user name and password.</span></span>

   ![Password authentication of Windows VM Image][img-cert-vm-pswd-win]

<span data-ttu-id="c5183-311">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="c5183-311">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="c5183-312">After a connection is established, select **Next** to start the test.</span><span class="sxs-lookup"><span data-stu-id="c5183-312">After a connection is established, select **Next** to start the test.</span></span>

<span data-ttu-id="c5183-313">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span><span class="sxs-lookup"><span data-stu-id="c5183-313">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span></span>

![Test cases for Linux VM Image][img-cert-vm-test-lnx]

![Test cases for Windows VM Image][img-cert-vm-test-win]

<span data-ttu-id="c5183-316">If any of the tests fail, your image will not be certified.</span><span class="sxs-lookup"><span data-stu-id="c5183-316">If any of the tests fail, your image will not be certified.</span></span> <span data-ttu-id="c5183-317">If this occurs, review the requirements and make any necessary changes.</span><span class="sxs-lookup"><span data-stu-id="c5183-317">If this occurs, review the requirements and make any necessary changes.</span></span>

<span data-ttu-id="c5183-318">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span><span class="sxs-lookup"><span data-stu-id="c5183-318">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="c5183-319">Complete the questions, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="c5183-319">Complete the questions, and then select **Next**.</span></span>

![Certification Tool Questionnaire][img-cert-vm-questionnaire]

![Certification Tool Questionnaire][img-cert-vm-questionnaire-2]

<span data-ttu-id="c5183-322">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span><span class="sxs-lookup"><span data-stu-id="c5183-322">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="c5183-323">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span><span class="sxs-lookup"><span data-stu-id="c5183-323">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span></span> <span data-ttu-id="c5183-324">Save the results in the same container as your VHDs.</span><span class="sxs-lookup"><span data-stu-id="c5183-324">Save the results in the same container as your VHDs.</span></span>

![Save certification test results][img-cert-vm-results]

### <a name="52-get-the-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="c5183-326">5.2 Get the shared access signature URI for your VM images</span><span class="sxs-lookup"><span data-stu-id="c5183-326">5.2 Get the shared access signature URI for your VM images</span></span>
<span data-ttu-id="c5183-327">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-327">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span></span> <span data-ttu-id="c5183-328">Microsoft needs access to these VHDs during the certification process.</span><span class="sxs-lookup"><span data-stu-id="c5183-328">Microsoft needs access to these VHDs during the certification process.</span></span> <span data-ttu-id="c5183-329">Therefore, you need to create a shared access signature URI for each VHD.</span><span class="sxs-lookup"><span data-stu-id="c5183-329">Therefore, you need to create a shared access signature URI for each VHD.</span></span> <span data-ttu-id="c5183-330">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-330">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span></span>

<span data-ttu-id="c5183-331">The shared access signature URI created should adhere to the following requirements:</span><span class="sxs-lookup"><span data-stu-id="c5183-331">The shared access signature URI created should adhere to the following requirements:</span></span>

<span data-ttu-id="c5183-332">Note:The following instructions are applicable only for unmanaged disks which are the only kind supported.</span><span class="sxs-lookup"><span data-stu-id="c5183-332">Note:The following instructions are applicable only for unmanaged disks which are the only kind supported.</span></span>

* <span data-ttu-id="c5183-333">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span><span class="sxs-lookup"><span data-stu-id="c5183-333">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="c5183-334">Do not provide Write or Delete access.</span><span class="sxs-lookup"><span data-stu-id="c5183-334">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="c5183-335">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span><span class="sxs-lookup"><span data-stu-id="c5183-335">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span></span>
* <span data-ttu-id="c5183-336">To safeguard for UTC time, select the day before the current date.</span><span class="sxs-lookup"><span data-stu-id="c5183-336">To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c5183-337">For example, if the current date is October 6, 2014, select 10/5/2014.</span><span class="sxs-lookup"><span data-stu-id="c5183-337">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="c5183-338">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c5183-338">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="c5183-339">Following are the 3 recommended tools:</span><span class="sxs-lookup"><span data-stu-id="c5183-339">Following are the 3 recommended tools:</span></span>

1.  <span data-ttu-id="c5183-340">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c5183-340">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="c5183-341">Microsoft Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c5183-341">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="c5183-342">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5183-342">Azure CLI</span></span>

<span data-ttu-id="c5183-343">**Azure Storage Explorer (Recommended for Windows Users)**</span><span class="sxs-lookup"><span data-stu-id="c5183-343">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="c5183-344">Following are the steps for generating SAS URL by using Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c5183-344">Following are the steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="c5183-345">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span><span class="sxs-lookup"><span data-stu-id="c5183-345">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="c5183-346">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span><span class="sxs-lookup"><span data-stu-id="c5183-346">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="c5183-348">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span><span class="sxs-lookup"><span data-stu-id="c5183-348">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="c5183-350">After it is installed, open the application.</span><span class="sxs-lookup"><span data-stu-id="c5183-350">After it is installed, open the application.</span></span>
4. <span data-ttu-id="c5183-351">Click **Add Account**.</span><span class="sxs-lookup"><span data-stu-id="c5183-351">Click **Add Account**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="c5183-353">Specify the storage account name, storage account key, and storage endpoints domain.</span><span class="sxs-lookup"><span data-stu-id="c5183-353">Specify the storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="c5183-354">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-354">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="c5183-356">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span><span class="sxs-lookup"><span data-stu-id="c5183-356">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span></span> <span data-ttu-id="c5183-357">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span><span class="sxs-lookup"><span data-stu-id="c5183-357">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="c5183-359">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span><span class="sxs-lookup"><span data-stu-id="c5183-359">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span></span> <span data-ttu-id="c5183-360">Select the image file (.vhd) that needs to be submitted.</span><span class="sxs-lookup"><span data-stu-id="c5183-360">Select the image file (.vhd) that needs to be submitted.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="c5183-362">After selecting the .vhd file in the container, click the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="c5183-362">After selecting the .vhd file in the container, click the **Security** tab.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="c5183-364">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span><span class="sxs-lookup"><span data-stu-id="c5183-364">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="c5183-366">Follow the steps below to generate a shared access signature URI for the .vhd image:</span><span class="sxs-lookup"><span data-stu-id="c5183-366">Follow the steps below to generate a shared access signature URI for the .vhd image:</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="c5183-368">a.</span><span class="sxs-lookup"><span data-stu-id="c5183-368">a.</span></span> <span data-ttu-id="c5183-369">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span><span class="sxs-lookup"><span data-stu-id="c5183-369">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c5183-370">For example, if the current date is October 6, 2014, select 10/5/2014.</span><span class="sxs-lookup"><span data-stu-id="c5183-370">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="c5183-371">b.</span><span class="sxs-lookup"><span data-stu-id="c5183-371">b.</span></span> <span data-ttu-id="c5183-372">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span><span class="sxs-lookup"><span data-stu-id="c5183-372">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span></span>

    <span data-ttu-id="c5183-373">c.</span><span class="sxs-lookup"><span data-stu-id="c5183-373">c.</span></span> <span data-ttu-id="c5183-374">**Actions permitted:** Select the **List** and **Read** permissions.</span><span class="sxs-lookup"><span data-stu-id="c5183-374">**Actions permitted:** Select the **List** and **Read** permissions.</span></span>

    <span data-ttu-id="c5183-375">d.</span><span class="sxs-lookup"><span data-stu-id="c5183-375">d.</span></span> <span data-ttu-id="c5183-376">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span><span class="sxs-lookup"><span data-stu-id="c5183-376">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span></span>

    <span data-ttu-id="c5183-377">e.</span><span class="sxs-lookup"><span data-stu-id="c5183-377">e.</span></span> <span data-ttu-id="c5183-378">Click **Generate Signature**.</span><span class="sxs-lookup"><span data-stu-id="c5183-378">Click **Generate Signature**.</span></span>

    <span data-ttu-id="c5183-379">f.</span><span class="sxs-lookup"><span data-stu-id="c5183-379">f.</span></span> <span data-ttu-id="c5183-380">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span><span class="sxs-lookup"><span data-stu-id="c5183-380">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span></span>

       - <span data-ttu-id="c5183-381">Make sure that your image file name and **".vhd"** are in the URI.</span><span class="sxs-lookup"><span data-stu-id="c5183-381">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
       - <span data-ttu-id="c5183-382">At the end of the signature, make sure that **"=rl"** appears.</span><span class="sxs-lookup"><span data-stu-id="c5183-382">At the end of the signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="c5183-383">This demonstrates that Read and List access was provided successfully.</span><span class="sxs-lookup"><span data-stu-id="c5183-383">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="c5183-384">In middle of the signature, make sure that **"sr=c"** appears.</span><span class="sxs-lookup"><span data-stu-id="c5183-384">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="c5183-385">This demonstrates that you have container level access</span><span class="sxs-lookup"><span data-stu-id="c5183-385">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="c5183-386">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span><span class="sxs-lookup"><span data-stu-id="c5183-386">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="c5183-387">It should start the download process.</span><span class="sxs-lookup"><span data-stu-id="c5183-387">It should start the download process.</span></span>

12. <span data-ttu-id="c5183-388">Copy the shared access signature URI.</span><span class="sxs-lookup"><span data-stu-id="c5183-388">Copy the shared access signature URI.</span></span> <span data-ttu-id="c5183-389">This is the URI to paste into the Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-389">This is the URI to paste into the Publishing Portal.</span></span>

13. <span data-ttu-id="c5183-390">Repeat steps 6-10 for each VHD in the SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-390">Repeat steps 6-10 for each VHD in the SKU.</span></span>

<span data-ttu-id="c5183-391">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="c5183-391">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="c5183-392">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c5183-392">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="c5183-393">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span><span class="sxs-lookup"><span data-stu-id="c5183-393">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="c5183-394">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span><span class="sxs-lookup"><span data-stu-id="c5183-394">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="c5183-396">After it is installed, open the application.</span><span class="sxs-lookup"><span data-stu-id="c5183-396">After it is installed, open the application.</span></span>

3.  <span data-ttu-id="c5183-397">Click **Add Account**.</span><span class="sxs-lookup"><span data-stu-id="c5183-397">Click **Add Account**.</span></span>

4.  <span data-ttu-id="c5183-398">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span><span class="sxs-lookup"><span data-stu-id="c5183-398">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="c5183-400">Go to storage account and select the Container</span><span class="sxs-lookup"><span data-stu-id="c5183-400">Go to storage account and select the Container</span></span>

6.  <span data-ttu-id="c5183-401">Select **“Get Share Access Signature..”**</span><span class="sxs-lookup"><span data-stu-id="c5183-401">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="c5183-402">by using Right Click of the **container**</span><span class="sxs-lookup"><span data-stu-id="c5183-402">by using Right Click of the **container**</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="c5183-404">Update Start time, Expiry time and Permissions as per following</span><span class="sxs-lookup"><span data-stu-id="c5183-404">Update Start time, Expiry time and Permissions as per following</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="c5183-406">a.</span><span class="sxs-lookup"><span data-stu-id="c5183-406">a.</span></span>  <span data-ttu-id="c5183-407">**Start Time:** To safeguard for UTC time, select the day before the current date.</span><span class="sxs-lookup"><span data-stu-id="c5183-407">**Start Time:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c5183-408">For example, if the current date is October 6, 2014, select 10/5/2014.</span><span class="sxs-lookup"><span data-stu-id="c5183-408">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="c5183-409">b.</span><span class="sxs-lookup"><span data-stu-id="c5183-409">b.</span></span>  <span data-ttu-id="c5183-410">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span><span class="sxs-lookup"><span data-stu-id="c5183-410">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span></span>

    <span data-ttu-id="c5183-411">c.</span><span class="sxs-lookup"><span data-stu-id="c5183-411">c.</span></span>  <span data-ttu-id="c5183-412">**Permissions:** Select the **List** and **Read** permissions</span><span class="sxs-lookup"><span data-stu-id="c5183-412">**Permissions:** Select the **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="c5183-413">Copy Container shared access signature URI</span><span class="sxs-lookup"><span data-stu-id="c5183-413">Copy Container shared access signature URI</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="c5183-415">Generated SAS URL is for container Level and now we need to add VHD name in it.</span><span class="sxs-lookup"><span data-stu-id="c5183-415">Generated SAS URL is for container Level and now we need to add VHD name in it.</span></span>

    <span data-ttu-id="c5183-416">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="c5183-416">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="c5183-417">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="c5183-417">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="c5183-418">Example:</span><span class="sxs-lookup"><span data-stu-id="c5183-418">Example:</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="c5183-420">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="c5183-420">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="c5183-421">Make sure that your image file name and **".vhd"** are in the URI.</span><span class="sxs-lookup"><span data-stu-id="c5183-421">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
    - <span data-ttu-id="c5183-422">In middle of the signature, make sure that **"sp=rl"** appears.</span><span class="sxs-lookup"><span data-stu-id="c5183-422">In middle of the signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="c5183-423">This demonstrates that Read and List access was provided successfully.</span><span class="sxs-lookup"><span data-stu-id="c5183-423">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="c5183-424">In middle of the signature, make sure that **"sr=c"** appears.</span><span class="sxs-lookup"><span data-stu-id="c5183-424">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="c5183-425">This demonstrates that you have container level access</span><span class="sxs-lookup"><span data-stu-id="c5183-425">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="c5183-426">To ensure that the generated shared access signature URI works, test it in browser.</span><span class="sxs-lookup"><span data-stu-id="c5183-426">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="c5183-427">It should start the download process</span><span class="sxs-lookup"><span data-stu-id="c5183-427">It should start the download process</span></span>

10. <span data-ttu-id="c5183-428">Copy the shared access signature URI.</span><span class="sxs-lookup"><span data-stu-id="c5183-428">Copy the shared access signature URI.</span></span> <span data-ttu-id="c5183-429">This is the URI to paste into the Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-429">This is the URI to paste into the Publishing Portal.</span></span>

11. <span data-ttu-id="c5183-430">Repeat these steps for each VHD in the SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-430">Repeat these steps for each VHD in the SKU.</span></span>

<span data-ttu-id="c5183-431">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span><span class="sxs-lookup"><span data-stu-id="c5183-431">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="c5183-432">Following are the steps for generating SAS URL by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5183-432">Following are the steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="c5183-433">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span><span class="sxs-lookup"><span data-stu-id="c5183-433">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="c5183-434">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span><span class="sxs-lookup"><span data-stu-id="c5183-434">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="c5183-435">Once it is downloaded, please install</span><span class="sxs-lookup"><span data-stu-id="c5183-435">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="c5183-436">Create a PowerShell (or other script executable) file with following code and save it locally</span><span class="sxs-lookup"><span data-stu-id="c5183-436">Create a PowerShell (or other script executable) file with following code and save it locally</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="c5183-437">Update the following parameters in above</span><span class="sxs-lookup"><span data-stu-id="c5183-437">Update the following parameters in above</span></span>

    <span data-ttu-id="c5183-438">a.</span><span class="sxs-lookup"><span data-stu-id="c5183-438">a.</span></span> <span data-ttu-id="c5183-439">**`<StorageAccountName>`**: Give your storage account name</span><span class="sxs-lookup"><span data-stu-id="c5183-439">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="c5183-440">b.</span><span class="sxs-lookup"><span data-stu-id="c5183-440">b.</span></span> <span data-ttu-id="c5183-441">**`<Storage Account Key>`**: Give your storage account key</span><span class="sxs-lookup"><span data-stu-id="c5183-441">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="c5183-442">c.</span><span class="sxs-lookup"><span data-stu-id="c5183-442">c.</span></span> <span data-ttu-id="c5183-443">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span><span class="sxs-lookup"><span data-stu-id="c5183-443">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c5183-444">For example, if the current date is October 26, 2016, then value should be 10/25/2016.</span><span class="sxs-lookup"><span data-stu-id="c5183-444">For example, if the current date is October 26, 2016, then value should be 10/25/2016.</span></span> <span data-ttu-id="c5183-445">If using Azure CLI 2.0 (az command), provide both the date and time in the Start and End Dates, for example: 10-25-2016T00:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="c5183-445">If using Azure CLI 2.0 (az command), provide both the date and time in the Start and End Dates, for example: 10-25-2016T00:00:00Z.</span></span>

    <span data-ttu-id="c5183-446">d.</span><span class="sxs-lookup"><span data-stu-id="c5183-446">d.</span></span> <span data-ttu-id="c5183-447">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span><span class="sxs-lookup"><span data-stu-id="c5183-447">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span></span> <span data-ttu-id="c5183-448">The value should be **11/02/2016**.</span><span class="sxs-lookup"><span data-stu-id="c5183-448">The value should be **11/02/2016**.</span></span> <span data-ttu-id="c5183-449">If using Azure CLI 2.0 (az command), provide both the date and time in the Start and End Dates, for example: 11-02-2016T00:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="c5183-449">If using Azure CLI 2.0 (az command), provide both the date and time in the Start and End Dates, for example: 11-02-2016T00:00:00Z.</span></span>

    <span data-ttu-id="c5183-450">Following is the example code after updating proper parameters</span><span class="sxs-lookup"><span data-stu-id="c5183-450">Following is the example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Open Powershell editor with “Run as Administrator” mode and open file in step #3. <span data-ttu-id="c5183-452">You can use any script editor that is available on your OS.</span><span class="sxs-lookup"><span data-stu-id="c5183-452">You can use any script editor that is available on your OS.</span></span>

5.  <span data-ttu-id="c5183-453">Run the script and it will provide you the SAS URL for container level access</span><span class="sxs-lookup"><span data-stu-id="c5183-453">Run the script and it will provide you the SAS URL for container level access</span></span>

    <span data-ttu-id="c5183-454">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span><span class="sxs-lookup"><span data-stu-id="c5183-454">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="c5183-456">Now you will get container level SAS URL and you need to add VHD name in it.</span><span class="sxs-lookup"><span data-stu-id="c5183-456">Now you will get container level SAS URL and you need to add VHD name in it.</span></span>

    <span data-ttu-id="c5183-457">Container level SAS URL #</span><span class="sxs-lookup"><span data-stu-id="c5183-457">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="c5183-458">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="c5183-458">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="c5183-459">Example:</span><span class="sxs-lookup"><span data-stu-id="c5183-459">Example:</span></span>

    <span data-ttu-id="c5183-460">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span><span class="sxs-lookup"><span data-stu-id="c5183-460">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="c5183-461">Make sure that your image file name and ".vhd" are in the URI.</span><span class="sxs-lookup"><span data-stu-id="c5183-461">Make sure that your image file name and ".vhd" are in the URI.</span></span>
    -   <span data-ttu-id="c5183-462">In middle of the signature, make sure that "sp=rl" appears.</span><span class="sxs-lookup"><span data-stu-id="c5183-462">In middle of the signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="c5183-463">This demonstrates that Read and List access was provided successfully.</span><span class="sxs-lookup"><span data-stu-id="c5183-463">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="c5183-464">In middle of the signature, make sure that "sr=c" appears.</span><span class="sxs-lookup"><span data-stu-id="c5183-464">In middle of the signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="c5183-465">This demonstrates that you have container level access</span><span class="sxs-lookup"><span data-stu-id="c5183-465">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="c5183-466">To ensure that the generated shared access signature URI works, test it in browser.</span><span class="sxs-lookup"><span data-stu-id="c5183-466">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="c5183-467">It should start the download process</span><span class="sxs-lookup"><span data-stu-id="c5183-467">It should start the download process</span></span>

9.  <span data-ttu-id="c5183-468">Copy the shared access signature URI.</span><span class="sxs-lookup"><span data-stu-id="c5183-468">Copy the shared access signature URI.</span></span> <span data-ttu-id="c5183-469">This is the URI to paste into the Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="c5183-469">This is the URI to paste into the Publishing Portal.</span></span>

10. <span data-ttu-id="c5183-470">Repeat these steps for each VHD in the SKU.</span><span class="sxs-lookup"><span data-stu-id="c5183-470">Repeat these steps for each VHD in the SKU.</span></span>


### <a name="53-provide-information-about-the-vm-image-and-request-certification-in-the-publishing-portal"></a><span data-ttu-id="c5183-471">5.3 Provide information about the VM image and request certification in the Publishing Portal</span><span class="sxs-lookup"><span data-stu-id="c5183-471">5.3 Provide information about the VM image and request certification in the Publishing Portal</span></span>
<span data-ttu-id="c5183-472">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span><span class="sxs-lookup"><span data-stu-id="c5183-472">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span></span>

1. <span data-ttu-id="c5183-473">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span><span class="sxs-lookup"><span data-stu-id="c5183-473">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="c5183-474">Select the **VM images** tab.</span><span class="sxs-lookup"><span data-stu-id="c5183-474">Select the **VM images** tab.</span></span>
3. <span data-ttu-id="c5183-475">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span><span class="sxs-lookup"><span data-stu-id="c5183-475">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span></span>
4. <span data-ttu-id="c5183-476">Fill out the properties under the **SKUs** section.</span><span class="sxs-lookup"><span data-stu-id="c5183-476">Fill out the properties under the **SKUs** section.</span></span>
5. <span data-ttu-id="c5183-477">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span><span class="sxs-lookup"><span data-stu-id="c5183-477">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span></span>
6. <span data-ttu-id="c5183-478">In the **Operating system** box, describe the operating system.</span><span class="sxs-lookup"><span data-stu-id="c5183-478">In the **Operating system** box, describe the operating system.</span></span> <span data-ttu-id="c5183-479">Consider a format such as operating system family, type, version, and updates.</span><span class="sxs-lookup"><span data-stu-id="c5183-479">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="c5183-480">An example is "Windows Server Datacenter 2014 R2."</span><span class="sxs-lookup"><span data-stu-id="c5183-480">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="c5183-481">Select up to six recommended virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="c5183-481">Select up to six recommended virtual machine sizes.</span></span> <span data-ttu-id="c5183-482">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span><span class="sxs-lookup"><span data-stu-id="c5183-482">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span></span> <span data-ttu-id="c5183-483">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span><span class="sxs-lookup"><span data-stu-id="c5183-483">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span></span>
8. <span data-ttu-id="c5183-484">Enter the version.</span><span class="sxs-lookup"><span data-stu-id="c5183-484">Enter the version.</span></span> <span data-ttu-id="c5183-485">The version field encapsulates a semantic version to identify the product and its updates:</span><span class="sxs-lookup"><span data-stu-id="c5183-485">The version field encapsulates a semantic version to identify the product and its updates:</span></span>
   * <span data-ttu-id="c5183-486">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span><span class="sxs-lookup"><span data-stu-id="c5183-486">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="c5183-487">Images in different SKUs can have different major and minor versions.</span><span class="sxs-lookup"><span data-stu-id="c5183-487">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="c5183-488">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span><span class="sxs-lookup"><span data-stu-id="c5183-488">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="c5183-489">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span><span class="sxs-lookup"><span data-stu-id="c5183-489">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span></span>
10. <span data-ttu-id="c5183-490">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span><span class="sxs-lookup"><span data-stu-id="c5183-490">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span></span>
11. <span data-ttu-id="c5183-491">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span><span class="sxs-lookup"><span data-stu-id="c5183-491">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="c5183-493">Common SAS URL issues & fixes</span><span class="sxs-lookup"><span data-stu-id="c5183-493">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="c5183-494">Issue</span><span class="sxs-lookup"><span data-stu-id="c5183-494">Issue</span></span>|<span data-ttu-id="c5183-495">Failure Message</span><span class="sxs-lookup"><span data-stu-id="c5183-495">Failure Message</span></span>|<span data-ttu-id="c5183-496">Fix</span><span class="sxs-lookup"><span data-stu-id="c5183-496">Fix</span></span>|<span data-ttu-id="c5183-497">Documentation Link</span><span class="sxs-lookup"><span data-stu-id="c5183-497">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="c5183-498">Failure in copying images - "?" is not found in SAS url</span><span class="sxs-lookup"><span data-stu-id="c5183-498">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="c5183-499">Failure: Copying Images.</span><span class="sxs-lookup"><span data-stu-id="c5183-499">Failure: Copying Images.</span></span> <span data-ttu-id="c5183-500">Not able to download blob using provided SAS Uri.</span><span class="sxs-lookup"><span data-stu-id="c5183-500">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="c5183-501">Update the SAS Url using recommended tools</span><span class="sxs-lookup"><span data-stu-id="c5183-501">Update the SAS Url using recommended tools</span></span>|[https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c5183-502">Failure in copying images - “st” and “se” parameters not in SAS url</span><span class="sxs-lookup"><span data-stu-id="c5183-502">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="c5183-503">Failure: Copying Images.</span><span class="sxs-lookup"><span data-stu-id="c5183-503">Failure: Copying Images.</span></span> <span data-ttu-id="c5183-504">Not able to download blob using provided SAS Uri.</span><span class="sxs-lookup"><span data-stu-id="c5183-504">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="c5183-505">Update the SAS Url with Start and End dates on it</span><span class="sxs-lookup"><span data-stu-id="c5183-505">Update the SAS Url with Start and End dates on it</span></span>|[https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c5183-506">Failure in copying images - “sp=rl” not in SAS url</span><span class="sxs-lookup"><span data-stu-id="c5183-506">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="c5183-507">Failure: Copying Images.</span><span class="sxs-lookup"><span data-stu-id="c5183-507">Failure: Copying Images.</span></span> <span data-ttu-id="c5183-508">Not able to download blob using provided SAS Uri</span><span class="sxs-lookup"><span data-stu-id="c5183-508">Not able to download blob using provided SAS Uri</span></span>|<span data-ttu-id="c5183-509">Update the SAS Url with permissions set as “Read” & “List</span><span class="sxs-lookup"><span data-stu-id="c5183-509">Update the SAS Url with permissions set as “Read” & “List</span></span>|[https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c5183-510">Failure in copying images - SAS url have white spaces in vhd name</span><span class="sxs-lookup"><span data-stu-id="c5183-510">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="c5183-511">Failure: Copying Images.</span><span class="sxs-lookup"><span data-stu-id="c5183-511">Failure: Copying Images.</span></span> <span data-ttu-id="c5183-512">Not able to download blob using provided SAS Uri.</span><span class="sxs-lookup"><span data-stu-id="c5183-512">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="c5183-513">Update the SAS Url without white spaces</span><span class="sxs-lookup"><span data-stu-id="c5183-513">Update the SAS Url without white spaces</span></span>|[https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c5183-514">Failure in copying images – SAS Url Authorization error</span><span class="sxs-lookup"><span data-stu-id="c5183-514">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="c5183-515">Failure: Copying Images.</span><span class="sxs-lookup"><span data-stu-id="c5183-515">Failure: Copying Images.</span></span> <span data-ttu-id="c5183-516">Not able to download blob due to authorization error</span><span class="sxs-lookup"><span data-stu-id="c5183-516">Not able to download blob due to authorization error</span></span>|<span data-ttu-id="c5183-517">Regenerate the SAS Url</span><span class="sxs-lookup"><span data-stu-id="c5183-517">Regenerate the SAS Url</span></span>|[https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c5183-518">Failure in copying images – SAS Url "st" and "se" parameters do not have full date-time specification</span><span class="sxs-lookup"><span data-stu-id="c5183-518">Failure in copying images – SAS Url "st" and "se" parameters do not have full date-time specification</span></span>|<span data-ttu-id="c5183-519">Failure: Copying Images.</span><span class="sxs-lookup"><span data-stu-id="c5183-519">Failure: Copying Images.</span></span> <span data-ttu-id="c5183-520">Not able to download blob due to incorrect SAS Url</span><span class="sxs-lookup"><span data-stu-id="c5183-520">Not able to download blob due to incorrect SAS Url</span></span> |<span data-ttu-id="c5183-521">SAS Url Start and End Date parameters ("st", "se") are required to have full date-time specification, such as 11-02-2017T00:00:00Z, and not only the date or shortened versions for the time.</span><span class="sxs-lookup"><span data-stu-id="c5183-521">SAS Url Start and End Date parameters ("st", "se") are required to have full date-time specification, such as 11-02-2017T00:00:00Z, and not only the date or shortened versions for the time.</span></span> <span data-ttu-id="c5183-522">It is possible to encounter this scenario using Azure CLI 2.0 (az command).</span><span class="sxs-lookup"><span data-stu-id="c5183-522">It is possible to encounter this scenario using Azure CLI 2.0 (az command).</span></span> <span data-ttu-id="c5183-523">Be sure to provide the full date-time specification and regenerate the SAS Url.</span><span class="sxs-lookup"><span data-stu-id="c5183-523">Be sure to provide the full date-time specification and regenerate the SAS Url.</span></span>|[https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|

## <a name="next-step"></a><span data-ttu-id="c5183-524">Next step</span><span class="sxs-lookup"><span data-stu-id="c5183-524">Next step</span></span>
<span data-ttu-id="c5183-525">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span><span class="sxs-lookup"><span data-stu-id="c5183-525">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="c5183-526">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span><span class="sxs-lookup"><span data-stu-id="c5183-526">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c5183-527">See also</span><span class="sxs-lookup"><span data-stu-id="c5183-527">See also</span></span>
* [<span data-ttu-id="c5183-528">Getting started: How to publish an offer to the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="c5183-528">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
