---
title: Using redirection in Azure RemoteApp | Microsoft Docs
description: Learn how to configure and use redirection in RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cab03e7765dc7116a7f974833871fae652e8363c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551338"
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="23499-103">Using redirection in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="23499-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="23499-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="23499-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="23499-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="23499-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="23499-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span><span class="sxs-lookup"><span data-stu-id="23499-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="23499-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span><span class="sxs-lookup"><span data-stu-id="23499-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="23499-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span><span class="sxs-lookup"><span data-stu-id="23499-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="23499-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span><span class="sxs-lookup"><span data-stu-id="23499-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="23499-110">What redirection is enabled by default?</span><span class="sxs-lookup"><span data-stu-id="23499-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="23499-111">When you use RemoteApp, the following redirections are enabled by default.</span><span class="sxs-lookup"><span data-stu-id="23499-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="23499-112">The information in parentheses show the RDP setting.</span><span class="sxs-lookup"><span data-stu-id="23499-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="23499-113">Play sounds on the local computer (**Play on this computer**).</span><span class="sxs-lookup"><span data-stu-id="23499-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="23499-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="23499-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="23499-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span><span class="sxs-lookup"><span data-stu-id="23499-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="23499-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="23499-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="23499-117">Print to local printers (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="23499-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="23499-118">COM ports (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="23499-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="23499-119">Smart card device (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="23499-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="23499-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="23499-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="23499-121">Clear type font smoothing (allow font smoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="23499-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="23499-122">Redirect all supported Plug and Play devices.</span><span class="sxs-lookup"><span data-stu-id="23499-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="23499-123">(devicestoredirect:s:\*)</span><span class="sxs-lookup"><span data-stu-id="23499-123">(devicestoredirect:s:\*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="23499-124">What other redirection is available?</span><span class="sxs-lookup"><span data-stu-id="23499-124">What other redirection is available?</span></span>
<span data-ttu-id="23499-125">Two redirection options are disabled by default:</span><span class="sxs-lookup"><span data-stu-id="23499-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="23499-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span><span class="sxs-lookup"><span data-stu-id="23499-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="23499-127">This lets you save or open files from your local drives while you work in the remote session.</span><span class="sxs-lookup"><span data-stu-id="23499-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="23499-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span><span class="sxs-lookup"><span data-stu-id="23499-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="23499-129">Change your redirection settings in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="23499-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="23499-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span><span class="sxs-lookup"><span data-stu-id="23499-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="23499-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="23499-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="23499-132">Then use a command similar to the following to set the custom RDP properties:</span><span class="sxs-lookup"><span data-stu-id="23499-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="23499-133">(Note that *\`n* is used as a delimiter between individual properties.)</span><span class="sxs-lookup"><span data-stu-id="23499-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="23499-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23499-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="23499-135">Note that only custom properties are shown as output results and not the default properties:</span><span class="sxs-lookup"><span data-stu-id="23499-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="23499-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span><span class="sxs-lookup"><span data-stu-id="23499-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="23499-137">Common examples</span><span class="sxs-lookup"><span data-stu-id="23499-137">Common examples</span></span>
<span data-ttu-id="23499-138">Use the following cmdlet to enable drive redirection:</span><span class="sxs-lookup"><span data-stu-id="23499-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="23499-139">Use this cmdlet to enable both USB and Drive redirection:</span><span class="sxs-lookup"><span data-stu-id="23499-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="23499-140">Use this cmdlet to disable clipboard sharing:</span><span class="sxs-lookup"><span data-stu-id="23499-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="23499-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span><span class="sxs-lookup"><span data-stu-id="23499-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="23499-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span><span class="sxs-lookup"><span data-stu-id="23499-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="23499-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span><span class="sxs-lookup"><span data-stu-id="23499-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="23499-144">Change USB redirection settings on your Windows client</span><span class="sxs-lookup"><span data-stu-id="23499-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="23499-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span><span class="sxs-lookup"><span data-stu-id="23499-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="23499-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23499-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="23499-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span><span class="sxs-lookup"><span data-stu-id="23499-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="23499-148">This step will need to be done for each user that wants to use USB redirection.</span><span class="sxs-lookup"><span data-stu-id="23499-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="23499-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span><span class="sxs-lookup"><span data-stu-id="23499-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="23499-150">Enable USB redirection for the RemoteApp collection</span><span class="sxs-lookup"><span data-stu-id="23499-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="23499-151">Use the following cmdlet to enable USB redirection at the collection level:</span><span class="sxs-lookup"><span data-stu-id="23499-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="23499-152">Enable USB redirection for the client computer</span><span class="sxs-lookup"><span data-stu-id="23499-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="23499-153">To configure USB redirection settings on your computer:</span><span class="sxs-lookup"><span data-stu-id="23499-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="23499-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span><span class="sxs-lookup"><span data-stu-id="23499-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="23499-155">(Run gpedit.msc from a command prompt.)</span><span class="sxs-lookup"><span data-stu-id="23499-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="23499-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span><span class="sxs-lookup"><span data-stu-id="23499-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="23499-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span><span class="sxs-lookup"><span data-stu-id="23499-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="23499-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span><span class="sxs-lookup"><span data-stu-id="23499-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="23499-159">Open a command prompt with administrative permissions, and run the following command:</span><span class="sxs-lookup"><span data-stu-id="23499-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="23499-160">Restart the computer.</span><span class="sxs-lookup"><span data-stu-id="23499-160">Restart the computer.</span></span>

<span data-ttu-id="23499-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span><span class="sxs-lookup"><span data-stu-id="23499-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="23499-162">Log into the domain controller as the domain administrator.</span><span class="sxs-lookup"><span data-stu-id="23499-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="23499-163">Open the Group Policy Management Console.</span><span class="sxs-lookup"><span data-stu-id="23499-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="23499-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span><span class="sxs-lookup"><span data-stu-id="23499-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="23499-165">Navigate to the domain or organizational unit for which you want to create the policy.</span><span class="sxs-lookup"><span data-stu-id="23499-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="23499-166">Right-click **Default Domain Policy**, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="23499-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="23499-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span><span class="sxs-lookup"><span data-stu-id="23499-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="23499-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span><span class="sxs-lookup"><span data-stu-id="23499-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="23499-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span><span class="sxs-lookup"><span data-stu-id="23499-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="23499-170">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="23499-170">Click **OK**.</span></span>  

