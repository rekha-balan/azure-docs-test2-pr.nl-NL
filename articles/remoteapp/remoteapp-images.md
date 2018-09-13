---
title: What is in the Azure RemoteApp template images? | Microsoft Docs
description: Learn about the template images included with Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 348306795fd3c8275b21e4ec6dceae408916bf72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564082"
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a><span data-ttu-id="fd6e9-104">What is in the Azure RemoteApp template images?</span><span class="sxs-lookup"><span data-stu-id="fd6e9-104">What is in the Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fd6e9-105">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fd6e9-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fd6e9-107">Your Azure RemoteApp subscription includes three template images:</span><span class="sxs-lookup"><span data-stu-id="fd6e9-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="fd6e9-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fd6e9-108">Windows Server 2012</span></span>
* <span data-ttu-id="fd6e9-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="fd6e9-110">Microsoft Office 2013 Professional Plus (trial only)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd6e9-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="fd6e9-112">This means that you can share the programs or apps on the template images with your users.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-112">This means that you can share the programs or apps on the template images with your users.</span></span> <span data-ttu-id="fd6e9-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span></span>
> 
> <span data-ttu-id="fd6e9-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="fd6e9-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span></span>
> 
> 

<span data-ttu-id="fd6e9-116">Read on for details on what each image contains.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--the-vanilla-image"></a><span data-ttu-id="fd6e9-117">Windows Server 2012 R2  ("the vanilla image")</span><span class="sxs-lookup"><span data-stu-id="fd6e9-117">Windows Server 2012 R2  ("the vanilla image")</span></span>
<span data-ttu-id="fd6e9-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span><span class="sxs-lookup"><span data-stu-id="fd6e9-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="fd6e9-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="fd6e9-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="fd6e9-120">Desktop Experience</span><span class="sxs-lookup"><span data-stu-id="fd6e9-120">Desktop Experience</span></span>
* <span data-ttu-id="fd6e9-121">Ink and Handwriting Services</span><span class="sxs-lookup"><span data-stu-id="fd6e9-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="fd6e9-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="fd6e9-122">Media Foundation</span></span>
* <span data-ttu-id="fd6e9-123">Remote Desktop Session Host</span><span class="sxs-lookup"><span data-stu-id="fd6e9-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="fd6e9-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="fd6e9-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="fd6e9-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="fd6e9-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="fd6e9-126">WoW64 Support</span><span class="sxs-lookup"><span data-stu-id="fd6e9-126">WoW64 Support</span></span>

<span data-ttu-id="fd6e9-127">This image also has the following applications installed:</span><span class="sxs-lookup"><span data-stu-id="fd6e9-127">This image also has the following applications installed:</span></span>

* <span data-ttu-id="fd6e9-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="fd6e9-128">Adobe Flash Player</span></span>
* <span data-ttu-id="fd6e9-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="fd6e9-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="fd6e9-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="fd6e9-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="fd6e9-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="fd6e9-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="fd6e9-132">Microsoft Office 365 ProPlus (subscription required)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="fd6e9-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span></span>

<span data-ttu-id="fd6e9-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span><span class="sxs-lookup"><span data-stu-id="fd6e9-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="fd6e9-135">Access</span><span class="sxs-lookup"><span data-stu-id="fd6e9-135">Access</span></span>
* <span data-ttu-id="fd6e9-136">Excel</span><span class="sxs-lookup"><span data-stu-id="fd6e9-136">Excel</span></span>
* <span data-ttu-id="fd6e9-137">Lync</span><span class="sxs-lookup"><span data-stu-id="fd6e9-137">Lync</span></span>
* <span data-ttu-id="fd6e9-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="fd6e9-138">OneNote</span></span>
* <span data-ttu-id="fd6e9-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="fd6e9-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="fd6e9-140">Outlook</span></span>
* <span data-ttu-id="fd6e9-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="fd6e9-141">PowerPoint</span></span>
* <span data-ttu-id="fd6e9-142">Word</span><span class="sxs-lookup"><span data-stu-id="fd6e9-142">Word</span></span>
* <span data-ttu-id="fd6e9-143">Microsoft Office Proofing Tools</span><span class="sxs-lookup"><span data-stu-id="fd6e9-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="fd6e9-144">The image also includes Visio Pro and Project Pro.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-144">The image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="fd6e9-145">And the following applications, as well:</span><span class="sxs-lookup"><span data-stu-id="fd6e9-145">And the following applications, as well:</span></span>

* <span data-ttu-id="fd6e9-146">SQL Native client</span><span class="sxs-lookup"><span data-stu-id="fd6e9-146">SQL Native client</span></span>
* <span data-ttu-id="fd6e9-147">ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="fd6e9-147">ODBC Driver</span></span>
* <span data-ttu-id="fd6e9-148">SQL Server Data Mining client</span><span class="sxs-lookup"><span data-stu-id="fd6e9-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="fd6e9-149">MasterDataServices client</span><span class="sxs-lookup"><span data-stu-id="fd6e9-149">MasterDataServices client</span></span>
* <span data-ttu-id="fd6e9-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="fd6e9-150">Microsoft Publisher</span></span>
* <span data-ttu-id="fd6e9-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="fd6e9-151">PowerQuery</span></span>
* <span data-ttu-id="fd6e9-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="fd6e9-152">PowerMap</span></span>

<span data-ttu-id="fd6e9-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="fd6e9-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd6e9-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="fd6e9-155">Still have questions?</span><span class="sxs-lookup"><span data-stu-id="fd6e9-155">Still have questions?</span></span> <span data-ttu-id="fd6e9-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="fd6e9-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="fd6e9-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="fd6e9-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="fd6e9-159">Microsoft Office 2013 Professional Plus (trial only)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="fd6e9-160">During the free trial period, you can test the service with the Office 2013 image.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-160">During the free trial period, you can test the service with the Office 2013 image.</span></span>

<span data-ttu-id="fd6e9-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span><span class="sxs-lookup"><span data-stu-id="fd6e9-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="fd6e9-162">Access</span><span class="sxs-lookup"><span data-stu-id="fd6e9-162">Access</span></span>
* <span data-ttu-id="fd6e9-163">Excel</span><span class="sxs-lookup"><span data-stu-id="fd6e9-163">Excel</span></span>
* <span data-ttu-id="fd6e9-164">Lync</span><span class="sxs-lookup"><span data-stu-id="fd6e9-164">Lync</span></span>
* <span data-ttu-id="fd6e9-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="fd6e9-165">OneNote</span></span>
* <span data-ttu-id="fd6e9-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="fd6e9-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="fd6e9-167">Outlook</span></span>
* <span data-ttu-id="fd6e9-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="fd6e9-168">PowerPoint</span></span>
* <span data-ttu-id="fd6e9-169">Project</span><span class="sxs-lookup"><span data-stu-id="fd6e9-169">Project</span></span>
* <span data-ttu-id="fd6e9-170">Visio</span><span class="sxs-lookup"><span data-stu-id="fd6e9-170">Visio</span></span>
* <span data-ttu-id="fd6e9-171">Word</span><span class="sxs-lookup"><span data-stu-id="fd6e9-171">Word</span></span>
* <span data-ttu-id="fd6e9-172">Microsoft Office Proofing Tools</span><span class="sxs-lookup"><span data-stu-id="fd6e9-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd6e9-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="fd6e9-174">The Office 2013 Professional Plus image is intended for trial use only.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-174">The Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="fd6e9-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span><span class="sxs-lookup"><span data-stu-id="fd6e9-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span></span> <span data-ttu-id="fd6e9-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="fd6e9-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

