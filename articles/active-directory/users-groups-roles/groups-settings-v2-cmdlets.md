---
title: PowerShell examples for managing groups in Azure Active Directory  | Microsoft Docs
description: This page provides PowerShell examples to help you manage your groups in Azure Active Directory
keywords: Azure AD, Azure Active Directory, PowerShell, Groups, Group management
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 06/07/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 2ecd65bab478c37f1d3daa3ff86fdfadc788b301
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865587"
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="697d9-104">Azure Active Directory version 2 cmdlets for group management</span><span class="sxs-lookup"><span data-stu-id="697d9-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](../fundamentals/active-directory-groups-create-azure-portal.md)
> * [PowerShell](groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="697d9-107">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="697d9-107">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="697d9-108">It also tells you how to get set up with the Azure AD PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="697d9-108">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="697d9-109">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="697d9-109">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="697d9-110">Install the Azure AD PowerShell module</span><span class="sxs-lookup"><span data-stu-id="697d9-110">Install the Azure AD PowerShell module</span></span>
<span data-ttu-id="697d9-111">To install the Azure AD PowerShell module, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="697d9-111">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread
    PS C:\Windows\system32> import-module azuread

<span data-ttu-id="697d9-112">To verify that the module is ready to use, use the following command:</span><span class="sxs-lookup"><span data-stu-id="697d9-112">To verify that the module is ready to use, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="697d9-113">Now you can start using the cmdlets in the module.</span><span class="sxs-lookup"><span data-stu-id="697d9-113">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="697d9-114">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="697d9-114">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connect-to-the-directory"></a><span data-ttu-id="697d9-115">Connect to the directory</span><span class="sxs-lookup"><span data-stu-id="697d9-115">Connect to the directory</span></span>
<span data-ttu-id="697d9-116">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span><span class="sxs-lookup"><span data-stu-id="697d9-116">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="697d9-117">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="697d9-117">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="697d9-118">The cmdlet prompts you for the credentials you want to use to access your directory.</span><span class="sxs-lookup"><span data-stu-id="697d9-118">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="697d9-119">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span><span class="sxs-lookup"><span data-stu-id="697d9-119">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="697d9-120">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span><span class="sxs-lookup"><span data-stu-id="697d9-120">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="697d9-121">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span><span class="sxs-lookup"><span data-stu-id="697d9-121">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieve-groups"></a><span data-ttu-id="697d9-122">Retrieve groups</span><span class="sxs-lookup"><span data-stu-id="697d9-122">Retrieve groups</span></span>
<span data-ttu-id="697d9-123">To retrieve existing groups from your directory, use the Get-AzureADGroups cmdlet.</span><span class="sxs-lookup"><span data-stu-id="697d9-123">To retrieve existing groups from your directory, use the Get-AzureADGroups cmdlet.</span></span> 

<span data-ttu-id="697d9-124">To retrieve all groups in the directory, use the cmdlet without parameters:</span><span class="sxs-lookup"><span data-stu-id="697d9-124">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="697d9-125">The cmdlet returns all groups in the connected directory.</span><span class="sxs-lookup"><span data-stu-id="697d9-125">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="697d9-126">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span><span class="sxs-lookup"><span data-stu-id="697d9-126">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="697d9-127">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span><span class="sxs-lookup"><span data-stu-id="697d9-127">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="697d9-128">You can search for a specific group using the -filter parameter.</span><span class="sxs-lookup"><span data-stu-id="697d9-128">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="697d9-129">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="697d9-129">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> The Azure AD PowerShell cmdlets implement the OData query standard. For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="create-groups"></a><span data-ttu-id="697d9-132">Create groups</span><span class="sxs-lookup"><span data-stu-id="697d9-132">Create groups</span></span>
<span data-ttu-id="697d9-133">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="697d9-133">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="697d9-134">This cmdlet creates a new security group called “Marketing":</span><span class="sxs-lookup"><span data-stu-id="697d9-134">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="update-groups"></a><span data-ttu-id="697d9-135">Update groups</span><span class="sxs-lookup"><span data-stu-id="697d9-135">Update groups</span></span>
<span data-ttu-id="697d9-136">To update an existing group, use the Set-AzureADGroup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="697d9-136">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="697d9-137">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span><span class="sxs-lookup"><span data-stu-id="697d9-137">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="697d9-138">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span><span class="sxs-lookup"><span data-stu-id="697d9-138">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="697d9-139">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span><span class="sxs-lookup"><span data-stu-id="697d9-139">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="697d9-140">Now if we find the group again, we see the Description property is updated to reflect the new value:</span><span class="sxs-lookup"><span data-stu-id="697d9-140">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="delete-groups"></a><span data-ttu-id="697d9-141">Delete groups</span><span class="sxs-lookup"><span data-stu-id="697d9-141">Delete groups</span></span>
<span data-ttu-id="697d9-142">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span><span class="sxs-lookup"><span data-stu-id="697d9-142">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="manage-group-membership"></a><span data-ttu-id="697d9-143">Manage group membership</span><span class="sxs-lookup"><span data-stu-id="697d9-143">Manage group membership</span></span> 
### <a name="add-members"></a><span data-ttu-id="697d9-144">Add members</span><span class="sxs-lookup"><span data-stu-id="697d9-144">Add members</span></span>
<span data-ttu-id="697d9-145">To add new members to a group, use the Add-AzureADGroupMember cmdlet.</span><span class="sxs-lookup"><span data-stu-id="697d9-145">To add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="697d9-146">This command adds a member to the Intune Administrators group we used in the previous example:</span><span class="sxs-lookup"><span data-stu-id="697d9-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="697d9-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span><span class="sxs-lookup"><span data-stu-id="697d9-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

### <a name="get-members"></a><span data-ttu-id="697d9-148">Get members</span><span class="sxs-lookup"><span data-stu-id="697d9-148">Get members</span></span>
<span data-ttu-id="697d9-149">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span><span class="sxs-lookup"><span data-stu-id="697d9-149">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

### <a name="remove-members"></a><span data-ttu-id="697d9-150">Remove members</span><span class="sxs-lookup"><span data-stu-id="697d9-150">Remove members</span></span>
<span data-ttu-id="697d9-151">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span><span class="sxs-lookup"><span data-stu-id="697d9-151">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

### <a name="verify-members"></a><span data-ttu-id="697d9-152">Verify members</span><span class="sxs-lookup"><span data-stu-id="697d9-152">Verify members</span></span>
<span data-ttu-id="697d9-153">To verify the group memberships of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span><span class="sxs-lookup"><span data-stu-id="697d9-153">To verify the group memberships of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="697d9-154">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span><span class="sxs-lookup"><span data-stu-id="697d9-154">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="697d9-155">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span><span class="sxs-lookup"><span data-stu-id="697d9-155">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="697d9-156">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span><span class="sxs-lookup"><span data-stu-id="697d9-156">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="697d9-157">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span><span class="sxs-lookup"><span data-stu-id="697d9-157">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="697d9-158">The value returned is a list of groups of which this user is a member.</span><span class="sxs-lookup"><span data-stu-id="697d9-158">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="697d9-159">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="697d9-159">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="disable-group-creation-by-your-users"></a><span data-ttu-id="697d9-160">Disable group creation by your users</span><span class="sxs-lookup"><span data-stu-id="697d9-160">Disable group creation by your users</span></span>
<span data-ttu-id="697d9-161">You can prevent non-admin users from creating security groups.</span><span class="sxs-lookup"><span data-stu-id="697d9-161">You can prevent non-admin users from creating security groups.</span></span> <span data-ttu-id="697d9-162">The default behavior in Microsoft Online Directory Services (MSODS) is to allow non-admin users to create groups, whether or not self-service group management (SSGM) is also enabled.</span><span class="sxs-lookup"><span data-stu-id="697d9-162">The default behavior in Microsoft Online Directory Services (MSODS) is to allow non-admin users to create groups, whether or not self-service group management (SSGM) is also enabled.</span></span> <span data-ttu-id="697d9-163">The SSGM setting  controls behavior only in the My Apps access panel.</span><span class="sxs-lookup"><span data-stu-id="697d9-163">The SSGM setting  controls behavior only in the My Apps access panel.</span></span> 

<span data-ttu-id="697d9-164">To disable group creation for non-admin users:</span><span class="sxs-lookup"><span data-stu-id="697d9-164">To disable group creation for non-admin users:</span></span>

1. <span data-ttu-id="697d9-165">Verify that non-admin users are allowed to create groups:</span><span class="sxs-lookup"><span data-stu-id="697d9-165">Verify that non-admin users are allowed to create groups:</span></span>
   
  ````
  PS C:\> Get-MsolCompanyInformation | fl UsersPermissionToCreateGroupsEnabled
  ````
  
2. <span data-ttu-id="697d9-166">If it returns `UsersPermissionToCreateGroupsEnabled : True`, then non-admin users can create groups.</span><span class="sxs-lookup"><span data-stu-id="697d9-166">If it returns `UsersPermissionToCreateGroupsEnabled : True`, then non-admin users can create groups.</span></span> <span data-ttu-id="697d9-167">To disable this feature:</span><span class="sxs-lookup"><span data-stu-id="697d9-167">To disable this feature:</span></span>
  
  ```` 
  Set-MsolCompanySettings -UsersPermissionToCreateGroupsEnabled $False
  ````
  
## <a name="manage-owners-of-groups"></a><span data-ttu-id="697d9-168">Manage owners of groups</span><span class="sxs-lookup"><span data-stu-id="697d9-168">Manage owners of groups</span></span>
<span data-ttu-id="697d9-169">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="697d9-169">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="697d9-170">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span><span class="sxs-lookup"><span data-stu-id="697d9-170">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="697d9-171">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="697d9-171">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="697d9-172">The cmdlet returns the list of owners for the specified group:</span><span class="sxs-lookup"><span data-stu-id="697d9-172">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="697d9-173">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="697d9-173">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="697d9-174">Reserved aliases</span><span class="sxs-lookup"><span data-stu-id="697d9-174">Reserved aliases</span></span> 
<span data-ttu-id="697d9-175">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span><span class="sxs-lookup"><span data-stu-id="697d9-175">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="697d9-176">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span><span class="sxs-lookup"><span data-stu-id="697d9-176">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="697d9-177">abuse</span><span class="sxs-lookup"><span data-stu-id="697d9-177">abuse</span></span> 
* <span data-ttu-id="697d9-178">admin</span><span class="sxs-lookup"><span data-stu-id="697d9-178">admin</span></span> 
* <span data-ttu-id="697d9-179">administrator</span><span class="sxs-lookup"><span data-stu-id="697d9-179">administrator</span></span> 
* <span data-ttu-id="697d9-180">hostmaster</span><span class="sxs-lookup"><span data-stu-id="697d9-180">hostmaster</span></span> 
* <span data-ttu-id="697d9-181">majordomo</span><span class="sxs-lookup"><span data-stu-id="697d9-181">majordomo</span></span> 
* <span data-ttu-id="697d9-182">postmaster</span><span class="sxs-lookup"><span data-stu-id="697d9-182">postmaster</span></span> 
* <span data-ttu-id="697d9-183">root</span><span class="sxs-lookup"><span data-stu-id="697d9-183">root</span></span> 
* <span data-ttu-id="697d9-184">secure</span><span class="sxs-lookup"><span data-stu-id="697d9-184">secure</span></span> 
* <span data-ttu-id="697d9-185">security</span><span class="sxs-lookup"><span data-stu-id="697d9-185">security</span></span> 
* <span data-ttu-id="697d9-186">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="697d9-186">ssl-admin</span></span> 
* <span data-ttu-id="697d9-187">webmaster</span><span class="sxs-lookup"><span data-stu-id="697d9-187">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="697d9-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="697d9-188">Next steps</span></span>
<span data-ttu-id="697d9-189">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="697d9-189">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="697d9-190">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="697d9-190">Managing access to resources with Azure Active Directory groups</span></span>](../fundamentals/active-directory-manage-groups.md)
* [<span data-ttu-id="697d9-191">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="697d9-191">Integrating your on-premises identities with Azure Active Directory</span></span>](../connect/active-directory-aadconnect.md)
