---
title: Azure Cloud Shell troubleshooting | Microsoft Docs
description: Troubleshooting Azure Cloud Shell
services: azure
documentationcenter: ''
author: maertendMSFT
manager: hemantm
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/24/2018
ms.author: damaerte
ms.openlocfilehash: 089c623ff2c53a59c60c3fe1a53876c16a5353dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864957"
---
# <a name="troubleshooting--limitations-of-azure-cloud-shell"></a><span data-ttu-id="57bf6-103">Troubleshooting & Limitations of Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="57bf6-103">Troubleshooting & Limitations of Azure Cloud Shell</span></span>

<span data-ttu-id="57bf6-104">Known resolutions for troubleshooting issues in Azure Cloud Shell include:</span><span class="sxs-lookup"><span data-stu-id="57bf6-104">Known resolutions for troubleshooting issues in Azure Cloud Shell include:</span></span>

## <a name="general-troubleshooting"></a><span data-ttu-id="57bf6-105">General troubleshooting</span><span class="sxs-lookup"><span data-stu-id="57bf6-105">General troubleshooting</span></span>

### <a name="early-timeouts-in-firefox"></a><span data-ttu-id="57bf6-106">Early timeouts in FireFox</span><span class="sxs-lookup"><span data-stu-id="57bf6-106">Early timeouts in FireFox</span></span>

- <span data-ttu-id="57bf6-107">**Details**: Cloud Shell utilizes an open websocket to pass input/output to your browser.</span><span class="sxs-lookup"><span data-stu-id="57bf6-107">**Details**: Cloud Shell utilizes an open websocket to pass input/output to your browser.</span></span> <span data-ttu-id="57bf6-108">FireFox has preset policies that can close the websocket prematurely causing early timeouts in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="57bf6-108">FireFox has preset policies that can close the websocket prematurely causing early timeouts in Cloud Shell.</span></span>
- <span data-ttu-id="57bf6-109">**Resolution**: Open FireFox and navigate to "about:config" in the URL box.</span><span class="sxs-lookup"><span data-stu-id="57bf6-109">**Resolution**: Open FireFox and navigate to "about:config" in the URL box.</span></span> <span data-ttu-id="57bf6-110">Search for "network.websocket.timeout.ping.request" and change the value from 0 to 10.</span><span class="sxs-lookup"><span data-stu-id="57bf6-110">Search for "network.websocket.timeout.ping.request" and change the value from 0 to 10.</span></span>

### <a name="disabling-cloud-shell-in-a-locked-down-network-environment"></a><span data-ttu-id="57bf6-111">Disabling Cloud Shell in a locked down network environment</span><span class="sxs-lookup"><span data-stu-id="57bf6-111">Disabling Cloud Shell in a locked down network environment</span></span>

- <span data-ttu-id="57bf6-112">**Details**: Administrators may wish to disable access to Cloud Shell for their users.</span><span class="sxs-lookup"><span data-stu-id="57bf6-112">**Details**: Administrators may wish to disable access to Cloud Shell for their users.</span></span> <span data-ttu-id="57bf6-113">Cloud Shell utilizes access to the `ux.console.azure.com` domain which can be denied, stopping any access to Cloud Shell's entrypoints including portal.azure.com, shell.azure.com, Visual Studio Code Azure Account extension, and docs.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="57bf6-113">Cloud Shell utilizes access to the `ux.console.azure.com` domain which can be denied, stopping any access to Cloud Shell's entrypoints including portal.azure.com, shell.azure.com, Visual Studio Code Azure Account extension, and docs.microsoft.com.</span></span>
- <span data-ttu-id="57bf6-114">**Resolution**: Restrict access to `ux.console.azure.com` via network settings to your environment.</span><span class="sxs-lookup"><span data-stu-id="57bf6-114">**Resolution**: Restrict access to `ux.console.azure.com` via network settings to your environment.</span></span> <span data-ttu-id="57bf6-115">The Cloud Shell icon will still exist in portal.azure.com, but will not successfully connect to the service.</span><span class="sxs-lookup"><span data-stu-id="57bf6-115">The Cloud Shell icon will still exist in portal.azure.com, but will not successfully connect to the service.</span></span>

### <a name="storage-dialog---error-403-requestdisallowedbypolicy"></a><span data-ttu-id="57bf6-116">Storage Dialog - Error: 403 RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="57bf6-116">Storage Dialog - Error: 403 RequestDisallowedByPolicy</span></span>

- <span data-ttu-id="57bf6-117">**Details**: When creating a storage account through Cloud Shell, it is unsuccessful due to an Azure policy placed by your admin. Error message will include: `The resource action 'Microsoft.Storage/storageAccounts/write' is disallowed by one or more policies.`</span><span class="sxs-lookup"><span data-stu-id="57bf6-117">**Details**: When creating a storage account through Cloud Shell, it is unsuccessful due to an Azure policy placed by your admin. Error message will include: `The resource action 'Microsoft.Storage/storageAccounts/write' is disallowed by one or more policies.`</span></span>
- <span data-ttu-id="57bf6-118">**Resolution**: Contact your Azure administrator to remove or update the Azure policy denying storage creation.</span><span class="sxs-lookup"><span data-stu-id="57bf6-118">**Resolution**: Contact your Azure administrator to remove or update the Azure policy denying storage creation.</span></span>

### <a name="storage-dialog---error-400-disallowedoperation"></a><span data-ttu-id="57bf6-119">Storage Dialog - Error: 400 DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="57bf6-119">Storage Dialog - Error: 400 DisallowedOperation</span></span>

- <span data-ttu-id="57bf6-120">**Details**: When using an Azure Active Directory subscription, you cannot create storage.</span><span class="sxs-lookup"><span data-stu-id="57bf6-120">**Details**: When using an Azure Active Directory subscription, you cannot create storage.</span></span>
- <span data-ttu-id="57bf6-121">**Resolution**: Use an Azure subscription capable of creating storage resources.</span><span class="sxs-lookup"><span data-stu-id="57bf6-121">**Resolution**: Use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="57bf6-122">Azure AD subscriptions are not able to create Azure resources.</span><span class="sxs-lookup"><span data-stu-id="57bf6-122">Azure AD subscriptions are not able to create Azure resources.</span></span>

### <a name="terminal-output---error-failed-to-connect-terminal-websocket-cannot-be-established-press-enter-to-reconnect"></a><span data-ttu-id="57bf6-123">Terminal output - Error: Failed to connect terminal: websocket cannot be established.</span><span class="sxs-lookup"><span data-stu-id="57bf6-123">Terminal output - Error: Failed to connect terminal: websocket cannot be established.</span></span> <span data-ttu-id="57bf6-124">Press `Enter` to reconnect.</span><span class="sxs-lookup"><span data-stu-id="57bf6-124">Press `Enter` to reconnect.</span></span>
- <span data-ttu-id="57bf6-125">**Details**: Cloud Shell requires the ability to establish a websocket connection to Cloud Shell infrastructure.</span><span class="sxs-lookup"><span data-stu-id="57bf6-125">**Details**: Cloud Shell requires the ability to establish a websocket connection to Cloud Shell infrastructure.</span></span>
- <span data-ttu-id="57bf6-126">**Resolution**: Check you have configured your network settings to enable sending https requests and websocket requests to domains at \*.console.azure.com.</span><span class="sxs-lookup"><span data-stu-id="57bf6-126">**Resolution**: Check you have configured your network settings to enable sending https requests and websocket requests to domains at \*.console.azure.com.</span></span>

### <a name="set-your-cloud-shell-connection-to-support-using-tls-12"></a><span data-ttu-id="57bf6-127">Set your Cloud Shell connection to support using TLS 1.2</span><span class="sxs-lookup"><span data-stu-id="57bf6-127">Set your Cloud Shell connection to support using TLS 1.2</span></span>
 - <span data-ttu-id="57bf6-128">**Details**: To define the version of TLS for your connection to Cloud Shell, you must set browser specific settings.</span><span class="sxs-lookup"><span data-stu-id="57bf6-128">**Details**: To define the version of TLS for your connection to Cloud Shell, you must set browser specific settings.</span></span>
 - <span data-ttu-id="57bf6-129">**Resolution**: Navigate to the security settings of your browser and select the checkbox next to "Use TLS 1.2".</span><span class="sxs-lookup"><span data-stu-id="57bf6-129">**Resolution**: Navigate to the security settings of your browser and select the checkbox next to "Use TLS 1.2".</span></span>

## <a name="bash-troubleshooting"></a><span data-ttu-id="57bf6-130">Bash troubleshooting</span><span class="sxs-lookup"><span data-stu-id="57bf6-130">Bash troubleshooting</span></span>

### <a name="cannot-run-the-docker-daemon"></a><span data-ttu-id="57bf6-131">Cannot run the docker daemon</span><span class="sxs-lookup"><span data-stu-id="57bf6-131">Cannot run the docker daemon</span></span>

- <span data-ttu-id="57bf6-132">**Details**: Cloud Shell utilizes a container to host your shell environment, as a result running the daemon is disallowed.</span><span class="sxs-lookup"><span data-stu-id="57bf6-132">**Details**: Cloud Shell utilizes a container to host your shell environment, as a result running the daemon is disallowed.</span></span>
- <span data-ttu-id="57bf6-133">**Resolution**: Utilize [docker-machine](https://docs.docker.com/machine/overview/), which is installed by default, to manage docker containers from a remote Docker host.</span><span class="sxs-lookup"><span data-stu-id="57bf6-133">**Resolution**: Utilize [docker-machine](https://docs.docker.com/machine/overview/), which is installed by default, to manage docker containers from a remote Docker host.</span></span>

## <a name="powershell-troubleshooting"></a><span data-ttu-id="57bf6-134">PowerShell troubleshooting</span><span class="sxs-lookup"><span data-stu-id="57bf6-134">PowerShell troubleshooting</span></span>

### <a name="gui-applications-are-not-supported"></a><span data-ttu-id="57bf6-135">GUI applications are not supported</span><span class="sxs-lookup"><span data-stu-id="57bf6-135">GUI applications are not supported</span></span>

- <span data-ttu-id="57bf6-136">**Details**: If a user launches a GUI application, the prompt does not return.</span><span class="sxs-lookup"><span data-stu-id="57bf6-136">**Details**: If a user launches a GUI application, the prompt does not return.</span></span> <span data-ttu-id="57bf6-137">For example, when one clone a private GitHub repo that has two factor authentication enabled, a dialog box is displayed for completing the two factor authentication.</span><span class="sxs-lookup"><span data-stu-id="57bf6-137">For example, when one clone a private GitHub repo that has two factor authentication enabled, a dialog box is displayed for completing the two factor authentication.</span></span>
- <span data-ttu-id="57bf6-138">**Resolution**: Close and reopen the shell.</span><span class="sxs-lookup"><span data-stu-id="57bf6-138">**Resolution**: Close and reopen the shell.</span></span>

### <a name="troubleshooting-remote-management-of-azure-vms"></a><span data-ttu-id="57bf6-139">Troubleshooting remote management of Azure VMs</span><span class="sxs-lookup"><span data-stu-id="57bf6-139">Troubleshooting remote management of Azure VMs</span></span>

- <span data-ttu-id="57bf6-140">**Details**: Due to the default Windows Firewall settings for WinRM the user may see the following error: `Ensure the WinRM service is running. Remote Desktop into the VM for the first time and ensure it can be discovered.`</span><span class="sxs-lookup"><span data-stu-id="57bf6-140">**Details**: Due to the default Windows Firewall settings for WinRM the user may see the following error: `Ensure the WinRM service is running. Remote Desktop into the VM for the first time and ensure it can be discovered.`</span></span>
- <span data-ttu-id="57bf6-141">**Resolution**:  Run `Enable-AzureRmVMPSRemoting` to enable all aspects of PowerShell remoting on the target machine.</span><span class="sxs-lookup"><span data-stu-id="57bf6-141">**Resolution**:  Run `Enable-AzureRmVMPSRemoting` to enable all aspects of PowerShell remoting on the target machine.</span></span>

### <a name="dir-does-not-update-the-result-in-azure-drive"></a><span data-ttu-id="57bf6-142">`dir` does not update the result in Azure drive</span><span class="sxs-lookup"><span data-stu-id="57bf6-142">`dir` does not update the result in Azure drive</span></span>

- <span data-ttu-id="57bf6-143">**Details**: By default, to optimize for user experience, the results of `dir` is cached in Azure drive.</span><span class="sxs-lookup"><span data-stu-id="57bf6-143">**Details**: By default, to optimize for user experience, the results of `dir` is cached in Azure drive.</span></span>
- <span data-ttu-id="57bf6-144">**Resolution**: After you create, update or remove an Azure resource, run `dir -force` to update the results in the Azure drive.</span><span class="sxs-lookup"><span data-stu-id="57bf6-144">**Resolution**: After you create, update or remove an Azure resource, run `dir -force` to update the results in the Azure drive.</span></span>

## <a name="general-limitations"></a><span data-ttu-id="57bf6-145">General limitations</span><span class="sxs-lookup"><span data-stu-id="57bf6-145">General limitations</span></span>

<span data-ttu-id="57bf6-146">Azure Cloud Shell has the following known limitations:</span><span class="sxs-lookup"><span data-stu-id="57bf6-146">Azure Cloud Shell has the following known limitations:</span></span>

### <a name="system-state-and-persistence"></a><span data-ttu-id="57bf6-147">System state and persistence</span><span class="sxs-lookup"><span data-stu-id="57bf6-147">System state and persistence</span></span>

<span data-ttu-id="57bf6-148">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="57bf6-148">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="57bf6-149">Cloud Shell requires an Azure file share to be mounted.</span><span class="sxs-lookup"><span data-stu-id="57bf6-149">Cloud Shell requires an Azure file share to be mounted.</span></span> <span data-ttu-id="57bf6-150">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="57bf6-150">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="57bf6-151">Other considerations include:</span><span class="sxs-lookup"><span data-stu-id="57bf6-151">Other considerations include:</span></span>

- <span data-ttu-id="57bf6-152">With mounted storage, only modifications within the `clouddrive` directory are persisted.</span><span class="sxs-lookup"><span data-stu-id="57bf6-152">With mounted storage, only modifications within the `clouddrive` directory are persisted.</span></span> <span data-ttu-id="57bf6-153">In Bash, your `$HOME` directory is also persisted.</span><span class="sxs-lookup"><span data-stu-id="57bf6-153">In Bash, your `$HOME` directory is also persisted.</span></span>
- <span data-ttu-id="57bf6-154">Azure file shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="57bf6-154">Azure file shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
  - <span data-ttu-id="57bf6-155">In Bash, run `env` to find your region set as `ACC_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="57bf6-155">In Bash, run `env` to find your region set as `ACC_LOCATION`.</span></span>
- <span data-ttu-id="57bf6-156">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span><span class="sxs-lookup"><span data-stu-id="57bf6-156">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

### <a name="browser-support"></a><span data-ttu-id="57bf6-157">Browser support</span><span class="sxs-lookup"><span data-stu-id="57bf6-157">Browser support</span></span>

<span data-ttu-id="57bf6-158">Cloud Shell supports the latest versions of following browsers:</span><span class="sxs-lookup"><span data-stu-id="57bf6-158">Cloud Shell supports the latest versions of following browsers:</span></span>

- <span data-ttu-id="57bf6-159">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="57bf6-159">Microsoft Edge</span></span>
- <span data-ttu-id="57bf6-160">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="57bf6-160">Microsoft Internet Explorer</span></span>
- <span data-ttu-id="57bf6-161">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="57bf6-161">Google Chrome</span></span>
- <span data-ttu-id="57bf6-162">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="57bf6-162">Mozilla Firefox</span></span>
- <span data-ttu-id="57bf6-163">Apple Safari</span><span class="sxs-lookup"><span data-stu-id="57bf6-163">Apple Safari</span></span>
  - <span data-ttu-id="57bf6-164">Safari in private mode is not supported.</span><span class="sxs-lookup"><span data-stu-id="57bf6-164">Safari in private mode is not supported.</span></span>

### <a name="copy-and-paste"></a><span data-ttu-id="57bf6-165">Copy and paste</span><span class="sxs-lookup"><span data-stu-id="57bf6-165">Copy and paste</span></span>

[!INCLUDE [copy-paste](../../includes/cloud-shell-copy-paste.md)]

### <a name="for-a-given-user-only-one-shell-can-be-active"></a><span data-ttu-id="57bf6-166">For a given user, only one shell can be active</span><span class="sxs-lookup"><span data-stu-id="57bf6-166">For a given user, only one shell can be active</span></span>

<span data-ttu-id="57bf6-167">Users can only launch one type of shell at a time, either **Bash** or **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="57bf6-167">Users can only launch one type of shell at a time, either **Bash** or **PowerShell**.</span></span> <span data-ttu-id="57bf6-168">However, you may have multiple instances of Bash or PowerShell running at one time.</span><span class="sxs-lookup"><span data-stu-id="57bf6-168">However, you may have multiple instances of Bash or PowerShell running at one time.</span></span> <span data-ttu-id="57bf6-169">Swapping between Bash or PowerShell causes Cloud Shell to restart, which terminates existing sessions.</span><span class="sxs-lookup"><span data-stu-id="57bf6-169">Swapping between Bash or PowerShell causes Cloud Shell to restart, which terminates existing sessions.</span></span>

### <a name="usage-limits"></a><span data-ttu-id="57bf6-170">Usage limits</span><span class="sxs-lookup"><span data-stu-id="57bf6-170">Usage limits</span></span>

<span data-ttu-id="57bf6-171">Cloud Shell is intended for interactive use cases.</span><span class="sxs-lookup"><span data-stu-id="57bf6-171">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="57bf6-172">As a result, any long-running non-interactive sessions are ended without warning.</span><span class="sxs-lookup"><span data-stu-id="57bf6-172">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

### <a name="user-permissions"></a><span data-ttu-id="57bf6-173">User permissions</span><span class="sxs-lookup"><span data-stu-id="57bf6-173">User permissions</span></span>

<span data-ttu-id="57bf6-174">Permissions are set as regular users without sudo access.</span><span class="sxs-lookup"><span data-stu-id="57bf6-174">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="57bf6-175">Any installation outside your `$Home` directory is not persisted.</span><span class="sxs-lookup"><span data-stu-id="57bf6-175">Any installation outside your `$Home` directory is not persisted.</span></span>

## <a name="bash-limitations"></a><span data-ttu-id="57bf6-176">Bash limitations</span><span class="sxs-lookup"><span data-stu-id="57bf6-176">Bash limitations</span></span>

### <a name="editing-bashrc"></a><span data-ttu-id="57bf6-177">Editing .bashrc</span><span class="sxs-lookup"><span data-stu-id="57bf6-177">Editing .bashrc</span></span>

<span data-ttu-id="57bf6-178">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="57bf6-178">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="powershell-limitations"></a><span data-ttu-id="57bf6-179">PowerShell limitations</span><span class="sxs-lookup"><span data-stu-id="57bf6-179">PowerShell limitations</span></span>

### <a name="preview-version-of-azuread-module"></a><span data-ttu-id="57bf6-180">Preview version of AzureAD module</span><span class="sxs-lookup"><span data-stu-id="57bf6-180">Preview version of AzureAD module</span></span>

<span data-ttu-id="57bf6-181">Currently, `AzureAD.Standard.Preview`, a preview version of .NET Standard-based, module is available.</span><span class="sxs-lookup"><span data-stu-id="57bf6-181">Currently, `AzureAD.Standard.Preview`, a preview version of .NET Standard-based, module is available.</span></span> <span data-ttu-id="57bf6-182">This module provides the same functionality as `AzureAD`.</span><span class="sxs-lookup"><span data-stu-id="57bf6-182">This module provides the same functionality as `AzureAD`.</span></span>

### <a name="sqlserver-module-functionality"></a><span data-ttu-id="57bf6-183">`SqlServer` module functionality</span><span class="sxs-lookup"><span data-stu-id="57bf6-183">`SqlServer` module functionality</span></span>

<span data-ttu-id="57bf6-184">The `SqlServer` module included in Cloud Shell has only prerelease support for PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="57bf6-184">The `SqlServer` module included in Cloud Shell has only prerelease support for PowerShell Core.</span></span> <span data-ttu-id="57bf6-185">In particular, `Invoke-SqlCmd` is not available yet.</span><span class="sxs-lookup"><span data-stu-id="57bf6-185">In particular, `Invoke-SqlCmd` is not available yet.</span></span>

### <a name="default-file-location-when-created-from-azure-drive"></a><span data-ttu-id="57bf6-186">Default file location when created from Azure drive</span><span class="sxs-lookup"><span data-stu-id="57bf6-186">Default file location when created from Azure drive</span></span>

<span data-ttu-id="57bf6-187">Using PowerShell cmdlets, users cannot create files under the Azure drive.</span><span class="sxs-lookup"><span data-stu-id="57bf6-187">Using PowerShell cmdlets, users cannot create files under the Azure drive.</span></span> <span data-ttu-id="57bf6-188">When users create new files using other tools, such as vim or nano, the files are saved to the `$HOME` by default.</span><span class="sxs-lookup"><span data-stu-id="57bf6-188">When users create new files using other tools, such as vim or nano, the files are saved to the `$HOME` by default.</span></span>

### <a name="commands-that-create-gui-pop-ups-are-not-supported"></a><span data-ttu-id="57bf6-189">Commands that create GUI pop-ups are not supported</span><span class="sxs-lookup"><span data-stu-id="57bf6-189">Commands that create GUI pop-ups are not supported</span></span>

<span data-ttu-id="57bf6-190">If the user runs a command that would create a Windows dialog box, such as `Connect-AzureAD` or `Connect-AzureRmAccount`, one sees an error message such as: `Unable to load DLL 'IEFRAME.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)`.</span><span class="sxs-lookup"><span data-stu-id="57bf6-190">If the user runs a command that would create a Windows dialog box, such as `Connect-AzureAD` or `Connect-AzureRmAccount`, one sees an error message such as: `Unable to load DLL 'IEFRAME.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)`.</span></span>

### <a name="tab-completion-can-throw-psreadline-exception"></a><span data-ttu-id="57bf6-191">Tab completion can throw PSReadline exception</span><span class="sxs-lookup"><span data-stu-id="57bf6-191">Tab completion can throw PSReadline exception</span></span>

<span data-ttu-id="57bf6-192">If the user's PSReadline EditMode is set to Emacs, the user tries to display all possibilities via tab completion, and the window size is too small to display all the possibilities, PSReadline will throw unhandled exception.</span><span class="sxs-lookup"><span data-stu-id="57bf6-192">If the user's PSReadline EditMode is set to Emacs, the user tries to display all possibilities via tab completion, and the window size is too small to display all the possibilities, PSReadline will throw unhandled exception.</span></span>

### <a name="large-gap-after-displaying-progress-bar"></a><span data-ttu-id="57bf6-193">Large gap after displaying progress bar</span><span class="sxs-lookup"><span data-stu-id="57bf6-193">Large gap after displaying progress bar</span></span>

<span data-ttu-id="57bf6-194">If a command or user action displays a progress bar, such a tab completing while in the `Azure:` drive, then it is possible that the cursor is not set properly and a gap appears where the progress bar was previously.</span><span class="sxs-lookup"><span data-stu-id="57bf6-194">If a command or user action displays a progress bar, such a tab completing while in the `Azure:` drive, then it is possible that the cursor is not set properly and a gap appears where the progress bar was previously.</span></span>

### <a name="random-characters-appear-inline"></a><span data-ttu-id="57bf6-195">Random characters appear inline</span><span class="sxs-lookup"><span data-stu-id="57bf6-195">Random characters appear inline</span></span>

<span data-ttu-id="57bf6-196">The cursor position sequence codes, for example `5;13R`, can appear in the user input.</span><span class="sxs-lookup"><span data-stu-id="57bf6-196">The cursor position sequence codes, for example `5;13R`, can appear in the user input.</span></span> <span data-ttu-id="57bf6-197">The characters can be manually removed.</span><span class="sxs-lookup"><span data-stu-id="57bf6-197">The characters can be manually removed.</span></span>

## <a name="personal-data-in-cloud-shell"></a><span data-ttu-id="57bf6-198">Personal data in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="57bf6-198">Personal data in Cloud Shell</span></span>

<span data-ttu-id="57bf6-199">Azure Cloud Shell takes your personal data seriously, the data captured and stored by the Azure Cloud Shell service are used to provide defaults for your experience such as your most recently used shell, preferred font size, preferred font type, and file share details that back cloud drive.</span><span class="sxs-lookup"><span data-stu-id="57bf6-199">Azure Cloud Shell takes your personal data seriously, the data captured and stored by the Azure Cloud Shell service are used to provide defaults for your experience such as your most recently used shell, preferred font size, preferred font type, and file share details that back cloud drive.</span></span> <span data-ttu-id="57bf6-200">Should you wish to export or delete this data, use the following instructions.</span><span class="sxs-lookup"><span data-stu-id="57bf6-200">Should you wish to export or delete this data, use the following instructions.</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

### <a name="export"></a><span data-ttu-id="57bf6-201">Export</span><span class="sxs-lookup"><span data-stu-id="57bf6-201">Export</span></span>
<span data-ttu-id="57bf6-202">In order to **export** the user settings Cloud Shell saves for you such as preferred shell, font size, and font type run the following commands.</span><span class="sxs-lookup"><span data-stu-id="57bf6-202">In order to **export** the user settings Cloud Shell saves for you such as preferred shell, font size, and font type run the following commands.</span></span>

1. <span data-ttu-id="57bf6-203">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="57bf6-203">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span></span>
2. <span data-ttu-id="57bf6-204">Run the following commands in Bash or PowerShell:</span><span class="sxs-lookup"><span data-stu-id="57bf6-204">Run the following commands in Bash or PowerShell:</span></span>

<span data-ttu-id="57bf6-205">Bash:</span><span class="sxs-lookup"><span data-stu-id="57bf6-205">Bash:</span></span>

  ```
  token="Bearer $(curl http://localhost:50342/oauth2/token --data "resource=https://management.azure.com/" -H Metadata:true -s | jq -r ".access_token")"
  curl https://management.azure.com/providers/Microsoft.Portal/usersettings/cloudconsole?api-version=2017-12-01-preview -H Authorization:"$token" -s | jq
  ```

<span data-ttu-id="57bf6-206">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="57bf6-206">PowerShell:</span></span>

  ```powershell
  $token= ((Invoke-WebRequest -Uri "$env:MSI_ENDPOINT`?resource=https://management.core.windows.net/" -Headers @{Metadata='true'}).content |  ConvertFrom-Json).access_token
  ((Invoke-WebRequest -Uri https://management.azure.com/providers/Microsoft.Portal/usersettings/cloudconsole?api-version=2017-12-01-preview -Headers @{Authorization = "Bearer $token"}).Content | ConvertFrom-Json).properties | Format-List
```

### <a name="delete"></a><span data-ttu-id="57bf6-207">Delete</span><span class="sxs-lookup"><span data-stu-id="57bf6-207">Delete</span></span>
<span data-ttu-id="57bf6-208">In order to **delete** your user settings Cloud Shell saves for you such as preferred shell, font size, and font type run the following commands.</span><span class="sxs-lookup"><span data-stu-id="57bf6-208">In order to **delete** your user settings Cloud Shell saves for you such as preferred shell, font size, and font type run the following commands.</span></span> <span data-ttu-id="57bf6-209">The next time you start Cloud Shell you will be asked to onboard a file share again.</span><span class="sxs-lookup"><span data-stu-id="57bf6-209">The next time you start Cloud Shell you will be asked to onboard a file share again.</span></span> 

>[!Note]
> <span data-ttu-id="57bf6-210">If you delete your user settings, the actual Azure Files share will not be deleted.</span><span class="sxs-lookup"><span data-stu-id="57bf6-210">If you delete your user settings, the actual Azure Files share will not be deleted.</span></span> <span data-ttu-id="57bf6-211">Go to your Azure Files to complete that action.</span><span class="sxs-lookup"><span data-stu-id="57bf6-211">Go to your Azure Files to complete that action.</span></span>

1. <span data-ttu-id="57bf6-212">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span><span class="sxs-lookup"><span data-stu-id="57bf6-212">[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)</span></span>
2. <span data-ttu-id="57bf6-213">Run the following commands in Bash or PowerShell:</span><span class="sxs-lookup"><span data-stu-id="57bf6-213">Run the following commands in Bash or PowerShell:</span></span>

<span data-ttu-id="57bf6-214">Bash:</span><span class="sxs-lookup"><span data-stu-id="57bf6-214">Bash:</span></span>

  ```
  token="Bearer $(curl http://localhost:50342/oauth2/token --data "resource=https://management.azure.com/" -H Metadata:true -s | jq -r ".access_token")"
  curl -X DELETE https://management.azure.com/providers/Microsoft.Portal/usersettings/cloudconsole?api-version=2017-12-01-preview -H Authorization:"$token"
  ```

<span data-ttu-id="57bf6-215">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="57bf6-215">PowerShell:</span></span>

  ```powershell
  $token= ((Invoke-WebRequest -Uri "$env:MSI_ENDPOINT`?resource=https://management.core.windows.net/" -Headers @{Metadata='true'}).content |  ConvertFrom-Json).access_token
  Invoke-WebRequest -Method Delete -Uri https://management.azure.com/providers/Microsoft.Portal/usersettings/cloudconsole?api-version=2017-12-01-preview -Headers @{Authorization = "Bearer $token"}
  ```
