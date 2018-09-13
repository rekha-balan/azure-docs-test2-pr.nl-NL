---
title: Migration of identity resources from Azure Germany to global Azure
description: This article provides help for migrating identity resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: d417206ead8cd5639a157326762cdf3ffe56a61c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865897"
---
# <a name="migration-of-identity-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="366f0-103">Migration of identity resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="366f0-103">Migration of identity resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="366f0-104">This article will provide you some help for the migration of Azure Identity resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="366f0-104">This article will provide you some help for the migration of Azure Identity resources from Azure Germany to global Azure.</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="366f0-105">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="366f0-105">Azure Active Directory</span></span>

<span data-ttu-id="366f0-106">Azure Active Directory in Azure Germany is separated from the Azure AD in global Azure.</span><span class="sxs-lookup"><span data-stu-id="366f0-106">Azure Active Directory in Azure Germany is separated from the Azure AD in global Azure.</span></span> <span data-ttu-id="366f0-107">There's currently no way to move users between Azure Germany and global Azure.</span><span class="sxs-lookup"><span data-stu-id="366f0-107">There's currently no way to move users between Azure Germany and global Azure.</span></span>

<span data-ttu-id="366f0-108">Default tenant names are always different, since Azure appends the suffix automatically depending on the environment.</span><span class="sxs-lookup"><span data-stu-id="366f0-108">Default tenant names are always different, since Azure appends the suffix automatically depending on the environment.</span></span> <span data-ttu-id="366f0-109">For example, a user name for a member of the "contoso" tenant in global Azure is `user1@contoso.microsoftazure.com`, in Azure Germany it's `user1@contoso.microsoftazure.de`.</span><span class="sxs-lookup"><span data-stu-id="366f0-109">For example, a user name for a member of the "contoso" tenant in global Azure is `user1@contoso.microsoftazure.com`, in Azure Germany it's `user1@contoso.microsoftazure.de`.</span></span>

<span data-ttu-id="366f0-110">When using custom domain names in Azure AD (like `contoso.com`), the domain name must first be registered in Azure.</span><span class="sxs-lookup"><span data-stu-id="366f0-110">When using custom domain names in Azure AD (like `contoso.com`), the domain name must first be registered in Azure.</span></span> <span data-ttu-id="366f0-111">Custom domain names can be defined **only in one** of the cloud environments at the same time.</span><span class="sxs-lookup"><span data-stu-id="366f0-111">Custom domain names can be defined **only in one** of the cloud environments at the same time.</span></span> <span data-ttu-id="366f0-112">The domain validation fails when the domain is already registered in *any* Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="366f0-112">The domain validation fails when the domain is already registered in *any* Azure Active Directory.</span></span> <span data-ttu-id="366f0-113">That means, a user `user1@contoso.com` that exists in Azure Germany can't exist also in global Azure under the same name at the same time.</span><span class="sxs-lookup"><span data-stu-id="366f0-113">That means, a user `user1@contoso.com` that exists in Azure Germany can't exist also in global Azure under the same name at the same time.</span></span> <span data-ttu-id="366f0-114">The registration for `contoso.com` would already fail.</span><span class="sxs-lookup"><span data-stu-id="366f0-114">The registration for `contoso.com` would already fail.</span></span>

<span data-ttu-id="366f0-115">A "soft" migration, where some users are already in the new and some are still in the old environment, would require different sign-in names for the different cloud environments.</span><span class="sxs-lookup"><span data-stu-id="366f0-115">A "soft" migration, where some users are already in the new and some are still in the old environment, would require different sign-in names for the different cloud environments.</span></span>

<span data-ttu-id="366f0-116">It's beyond the scope of this document to cover each possible migration scenario.</span><span class="sxs-lookup"><span data-stu-id="366f0-116">It's beyond the scope of this document to cover each possible migration scenario.</span></span> <span data-ttu-id="366f0-117">A recommendation depends, for example, on how you do provisioning of users, what options you have using different user names or UserPrincipalNames, or other dependencies that have to be taken into consideration.</span><span class="sxs-lookup"><span data-stu-id="366f0-117">A recommendation depends, for example, on how you do provisioning of users, what options you have using different user names or UserPrincipalNames, or other dependencies that have to be taken into consideration.</span></span> <span data-ttu-id="366f0-118">However, here are some hints how to inventory users and groups from your current environment.</span><span class="sxs-lookup"><span data-stu-id="366f0-118">However, here are some hints how to inventory users and groups from your current environment.</span></span>

<span data-ttu-id="366f0-119">For a list of all available cmdlets related to Azure AD, use:</span><span class="sxs-lookup"><span data-stu-id="366f0-119">For a list of all available cmdlets related to Azure AD, use:</span></span>

```powershell
Get-Help Get-AzureAD*
```

### <a name="inventory-of-users"></a><span data-ttu-id="366f0-120">Inventory of Users</span><span class="sxs-lookup"><span data-stu-id="366f0-120">Inventory of Users</span></span>

<span data-ttu-id="366f0-121">To get an overview of all the users and groups that exist in your Azure Active Directory, you can use the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="366f0-121">To get an overview of all the users and groups that exist in your Azure Active Directory, you can use the following PowerShell command:</span></span>

```powershell
Get-AzureADUser -All $true
```

<span data-ttu-id="366f0-122">To list only enabled accounts, use the following filter:</span><span class="sxs-lookup"><span data-stu-id="366f0-122">To list only enabled accounts, use the following filter:</span></span>

```powershell
Get-AzureADUser -All $true | Where-Object {$_.AccountEnabled -eq $true}
```

<span data-ttu-id="366f0-123">Make a full dump of all attributes in case you forget something:</span><span class="sxs-lookup"><span data-stu-id="366f0-123">Make a full dump of all attributes in case you forget something:</span></span>

```powershell
Get-AzureADUser -All $true | Where-Object {$_.AccountEnabled -eq $true} | Format-List *
```

<span data-ttu-id="366f0-124">Select the attributes you need to re-create the users:</span><span class="sxs-lookup"><span data-stu-id="366f0-124">Select the attributes you need to re-create the users:</span></span>

```powershell
Get-AzureADUser -All $true | Where-Object {$_.AccountEnabled -eq $true} | select UserPrincipalName,DisplayName,GivenName,Surname
```

<span data-ttu-id="366f0-125">To export the list to excel, use the `Export-Csv` cmdlet at the end.</span><span class="sxs-lookup"><span data-stu-id="366f0-125">To export the list to excel, use the `Export-Csv` cmdlet at the end.</span></span> <span data-ttu-id="366f0-126">A complete export might look like this example:</span><span class="sxs-lookup"><span data-stu-id="366f0-126">A complete export might look like this example:</span></span>

```powershell
Get-AzureADUser -All $true | Where-Object {$_.AccountEnabled -eq $true} | select UserPrincipalName,DisplayName,GivenName,Surname | Export-Csv -Path c:\temp\alluserUTF8.csv -Delimiter ";" -Encoding UTF8
```

> [!NOTE]
> <span data-ttu-id="366f0-127">Passwords can't be migrated.</span><span class="sxs-lookup"><span data-stu-id="366f0-127">Passwords can't be migrated.</span></span> <span data-ttu-id="366f0-128">You have to assign new passwords or use a self-service mechanism depending on your scenario.</span><span class="sxs-lookup"><span data-stu-id="366f0-128">You have to assign new passwords or use a self-service mechanism depending on your scenario.</span></span>


> [!NOTE]
> <span data-ttu-id="366f0-129">Depending on your environment, there might be other information you need to collect, for example Extensions, DirectReport, LicenceDetail etc.</span><span class="sxs-lookup"><span data-stu-id="366f0-129">Depending on your environment, there might be other information you need to collect, for example Extensions, DirectReport, LicenceDetail etc.</span></span>

<span data-ttu-id="366f0-130">Format your CSV as needed and follow the steps given in [Importing data from CSV](/powershell/azure/active-directory/importing-data.md?view=azureadps-2.0) to re-create the users in the new environment.</span><span class="sxs-lookup"><span data-stu-id="366f0-130">Format your CSV as needed and follow the steps given in [Importing data from CSV](/powershell/azure/active-directory/importing-data.md?view=azureadps-2.0) to re-create the users in the new environment.</span></span>

### <a name="inventory-of-groups"></a><span data-ttu-id="366f0-131">Inventory of Groups</span><span class="sxs-lookup"><span data-stu-id="366f0-131">Inventory of Groups</span></span>

<span data-ttu-id="366f0-132">To document group membership, use the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="366f0-132">To document group membership, use the following PowerShell cmdlets:</span></span>

```powershell
Get-AzureADGroup
```

<span data-ttu-id="366f0-133">Walk through the list of groups to get the list of members for each group:</span><span class="sxs-lookup"><span data-stu-id="366f0-133">Walk through the list of groups to get the list of members for each group:</span></span>

```powershell
Get-AzureADGroup | ForEach-Object {$_.DisplayName; Get-AzureADGroupMember -ObjectId $_.ObjectId}
```

### <a name="inventory-of-service-principals-and-applications"></a><span data-ttu-id="366f0-134">Inventory of Service Principals and Applications</span><span class="sxs-lookup"><span data-stu-id="366f0-134">Inventory of Service Principals and Applications</span></span>

<span data-ttu-id="366f0-135">Although all your service principals and applications have to be created new, it's good practice to document the status.</span><span class="sxs-lookup"><span data-stu-id="366f0-135">Although all your service principals and applications have to be created new, it's good practice to document the status.</span></span> <span data-ttu-id="366f0-136">You can use the following cmdlets to get an extensive list of all the service principals.</span><span class="sxs-lookup"><span data-stu-id="366f0-136">You can use the following cmdlets to get an extensive list of all the service principals.</span></span>

```powershell
Get-AzureADServicePrincipal |Format-List *
```

```powershell
Get-AzureADApplication |Format-List *
```

<span data-ttu-id="366f0-137">You can get more information by using other cmdlets starting with `Get-AzureADServicePrincipal*` or `Get-AzureADApplication*`.</span><span class="sxs-lookup"><span data-stu-id="366f0-137">You can get more information by using other cmdlets starting with `Get-AzureADServicePrincipal*` or `Get-AzureADApplication*`.</span></span> 

### <a name="directory-roles"></a><span data-ttu-id="366f0-138">Directory Roles</span><span class="sxs-lookup"><span data-stu-id="366f0-138">Directory Roles</span></span>

<span data-ttu-id="366f0-139">To document the current role assignment, use a similar way like shown above with groups:</span><span class="sxs-lookup"><span data-stu-id="366f0-139">To document the current role assignment, use a similar way like shown above with groups:</span></span>

```powershell
Get-AzureADDirectoryRole
```

<span data-ttu-id="366f0-140">Walk through each role to find users or applications associated with that role:</span><span class="sxs-lookup"><span data-stu-id="366f0-140">Walk through each role to find users or applications associated with that role:</span></span>

```powershell
Get-AzureADDirectoryRole | ForEach-Object {$_.DisplayName; Get-AzureADDirectoryRoleMember -ObjectId
$_.ObjectId | Format-Table}
```



## <a name="next-steps"></a><span data-ttu-id="366f0-141">Next Steps</span><span class="sxs-lookup"><span data-stu-id="366f0-141">Next Steps</span></span>

- <span data-ttu-id="366f0-142">Learn about [hybrid identity solutions](../active-directory/choose-hybrid-identity-solution.md)</span><span class="sxs-lookup"><span data-stu-id="366f0-142">Learn about [hybrid identity solutions](../active-directory/choose-hybrid-identity-solution.md)</span></span>
- <span data-ttu-id="366f0-143">Read [this blog](https://blogs.technet.microsoft.com/ralfwi/2017/01/24/using-adconnect-with-multiple-clouds/) about ways to synchronize into different cloud environments</span><span class="sxs-lookup"><span data-stu-id="366f0-143">Read [this blog](https://blogs.technet.microsoft.com/ralfwi/2017/01/24/using-adconnect-with-multiple-clouds/) about ways to synchronize into different cloud environments</span></span>

## <a name="references"></a><span data-ttu-id="366f0-144">References</span><span class="sxs-lookup"><span data-stu-id="366f0-144">References</span></span>

- [<span data-ttu-id="366f0-145">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="366f0-145">Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/)
- [<span data-ttu-id="366f0-146">Custom Domain Names</span><span class="sxs-lookup"><span data-stu-id="366f0-146">Custom Domain Names</span></span>](../active-directory/fundamentals/add-custom-domain.md)
- [<span data-ttu-id="366f0-147">Import data from CSV to Azure AD</span><span class="sxs-lookup"><span data-stu-id="366f0-147">Import data from CSV to Azure AD</span></span>](/powershell/azure/active-directory/importing-data.md?view=azureadps-2.0)

## <a name="adconnect"></a><span data-ttu-id="366f0-148">ADConnect</span><span class="sxs-lookup"><span data-stu-id="366f0-148">ADConnect</span></span>

<span data-ttu-id="366f0-149">ADConnect is a tool that synchronizes your identity data between on-premise Active Directory and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="366f0-149">ADConnect is a tool that synchronizes your identity data between on-premise Active Directory and Azure Active Directory.</span></span> <span data-ttu-id="366f0-150">The current version of ADConnect works for both cloud environments, Azure Germany and global Azure.</span><span class="sxs-lookup"><span data-stu-id="366f0-150">The current version of ADConnect works for both cloud environments, Azure Germany and global Azure.</span></span> <span data-ttu-id="366f0-151">ADConnect can only synchronize to one Azure AD at the same time.</span><span class="sxs-lookup"><span data-stu-id="366f0-151">ADConnect can only synchronize to one Azure AD at the same time.</span></span> <span data-ttu-id="366f0-152">If you want to synchronize to Azure Germany and global Azure at the same time, consider these topics:</span><span class="sxs-lookup"><span data-stu-id="366f0-152">If you want to synchronize to Azure Germany and global Azure at the same time, consider these topics:</span></span>

- <span data-ttu-id="366f0-153">Use an additional server for a second instance of ADConnect.</span><span class="sxs-lookup"><span data-stu-id="366f0-153">Use an additional server for a second instance of ADConnect.</span></span> <span data-ttu-id="366f0-154">It's not supported to have multiple instances of ADConnect on the same server.</span><span class="sxs-lookup"><span data-stu-id="366f0-154">It's not supported to have multiple instances of ADConnect on the same server.</span></span>
- <span data-ttu-id="366f0-155">Define a new sign-in name for your users.</span><span class="sxs-lookup"><span data-stu-id="366f0-155">Define a new sign-in name for your users.</span></span> <span data-ttu-id="366f0-156">The domain part (after the "@") of the sign-in name must be different in both environments.</span><span class="sxs-lookup"><span data-stu-id="366f0-156">The domain part (after the "@") of the sign-in name must be different in both environments.</span></span>
- <span data-ttu-id="366f0-157">Define a clear "source of truth" when you also synchronize backwards (from Azure AD to on-premise AD).</span><span class="sxs-lookup"><span data-stu-id="366f0-157">Define a clear "source of truth" when you also synchronize backwards (from Azure AD to on-premise AD).</span></span>

<span data-ttu-id="366f0-158">For more information how to synchronize in different cloud environments with ADConnect, read [this blog](https://blogs.technet.microsoft.com/ralfwi/2017/01/24/using-adconnect-with-multiple-clouds/).</span><span class="sxs-lookup"><span data-stu-id="366f0-158">For more information how to synchronize in different cloud environments with ADConnect, read [this blog](https://blogs.technet.microsoft.com/ralfwi/2017/01/24/using-adconnect-with-multiple-clouds/).</span></span>

<span data-ttu-id="366f0-159">If you're already using ADConnect for synchronization to and from Azure Germany, make sure you don't forget to migrate any manually created users.</span><span class="sxs-lookup"><span data-stu-id="366f0-159">If you're already using ADConnect for synchronization to and from Azure Germany, make sure you don't forget to migrate any manually created users.</span></span> <span data-ttu-id="366f0-160">The following PowerShell cmdlet lists all users that are not synchronized by ADConnect:</span><span class="sxs-lookup"><span data-stu-id="366f0-160">The following PowerShell cmdlet lists all users that are not synchronized by ADConnect:</span></span>

```powershell
Get-AzureADUser -All $true |Where-Object {$_.DirSyncEnabled -ne "True"}
```

### <a name="next-steps"></a><span data-ttu-id="366f0-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="366f0-161">Next Steps</span></span>

- <span data-ttu-id="366f0-162">Learn about [ADConnect](../active-directory/connect/active-directory-aadconnect-dirsync-deprecated.md)</span><span class="sxs-lookup"><span data-stu-id="366f0-162">Learn about [ADConnect](../active-directory/connect/active-directory-aadconnect-dirsync-deprecated.md)</span></span>







## <a name="multi-factor-authentication"></a><span data-ttu-id="366f0-163">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="366f0-163">Multi-Factor Authentication</span></span>

<span data-ttu-id="366f0-164">Since users have to be re-created in the new environment, the multi-factor authentication has to be redefined also.</span><span class="sxs-lookup"><span data-stu-id="366f0-164">Since users have to be re-created in the new environment, the multi-factor authentication has to be redefined also.</span></span> <span data-ttu-id="366f0-165">To get a list of user accounts that have multi-factor authentication enabled or enforced, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="366f0-165">To get a list of user accounts that have multi-factor authentication enabled or enforced, follow these steps:</span></span>

- <span data-ttu-id="366f0-166">sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="366f0-166">sign in to the Azure portal</span></span>
- <span data-ttu-id="366f0-167">select `Users` > `All Users` > `Multi-Factor Authentication`</span><span class="sxs-lookup"><span data-stu-id="366f0-167">select `Users` > `All Users` > `Multi-Factor Authentication`</span></span>
- <span data-ttu-id="366f0-168">after being redirected to the multi-factor authentication service page, set the appropriate filters to get a list of users.</span><span class="sxs-lookup"><span data-stu-id="366f0-168">after being redirected to the multi-factor authentication service page, set the appropriate filters to get a list of users.</span></span>

### <a name="next-steps"></a><span data-ttu-id="366f0-169">Next Steps</span><span class="sxs-lookup"><span data-stu-id="366f0-169">Next Steps</span></span>

- <span data-ttu-id="366f0-170">Learn about [Azure Multi-Factor Authentication](../active-directory/authentication/howto-mfa-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="366f0-170">Learn about [Azure Multi-Factor Authentication](../active-directory/authentication/howto-mfa-getstarted.md)</span></span>