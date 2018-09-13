---
title: Use PowerShell cmdlets with Azure RemoteApp | Microsoft Docs
description: Learn how to use Windows PowerShell cmdlets in Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: guscatalano
manager: mbaldwin
editor: ''
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9134b5893413abbc49e2332651fb4a8b549ce559
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660707"
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="0fc26-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0fc26-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0fc26-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="0fc26-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0fc26-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="0fc26-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="0fc26-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span><span class="sxs-lookup"><span data-stu-id="0fc26-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="0fc26-107">Use the following information to get started.</span><span class="sxs-lookup"><span data-stu-id="0fc26-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="0fc26-108">Get the cmdlets</span><span class="sxs-lookup"><span data-stu-id="0fc26-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="0fc26-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span><span class="sxs-lookup"><span data-stu-id="0fc26-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="0fc26-110">Check out the [Azure RemoteApp cmdlet help](https://msdn.microsoft.com/library/mt428031.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fc26-110">Check out the [Azure RemoteApp cmdlet help](https://msdn.microsoft.com/library/mt428031.aspx).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="0fc26-111">Configure Azure cmdlets to use your subscription</span><span class="sxs-lookup"><span data-stu-id="0fc26-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="0fc26-112">Follow [this guide](/powershell/azureps-cmdlets-docs) so you can use the cmdlets against your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0fc26-112">Follow [this guide](/powershell/azureps-cmdlets-docs) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="0fc26-113">You can use these steps to get started quickly:</span><span class="sxs-lookup"><span data-stu-id="0fc26-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="0fc26-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="0fc26-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="0fc26-115">Launch Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fc26-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="0fc26-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0fc26-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="0fc26-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0fc26-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="0fc26-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span><span class="sxs-lookup"><span data-stu-id="0fc26-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="0fc26-119">Run **Select-AzureSubscription** and specify the subscription name or ID to use in the PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="0fc26-119">Run **Select-AzureSubscription** and specify the subscription name or ID to use in the PowerShell console.</span></span>

<span data-ttu-id="0fc26-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span><span class="sxs-lookup"><span data-stu-id="0fc26-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="0fc26-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="0fc26-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  

## <a name="create-a-cloud-collection"></a><span data-ttu-id="0fc26-122">Create a cloud collection</span><span class="sxs-lookup"><span data-stu-id="0fc26-122">Create a cloud collection</span></span>
- - -
<span data-ttu-id="0fc26-123">It's simple, run the following command:</span><span class="sxs-lookup"><span data-stu-id="0fc26-123">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="0fc26-124">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span><span class="sxs-lookup"><span data-stu-id="0fc26-124">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="0fc26-125">Collection creation can take 30 minutes or longer to complete.</span><span class="sxs-lookup"><span data-stu-id="0fc26-125">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="0fc26-126">Therefore, this command returns a tracking ID that you can use as follows:</span><span class="sxs-lookup"><span data-stu-id="0fc26-126">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="0fc26-127">After the collection is done, you can add users to the collection with the following command:</span><span class="sxs-lookup"><span data-stu-id="0fc26-127">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="0fc26-128">And you're done!</span><span class="sxs-lookup"><span data-stu-id="0fc26-128">And you're done!</span></span> <span data-ttu-id="0fc26-129">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="0fc26-129">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="0fc26-130">Available cmdlets</span><span class="sxs-lookup"><span data-stu-id="0fc26-130">Available cmdlets</span></span>
<span data-ttu-id="0fc26-131">There are lots of other commands that we have, the documentation for them will be coming shortly:</span><span class="sxs-lookup"><span data-stu-id="0fc26-131">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="0fc26-132">Basic RemoteApp Collection  cmdlets:</span><span class="sxs-lookup"><span data-stu-id="0fc26-132">Basic RemoteApp Collection  cmdlets:</span></span> 

* <span data-ttu-id="0fc26-133">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="0fc26-133">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="0fc26-134">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="0fc26-134">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="0fc26-135">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="0fc26-135">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="0fc26-136">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="0fc26-136">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="0fc26-137">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="0fc26-137">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="0fc26-138">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="0fc26-138">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="0fc26-139">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="0fc26-139">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="0fc26-140">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="0fc26-140">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="0fc26-141">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="0fc26-141">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="0fc26-142">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="0fc26-142">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="0fc26-143">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="0fc26-143">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="0fc26-144">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="0fc26-144">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="0fc26-145">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="0fc26-145">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="0fc26-146">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="0fc26-146">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="0fc26-147">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="0fc26-147">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="0fc26-148">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="0fc26-148">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="0fc26-149">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="0fc26-149">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="0fc26-150">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="0fc26-150">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="0fc26-151">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="0fc26-151">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="0fc26-152">RemoteApp virtual network cmdlets:</span><span class="sxs-lookup"><span data-stu-id="0fc26-152">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="0fc26-153">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="0fc26-153">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="0fc26-154">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="0fc26-154">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="0fc26-155">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="0fc26-155">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="0fc26-156">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="0fc26-156">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="0fc26-157">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="0fc26-157">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="0fc26-158">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="0fc26-158">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="0fc26-159">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="0fc26-159">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="0fc26-160">RemoteApp template image cmdlets:</span><span class="sxs-lookup"><span data-stu-id="0fc26-160">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="0fc26-161">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="0fc26-161">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="0fc26-162">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="0fc26-162">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="0fc26-163">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="0fc26-163">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="0fc26-164">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="0fc26-164">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="0fc26-165">Other RemoteApp cmdlets:</span><span class="sxs-lookup"><span data-stu-id="0fc26-165">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="0fc26-166">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="0fc26-166">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="0fc26-167">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="0fc26-167">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="0fc26-168">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="0fc26-168">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="0fc26-169">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="0fc26-169">Get-AzureRemoteAppOperationResult</span></span>

