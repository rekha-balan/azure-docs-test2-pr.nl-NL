---
title: Configure group settings using Azure Active Directory cmdlets | Microsoft Docs
description: How manage the settings for groups using Azure Active Directory cmdlets.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2017
ms.author: curtand
ms.openlocfilehash: 273f0f43a98cebba2d59a2e600be72eea3cb952e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554182"
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="1499e-103">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="1499e-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1499e-104">This content applies only to Unified groups, also known as Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="1499e-104">This content applies only to Unified groups, also known as Office 365 groups.</span></span> <span data-ttu-id="1499e-105">These cmdlets are in Public Preview at this moment.</span><span class="sxs-lookup"><span data-stu-id="1499e-105">These cmdlets are in Public Preview at this moment.</span></span>

<span data-ttu-id="1499e-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span><span class="sxs-lookup"><span data-stu-id="1499e-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="1499e-107">Initially, you will not see any Settings objects in your directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-107">Initially, you will not see any Settings objects in your directory.</span></span> <span data-ttu-id="1499e-108">This means your directory is configured with the default settings.</span><span class="sxs-lookup"><span data-stu-id="1499e-108">This means your directory is configured with the default settings.</span></span> <span data-ttu-id="1499e-109">To change the default settings, you must create a new settings object using a settings template.</span><span class="sxs-lookup"><span data-stu-id="1499e-109">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="1499e-110">Settings templates are defined by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1499e-110">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="1499e-111">There are several different settings templates.</span><span class="sxs-lookup"><span data-stu-id="1499e-111">There are several different settings templates.</span></span> <span data-ttu-id="1499e-112">To configure group settings for your directory, you will use the template named "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="1499e-112">To configure group settings for your directory, you will use the template named "Group.Unified".</span></span> <span data-ttu-id="1499e-113">To configure group settings on a single group, use the template named "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="1499e-113">To configure group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="1499e-114">This template is used to manage guest access to a group.</span><span class="sxs-lookup"><span data-stu-id="1499e-114">This template is used to manage guest access to a group.</span></span> 

<span data-ttu-id="1499e-115">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span><span class="sxs-lookup"><span data-stu-id="1499e-115">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="1499e-116">For more information about this module and for instructions how to download and install the module on your computer, please refer to [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="1499e-116">For more information about this module and for instructions how to download and install the module on your computer, please refer to [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="1499e-117">Please note that since these cmdlets are in public preview right now you will need to install the preview release of the module, which can be found [here](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.85).</span><span class="sxs-lookup"><span data-stu-id="1499e-117">Please note that since these cmdlets are in public preview right now you will need to install the preview release of the module, which can be found [here](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.85).</span></span>

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="1499e-118">Create settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="1499e-118">Create settings at the directory level</span></span>
<span data-ttu-id="1499e-119">These steps create settings at directory level, which apply to all Unified groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-119">These steps create settings at directory level, which apply to all Unified groups in the directory.</span></span>

1. <span data-ttu-id="1499e-120">In the DirectorySettings cmdlets you will need to specify the ID of the SettingsTemplate you want to use.</span><span class="sxs-lookup"><span data-stu-id="1499e-120">In the DirectorySettings cmdlets you will need to specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="1499e-121">If you do not know this ID, this cmdlet returns the list of all settings templates:</span><span class="sxs-lookup"><span data-stu-id="1499e-121">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="1499e-122">This cmdlet call returns all templates that are available:</span><span class="sxs-lookup"><span data-stu-id="1499e-122">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="1499e-123">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span><span class="sxs-lookup"><span data-stu-id="1499e-123">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="1499e-124">Next, create a new settings object based on that template:</span><span class="sxs-lookup"><span data-stu-id="1499e-124">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="1499e-125">Then update the usage guideline value:</span><span class="sxs-lookup"><span data-stu-id="1499e-125">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="1499e-126">Finally, apply the settings:</span><span class="sxs-lookup"><span data-stu-id="1499e-126">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $settings
  ```

<span data-ttu-id="1499e-127">Upon successful completion, the cmdlet returns the ID of the new settings object:</span><span class="sxs-lookup"><span data-stu-id="1499e-127">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="1499e-128">Here are the settings defined in the Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="1499e-128">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="1499e-129">**Setting**</span><span class="sxs-lookup"><span data-stu-id="1499e-129">**Setting**</span></span> | <span data-ttu-id="1499e-130">**Description**</span><span class="sxs-lookup"><span data-stu-id="1499e-130">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="1499e-131">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="1499e-131">EnableGroupCreation</span></span><li><span data-ttu-id="1499e-132">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="1499e-132">Type: Boolean</span></span><li><span data-ttu-id="1499e-133">Default: True</span><span class="sxs-lookup"><span data-stu-id="1499e-133">Default: True</span></span> |<span data-ttu-id="1499e-134">The flag indicating whether Unified Group creation is allowed in the directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-134">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="1499e-135">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="1499e-135">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="1499e-136">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-136">Type: String</span></span><li><span data-ttu-id="1499e-137">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-137">Default: “”</span></span> |<span data-ttu-id="1499e-138">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="1499e-138">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="1499e-139">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="1499e-139">UsageGuidelinesUrl</span></span><li><span data-ttu-id="1499e-140">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-140">Type: String</span></span><li><span data-ttu-id="1499e-141">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-141">Default: “”</span></span> |<span data-ttu-id="1499e-142">A link to the Group Usage Guidelines.</span><span class="sxs-lookup"><span data-stu-id="1499e-142">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="1499e-143">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="1499e-143">ClassificationDescriptions</span></span><li><span data-ttu-id="1499e-144">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-144">Type: String</span></span><li><span data-ttu-id="1499e-145">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-145">Default: “”</span></span> | <span data-ttu-id="1499e-146">A comma-delimited list of classification descriptions.</span><span class="sxs-lookup"><span data-stu-id="1499e-146">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="1499e-147">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="1499e-147">DefaultClassification</span></span><li><span data-ttu-id="1499e-148">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-148">Type: String</span></span><li><span data-ttu-id="1499e-149">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-149">Default: “”</span></span> | <span data-ttu-id="1499e-150">The classification that is to be used as the default classification for a group if none was specified.</span><span class="sxs-lookup"><span data-stu-id="1499e-150">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="1499e-151">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="1499e-151">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="1499e-152">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-152">Type: String</span></span><li><span data-ttu-id="1499e-153">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-153">Default: “”</span></span> |<span data-ttu-id="1499e-154">Not implemented yet</span><span class="sxs-lookup"><span data-stu-id="1499e-154">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="1499e-155">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="1499e-155">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="1499e-156">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="1499e-156">Type: Boolean</span></span><li><span data-ttu-id="1499e-157">Default: False</span><span class="sxs-lookup"><span data-stu-id="1499e-157">Default: False</span></span> | <span data-ttu-id="1499e-158">Boolean indicating whether or not a guest user can be an owner of groups.</span><span class="sxs-lookup"><span data-stu-id="1499e-158">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="1499e-159">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="1499e-159">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="1499e-160">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="1499e-160">Type: Boolean</span></span><li><span data-ttu-id="1499e-161">Default: True</span><span class="sxs-lookup"><span data-stu-id="1499e-161">Default: True</span></span> | <span data-ttu-id="1499e-162">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span><span class="sxs-lookup"><span data-stu-id="1499e-162">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="1499e-163">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="1499e-163">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="1499e-164">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-164">Type: String</span></span><li><span data-ttu-id="1499e-165">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-165">Default: “”</span></span> | <span data-ttu-id="1499e-166">The url of a link to the guest usage guidelines.</span><span class="sxs-lookup"><span data-stu-id="1499e-166">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="1499e-167">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="1499e-167">AllowToAddGuests</span></span><li><span data-ttu-id="1499e-168">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="1499e-168">Type: Boolean</span></span><li><span data-ttu-id="1499e-169">Default: True</span><span class="sxs-lookup"><span data-stu-id="1499e-169">Default: True</span></span> | <span data-ttu-id="1499e-170">A boolean indicating whether or not is is allowed to add guests to this directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-170">A boolean indicating whether or not is is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="1499e-171">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="1499e-171">ClassificationList</span></span><li><span data-ttu-id="1499e-172">Type: String</span><span class="sxs-lookup"><span data-stu-id="1499e-172">Type: String</span></span><li><span data-ttu-id="1499e-173">Default: “”</span><span class="sxs-lookup"><span data-stu-id="1499e-173">Default: “”</span></span> |<span data-ttu-id="1499e-174">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span><span class="sxs-lookup"><span data-stu-id="1499e-174">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="1499e-175">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="1499e-175">EnableGroupCreation</span></span><li><span data-ttu-id="1499e-176">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="1499e-176">Type: Boolean</span></span><li><span data-ttu-id="1499e-177">Default: True</span><span class="sxs-lookup"><span data-stu-id="1499e-177">Default: True</span></span> | <span data-ttu-id="1499e-178">A boolean indicating whether or not non-admin users can create new Unified groups.</span><span class="sxs-lookup"><span data-stu-id="1499e-178">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="1499e-179">Read settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="1499e-179">Read settings at the directory level</span></span>
<span data-ttu-id="1499e-180">These steps read settings at directory level, which apply to all Office groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-180">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="1499e-181">Read all existing directory settings:</span><span class="sxs-lookup"><span data-stu-id="1499e-181">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="1499e-182">This cmdlet returns a list of all directory settings:</span><span class="sxs-lookup"><span data-stu-id="1499e-182">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="1499e-183">Read all settings for a specific group:</span><span class="sxs-lookup"><span data-stu-id="1499e-183">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="1499e-184">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span><span class="sxs-lookup"><span data-stu-id="1499e-184">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="1499e-185">This cmdlet returns the names and values in this settings object for this specific group:</span><span class="sxs-lookup"><span data-stu-id="1499e-185">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="1499e-186">Update settings for a specific group</span><span class="sxs-lookup"><span data-stu-id="1499e-186">Update settings for a specific group</span></span>

1. <span data-ttu-id="1499e-187">Search for the settings template named "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="1499e-187">Search for the settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="1499e-188">Retrieve the template object for the Groups.Unified.Guest template:</span><span class="sxs-lookup"><span data-stu-id="1499e-188">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="1499e-189">Create a new settings object from the template:</span><span class="sxs-lookup"><span data-stu-id="1499e-189">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="1499e-190">Set the setting to the required value:</span><span class="sxs-lookup"><span data-stu-id="1499e-190">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="1499e-191">Create the new setting for the required group in the directory:</span><span class="sxs-lookup"><span data-stu-id="1499e-191">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="1499e-192">Update settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="1499e-192">Update settings at the directory level</span></span>

<span data-ttu-id="1499e-193">These steps update settings at directory level, which apply to all Unified groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-193">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="1499e-194">These examples assume there is already a Settings object in your directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-194">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="1499e-195">Find the existing Settings object:</span><span class="sxs-lookup"><span data-stu-id="1499e-195">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="1499e-196">Update the value:</span><span class="sxs-lookup"><span data-stu-id="1499e-196">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="1499e-197">Update the setting:</span><span class="sxs-lookup"><span data-stu-id="1499e-197">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="1499e-198">Remove settings at the directory level</span><span class="sxs-lookup"><span data-stu-id="1499e-198">Remove settings at the directory level</span></span>
<span data-ttu-id="1499e-199">This step removes settings at directory level, which apply to all Office groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="1499e-199">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="1499e-200">Cmdlet syntax reference</span><span class="sxs-lookup"><span data-stu-id="1499e-200">Cmdlet syntax reference</span></span>
<span data-ttu-id="1499e-201">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="1499e-201">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](https://docs.microsoft.com/powershell/azuread/).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="1499e-202">Additional reading</span><span class="sxs-lookup"><span data-stu-id="1499e-202">Additional reading</span></span>

* [<span data-ttu-id="1499e-203">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="1499e-203">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="1499e-204">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1499e-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
