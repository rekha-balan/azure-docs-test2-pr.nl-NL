---
title: Azure Active Directory PowerShell cmdlets for group management in Azure AD | Microsoft Docs
description: This page provides PowerShell examples to help you manage your groups in Azure Active Directory
keywords: Azure AD, Azure Active Directory, PowerShell, Groups, Group management
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: curtand
ms.openlocfilehash: f4aeeaf13604443e0902112b4cc998ae1dcce4c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551963"
---
# <a name="azure-active-directory-preview-cmdlets-for-group-management"></a><span data-ttu-id="33059-104">Azure Active Directory preview cmdlets for group management</span><span class="sxs-lookup"><span data-stu-id="33059-104">Azure Active Directory preview cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Azure classic portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="33059-108">The following document will provide you with examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33059-108">The following document will provide you with examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="33059-109">It also provides information on how to get set up with the Azure AD PowerShell preview module.</span><span class="sxs-lookup"><span data-stu-id="33059-109">It also provides information on how to get set up with the Azure AD PowerShell preview module.</span></span> <span data-ttu-id="33059-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="33059-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="33059-111">Installing the Azure AD PowerShell module</span><span class="sxs-lookup"><span data-stu-id="33059-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="33059-112">To install the AzureAD PowerShell module, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="33059-112">To install the AzureAD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="33059-113">To verify that the preview module was installed, use the following command:</span><span class="sxs-lookup"><span data-stu-id="33059-113">To verify that the preview module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azureadpreview

    ModuleType Version    Name                                ExportedCommands
    ---------- -------    ----                                ----------------
    Binary     1.1.146.0  azureadpreview                      {Add-AzureADAdministrati...}

<span data-ttu-id="33059-114">Now you can start using the cmdlets in the module.</span><span class="sxs-lookup"><span data-stu-id="33059-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="33059-115">For a full description of the cmdlets in the Azure AD module, please refer to the [online reference documentation](https://docs.microsoft.com/en-us/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="33059-115">For a full description of the cmdlets in the Azure AD module, please refer to the [online reference documentation](https://docs.microsoft.com/en-us/powershell/azuread/).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="33059-116">Connecting to the directory</span><span class="sxs-lookup"><span data-stu-id="33059-116">Connecting to the directory</span></span>
<span data-ttu-id="33059-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span><span class="sxs-lookup"><span data-stu-id="33059-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="33059-118">To do this, use the following command:</span><span class="sxs-lookup"><span data-stu-id="33059-118">To do this, use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="33059-119">The cmdlet will prompt you for the credentials you want to use to access your directory.</span><span class="sxs-lookup"><span data-stu-id="33059-119">The cmdlet will prompt you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="33059-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span><span class="sxs-lookup"><span data-stu-id="33059-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="33059-121">The cmdlet will return a confirmation to show the session was connected successfully to your directory:</span><span class="sxs-lookup"><span data-stu-id="33059-121">The cmdlet will return a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="33059-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span><span class="sxs-lookup"><span data-stu-id="33059-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="33059-123">Retrieving groups</span><span class="sxs-lookup"><span data-stu-id="33059-123">Retrieving groups</span></span>
<span data-ttu-id="33059-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span><span class="sxs-lookup"><span data-stu-id="33059-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="33059-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span><span class="sxs-lookup"><span data-stu-id="33059-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="33059-126">The cmdlet will return all groups in the connected directory.</span><span class="sxs-lookup"><span data-stu-id="33059-126">The cmdlet will return all groups in the connected directory.</span></span>

<span data-ttu-id="33059-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span><span class="sxs-lookup"><span data-stu-id="33059-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="33059-128">The cmdlet will now return the group whose objectID matches the value of the parameter you entered:</span><span class="sxs-lookup"><span data-stu-id="33059-128">The cmdlet will now return the group whose objectID matches the value of the parameter you entered:</span></span>

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

<span data-ttu-id="33059-129">You can search for a specific group using the -filter parameter.</span><span class="sxs-lookup"><span data-stu-id="33059-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="33059-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="33059-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

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

<span data-ttu-id="33059-131">Note that the AzureAD PowerShell cmdlets implement the OData query standard, more information can be found [here](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="33059-131">Note that the AzureAD PowerShell cmdlets implement the OData query standard, more information can be found [here](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="33059-132">Creating groups</span><span class="sxs-lookup"><span data-stu-id="33059-132">Creating groups</span></span>
<span data-ttu-id="33059-133">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="33059-133">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="33059-134">This cmdlet creates a new security group called “Marketing":</span><span class="sxs-lookup"><span data-stu-id="33059-134">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="33059-135">Updating groups</span><span class="sxs-lookup"><span data-stu-id="33059-135">Updating groups</span></span>
<span data-ttu-id="33059-136">To update an existing group, use the Set-AzureADGroup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="33059-136">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="33059-137">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span><span class="sxs-lookup"><span data-stu-id="33059-137">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="33059-138">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span><span class="sxs-lookup"><span data-stu-id="33059-138">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

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

<span data-ttu-id="33059-139">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span><span class="sxs-lookup"><span data-stu-id="33059-139">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="33059-140">Now if we find the group again, we see the Description property is updated to reflect the new value:</span><span class="sxs-lookup"><span data-stu-id="33059-140">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="33059-141">Deleting groups</span><span class="sxs-lookup"><span data-stu-id="33059-141">Deleting groups</span></span>
<span data-ttu-id="33059-142">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span><span class="sxs-lookup"><span data-stu-id="33059-142">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="33059-143">Managing members of groups</span><span class="sxs-lookup"><span data-stu-id="33059-143">Managing members of groups</span></span>
<span data-ttu-id="33059-144">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span><span class="sxs-lookup"><span data-stu-id="33059-144">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="33059-145">This command adds a member to the Intune Administrators group we used in the previous example:</span><span class="sxs-lookup"><span data-stu-id="33059-145">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="33059-146">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span><span class="sxs-lookup"><span data-stu-id="33059-146">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="33059-147">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span><span class="sxs-lookup"><span data-stu-id="33059-147">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="33059-148">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span><span class="sxs-lookup"><span data-stu-id="33059-148">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="33059-149">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span><span class="sxs-lookup"><span data-stu-id="33059-149">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="33059-150">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span><span class="sxs-lookup"><span data-stu-id="33059-150">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="33059-151">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span><span class="sxs-lookup"><span data-stu-id="33059-151">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="33059-152">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span><span class="sxs-lookup"><span data-stu-id="33059-152">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="33059-153">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span><span class="sxs-lookup"><span data-stu-id="33059-153">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="33059-154">The value returned is a list of groups of which this user is a member.</span><span class="sxs-lookup"><span data-stu-id="33059-154">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="33059-155">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="33059-155">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="33059-156">Managing owners of groups</span><span class="sxs-lookup"><span data-stu-id="33059-156">Managing owners of groups</span></span>
<span data-ttu-id="33059-157">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="33059-157">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="33059-158">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span><span class="sxs-lookup"><span data-stu-id="33059-158">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="33059-159">To retrieve the owners of a group, use the Get-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="33059-159">To retrieve the owners of a group, use the Get-AzureADGroupOwner:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="33059-160">The cmdlet will return the list of owners for the specified group:</span><span class="sxs-lookup"><span data-stu-id="33059-160">The cmdlet will return the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="33059-161">If you want to remove an owner from a group, use Remove-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="33059-161">If you want to remove an owner from a group, use Remove-AzureADGroupOwner:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="next-steps"></a><span data-ttu-id="33059-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="33059-162">Next steps</span></span>
<span data-ttu-id="33059-163">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](https://docs.microsoft.com/en-us/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="33059-163">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](https://docs.microsoft.com/en-us/powershell/azuread/).</span></span>

* [<span data-ttu-id="33059-164">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="33059-164">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="33059-165">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33059-165">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
