---
title: Configure group settings using PowerShell in Azure Active Directory | Microsoft Docs
description: How manage the settings for groups using Azure Active Directory cmdlets
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 06/13/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 9e065b04083cce958bc42f2efade0038bf137f8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967829"
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="b7022-103">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="b7022-103">Azure Active Directory cmdlets for configuring group settings</span></span>
<span data-ttu-id="b7022-104">This article contains instructions for using Azure Active Directory (Azure AD) PowerShell cmdlets to create and update groups.</span><span class="sxs-lookup"><span data-stu-id="b7022-104">This article contains instructions for using Azure Active Directory (Azure AD) PowerShell cmdlets to create and update groups.</span></span> <span data-ttu-id="b7022-105">This content applies only to Office 365 groups (sometimes called unified groups).</span><span class="sxs-lookup"><span data-stu-id="b7022-105">This content applies only to Office 365 groups (sometimes called unified groups).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b7022-106">Some settings require an Azure Active Directory Premium P1 license.</span><span class="sxs-lookup"><span data-stu-id="b7022-106">Some settings require an Azure Active Directory Premium P1 license.</span></span> <span data-ttu-id="b7022-107">For more information, see the [Template settings](#template-settings) table.</span><span class="sxs-lookup"><span data-stu-id="b7022-107">For more information, see the [Template settings](#template-settings) table.</span></span>

<span data-ttu-id="b7022-108">For more information on how to prevent non-administrator users to create *security* groups, set `Set-MsolCompanySettings -UsersPermissionToCreateGroupsEnabled $False` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="b7022-108">For more information on how to prevent non-administrator users to create *security* groups, set `Set-MsolCompanySettings -UsersPermissionToCreateGroupsEnabled $False` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="b7022-109">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span><span class="sxs-lookup"><span data-stu-id="b7022-109">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="b7022-110">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span><span class="sxs-lookup"><span data-stu-id="b7022-110">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="b7022-111">To change the default settings, you must create a new settings object using a settings template.</span><span class="sxs-lookup"><span data-stu-id="b7022-111">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="b7022-112">Settings templates are defined by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b7022-112">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="b7022-113">There are several different settings templates.</span><span class="sxs-lookup"><span data-stu-id="b7022-113">There are several different settings templates.</span></span> <span data-ttu-id="b7022-114">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="b7022-114">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="b7022-115">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="b7022-115">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="b7022-116">This template is used to manage guest access to an Office 365 group.</span><span class="sxs-lookup"><span data-stu-id="b7022-116">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="b7022-117">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span><span class="sxs-lookup"><span data-stu-id="b7022-117">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="b7022-118">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="b7022-118">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="b7022-119">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="b7022-119">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="b7022-120">Retrieve a specific settings value</span><span class="sxs-lookup"><span data-stu-id="b7022-120">Retrieve a specific settings value</span></span>
<span data-ttu-id="b7022-121">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span><span class="sxs-lookup"><span data-stu-id="b7022-121">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="b7022-122">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span><span class="sxs-lookup"><span data-stu-id="b7022-122">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="b7022-123">You can read more about directory settings and their names further down in this article.</span><span class="sxs-lookup"><span data-stu-id="b7022-123">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="b7022-124">Create settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="b7022-124">Create settings at the directory level</span></span>
<span data-ttu-id="b7022-125">These steps create settings at directory level, which apply to all Office 365 groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="b7022-125">These steps create settings at directory level, which apply to all Office 365 groups in the directory.</span></span> <span data-ttu-id="b7022-126">The Get-AzureADDirectorySettingTemplate cmdlet is available only in the [Azure AD PowerShell Preview module for Graph](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="b7022-126">The Get-AzureADDirectorySettingTemplate cmdlet is available only in the [Azure AD PowerShell Preview module for Graph](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

1. <span data-ttu-id="b7022-127">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span><span class="sxs-lookup"><span data-stu-id="b7022-127">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="b7022-128">If you do not know this ID, this cmdlet returns the list of all settings templates:</span><span class="sxs-lookup"><span data-stu-id="b7022-128">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="b7022-129">This cmdlet call returns all templates that are available:</span><span class="sxs-lookup"><span data-stu-id="b7022-129">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Office 365 group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="b7022-130">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span><span class="sxs-lookup"><span data-stu-id="b7022-130">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="b7022-131">Next, create a new settings object based on that template:</span><span class="sxs-lookup"><span data-stu-id="b7022-131">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="b7022-132">Then update the usage guideline value:</span><span class="sxs-lookup"><span data-stu-id="b7022-132">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "https://guideline.example.com"

  ```  
5. <span data-ttu-id="b7022-133">Finally, apply the settings:</span><span class="sxs-lookup"><span data-stu-id="b7022-133">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="b7022-134">Upon successful completion, the cmdlet returns the ID of the new settings object:</span><span class="sxs-lookup"><span data-stu-id="b7022-134">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
## <a name="template-settings"></a><span data-ttu-id="b7022-135">Template settings</span><span class="sxs-lookup"><span data-stu-id="b7022-135">Template settings</span></span>
<span data-ttu-id="b7022-136">Here are the settings defined in the Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="b7022-136">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span> <span data-ttu-id="b7022-137">Unless otherwise indicated, these features require an Azure Active Directory Premium P1 license.</span><span class="sxs-lookup"><span data-stu-id="b7022-137">Unless otherwise indicated, these features require an Azure Active Directory Premium P1 license.</span></span> 

| <span data-ttu-id="b7022-138">**Setting**</span><span class="sxs-lookup"><span data-stu-id="b7022-138">**Setting**</span></span> | <span data-ttu-id="b7022-139">**Description**</span><span class="sxs-lookup"><span data-stu-id="b7022-139">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="b7022-140">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="b7022-140">EnableGroupCreation</span></span><li><span data-ttu-id="b7022-141">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="b7022-141">Type: Boolean</span></span><li><span data-ttu-id="b7022-142">Default: True</span><span class="sxs-lookup"><span data-stu-id="b7022-142">Default: True</span></span> |<span data-ttu-id="b7022-143">The flag indicating whether Office 365 group creation is allowed in the directory by non-admin users.</span><span class="sxs-lookup"><span data-stu-id="b7022-143">The flag indicating whether Office 365 group creation is allowed in the directory by non-admin users.</span></span> <span data-ttu-id="b7022-144">This setting does not require an Azure Active Directory Premium P1 license.</span><span class="sxs-lookup"><span data-stu-id="b7022-144">This setting does not require an Azure Active Directory Premium P1 license.</span></span>|
|  <ul><li><span data-ttu-id="b7022-145">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="b7022-145">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="b7022-146">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-146">Type: String</span></span><li><span data-ttu-id="b7022-147">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-147">Default: “”</span></span> |<span data-ttu-id="b7022-148">GUID of the security group for which the members are allowed to create Office 365 groups even when EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="b7022-148">GUID of the security group for which the members are allowed to create Office 365 groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="b7022-149">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="b7022-149">UsageGuidelinesUrl</span></span><li><span data-ttu-id="b7022-150">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-150">Type: String</span></span><li><span data-ttu-id="b7022-151">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-151">Default: “”</span></span> |<span data-ttu-id="b7022-152">A link to the Group Usage Guidelines.</span><span class="sxs-lookup"><span data-stu-id="b7022-152">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="b7022-153">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="b7022-153">ClassificationDescriptions</span></span><li><span data-ttu-id="b7022-154">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-154">Type: String</span></span><li><span data-ttu-id="b7022-155">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-155">Default: “”</span></span> | <span data-ttu-id="b7022-156">A comma-delimited list of classification descriptions.</span><span class="sxs-lookup"><span data-stu-id="b7022-156">A comma-delimited list of classification descriptions.</span></span> <span data-ttu-id="b7022-157">The value of ClassificationDescriptions is only valid in this format:</span><span class="sxs-lookup"><span data-stu-id="b7022-157">The value of ClassificationDescriptions is only valid in this format:</span></span>
  <span data-ttu-id="b7022-158">$setting[“ClassificationDescriptions”] ="Classification:Description,Classification:Description", where Classification matches the       strings in the ClassificationList.</span><span class="sxs-lookup"><span data-stu-id="b7022-158">$setting[“ClassificationDescriptions”] ="Classification:Description,Classification:Description", where Classification matches the       strings in the ClassificationList.</span></span>|
|  <ul><li><span data-ttu-id="b7022-159">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="b7022-159">DefaultClassification</span></span><li><span data-ttu-id="b7022-160">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-160">Type: String</span></span><li><span data-ttu-id="b7022-161">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-161">Default: “”</span></span> | <span data-ttu-id="b7022-162">The classification that is to be used as the default classification for a group if none was specified.</span><span class="sxs-lookup"><span data-stu-id="b7022-162">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="b7022-163">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="b7022-163">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="b7022-164">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-164">Type: String</span></span><li><span data-ttu-id="b7022-165">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-165">Default: “”</span></span> | <span data-ttu-id="b7022-166">String of a maximum length of 64 characters that defines the naming convention configured for Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="b7022-166">String of a maximum length of 64 characters that defines the naming convention configured for Office 365 groups.</span></span> <span data-ttu-id="b7022-167">For more information, see [Enforce a naming policy for Office 365 groups](groups-naming-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b7022-167">For more information, see [Enforce a naming policy for Office 365 groups](groups-naming-policy.md).</span></span> |
| <ul><li><span data-ttu-id="b7022-168">CustomBlockedWordsList</span><span class="sxs-lookup"><span data-stu-id="b7022-168">CustomBlockedWordsList</span></span><li><span data-ttu-id="b7022-169">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-169">Type: String</span></span><li><span data-ttu-id="b7022-170">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-170">Default: “”</span></span> | <span data-ttu-id="b7022-171">Comma-separated string of phrases that users will not be permitted to use in group names or aliases.</span><span class="sxs-lookup"><span data-stu-id="b7022-171">Comma-separated string of phrases that users will not be permitted to use in group names or aliases.</span></span> <span data-ttu-id="b7022-172">For more information, see [Enforce a naming policy for Office 365 groups](groups-naming-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b7022-172">For more information, see [Enforce a naming policy for Office 365 groups](groups-naming-policy.md).</span></span> |
| <ul><li><span data-ttu-id="b7022-173">EnableMSStandardBlockedWords</span><span class="sxs-lookup"><span data-stu-id="b7022-173">EnableMSStandardBlockedWords</span></span><li><span data-ttu-id="b7022-174">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="b7022-174">Type: Boolean</span></span><li><span data-ttu-id="b7022-175">Default: “False”</span><span class="sxs-lookup"><span data-stu-id="b7022-175">Default: “False”</span></span> | <span data-ttu-id="b7022-176">Do not use</span><span class="sxs-lookup"><span data-stu-id="b7022-176">Do not use</span></span>
|  <ul><li><span data-ttu-id="b7022-177">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="b7022-177">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="b7022-178">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="b7022-178">Type: Boolean</span></span><li><span data-ttu-id="b7022-179">Default: False</span><span class="sxs-lookup"><span data-stu-id="b7022-179">Default: False</span></span> | <span data-ttu-id="b7022-180">Boolean indicating whether or not a guest user can be an owner of groups.</span><span class="sxs-lookup"><span data-stu-id="b7022-180">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="b7022-181">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="b7022-181">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="b7022-182">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="b7022-182">Type: Boolean</span></span><li><span data-ttu-id="b7022-183">Default: True</span><span class="sxs-lookup"><span data-stu-id="b7022-183">Default: True</span></span> | <span data-ttu-id="b7022-184">Boolean indicating whether or not a guest user can have access to Office 365 groups content.</span><span class="sxs-lookup"><span data-stu-id="b7022-184">Boolean indicating whether or not a guest user can have access to Office 365 groups content.</span></span>  <span data-ttu-id="b7022-185">This setting does not require an Azure Active Directory Premium P1 license.</span><span class="sxs-lookup"><span data-stu-id="b7022-185">This setting does not require an Azure Active Directory Premium P1 license.</span></span>|
|  <ul><li><span data-ttu-id="b7022-186">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="b7022-186">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="b7022-187">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-187">Type: String</span></span><li><span data-ttu-id="b7022-188">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-188">Default: “”</span></span> | <span data-ttu-id="b7022-189">The url of a link to the guest usage guidelines.</span><span class="sxs-lookup"><span data-stu-id="b7022-189">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="b7022-190">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="b7022-190">AllowToAddGuests</span></span><li><span data-ttu-id="b7022-191">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="b7022-191">Type: Boolean</span></span><li><span data-ttu-id="b7022-192">Default: True</span><span class="sxs-lookup"><span data-stu-id="b7022-192">Default: True</span></span> | <span data-ttu-id="b7022-193">A boolean indicating whether or not is allowed to add guests to this directory.</span><span class="sxs-lookup"><span data-stu-id="b7022-193">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="b7022-194">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="b7022-194">ClassificationList</span></span><li><span data-ttu-id="b7022-195">Type: String</span><span class="sxs-lookup"><span data-stu-id="b7022-195">Type: String</span></span><li><span data-ttu-id="b7022-196">Default: “”</span><span class="sxs-lookup"><span data-stu-id="b7022-196">Default: “”</span></span> |<span data-ttu-id="b7022-197">A comma-delimited list of valid classification values that can be applied to Office 365 Groups.</span><span class="sxs-lookup"><span data-stu-id="b7022-197">A comma-delimited list of valid classification values that can be applied to Office 365 Groups.</span></span> |

## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="b7022-198">Read settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="b7022-198">Read settings at the directory level</span></span>
<span data-ttu-id="b7022-199">These steps read settings at directory level, which apply to all Office groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="b7022-199">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="b7022-200">Read all existing directory settings:</span><span class="sxs-lookup"><span data-stu-id="b7022-200">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="b7022-201">This cmdlet returns a list of all directory settings:</span><span class="sxs-lookup"><span data-stu-id="b7022-201">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="b7022-202">Read all settings for a specific group:</span><span class="sxs-lookup"><span data-stu-id="b7022-202">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="b7022-203">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span><span class="sxs-lookup"><span data-stu-id="b7022-203">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="b7022-204">This cmdlet returns the names and values in this settings object for this specific group:</span><span class="sxs-lookup"><span data-stu-id="b7022-204">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  CustomBlockedWordsList        
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            https://guideline.example.com
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="b7022-205">Update settings for a specific group</span><span class="sxs-lookup"><span data-stu-id="b7022-205">Update settings for a specific group</span></span>

1. <span data-ttu-id="b7022-206">Search for the settings template named "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="b7022-206">Search for the settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Office 365 group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="b7022-207">Retrieve the template object for the Groups.Unified.Guest template:</span><span class="sxs-lookup"><span data-stu-id="b7022-207">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="b7022-208">Create a new settings object from the template:</span><span class="sxs-lookup"><span data-stu-id="b7022-208">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="b7022-209">Set the setting to the required value:</span><span class="sxs-lookup"><span data-stu-id="b7022-209">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="b7022-210">Create the new setting for the required group in the directory:</span><span class="sxs-lookup"><span data-stu-id="b7022-210">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="b7022-211">Update settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="b7022-211">Update settings at the directory level</span></span>

<span data-ttu-id="b7022-212">These steps update settings at directory level, which apply to all Office 365 groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="b7022-212">These steps update settings at directory level, which apply to all Office 365 groups in the directory.</span></span> <span data-ttu-id="b7022-213">These examples assume there is already a Settings object in your directory.</span><span class="sxs-lookup"><span data-stu-id="b7022-213">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="b7022-214">Find the existing Settings object:</span><span class="sxs-lookup"><span data-stu-id="b7022-214">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="b7022-215">Update the value:</span><span class="sxs-lookup"><span data-stu-id="b7022-215">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="b7022-216">Update the setting:</span><span class="sxs-lookup"><span data-stu-id="b7022-216">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="b7022-217">Remove settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="b7022-217">Remove settings at the directory level</span></span>
<span data-ttu-id="b7022-218">This step removes settings at directory level, which apply to all Office groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="b7022-218">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="b7022-219">Cmdlet syntax reference</span><span class="sxs-lookup"><span data-stu-id="b7022-219">Cmdlet syntax reference</span></span>
<span data-ttu-id="b7022-220">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="b7022-220">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="b7022-221">Additional reading</span><span class="sxs-lookup"><span data-stu-id="b7022-221">Additional reading</span></span>

* [<span data-ttu-id="b7022-222">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="b7022-222">Managing access to resources with Azure Active Directory groups</span></span>](../fundamentals/active-directory-manage-groups.md)
* [<span data-ttu-id="b7022-223">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7022-223">Integrating your on-premises identities with Azure Active Directory</span></span>](../connect/active-directory-aadconnect.md)
