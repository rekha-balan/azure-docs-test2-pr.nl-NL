---
title: Azure Cloud Shell limitations | Microsoft Docs
description: Overview of limitations of Azure Cloud Shell
services: azure
documentationcenter: ''
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/15/2018
ms.author: juluk
ms.openlocfilehash: 135496e17ae884db580922aa31f6824b2e7fd934
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856473"
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="87bd2-103">Limitations of Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="87bd2-103">Limitations of Azure Cloud Shell</span></span>

<span data-ttu-id="87bd2-104">Azure Cloud Shell has the following known limitations:</span><span class="sxs-lookup"><span data-stu-id="87bd2-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="general-limitations"></a><span data-ttu-id="87bd2-105">General limitations</span><span class="sxs-lookup"><span data-stu-id="87bd2-105">General limitations</span></span>

### <a name="system-state-and-persistence"></a><span data-ttu-id="87bd2-106">System state and persistence</span><span class="sxs-lookup"><span data-stu-id="87bd2-106">System state and persistence</span></span>

<span data-ttu-id="87bd2-107">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="87bd2-107">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="87bd2-108">Cloud Shell requires an Azure file share to be mounted.</span><span class="sxs-lookup"><span data-stu-id="87bd2-108">Cloud Shell requires an Azure file share to be mounted.</span></span> <span data-ttu-id="87bd2-109">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="87bd2-109">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="87bd2-110">Other considerations include:</span><span class="sxs-lookup"><span data-stu-id="87bd2-110">Other considerations include:</span></span>

* <span data-ttu-id="87bd2-111">With mounted storage, only modifications within the `$Home` directory are persisted.</span><span class="sxs-lookup"><span data-stu-id="87bd2-111">With mounted storage, only modifications within the `$Home` directory are persisted.</span></span>
* <span data-ttu-id="87bd2-112">Azure file shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="87bd2-112">Azure file shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
  * <span data-ttu-id="87bd2-113">In Bash, run `env` to find your region set as `ACC_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="87bd2-113">In Bash, run `env` to find your region set as `ACC_LOCATION`.</span></span>

### <a name="browser-support"></a><span data-ttu-id="87bd2-114">Browser support</span><span class="sxs-lookup"><span data-stu-id="87bd2-114">Browser support</span></span>

<span data-ttu-id="87bd2-115">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="87bd2-115">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="87bd2-116">Safari in private mode is not supported.</span><span class="sxs-lookup"><span data-stu-id="87bd2-116">Safari in private mode is not supported.</span></span>

### <a name="copy-and-paste"></a><span data-ttu-id="87bd2-117">Copy and paste</span><span class="sxs-lookup"><span data-stu-id="87bd2-117">Copy and paste</span></span>

[!INCLUDE [copy-paste](../../includes/cloud-shell-copy-paste.md)]

### <a name="for-a-given-user-only-one-shell-can-be-active"></a><span data-ttu-id="87bd2-118">For a given user, only one shell can be active</span><span class="sxs-lookup"><span data-stu-id="87bd2-118">For a given user, only one shell can be active</span></span>

<span data-ttu-id="87bd2-119">Users can only launch one type of shell at a time, either **Bash** or **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="87bd2-119">Users can only launch one type of shell at a time, either **Bash** or **PowerShell**.</span></span> <span data-ttu-id="87bd2-120">However, you may have multiple instances of Bash or PowerShell running at one time.</span><span class="sxs-lookup"><span data-stu-id="87bd2-120">However, you may have multiple instances of Bash or PowerShell running at one time.</span></span> <span data-ttu-id="87bd2-121">Swapping between Bash or PowerShell causes Cloud Shell to restart, which terminates existing sessions.</span><span class="sxs-lookup"><span data-stu-id="87bd2-121">Swapping between Bash or PowerShell causes Cloud Shell to restart, which terminates existing sessions.</span></span>

### <a name="usage-limits"></a><span data-ttu-id="87bd2-122">Usage limits</span><span class="sxs-lookup"><span data-stu-id="87bd2-122">Usage limits</span></span>

<span data-ttu-id="87bd2-123">Cloud Shell is intended for interactive use cases.</span><span class="sxs-lookup"><span data-stu-id="87bd2-123">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="87bd2-124">As a result, any long-running non-interactive sessions are ended without warning.</span><span class="sxs-lookup"><span data-stu-id="87bd2-124">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="bash-limitations"></a><span data-ttu-id="87bd2-125">Bash limitations</span><span class="sxs-lookup"><span data-stu-id="87bd2-125">Bash limitations</span></span>

### <a name="user-permissions"></a><span data-ttu-id="87bd2-126">User permissions</span><span class="sxs-lookup"><span data-stu-id="87bd2-126">User permissions</span></span>

<span data-ttu-id="87bd2-127">Permissions are set as regular users without sudo access.</span><span class="sxs-lookup"><span data-stu-id="87bd2-127">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="87bd2-128">Any installation outside your `$Home` directory is not persisted.</span><span class="sxs-lookup"><span data-stu-id="87bd2-128">Any installation outside your `$Home` directory is not persisted.</span></span>

### <a name="editing-bashrc"></a><span data-ttu-id="87bd2-129">Editing .bashrc</span><span class="sxs-lookup"><span data-stu-id="87bd2-129">Editing .bashrc</span></span>

<span data-ttu-id="87bd2-130">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="87bd2-130">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="powershell-limitations"></a><span data-ttu-id="87bd2-131">PowerShell limitations</span><span class="sxs-lookup"><span data-stu-id="87bd2-131">PowerShell limitations</span></span>

### <a name="azuread-module-name"></a><span data-ttu-id="87bd2-132">`AzureAD` module name</span><span class="sxs-lookup"><span data-stu-id="87bd2-132">`AzureAD` module name</span></span>

<span data-ttu-id="87bd2-133">The `AzureAD` module name is currently `AzureAD.Standard.Preview`, the module provides the same functionality.</span><span class="sxs-lookup"><span data-stu-id="87bd2-133">The `AzureAD` module name is currently `AzureAD.Standard.Preview`, the module provides the same functionality.</span></span>

### <a name="sqlserver-module-functionality"></a><span data-ttu-id="87bd2-134">`SqlServer` module functionality</span><span class="sxs-lookup"><span data-stu-id="87bd2-134">`SqlServer` module functionality</span></span>

<span data-ttu-id="87bd2-135">The `SqlServer` module included in Cloud Shell has only prerelease support for PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="87bd2-135">The `SqlServer` module included in Cloud Shell has only prerelease support for PowerShell Core.</span></span> <span data-ttu-id="87bd2-136">In particular, `Invoke-SqlCmd` is not available yet.</span><span class="sxs-lookup"><span data-stu-id="87bd2-136">In particular, `Invoke-SqlCmd` is not available yet.</span></span>

### <a name="default-file-location-when-created-from-azure-drive"></a><span data-ttu-id="87bd2-137">Default file location when created from Azure drive:</span><span class="sxs-lookup"><span data-stu-id="87bd2-137">Default file location when created from Azure drive:</span></span>

<span data-ttu-id="87bd2-138">Using PowerShell cmdlets, users can not create files under the Azure drive.</span><span class="sxs-lookup"><span data-stu-id="87bd2-138">Using PowerShell cmdlets, users can not create files under the Azure drive.</span></span> <span data-ttu-id="87bd2-139">When users create new files using other tools, such as vim or nano, the files are saved to the `$HOME` by default.</span><span class="sxs-lookup"><span data-stu-id="87bd2-139">When users create new files using other tools, such as vim or nano, the files are saved to the `$HOME` by default.</span></span> 

### <a name="gui-applications-are-not-supported"></a><span data-ttu-id="87bd2-140">GUI applications are not supported</span><span class="sxs-lookup"><span data-stu-id="87bd2-140">GUI applications are not supported</span></span>

<span data-ttu-id="87bd2-141">If the user runs a command that would create a Windows dialog box, such as `Connect-AzureAD` or `Connect-AzureRmAccount`, one sees an error message such as: `Unable to load DLL 'IEFRAME.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)`.</span><span class="sxs-lookup"><span data-stu-id="87bd2-141">If the user runs a command that would create a Windows dialog box, such as `Connect-AzureAD` or `Connect-AzureRmAccount`, one sees an error message such as: `Unable to load DLL 'IEFRAME.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)`.</span></span>

### <a name="tab-completion-crashes-psreadline"></a><span data-ttu-id="87bd2-142">Tab completion crashes PSReadline</span><span class="sxs-lookup"><span data-stu-id="87bd2-142">Tab completion crashes PSReadline</span></span>

<span data-ttu-id="87bd2-143">If the user's EditMode in PSReadline is set to Emacs, the user tries to display all possibilities via tab completion, and the window size is too small to display all the possibilities, PSReadline will crash.</span><span class="sxs-lookup"><span data-stu-id="87bd2-143">If the user's EditMode in PSReadline is set to Emacs, the user tries to display all possibilities via tab completion, and the window size is too small to display all the possibilities, PSReadline will crash.</span></span>

### <a name="large-gap-after-displaying-progress-bar"></a><span data-ttu-id="87bd2-144">Large Gap after displaying progress bar</span><span class="sxs-lookup"><span data-stu-id="87bd2-144">Large Gap after displaying progress bar</span></span>

<span data-ttu-id="87bd2-145">If the user performs an action that displays a progress bar, such a tab completing while in the `Azure:` drive, then it is possible that the cursor is not set properly and a gap appears where the progress bar was previously.</span><span class="sxs-lookup"><span data-stu-id="87bd2-145">If the user performs an action that displays a progress bar, such a tab completing while in the `Azure:` drive, then it is possible that the cursor is not set properly and a gap appears where the progress bar was previously.</span></span>

### <a name="random-characters-appear-inline"></a><span data-ttu-id="87bd2-146">Random characters appear inline</span><span class="sxs-lookup"><span data-stu-id="87bd2-146">Random characters appear inline</span></span>

<span data-ttu-id="87bd2-147">The cursor position sequence codes, for example `5;13R`, can appear in the user input.</span><span class="sxs-lookup"><span data-stu-id="87bd2-147">The cursor position sequence codes, for example `5;13R`, can appear in the user input.</span></span>  <span data-ttu-id="87bd2-148">The characters can be manually removed.</span><span class="sxs-lookup"><span data-stu-id="87bd2-148">The characters can be manually removed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87bd2-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="87bd2-149">Next steps</span></span>

[<span data-ttu-id="87bd2-150">Troubleshooting Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="87bd2-150">Troubleshooting Cloud Shell</span></span>](troubleshooting.md) <br>
[<span data-ttu-id="87bd2-151">Quickstart for Bash</span><span class="sxs-lookup"><span data-stu-id="87bd2-151">Quickstart for Bash</span></span>](quickstart.md) <br>
[<span data-ttu-id="87bd2-152">Quickstart for PowerShell</span><span class="sxs-lookup"><span data-stu-id="87bd2-152">Quickstart for PowerShell</span></span>](quickstart-powershell.md)
