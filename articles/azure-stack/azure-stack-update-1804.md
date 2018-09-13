---
title: Azure Stack 1804 Update | Microsoft Docs
description: Learn about what's in the 1804 update for Azure Stack integrated systems, the known issues, and where to download the update.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2018
ms.author: brenduns
ms.reviewer: justini
ms.openlocfilehash: 0190298cbf6352feeb71e365f5815e174c9e30cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967589"
---
# <a name="azure-stack-1804-update"></a><span data-ttu-id="3a801-103">Azure Stack 1804 update</span><span class="sxs-lookup"><span data-stu-id="3a801-103">Azure Stack 1804 update</span></span>

<span data-ttu-id="3a801-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="3a801-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="3a801-105">This article describes the improvements and fixes in the 1804 update package, known issues for this release, and where to download the update.</span><span class="sxs-lookup"><span data-stu-id="3a801-105">This article describes the improvements and fixes in the 1804 update package, known issues for this release, and where to download the update.</span></span> <span data-ttu-id="3a801-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span><span class="sxs-lookup"><span data-stu-id="3a801-106">Known issues are divided into issues directly related to the update process and issues with the build (post-installation).</span></span>

> [!IMPORTANT]        
> <span data-ttu-id="3a801-107">This update package is only for Azure Stack integrated systems.</span><span class="sxs-lookup"><span data-stu-id="3a801-107">This update package is only for Azure Stack integrated systems.</span></span> <span data-ttu-id="3a801-108">Do not apply this update package to the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="3a801-108">Do not apply this update package to the Azure Stack Development Kit.</span></span>

## <a name="build-reference"></a><span data-ttu-id="3a801-109">Build reference</span><span class="sxs-lookup"><span data-stu-id="3a801-109">Build reference</span></span>    
<span data-ttu-id="3a801-110">The Azure Stack 1804 update build number is **20180513.1**.</span><span class="sxs-lookup"><span data-stu-id="3a801-110">The Azure Stack 1804 update build number is **20180513.1**.</span></span>   

### <a name="new-features"></a><span data-ttu-id="3a801-111">New features</span><span class="sxs-lookup"><span data-stu-id="3a801-111">New features</span></span>
<span data-ttu-id="3a801-112">This update includes the following improvements for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a801-112">This update includes the following improvements for Azure Stack.</span></span>

- <span data-ttu-id="3a801-113"><!-- 15028744 - IS -->  **Visual Studio support for disconnected Azure Stack deployments using AD FS**.</span><span class="sxs-lookup"><span data-stu-id="3a801-113"><!-- 15028744 - IS -->  **Visual Studio support for disconnected Azure Stack deployments using AD FS**.</span></span> <span data-ttu-id="3a801-114">Within Visual Studio you now can add subscriptions and authenticate using AD FS federated User credentials.</span><span class="sxs-lookup"><span data-stu-id="3a801-114">Within Visual Studio you now can add subscriptions and authenticate using AD FS federated User credentials.</span></span> 
 
- <span data-ttu-id="3a801-115"><!-- 1779474, 1779458 - IS --> **Use Av2 and F series virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="3a801-115"><!-- 1779474, 1779458 - IS --> **Use Av2 and F series virtual machines**.</span></span> <span data-ttu-id="3a801-116">Azure Stack can now use virtual machines based on the Av2-series and F-series virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="3a801-116">Azure Stack can now use virtual machines based on the Av2-series and F-series virtual machine sizes.</span></span> <span data-ttu-id="3a801-117">For more information see [Virtual machine sizes supported in Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-vm-sizes).</span><span class="sxs-lookup"><span data-stu-id="3a801-117">For more information see [Virtual machine sizes supported in Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-vm-sizes).</span></span> 

- <span data-ttu-id="3a801-118"><!-- 1759172 - IS, ASDK --> **New administrative subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="3a801-118"><!-- 1759172 - IS, ASDK --> **New administrative subscriptions**.</span></span> <span data-ttu-id="3a801-119">With 1804 there are two new subscription types available in the portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-119">With 1804 there are two new subscription types available in the portal.</span></span> <span data-ttu-id="3a801-120">These new subscription types are in addition to the Default Provider subscription and visible with new Azure Stack installations beginning with version 1804.</span><span class="sxs-lookup"><span data-stu-id="3a801-120">These new subscription types are in addition to the Default Provider subscription and visible with new Azure Stack installations beginning with version 1804.</span></span> <span data-ttu-id="3a801-121">*Do not use these new subscription types with this version of Azure Stack*.</span><span class="sxs-lookup"><span data-stu-id="3a801-121">*Do not use these new subscription types with this version of Azure Stack*.</span></span> <span data-ttu-id="3a801-122">We will announce the availability to use these subscription types in with a future update.</span><span class="sxs-lookup"><span data-stu-id="3a801-122">We will announce the availability to use these subscription types in with a future update.</span></span> 

  <span data-ttu-id="3a801-123">If you update Azure Stack to version 1804, the two new subscription types are not visible.</span><span class="sxs-lookup"><span data-stu-id="3a801-123">If you update Azure Stack to version 1804, the two new subscription types are not visible.</span></span> <span data-ttu-id="3a801-124">However, new deployments of Azure Stack integrated systems and installations of the Azure Stack Development Kit version 1804 or later have access to all three subscription types.</span><span class="sxs-lookup"><span data-stu-id="3a801-124">However, new deployments of Azure Stack integrated systems and installations of the Azure Stack Development Kit version 1804 or later have access to all three subscription types.</span></span>  

  <span data-ttu-id="3a801-125">These new subscription types are part of a larger change to secure the Default Provider subscription, and to make it easier to deploy shared resources like SQL Hosting servers.</span><span class="sxs-lookup"><span data-stu-id="3a801-125">These new subscription types are part of a larger change to secure the Default Provider subscription, and to make it easier to deploy shared resources like SQL Hosting servers.</span></span> <span data-ttu-id="3a801-126">As we add more parts of this larger change with future updates to Azure Stack, resources deployed under these new subscription types might be lost.</span><span class="sxs-lookup"><span data-stu-id="3a801-126">As we add more parts of this larger change with future updates to Azure Stack, resources deployed under these new subscription types might be lost.</span></span> 

  <span data-ttu-id="3a801-127">The three subscription types now visible are:</span><span class="sxs-lookup"><span data-stu-id="3a801-127">The three subscription types now visible are:</span></span>  
  - <span data-ttu-id="3a801-128">Default Provider subscription:  Continue to use this subscription type.</span><span class="sxs-lookup"><span data-stu-id="3a801-128">Default Provider subscription:  Continue to use this subscription type.</span></span> 
  - <span data-ttu-id="3a801-129">Metering subscription: *Do not use this subscription type.*</span><span class="sxs-lookup"><span data-stu-id="3a801-129">Metering subscription: *Do not use this subscription type.*</span></span>
  - <span data-ttu-id="3a801-130">Consumption subscription: *Do not use this subscription type*</span><span class="sxs-lookup"><span data-stu-id="3a801-130">Consumption subscription: *Do not use this subscription type*</span></span>

  



## <a name="fixed-issues"></a><span data-ttu-id="3a801-131">Fixed issues</span><span class="sxs-lookup"><span data-stu-id="3a801-131">Fixed issues</span></span>

- <span data-ttu-id="3a801-132"><!-- IS, ASDK -->  In the admin portal, you no longer have to refresh the Update tile before it displays information.</span><span class="sxs-lookup"><span data-stu-id="3a801-132"><!-- IS, ASDK -->  In the admin portal, you no longer have to refresh the Update tile before it displays information.</span></span>
 
- <span data-ttu-id="3a801-133"><!-- 2050709  -->  You can now use the admin portal to edit storage metrics for Blob service, Table service, and Queue service.</span><span class="sxs-lookup"><span data-stu-id="3a801-133"><!-- 2050709  -->  You can now use the admin portal to edit storage metrics for Blob service, Table service, and Queue service.</span></span>
 
- <span data-ttu-id="3a801-134"><!-- IS, ASDK --> Under **Networking**, when you click **Connection** to set up a VPN connection, **Site-to-site (IPsec)** is now the only available option.</span><span class="sxs-lookup"><span data-stu-id="3a801-134"><!-- IS, ASDK --> Under **Networking**, when you click **Connection** to set up a VPN connection, **Site-to-site (IPsec)** is now the only available option.</span></span>

- <span data-ttu-id="3a801-135">**Various fixes** for performance, stability, security, and the operating system that is used by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a801-135">**Various fixes** for performance, stability, security, and the operating system that is used by Azure Stack.</span></span>

## <a name="additional-releases-timed-with-this-update"></a><span data-ttu-id="3a801-136">Additional releases timed with this update</span><span class="sxs-lookup"><span data-stu-id="3a801-136">Additional releases timed with this update</span></span>  
<span data-ttu-id="3a801-137">The following are now available, but don't require Azure Stack update 1804.</span><span class="sxs-lookup"><span data-stu-id="3a801-137">The following are now available, but don't require Azure Stack update 1804.</span></span>
- <span data-ttu-id="3a801-138">**Update to the Microsoft Azure Stack System Center Operations Manager Monitoring Pack**.</span><span class="sxs-lookup"><span data-stu-id="3a801-138">**Update to the Microsoft Azure Stack System Center Operations Manager Monitoring Pack**.</span></span> <span data-ttu-id="3a801-139">A new version (1.0.3.0) of the Microsoft System Center Operations Manager Monitoring Pack for Azure Stack is available for [download](https://www.microsoft.com/download/details.aspx?id=55184).</span><span class="sxs-lookup"><span data-stu-id="3a801-139">A new version (1.0.3.0) of the Microsoft System Center Operations Manager Monitoring Pack for Azure Stack is available for [download](https://www.microsoft.com/download/details.aspx?id=55184).</span></span> <span data-ttu-id="3a801-140">With this version, you can use Service Principals when you add a connected Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="3a801-140">With this version, you can use Service Principals when you add a connected Azure Stack deployment.</span></span> <span data-ttu-id="3a801-141">This version also features an Update Management experience that allows you to take remediation action directly from within Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3a801-141">This version also features an Update Management experience that allows you to take remediation action directly from within Operations Manager.</span></span> <span data-ttu-id="3a801-142">There are also new dashboards that display resource providers, scale units, and scale unit nodes.</span><span class="sxs-lookup"><span data-stu-id="3a801-142">There are also new dashboards that display resource providers, scale units, and scale unit nodes.</span></span>

- <span data-ttu-id="3a801-143">**New Azure Stack Admin PowerShell Version 1.3.0**.</span><span class="sxs-lookup"><span data-stu-id="3a801-143">**New Azure Stack Admin PowerShell Version 1.3.0**.</span></span>  <span data-ttu-id="3a801-144">Azure Stack PowerShell 1.3.0 is now available for installation.</span><span class="sxs-lookup"><span data-stu-id="3a801-144">Azure Stack PowerShell 1.3.0 is now available for installation.</span></span> <span data-ttu-id="3a801-145">This version provides commands for all Admin resource providers to manage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a801-145">This version provides commands for all Admin resource providers to manage Azure Stack.</span></span>  <span data-ttu-id="3a801-146">With this release, some content will be deprecated from the Azure Stack Tools GitHub [repository](https://github.com/Azure/AzureStack-Tools).</span><span class="sxs-lookup"><span data-stu-id="3a801-146">With this release, some content will be deprecated from the Azure Stack Tools GitHub [repository](https://github.com/Azure/AzureStack-Tools).</span></span> 

   <span data-ttu-id="3a801-147">For installation details, follow the [instructions](azure-stack-powershell-install.md) or the [help](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.3.0) content for Azure Stack Module 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="3a801-147">For installation details, follow the [instructions](azure-stack-powershell-install.md) or the [help](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.3.0) content for Azure Stack Module 1.3.0.</span></span> 

- <span data-ttu-id="3a801-148">**Initial release of Azure Stack API Rest Reference**.</span><span class="sxs-lookup"><span data-stu-id="3a801-148">**Initial release of Azure Stack API Rest Reference**.</span></span> <span data-ttu-id="3a801-149">The [API reference for all Azure Stack Admin resource providers](https://docs.microsoft.com/rest/api/azure-stack/) is now published.</span><span class="sxs-lookup"><span data-stu-id="3a801-149">The [API reference for all Azure Stack Admin resource providers](https://docs.microsoft.com/rest/api/azure-stack/) is now published.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="3a801-150">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3a801-150">Before you begin</span></span>    

### <a name="prerequisites"></a><span data-ttu-id="3a801-151">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3a801-151">Prerequisites</span></span>
- <span data-ttu-id="3a801-152">Install the Azure Stack [1803 Update](azure-stack-update-1803.md) before you apply the Azure Stack 1804 update.</span><span class="sxs-lookup"><span data-stu-id="3a801-152">Install the Azure Stack [1803 Update](azure-stack-update-1803.md) before you apply the Azure Stack 1804 update.</span></span>  
  
- <span data-ttu-id="3a801-153">Install the latest available [update or hotfix for version 1803](azure-stack-update-1803.md#post-update-steps).</span><span class="sxs-lookup"><span data-stu-id="3a801-153">Install the latest available [update or hotfix for version 1803](azure-stack-update-1803.md#post-update-steps).</span></span> 


### <a name="known-issues-with-the-update-process"></a><span data-ttu-id="3a801-154">Known issues with the update process</span><span class="sxs-lookup"><span data-stu-id="3a801-154">Known issues with the update process</span></span>   
- <span data-ttu-id="3a801-155">During installation of the 1804 update, you might see alerts with the title *Error – Template for FaultType UserAccounts.New is missing.*</span><span class="sxs-lookup"><span data-stu-id="3a801-155">During installation of the 1804 update, you might see alerts with the title *Error – Template for FaultType UserAccounts.New is missing.*</span></span>  <span data-ttu-id="3a801-156">You can safely ignore these alerts.</span><span class="sxs-lookup"><span data-stu-id="3a801-156">You can safely ignore these alerts.</span></span> <span data-ttu-id="3a801-157">These alerts will close automatically after the update to 1804 completes.</span><span class="sxs-lookup"><span data-stu-id="3a801-157">These alerts will close automatically after the update to 1804 completes.</span></span>   
 
- <span data-ttu-id="3a801-158"><!-- TBD - IS --> Do not attempt to create virtual machines during the installation of this update.</span><span class="sxs-lookup"><span data-stu-id="3a801-158"><!-- TBD - IS --> Do not attempt to create virtual machines during the installation of this update.</span></span> <span data-ttu-id="3a801-159">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span><span class="sxs-lookup"><span data-stu-id="3a801-159">For more information about managing updates, see [Manage updates in Azure Stack overview](azure-stack-updates.md#plan-for-updates).</span></span>


### <a name="post-update-steps"></a><span data-ttu-id="3a801-160">Post-update steps</span><span class="sxs-lookup"><span data-stu-id="3a801-160">Post-update steps</span></span>
<span data-ttu-id="3a801-161">After the installation of 1804, install any applicable Hotfixes.</span><span class="sxs-lookup"><span data-stu-id="3a801-161">After the installation of 1804, install any applicable Hotfixes.</span></span> <span data-ttu-id="3a801-162">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3a801-162">For more information view the following knowledge base articles, as well as our [Servicing Policy](azure-stack-servicing-policy.md).</span></span>  
 - <span data-ttu-id="3a801-163">[KB 4344114 - Azure Stack Hotfix 1.0.180527.15](https://support.microsoft.com/help/4344114).</span><span class="sxs-lookup"><span data-stu-id="3a801-163">[KB 4344114 - Azure Stack Hotfix 1.0.180527.15](https://support.microsoft.com/help/4344114).</span></span>




### <a name="known-issues-post-installation"></a><span data-ttu-id="3a801-164">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="3a801-164">Known issues (post-installation)</span></span>
<span data-ttu-id="3a801-165">The following are post-installation known issues for build  **20180513.1**.</span><span class="sxs-lookup"><span data-stu-id="3a801-165">The following are post-installation known issues for build  **20180513.1**.</span></span>

#### <a name="portal"></a><span data-ttu-id="3a801-166">Portal</span><span class="sxs-lookup"><span data-stu-id="3a801-166">Portal</span></span>
- <span data-ttu-id="3a801-167"><!-- TBD - IS ASDK --> You cannot apply driver updates by using an OEM Extension package with this version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a801-167"><!-- TBD - IS ASDK --> You cannot apply driver updates by using an OEM Extension package with this version of Azure Stack.</span></span>  <span data-ttu-id="3a801-168">There is no workaround for this problem.</span><span class="sxs-lookup"><span data-stu-id="3a801-168">There is no workaround for this problem.</span></span>

- <span data-ttu-id="3a801-169"><!-- 1272111 - IS --> After you install or update to this version of Azure Stack, you might not be able to view Azure Stack scale units in the Admin portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-169"><!-- 1272111 - IS --> After you install or update to this version of Azure Stack, you might not be able to view Azure Stack scale units in the Admin portal.</span></span>  
  <span data-ttu-id="3a801-170">Workaround: Use PowerShell to view information about Scale Units.</span><span class="sxs-lookup"><span data-stu-id="3a801-170">Workaround: Use PowerShell to view information about Scale Units.</span></span> <span data-ttu-id="3a801-171">For more information, see the [help](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.3.0) content for Azure Stack Module 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="3a801-171">For more information, see the [help](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.3.0) content for Azure Stack Module 1.3.0.</span></span> 

- <span data-ttu-id="3a801-172"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span><span class="sxs-lookup"><span data-stu-id="3a801-172"><!-- 2332636 - IS -->  When you use AD FS for your Azure Stack identity system and update to this version of Azure Stack, the default owner of the default provider subscription is reset to the built-in **CloudAdmin** user.</span></span>  
  <span data-ttu-id="3a801-173">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="3a801-173">Workaround:  To resolve this issue after you install this update, use step 3 from the [Trigger automation to configure claims provider trust in Azure Stack](azure-stack-integrate-identity.md#trigger-automation-to-configure-claims-provider-trust-in-azure-stack-1) procedure to reset the owner of the default provider subscription.</span></span>   

- <span data-ttu-id="3a801-174"><!-- TBD - IS ASDK --> Some administrative subscription types are not available.</span><span class="sxs-lookup"><span data-stu-id="3a801-174"><!-- TBD - IS ASDK --> Some administrative subscription types are not available.</span></span>  <span data-ttu-id="3a801-175">When you upgrade Azure Stack to this version, the two subscription types that were [introduced with version 1804](#new-features) are not visible in the console.</span><span class="sxs-lookup"><span data-stu-id="3a801-175">When you upgrade Azure Stack to this version, the two subscription types that were [introduced with version 1804](#new-features) are not visible in the console.</span></span> <span data-ttu-id="3a801-176">This is expected.</span><span class="sxs-lookup"><span data-stu-id="3a801-176">This is expected.</span></span> <span data-ttu-id="3a801-177">The unavailable subscription types are *Metering subscription*, and *Consumption subscription*.</span><span class="sxs-lookup"><span data-stu-id="3a801-177">The unavailable subscription types are *Metering subscription*, and *Consumption subscription*.</span></span> <span data-ttu-id="3a801-178">These subscription types are visible in new Azure Stack environments beginning with version 1804 but are not yet ready for use.</span><span class="sxs-lookup"><span data-stu-id="3a801-178">These subscription types are visible in new Azure Stack environments beginning with version 1804 but are not yet ready for use.</span></span> <span data-ttu-id="3a801-179">You should continue to use the *Default Provider* subscription type.</span><span class="sxs-lookup"><span data-stu-id="3a801-179">You should continue to use the *Default Provider* subscription type.</span></span>  


- <span data-ttu-id="3a801-180"><!-- TBD -  IS ASDK -->The ability [to open a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the administrator portal isn’t available.</span><span class="sxs-lookup"><span data-stu-id="3a801-180"><!-- TBD -  IS ASDK -->The ability [to open a new support request from the dropdown](azure-stack-manage-portals.md#quick-access-to-help-and-support) from within the administrator portal isn’t available.</span></span> <span data-ttu-id="3a801-181">Instead, use the following link:</span><span class="sxs-lookup"><span data-stu-id="3a801-181">Instead, use the following link:</span></span>     
    - <span data-ttu-id="3a801-182">For Azure Stack integrated systems, use https://aka.ms/newsupportrequest.</span><span class="sxs-lookup"><span data-stu-id="3a801-182">For Azure Stack integrated systems, use https://aka.ms/newsupportrequest.</span></span>

- <span data-ttu-id="3a801-183"><!-- 2403291 - IS ASDK --> You might not have use of the horizontal scroll bar along the bottom of the admin and user portals.</span><span class="sxs-lookup"><span data-stu-id="3a801-183"><!-- 2403291 - IS ASDK --> You might not have use of the horizontal scroll bar along the bottom of the admin and user portals.</span></span> <span data-ttu-id="3a801-184">If you can’t access the horizontal scroll bar, use the breadcrumbs to navigate to a previous blade in the portal by selecting the name of the blade you want to view from the breadcrumb list found at the top left of the portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-184">If you can’t access the horizontal scroll bar, use the breadcrumbs to navigate to a previous blade in the portal by selecting the name of the blade you want to view from the breadcrumb list found at the top left of the portal.</span></span>
  <span data-ttu-id="3a801-185">![Breadcrumb](media/azure-stack-update-1804/breadcrumb.png)</span><span class="sxs-lookup"><span data-stu-id="3a801-185">![Breadcrumb](media/azure-stack-update-1804/breadcrumb.png)</span></span> 

- <span data-ttu-id="3a801-186"><!-- TBD - IS --> It might not be possible to view compute or storage resources in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-186"><!-- TBD - IS --> It might not be possible to view compute or storage resources in the administrator portal.</span></span> <span data-ttu-id="3a801-187">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span><span class="sxs-lookup"><span data-stu-id="3a801-187">The cause of this issue is an error during the installation of the update that causes the update to be incorrectly reported as successful.</span></span> <span data-ttu-id="3a801-188">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span><span class="sxs-lookup"><span data-stu-id="3a801-188">If this issue occurs, contact Microsoft Customer Support Services for assistance.</span></span>

- <span data-ttu-id="3a801-189"><!-- TBD - IS --> You might see a blank dashboard in the portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-189"><!-- TBD - IS --> You might see a blank dashboard in the portal.</span></span> <span data-ttu-id="3a801-190">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span><span class="sxs-lookup"><span data-stu-id="3a801-190">To recover the dashboard, select the gear icon in the upper right corner of the portal, and then select **Restore default settings**.</span></span>

- <span data-ttu-id="3a801-191"><!-- TBD - IS ASDK --> Deleting user subscriptions results in orphaned resources.</span><span class="sxs-lookup"><span data-stu-id="3a801-191"><!-- TBD - IS ASDK --> Deleting user subscriptions results in orphaned resources.</span></span> <span data-ttu-id="3a801-192">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3a801-192">As a workaround, first delete user resources or the entire resource group, and then delete user subscriptions.</span></span>

- <span data-ttu-id="3a801-193"><!-- TBD - IS ASDK --> You cannot view permissions to your subscription using the Azure Stack portals.</span><span class="sxs-lookup"><span data-stu-id="3a801-193"><!-- TBD - IS ASDK --> You cannot view permissions to your subscription using the Azure Stack portals.</span></span> <span data-ttu-id="3a801-194">As a workaround, use PowerShell to verify permissions.</span><span class="sxs-lookup"><span data-stu-id="3a801-194">As a workaround, use PowerShell to verify permissions.</span></span>

- <span data-ttu-id="3a801-195"><!-- TBD - IS ASDK --> In the admin portal, you might see a critical alert for the *Microsoft.Update.Admin* component.</span><span class="sxs-lookup"><span data-stu-id="3a801-195"><!-- TBD - IS ASDK --> In the admin portal, you might see a critical alert for the *Microsoft.Update.Admin* component.</span></span> <span data-ttu-id="3a801-196">The Alert name, description, and remediation all display as:</span><span class="sxs-lookup"><span data-stu-id="3a801-196">The Alert name, description, and remediation all display as:</span></span>  
    - <span data-ttu-id="3a801-197">*ERROR - Template for FaultType ResourceProviderTimeout is missing.*</span><span class="sxs-lookup"><span data-stu-id="3a801-197">*ERROR - Template for FaultType ResourceProviderTimeout is missing.*</span></span>

  <span data-ttu-id="3a801-198">This alert can be safely ignored.</span><span class="sxs-lookup"><span data-stu-id="3a801-198">This alert can be safely ignored.</span></span> 


#### <a name="health-and-monitoring"></a><span data-ttu-id="3a801-199">Health and monitoring</span><span class="sxs-lookup"><span data-stu-id="3a801-199">Health and monitoring</span></span>
- <span data-ttu-id="3a801-200"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span><span class="sxs-lookup"><span data-stu-id="3a801-200"><!-- 1264761 - IS ASDK -->  You might see alerts for the *Health controller* component that have the following details:</span></span>  

   <span data-ttu-id="3a801-201">Alert #1:</span><span class="sxs-lookup"><span data-stu-id="3a801-201">Alert #1:</span></span>
   - <span data-ttu-id="3a801-202">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="3a801-202">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="3a801-203">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="3a801-203">SEVERITY: Warning</span></span>
   - <span data-ttu-id="3a801-204">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="3a801-204">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="3a801-205">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="3a801-205">DESCRIPTION: The health controller Heartbeat Scanner is unavailable.</span></span> <span data-ttu-id="3a801-206">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="3a801-206">This may affect health reports and metrics.</span></span>  

  <span data-ttu-id="3a801-207">Alert #2:</span><span class="sxs-lookup"><span data-stu-id="3a801-207">Alert #2:</span></span>
   - <span data-ttu-id="3a801-208">NAME:  Infrastructure role unhealthy</span><span class="sxs-lookup"><span data-stu-id="3a801-208">NAME:  Infrastructure role unhealthy</span></span>
   - <span data-ttu-id="3a801-209">SEVERITY: Warning</span><span class="sxs-lookup"><span data-stu-id="3a801-209">SEVERITY: Warning</span></span>
   - <span data-ttu-id="3a801-210">COMPONENT: Health controller</span><span class="sxs-lookup"><span data-stu-id="3a801-210">COMPONENT: Health controller</span></span>
   - <span data-ttu-id="3a801-211">DESCRIPTION: The health controller Fault Scanner is unavailable.</span><span class="sxs-lookup"><span data-stu-id="3a801-211">DESCRIPTION: The health controller Fault Scanner is unavailable.</span></span> <span data-ttu-id="3a801-212">This may affect health reports and metrics.</span><span class="sxs-lookup"><span data-stu-id="3a801-212">This may affect health reports and metrics.</span></span>

  <span data-ttu-id="3a801-213">Both alerts can be safely ignored.</span><span class="sxs-lookup"><span data-stu-id="3a801-213">Both alerts can be safely ignored.</span></span> <span data-ttu-id="3a801-214">They will close automatically over time.</span><span class="sxs-lookup"><span data-stu-id="3a801-214">They will close automatically over time.</span></span>  
 

#### <a name="compute"></a><span data-ttu-id="3a801-215">Compute</span><span class="sxs-lookup"><span data-stu-id="3a801-215">Compute</span></span>
- <span data-ttu-id="3a801-216"><!-- TBD - IS --> When selecting a virtual machine size for a virtual machine deployment, some F-Series VM sizes are not visible as part of the size selector when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="3a801-216"><!-- TBD - IS --> When selecting a virtual machine size for a virtual machine deployment, some F-Series VM sizes are not visible as part of the size selector when you create a VM.</span></span> <span data-ttu-id="3a801-217">The following VM sizes do not appear in the selector: *F8s_v2*, *F16s_v2*, *F32s_v2*, and *F64s_v2*.</span><span class="sxs-lookup"><span data-stu-id="3a801-217">The following VM sizes do not appear in the selector: *F8s_v2*, *F16s_v2*, *F32s_v2*, and *F64s_v2*.</span></span>  
  <span data-ttu-id="3a801-218">As a workaround, use one of the following methods to deploy a VM.</span><span class="sxs-lookup"><span data-stu-id="3a801-218">As a workaround, use one of the following methods to deploy a VM.</span></span> <span data-ttu-id="3a801-219">In each method, you need to specify the VM size you want to use.</span><span class="sxs-lookup"><span data-stu-id="3a801-219">In each method, you need to specify the VM size you want to use.</span></span>

  - <span data-ttu-id="3a801-220">**Azure Resource Manager template:** When you use a template, set the *vmSize* in the template to equal the desired VM size.</span><span class="sxs-lookup"><span data-stu-id="3a801-220">**Azure Resource Manager template:** When you use a template, set the *vmSize* in the template to equal the desired VM size.</span></span> <span data-ttu-id="3a801-221">For example, the following is used to deploy a VM that uses the *F32s_v2* size:</span><span class="sxs-lookup"><span data-stu-id="3a801-221">For example, the following is used to deploy a VM that uses the *F32s_v2* size:</span></span>  

    ```
        "properties": {
        "hardwareProfile": {
                "vmSize": "Standard_F32s_v2"
        },
    ```  
  - <span data-ttu-id="3a801-222">**Azure CLI:** You can use the [az vm create](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create) command and specify the VM size as a parameter, similar to `--size "Standard_F32s_v2"`.</span><span class="sxs-lookup"><span data-stu-id="3a801-222">**Azure CLI:** You can use the [az vm create](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create) command and specify the VM size as a parameter, similar to `--size "Standard_F32s_v2"`.</span></span>

  - <span data-ttu-id="3a801-223">**PowerShell:** With PowerShell you can use [New-AzureRMVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig?view=azurermps-6.0.0) with the parameter that specifies the VM size, similar to `-VMSize "Standard_F32s_v2"`.</span><span class="sxs-lookup"><span data-stu-id="3a801-223">**PowerShell:** With PowerShell you can use [New-AzureRMVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig?view=azurermps-6.0.0) with the parameter that specifies the VM size, similar to `-VMSize "Standard_F32s_v2"`.</span></span>


- <span data-ttu-id="3a801-224"><!-- TBD - IS ASDK --> Scaling settings for virtual machine scale sets are not available in the portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-224"><!-- TBD - IS ASDK --> Scaling settings for virtual machine scale sets are not available in the portal.</span></span> <span data-ttu-id="3a801-225">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span><span class="sxs-lookup"><span data-stu-id="3a801-225">As a workaround, you can use [Azure PowerShell](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-manage-powershell#change-the-capacity-of-a-scale-set).</span></span> <span data-ttu-id="3a801-226">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span><span class="sxs-lookup"><span data-stu-id="3a801-226">Because of PowerShell version differences, you must use the `-Name` parameter instead of `-VMScaleSetName`.</span></span>

- <span data-ttu-id="3a801-227"><!-- TBD - IS --> When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span><span class="sxs-lookup"><span data-stu-id="3a801-227"><!-- TBD - IS --> When you create an availability set in the portal by going to **New** > **Compute** > **Availability set**, you can only create an availability set with a fault domain and update domain of 1.</span></span> <span data-ttu-id="3a801-228">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span><span class="sxs-lookup"><span data-stu-id="3a801-228">As a workaround, when creating a new virtual machine, create the availability set by using PowerShell, CLI, or from within the portal.</span></span>

- <span data-ttu-id="3a801-229"><!-- TBD - IS ASDK --> When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a D series VM.</span><span class="sxs-lookup"><span data-stu-id="3a801-229"><!-- TBD - IS ASDK --> When you create virtual machines on the Azure Stack user portal, the portal displays an incorrect number of data disks that can attach to a D series VM.</span></span> <span data-ttu-id="3a801-230">All supported D series VMs can accommodate as many data disks as the Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="3a801-230">All supported D series VMs can accommodate as many data disks as the Azure configuration.</span></span>

- <span data-ttu-id="3a801-231"><!-- TBD - IS ASDK --> When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span><span class="sxs-lookup"><span data-stu-id="3a801-231"><!-- TBD - IS ASDK --> When a VM image fails to be created, a failed item that you cannot delete might be added to the VM images compute blade.</span></span>

  <span data-ttu-id="3a801-232">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span><span class="sxs-lookup"><span data-stu-id="3a801-232">As a workaround, create a new VM image with a dummy VHD that can be created through Hyper-V (New-VHD -Path C:\dummy.vhd -Fixed -SizeBytes 1 GB).</span></span> <span data-ttu-id="3a801-233">This process should fix the problem that prevents deleting the failed item.</span><span class="sxs-lookup"><span data-stu-id="3a801-233">This process should fix the problem that prevents deleting the failed item.</span></span> <span data-ttu-id="3a801-234">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span><span class="sxs-lookup"><span data-stu-id="3a801-234">Then, 15 minutes after creating the dummy image, you can successfully delete it.</span></span>

  <span data-ttu-id="3a801-235">You can then try to redownload the VM image that previously failed.</span><span class="sxs-lookup"><span data-stu-id="3a801-235">You can then try to redownload the VM image that previously failed.</span></span>

- <span data-ttu-id="3a801-236"><!-- TBD - IS ASDK --> If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span><span class="sxs-lookup"><span data-stu-id="3a801-236"><!-- TBD - IS ASDK --> If provisioning an extension on a VM deployment takes too long, users should let the provisioning time-out instead of trying to stop the process to deallocate or delete the VM.</span></span>  

- <span data-ttu-id="3a801-237"><!-- 1662991 IS ASDK --> Linux VM diagnostics is not supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a801-237"><!-- 1662991 IS ASDK --> Linux VM diagnostics is not supported in Azure Stack.</span></span> <span data-ttu-id="3a801-238">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span><span class="sxs-lookup"><span data-stu-id="3a801-238">When you deploy a Linux VM with VM diagnostics enabled, the deployment fails.</span></span> <span data-ttu-id="3a801-239">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="3a801-239">The deployment also fails if you enable the Linux VM basic metrics through diagnostic settings.</span></span>  


#### <a name="networking"></a><span data-ttu-id="3a801-240">Networking</span><span class="sxs-lookup"><span data-stu-id="3a801-240">Networking</span></span>
- <span data-ttu-id="3a801-241"><!-- 1766332 - IS ASDK --> Under **Networking**, if you click **Create VPN Gateway** to set up a VPN connection, **Policy Based** is listed as a VPN type.</span><span class="sxs-lookup"><span data-stu-id="3a801-241"><!-- 1766332 - IS ASDK --> Under **Networking**, if you click **Create VPN Gateway** to set up a VPN connection, **Policy Based** is listed as a VPN type.</span></span> <span data-ttu-id="3a801-242">Do not select this option.</span><span class="sxs-lookup"><span data-stu-id="3a801-242">Do not select this option.</span></span> <span data-ttu-id="3a801-243">Only the **Route Based** option is supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3a801-243">Only the **Route Based** option is supported in Azure Stack.</span></span>

- <span data-ttu-id="3a801-244"><!-- 2388980 - IS ASDK --> After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span><span class="sxs-lookup"><span data-stu-id="3a801-244"><!-- 2388980 - IS ASDK --> After a VM is created and associated with a public IP address, you can't disassociate that VM from that IP address.</span></span> <span data-ttu-id="3a801-245">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span><span class="sxs-lookup"><span data-stu-id="3a801-245">Disassociation appears to work, but the previously assigned public IP address remains associated with the original VM.</span></span>

  <span data-ttu-id="3a801-246">Currently, you must use only new public IP addresses for new VMs you create.</span><span class="sxs-lookup"><span data-stu-id="3a801-246">Currently, you must use only new public IP addresses for new VMs you create.</span></span>

  <span data-ttu-id="3a801-247">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span><span class="sxs-lookup"><span data-stu-id="3a801-247">This behavior occurs even if you reassign the IP address to a new VM (commonly referred to as a *VIP swap*).</span></span> <span data-ttu-id="3a801-248">All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one.</span><span class="sxs-lookup"><span data-stu-id="3a801-248">All future attempts to connect through this IP address result in a connection to the originally associated VM, and not to the new one.</span></span>

- <span data-ttu-id="3a801-249"><!-- 2292271 - IS ASDK --> If you raise a Quota limit for a Network resource that is part of an Offer and Plan that is associated with a tenant subscription, the new limit is not applied to that subscription.</span><span class="sxs-lookup"><span data-stu-id="3a801-249"><!-- 2292271 - IS ASDK --> If you raise a Quota limit for a Network resource that is part of an Offer and Plan that is associated with a tenant subscription, the new limit is not applied to that subscription.</span></span> <span data-ttu-id="3a801-250">However, the new limit does apply to new subscriptions that are created after the quota is increased.</span><span class="sxs-lookup"><span data-stu-id="3a801-250">However, the new limit does apply to new subscriptions that are created after the quota is increased.</span></span> 

  <span data-ttu-id="3a801-251">To work around this problem, use an Add-On plan to increase a Network Quota when the plan is already associated with a subscription.</span><span class="sxs-lookup"><span data-stu-id="3a801-251">To work around this problem, use an Add-On plan to increase a Network Quota when the plan is already associated with a subscription.</span></span> <span data-ttu-id="3a801-252">For more information, see how to [make an add-on plan available](azure-stack-subscribe-plan-provision-vm.md#to-make-an-add-on-plan-available).</span><span class="sxs-lookup"><span data-stu-id="3a801-252">For more information, see how to [make an add-on plan available](azure-stack-subscribe-plan-provision-vm.md#to-make-an-add-on-plan-available).</span></span>

- <span data-ttu-id="3a801-253"><!-- 2304134 IS ASDK --> You cannot delete a subscription that has DNS Zone resources or Route Table resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="3a801-253"><!-- 2304134 IS ASDK --> You cannot delete a subscription that has DNS Zone resources or Route Table resources associated with it.</span></span> <span data-ttu-id="3a801-254">To successfully delete the subscription, you must first delete DNS Zone and Route Table resources from the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="3a801-254">To successfully delete the subscription, you must first delete DNS Zone and Route Table resources from the tenant subscription.</span></span> 
  

- <span data-ttu-id="3a801-255"><!-- 1902460 - IS ASDK --> Azure Stack supports a single *local network gateway* per IP address.</span><span class="sxs-lookup"><span data-stu-id="3a801-255"><!-- 1902460 - IS ASDK --> Azure Stack supports a single *local network gateway* per IP address.</span></span> <span data-ttu-id="3a801-256">This is true across all tenant subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3a801-256">This is true across all tenant subscriptions.</span></span> <span data-ttu-id="3a801-257">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span><span class="sxs-lookup"><span data-stu-id="3a801-257">After the creation of the first local network gateway connection, subsequent attempts to create a local network gateway resource with the same IP address are blocked.</span></span>

- <span data-ttu-id="3a801-258"><!-- 16309153 - IS ASDK --> On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span><span class="sxs-lookup"><span data-stu-id="3a801-258"><!-- 16309153 - IS ASDK --> On a Virtual Network that was created with a DNS Server setting of *Automatic*, changing to a custom DNS Server fails.</span></span> <span data-ttu-id="3a801-259">The updated settings are not pushed to VMs in that Vnet.</span><span class="sxs-lookup"><span data-stu-id="3a801-259">The updated settings are not pushed to VMs in that Vnet.</span></span>

- <span data-ttu-id="3a801-260"><!-- TBD - IS ASDK --> Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span><span class="sxs-lookup"><span data-stu-id="3a801-260"><!-- TBD - IS ASDK --> Azure Stack does not support adding additional network interfaces to a VM instance after the VM is deployed.</span></span> <span data-ttu-id="3a801-261">If the VM requires more than one network interface, they must be defined at deployment time.</span><span class="sxs-lookup"><span data-stu-id="3a801-261">If the VM requires more than one network interface, they must be defined at deployment time.</span></span>

- <span data-ttu-id="3a801-262"><!-- 2096388 IS --> You cannot use the admin portal to update rules for a network security group.</span><span class="sxs-lookup"><span data-stu-id="3a801-262"><!-- 2096388 IS --> You cannot use the admin portal to update rules for a network security group.</span></span> 

    <span data-ttu-id="3a801-263">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a801-263">Workaround for App Service: If you need to remote desktop to the Controller instances, you modify the security rules within the network security groups with PowerShell.</span></span>  <span data-ttu-id="3a801-264">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span><span class="sxs-lookup"><span data-stu-id="3a801-264">Following are examples of how to *allow*, and then restore the configuration to *deny*:</span></span>  
    
    - <span data-ttu-id="3a801-265">*Allow:*</span><span class="sxs-lookup"><span data-stu-id="3a801-265">*Allow:*</span></span>
 
      ```powershell    
      Connect-AzureRmAccount -EnvironmentName AzureStackAdmin
      
      $nsg = Get-AzureRmNetworkSecurityGroup -Name "ControllersNsg" -ResourceGroupName "AppService.local"
      
      $RuleConfig_Inbound_Rdp_3389 =  $nsg | Get-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389"
      
      ##This doesn’t work. Need to set properties again even in case of edit
      
      #Set-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389" -NetworkSecurityGroup $nsg -Access Allow  
      
      Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
        -Name $RuleConfig_Inbound_Rdp_3389.Name `
        -Description "Inbound_Rdp_3389" `
        -Access Allow `
        -Protocol $RuleConfig_Inbound_Rdp_3389.Protocol `
        -Direction $RuleConfig_Inbound_Rdp_3389.Direction `
        -Priority $RuleConfig_Inbound_Rdp_3389.Priority `
        -SourceAddressPrefix $RuleConfig_Inbound_Rdp_3389.SourceAddressPrefix `
        -SourcePortRange $RuleConfig_Inbound_Rdp_3389.SourcePortRange `
        -DestinationAddressPrefix $RuleConfig_Inbound_Rdp_3389.DestinationAddressPrefix `
        -DestinationPortRange $RuleConfig_Inbound_Rdp_3389.DestinationPortRange
      
      # Commit the changes back to NSG
      Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
      ```

    - <span data-ttu-id="3a801-266">*Deny:*</span><span class="sxs-lookup"><span data-stu-id="3a801-266">*Deny:*</span></span>

        ```powershell
        
        Connect-AzureRmAccount -EnvironmentName AzureStackAdmin
        
        $nsg = Get-AzureRmNetworkSecurityGroup -Name "ControllersNsg" -ResourceGroupName "AppService.local"
        
        $RuleConfig_Inbound_Rdp_3389 =  $nsg | Get-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389"
        
        ##This doesn’t work. Need to set properties again even in case of edit
    
        #Set-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389" -NetworkSecurityGroup $nsg -Access Allow  
    
        Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
          -Name $RuleConfig_Inbound_Rdp_3389.Name `
          -Description "Inbound_Rdp_3389" `
          -Access Deny `
          -Protocol $RuleConfig_Inbound_Rdp_3389.Protocol `
          -Direction $RuleConfig_Inbound_Rdp_3389.Direction `
          -Priority $RuleConfig_Inbound_Rdp_3389.Priority `
          -SourceAddressPrefix $RuleConfig_Inbound_Rdp_3389.SourceAddressPrefix `
          -SourcePortRange $RuleConfig_Inbound_Rdp_3389.SourcePortRange `
          -DestinationAddressPrefix $RuleConfig_Inbound_Rdp_3389.DestinationAddressPrefix `
          -DestinationPortRange $RuleConfig_Inbound_Rdp_3389.DestinationPortRange
          
        # Commit the changes back to NSG
        Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg 
        ```

#### <a name="sql-and-mysql"></a><span data-ttu-id="3a801-267">SQL and MySQL</span><span class="sxs-lookup"><span data-stu-id="3a801-267">SQL and MySQL</span></span>

- <span data-ttu-id="3a801-268"><!-- TBD - IS --> Only the resource provider is supported to create items on servers that host SQL or MySQL.</span><span class="sxs-lookup"><span data-stu-id="3a801-268"><!-- TBD - IS --> Only the resource provider is supported to create items on servers that host SQL or MySQL.</span></span> <span data-ttu-id="3a801-269">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span><span class="sxs-lookup"><span data-stu-id="3a801-269">Items created on a host server that are not created by the resource provider might result in a mismatched state.</span></span>  

- <span data-ttu-id="3a801-270"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** or **Tier** names when you create a SKU for the SQL and MySQL resource providers.</span><span class="sxs-lookup"><span data-stu-id="3a801-270"><!-- IS, ASDK --> Special characters, including spaces and periods, are not supported in the **Family** or **Tier** names when you create a SKU for the SQL and MySQL resource providers.</span></span>


> [!NOTE]  
> <span data-ttu-id="3a801-271"><!-- TBD - IS --> After you update to Azure Stack 1804, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span><span class="sxs-lookup"><span data-stu-id="3a801-271"><!-- TBD - IS --> After you update to Azure Stack 1804, you can continue to use the SQL and MySQL resource providers that you previously deployed.</span></span>  <span data-ttu-id="3a801-272">We recommend you update SQL and MySQL when a new release becomes available.</span><span class="sxs-lookup"><span data-stu-id="3a801-272">We recommend you update SQL and MySQL when a new release becomes available.</span></span> <span data-ttu-id="3a801-273">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span><span class="sxs-lookup"><span data-stu-id="3a801-273">Like Azure Stack, apply updates to SQL and MySQL resource providers sequentially.</span></span>  <span data-ttu-id="3a801-274">For example, if you use version 1802, first apply version 1803, and then update to 1804.</span><span class="sxs-lookup"><span data-stu-id="3a801-274">For example, if you use version 1802, first apply version 1803, and then update to 1804.</span></span>      
>   
> <span data-ttu-id="3a801-275">The install of update 1804 does not affect the current use of SQL or MySQL resource providers by your users.</span><span class="sxs-lookup"><span data-stu-id="3a801-275">The install of update 1804 does not affect the current use of SQL or MySQL resource providers by your users.</span></span>
> <span data-ttu-id="3a801-276">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span><span class="sxs-lookup"><span data-stu-id="3a801-276">Regardless of the version of the resource providers you use, your users data in their databases is not touched, and remains accessible.</span></span>    



#### <a name="app-service"></a><span data-ttu-id="3a801-277">App Service</span><span class="sxs-lookup"><span data-stu-id="3a801-277">App Service</span></span>
- <span data-ttu-id="3a801-278"><!-- 2352906 - IS ASDK --> Users must register the storage resource provider before they create their first Azure Function in the subscription.</span><span class="sxs-lookup"><span data-stu-id="3a801-278"><!-- 2352906 - IS ASDK --> Users must register the storage resource provider before they create their first Azure Function in the subscription.</span></span>

- <span data-ttu-id="3a801-279"><!-- TBD - IS ASDK --> In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span><span class="sxs-lookup"><span data-stu-id="3a801-279"><!-- TBD - IS ASDK --> In order to scale out infrastructure (workers, management, front-end roles), you must use PowerShell as described in the release notes for Compute.</span></span>

- <span data-ttu-id="3a801-280"><!-- TBD - IS ASDK --> App Service can only be deployed into the **Default Provider Subscription** at this time.</span><span class="sxs-lookup"><span data-stu-id="3a801-280"><!-- TBD - IS ASDK --> App Service can only be deployed into the **Default Provider Subscription** at this time.</span></span>  <span data-ttu-id="3a801-281">In a future update App Service will deploy into the new Metering Subscription introduced in Azure Stack 1804 and all existing deployments will be migrated to this new subscription also.</span><span class="sxs-lookup"><span data-stu-id="3a801-281">In a future update App Service will deploy into the new Metering Subscription introduced in Azure Stack 1804 and all existing deployments will be migrated to this new subscription also.</span></span>

#### <a name="usage"></a><span data-ttu-id="3a801-282">Usage</span><span class="sxs-lookup"><span data-stu-id="3a801-282">Usage</span></span>  
- <span data-ttu-id="3a801-283"><!-- TBD - IS ASDK --> Usage Public IP address usage meter data shows the same *EventDateTime* value for each record instead of the *TimeDate* stamp that shows when the record was created.</span><span class="sxs-lookup"><span data-stu-id="3a801-283"><!-- TBD - IS ASDK --> Usage Public IP address usage meter data shows the same *EventDateTime* value for each record instead of the *TimeDate* stamp that shows when the record was created.</span></span> <span data-ttu-id="3a801-284">Currently, you can’t use this data to perform accurate accounting of public IP address usage.</span><span class="sxs-lookup"><span data-stu-id="3a801-284">Currently, you can’t use this data to perform accurate accounting of public IP address usage.</span></span>


<!-- #### Identity -->
<!-- #### Marketplace --> 


## <a name="download-the-update"></a><span data-ttu-id="3a801-285">Download the update</span><span class="sxs-lookup"><span data-stu-id="3a801-285">Download the update</span></span>
<span data-ttu-id="3a801-286">You can download the Azure Stack 1804 update package from [here](https://aka.ms/azurestackupdatedownload).</span><span class="sxs-lookup"><span data-stu-id="3a801-286">You can download the Azure Stack 1804 update package from [here](https://aka.ms/azurestackupdatedownload).</span></span>


## <a name="see-also"></a><span data-ttu-id="3a801-287">See also</span><span class="sxs-lookup"><span data-stu-id="3a801-287">See also</span></span>
- <span data-ttu-id="3a801-288">To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).</span><span class="sxs-lookup"><span data-stu-id="3a801-288">To use the Privileged End Point (PEP) to monitor and resume updates, see [Monitor updates in Azure Stack using the privileged endpoint](azure-stack-monitor-update.md).</span></span>
- <span data-ttu-id="3a801-289">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span><span class="sxs-lookup"><span data-stu-id="3a801-289">For an overview of the update management in Azure Stack, see [Manage updates in Azure Stack overview](azure-stack-updates.md).</span></span>
- <span data-ttu-id="3a801-290">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span><span class="sxs-lookup"><span data-stu-id="3a801-290">For more information about how to apply updates with Azure Stack, see [Apply updates in Azure Stack](azure-stack-apply-updates.md).</span></span>
