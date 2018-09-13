---
title: Publish applications to individual users in an Azure RemoteApp collection (Preview) | Microsoft Docs
description: Learn how you can publish apps to individual users, instead of depending on groups, in Azure RemoteApp.
services: remoteapp-preview
documentationcenter: ''
author: piotrci
manager: mbaldwin
editor: ''
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 88d2abdac0555d687f93201e431140d4ea898ad2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549598"
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="3dce3-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span><span class="sxs-lookup"><span data-stu-id="3dce3-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3dce3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="3dce3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3dce3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="3dce3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3dce3-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span><span class="sxs-lookup"><span data-stu-id="3dce3-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="3dce3-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span><span class="sxs-lookup"><span data-stu-id="3dce3-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="3dce3-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span><span class="sxs-lookup"><span data-stu-id="3dce3-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="3dce3-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span><span class="sxs-lookup"><span data-stu-id="3dce3-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="3dce3-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span><span class="sxs-lookup"><span data-stu-id="3dce3-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="3dce3-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span><span class="sxs-lookup"><span data-stu-id="3dce3-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="3dce3-112">Here is a brief summary of the new functionality:</span><span class="sxs-lookup"><span data-stu-id="3dce3-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="3dce3-113">A collection can be set into one of two modes:</span><span class="sxs-lookup"><span data-stu-id="3dce3-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="3dce3-114">the original collection mode, where all users in a collection can see all published applications.</span><span class="sxs-lookup"><span data-stu-id="3dce3-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="3dce3-115">This is the default mode.</span><span class="sxs-lookup"><span data-stu-id="3dce3-115">This is the default mode.</span></span>
   * <span data-ttu-id="3dce3-116">the new application mode, where users only see applications that have been explicitly assigned to them</span><span class="sxs-lookup"><span data-stu-id="3dce3-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="3dce3-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3dce3-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="3dce3-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3dce3-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="3dce3-119">User assignment has to be managed through PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3dce3-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="3dce3-120">Users will only see the applications published directly to them.</span><span class="sxs-lookup"><span data-stu-id="3dce3-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="3dce3-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span><span class="sxs-lookup"><span data-stu-id="3dce3-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="3dce3-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span><span class="sxs-lookup"><span data-stu-id="3dce3-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="3dce3-123">If you need to isolate users from applications, you will need to use separate collections for that.</span><span class="sxs-lookup"><span data-stu-id="3dce3-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="3dce3-124">How to get Azure RemoteApp PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="3dce3-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="3dce3-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3dce3-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3dce3-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span><span class="sxs-lookup"><span data-stu-id="3dce3-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="3dce3-127">First, make sure you have the [Azure PowerShell module](/powershell/azureps-cmdlets-docs) installed.</span><span class="sxs-lookup"><span data-stu-id="3dce3-127">First, make sure you have the [Azure PowerShell module](/powershell/azureps-cmdlets-docs) installed.</span></span>

<span data-ttu-id="3dce3-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dce3-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="3dce3-129">It will prompt you for your Azure user name and password.</span><span class="sxs-lookup"><span data-stu-id="3dce3-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="3dce3-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3dce3-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="3dce3-131">How to check which mode a collection is in</span><span class="sxs-lookup"><span data-stu-id="3dce3-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="3dce3-132">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dce3-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Check the collection mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="3dce3-134">The AclLevel property can have the following values:</span><span class="sxs-lookup"><span data-stu-id="3dce3-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="3dce3-135">Collection: the original publishing mode.</span><span class="sxs-lookup"><span data-stu-id="3dce3-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="3dce3-136">All users see all published apps.</span><span class="sxs-lookup"><span data-stu-id="3dce3-136">All users see all published apps.</span></span>
* <span data-ttu-id="3dce3-137">Application: the new publishing mode.</span><span class="sxs-lookup"><span data-stu-id="3dce3-137">Application: the new publishing mode.</span></span> <span data-ttu-id="3dce3-138">Users see only the apps published directly to them.</span><span class="sxs-lookup"><span data-stu-id="3dce3-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="3dce3-139">How to switch to application publishing mode</span><span class="sxs-lookup"><span data-stu-id="3dce3-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="3dce3-140">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dce3-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="3dce3-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span><span class="sxs-lookup"><span data-stu-id="3dce3-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="3dce3-142">How to list users who can see a specific application</span><span class="sxs-lookup"><span data-stu-id="3dce3-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="3dce3-143">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dce3-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="3dce3-144">This lists all users who can see the application.</span><span class="sxs-lookup"><span data-stu-id="3dce3-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="3dce3-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="3dce3-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="3dce3-146">How to assign an application to a user</span><span class="sxs-lookup"><span data-stu-id="3dce3-146">How to assign an application to a user</span></span>
<span data-ttu-id="3dce3-147">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dce3-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="3dce3-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span><span class="sxs-lookup"><span data-stu-id="3dce3-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="3dce3-149">How to remove an application from a user</span><span class="sxs-lookup"><span data-stu-id="3dce3-149">How to remove an application from a user</span></span>
<span data-ttu-id="3dce3-150">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3dce3-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="3dce3-151">Providing feedback</span><span class="sxs-lookup"><span data-stu-id="3dce3-151">Providing feedback</span></span>
<span data-ttu-id="3dce3-152">We appreciate your feedback and suggestions regarding this preview feature.</span><span class="sxs-lookup"><span data-stu-id="3dce3-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="3dce3-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span><span class="sxs-lookup"><span data-stu-id="3dce3-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="3dce3-154">Haven't had a chance to try the preview feature?</span><span class="sxs-lookup"><span data-stu-id="3dce3-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="3dce3-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span><span class="sxs-lookup"><span data-stu-id="3dce3-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>


