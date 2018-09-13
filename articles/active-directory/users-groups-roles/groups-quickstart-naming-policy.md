---
title: Add naming policy for Office 365 groups in Azure Active Directory | Microsoft Docs
description: Explains how to add new users or delete existing users in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/08/2018
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: 8ebdb22ba5ca04a5c811b3b368055f5f4371c75f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858070"
---
# <a name="quickstart-naming-policy-for-groups-in-azure-active-directory"></a><span data-ttu-id="f50b3-103">Quickstart: Naming policy for groups in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f50b3-103">Quickstart: Naming policy for groups in Azure Active Directory</span></span>

<span data-ttu-id="f50b3-104">In this quickstart, you will set up naming policy in your Azure Active Directory (Azure AD) tenant for user-created Office 365 groups, to help you sort and search your tenant’s groups.</span><span class="sxs-lookup"><span data-stu-id="f50b3-104">In this quickstart, you will set up naming policy in your Azure Active Directory (Azure AD) tenant for user-created Office 365 groups, to help you sort and search your tenant’s groups.</span></span> <span data-ttu-id="f50b3-105">For example, you could use the naming policy to:</span><span class="sxs-lookup"><span data-stu-id="f50b3-105">For example, you could use the naming policy to:</span></span>

* <span data-ttu-id="f50b3-106">Communicate the function of a group, membership, geographic region, or who created the group.</span><span class="sxs-lookup"><span data-stu-id="f50b3-106">Communicate the function of a group, membership, geographic region, or who created the group.</span></span>
* <span data-ttu-id="f50b3-107">Help categorize groups in the address book.</span><span class="sxs-lookup"><span data-stu-id="f50b3-107">Help categorize groups in the address book.</span></span>
* <span data-ttu-id="f50b3-108">Block specific words from being used in group names and aliases.</span><span class="sxs-lookup"><span data-stu-id="f50b3-108">Block specific words from being used in group names and aliases.</span></span>

<span data-ttu-id="f50b3-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f50b3-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="install-powershell-cmdlets"></a><span data-ttu-id="f50b3-110">Install PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="f50b3-110">Install PowerShell cmdlets</span></span>

<span data-ttu-id="f50b3-111">Be sure to uninstall any older version of the Azure Active Directory PowerShell for Graph Module for Windows PowerShell and install [Azure Active Directory PowerShell for Graph - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137) before you run the PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="f50b3-111">Be sure to uninstall any older version of the Azure Active Directory PowerShell for Graph Module for Windows PowerShell and install [Azure Active Directory PowerShell for Graph - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137) before you run the PowerShell commands.</span></span> 

1. <span data-ttu-id="f50b3-112">Open the Windows PowerShell app as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f50b3-112">Open the Windows PowerShell app as an administrator.</span></span>
2. <span data-ttu-id="f50b3-113">Uninstall any previous version of AzureADPreview.</span><span class="sxs-lookup"><span data-stu-id="f50b3-113">Uninstall any previous version of AzureADPreview.</span></span>
  
  ````
  Uninstall-Module AzureADPreview
  ````
3. <span data-ttu-id="f50b3-114">Install the latest version of AzureADPreview.</span><span class="sxs-lookup"><span data-stu-id="f50b3-114">Install the latest version of AzureADPreview.</span></span>
  
  ````
  Install-Module AzureADPreview
  ````
<span data-ttu-id="f50b3-115">If you are prompted about accessing an untrusted repository, type **Y**. It might take few minutes for the new module to install.</span><span class="sxs-lookup"><span data-stu-id="f50b3-115">If you are prompted about accessing an untrusted repository, type **Y**. It might take few minutes for the new module to install.</span></span>

## <a name="set-up-naming-policy"></a><span data-ttu-id="f50b3-116">Set up naming policy</span><span class="sxs-lookup"><span data-stu-id="f50b3-116">Set up naming policy</span></span>

### <a name="step-1-sign-in-using-powershell-cmdlets"></a><span data-ttu-id="f50b3-117">Step 1: Sign in using PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="f50b3-117">Step 1: Sign in using PowerShell cmdlets</span></span>

1. <span data-ttu-id="f50b3-118">Open the Windows PowerShell app.</span><span class="sxs-lookup"><span data-stu-id="f50b3-118">Open the Windows PowerShell app.</span></span> <span data-ttu-id="f50b3-119">You don't need elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="f50b3-119">You don't need elevated privileges.</span></span>

2. <span data-ttu-id="f50b3-120">Run the following commands to prepare to run the cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f50b3-120">Run the following commands to prepare to run the cmdlets.</span></span>
  
  ````
  Import-Module AzureADPreview
  Connect-AzureAD
  ````
  <span data-ttu-id="f50b3-121">In the **Sign in to your Account** screen that opens, enter your admin account and password to connect you to your service, and select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="f50b3-121">In the **Sign in to your Account** screen that opens, enter your admin account and password to connect you to your service, and select **Sign in**.</span></span>

3. <span data-ttu-id="f50b3-122">Follow the steps in [Azure Active Directory cmdlets for configuring group settings](groups-settings-cmdlets.md) to create group settings for this tenant.</span><span class="sxs-lookup"><span data-stu-id="f50b3-122">Follow the steps in [Azure Active Directory cmdlets for configuring group settings](groups-settings-cmdlets.md) to create group settings for this tenant.</span></span>

### <a name="step-2-view-the-current-settings"></a><span data-ttu-id="f50b3-123">Step 2: View the current settings</span><span class="sxs-lookup"><span data-stu-id="f50b3-123">Step 2: View the current settings</span></span>

1. <span data-ttu-id="f50b3-124">View the current naming policy settings.</span><span class="sxs-lookup"><span data-stu-id="f50b3-124">View the current naming policy settings.</span></span>
  
  ````
  $Setting = Get-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id
  ````
  
2. <span data-ttu-id="f50b3-125">Display the current group settings.</span><span class="sxs-lookup"><span data-stu-id="f50b3-125">Display the current group settings.</span></span>
  
  ````
  $Setting.Values
  ````
  
### <a name="step-3-set-the-naming-policy-and-any-custom-blocked-words"></a><span data-ttu-id="f50b3-126">Step 3: Set the naming policy and any custom blocked words</span><span class="sxs-lookup"><span data-stu-id="f50b3-126">Step 3: Set the naming policy and any custom blocked words</span></span>

1. <span data-ttu-id="f50b3-127">Set the group name prefixes and suffixes in Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f50b3-127">Set the group name prefixes and suffixes in Azure AD PowerShell.</span></span>
  
  ````
  $Setting["PrefixSuffixNamingRequirement"] =“GRP_[GroupName]_[Department]"
  ````
  
2. <span data-ttu-id="f50b3-128">Set the custom blocked words that you want to restrict.</span><span class="sxs-lookup"><span data-stu-id="f50b3-128">Set the custom blocked words that you want to restrict.</span></span> <span data-ttu-id="f50b3-129">The following example illustrates how you can add your own custom words.</span><span class="sxs-lookup"><span data-stu-id="f50b3-129">The following example illustrates how you can add your own custom words.</span></span>
  
  ````
  $Setting["CustomBlockedWordsList"]=“Payroll,CEO,HR"
  ````
  
3. <span data-ttu-id="f50b3-130">Save the settings for the new policy to be effective, such as in the following example.</span><span class="sxs-lookup"><span data-stu-id="f50b3-130">Save the settings for the new policy to be effective, such as in the following example.</span></span>
  
  ````
  Set-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id -DirectorySetting $Setting
  ````
  
<span data-ttu-id="f50b3-131">That's it.</span><span class="sxs-lookup"><span data-stu-id="f50b3-131">That's it.</span></span> <span data-ttu-id="f50b3-132">You've set your naming policy and added your custom blocked words.</span><span class="sxs-lookup"><span data-stu-id="f50b3-132">You've set your naming policy and added your custom blocked words.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f50b3-133">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f50b3-133">Clean up resources</span></span>

1. <span data-ttu-id="f50b3-134">Set the group name prefixes and suffixes in Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f50b3-134">Set the group name prefixes and suffixes in Azure AD PowerShell.</span></span>
  
  ````
  $Setting["PrefixSuffixNamingRequirement"] =""
  ````
  
2. <span data-ttu-id="f50b3-135">Set the custom blocked words that you want to restrict.</span><span class="sxs-lookup"><span data-stu-id="f50b3-135">Set the custom blocked words that you want to restrict.</span></span> <span data-ttu-id="f50b3-136">The following example illustrates how you can add your own custom words.</span><span class="sxs-lookup"><span data-stu-id="f50b3-136">The following example illustrates how you can add your own custom words.</span></span>
  
  ````
  $Setting["CustomBlockedWordsList"]=""
  ````
  
3. <span data-ttu-id="f50b3-137">Save the settings for the new policy to be effective, such as in the following example.</span><span class="sxs-lookup"><span data-stu-id="f50b3-137">Save the settings for the new policy to be effective, such as in the following example.</span></span>
  
  ````
  Set-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id -DirectorySetting $Setting
  ````

## <a name="next-steps"></a><span data-ttu-id="f50b3-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="f50b3-138">Next steps</span></span>

<span data-ttu-id="f50b3-139">In this quickstart, you’ve learned how to use PowerShell cmdlets to set the naming policy for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f50b3-139">In this quickstart, you’ve learned how to use PowerShell cmdlets to set the naming policy for your Azure AD tenant.</span></span>

<span data-ttu-id="f50b3-140">For more information about technical constraints, adding a list of custom blocked words, or the end user experiences across Office 365 apps, advance to the next article to learn more about naming policy details.</span><span class="sxs-lookup"><span data-stu-id="f50b3-140">For more information about technical constraints, adding a list of custom blocked words, or the end user experiences across Office 365 apps, advance to the next article to learn more about naming policy details.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f50b3-141">Naming policy all details</span><span class="sxs-lookup"><span data-stu-id="f50b3-141">Naming policy all details</span></span>](groups-naming-policy.md)