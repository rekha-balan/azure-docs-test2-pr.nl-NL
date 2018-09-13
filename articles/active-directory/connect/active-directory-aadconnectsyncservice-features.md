---
title: Azure AD Connect sync service features and configuration | Microsoft Docs
description: Describes service side features for Azure AD Connect sync service.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: f721c371687addfe48d753e7289df78c2be1f3c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804796"
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="fcda8-103">Azure AD Connect sync service features</span><span class="sxs-lookup"><span data-stu-id="fcda8-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="fcda8-104">The synchronization feature of Azure AD Connect has two components:</span><span class="sxs-lookup"><span data-stu-id="fcda8-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="fcda8-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span><span class="sxs-lookup"><span data-stu-id="fcda8-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="fcda8-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span><span class="sxs-lookup"><span data-stu-id="fcda8-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="fcda8-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fcda8-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="fcda8-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](https://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="fcda8-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](https://aka.ms/aadposh).</span></span> <span data-ttu-id="fcda8-109">Download and install it separately from Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="fcda8-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="fcda8-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="fcda8-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="fcda8-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span><span class="sxs-lookup"><span data-stu-id="fcda8-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="fcda8-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="fcda8-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="fcda8-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="fcda8-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="fcda8-114">Many of these settings can only be changed by Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="fcda8-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="fcda8-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="fcda8-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="fcda8-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="fcda8-116">DirSyncFeature</span></span> | <span data-ttu-id="fcda8-117">Comment</span><span class="sxs-lookup"><span data-stu-id="fcda8-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="fcda8-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="fcda8-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="fcda8-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span><span class="sxs-lookup"><span data-stu-id="fcda8-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="fcda8-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="fcda8-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="fcda8-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span><span class="sxs-lookup"><span data-stu-id="fcda8-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="fcda8-122">After you have enabled a feature, it cannot be disabled again.</span><span class="sxs-lookup"><span data-stu-id="fcda8-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="fcda8-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="fcda8-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="fcda8-124">This feature will also be rolled out and enabled on directories created before this date.</span><span class="sxs-lookup"><span data-stu-id="fcda8-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="fcda8-125">You will receive an email notification when your directory is about to get this feature enabled.</span><span class="sxs-lookup"><span data-stu-id="fcda8-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="fcda8-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="fcda8-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="fcda8-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="fcda8-127">DirSyncFeature</span></span> | <span data-ttu-id="fcda8-128">Comment</span><span class="sxs-lookup"><span data-stu-id="fcda8-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="fcda8-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="fcda8-129">DeviceWriteback</span></span> |[<span data-ttu-id="fcda8-130">Azure AD Connect: Enabling device writeback</span><span class="sxs-lookup"><span data-stu-id="fcda8-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="fcda8-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="fcda8-131">DirectoryExtensions</span></span> |[<span data-ttu-id="fcda8-132">Azure AD Connect sync: Directory extensions</span><span class="sxs-lookup"><span data-stu-id="fcda8-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="fcda8-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="fcda8-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="fcda8-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span><span class="sxs-lookup"><span data-stu-id="fcda8-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="fcda8-135">Password Hash Sync</span><span class="sxs-lookup"><span data-stu-id="fcda8-135">Password Hash Sync</span></span> |[<span data-ttu-id="fcda8-136">Implementing password hash synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="fcda8-136">Implementing password hash synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-hash-synchronization.md) |
|<span data-ttu-id="fcda8-137">Pass-through Authentication</span><span class="sxs-lookup"><span data-stu-id="fcda8-137">Pass-through Authentication</span></span>|[<span data-ttu-id="fcda8-138">User sign-in with Azure Active Directory Pass-through Authentication</span><span class="sxs-lookup"><span data-stu-id="fcda8-138">User sign-in with Azure Active Directory Pass-through Authentication</span></span>](active-directory-aadconnect-pass-through-authentication.md)|
| <span data-ttu-id="fcda8-139">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="fcda8-139">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="fcda8-140">Preview: Group writeback</span><span class="sxs-lookup"><span data-stu-id="fcda8-140">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="fcda8-141">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="fcda8-141">UserWriteback</span></span> |<span data-ttu-id="fcda8-142">Not currently supported.</span><span class="sxs-lookup"><span data-stu-id="fcda8-142">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="fcda8-143">Duplicate attribute resiliency</span><span class="sxs-lookup"><span data-stu-id="fcda8-143">Duplicate attribute resiliency</span></span>
<span data-ttu-id="fcda8-144">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span><span class="sxs-lookup"><span data-stu-id="fcda8-144">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="fcda8-145">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span><span class="sxs-lookup"><span data-stu-id="fcda8-145">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="fcda8-146">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="fcda8-146">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="fcda8-147">UserPrincipalName soft match</span><span class="sxs-lookup"><span data-stu-id="fcda8-147">UserPrincipalName soft match</span></span>
<span data-ttu-id="fcda8-148">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span><span class="sxs-lookup"><span data-stu-id="fcda8-148">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="fcda8-149">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span><span class="sxs-lookup"><span data-stu-id="fcda8-149">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="fcda8-150">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span><span class="sxs-lookup"><span data-stu-id="fcda8-150">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="fcda8-151">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span><span class="sxs-lookup"><span data-stu-id="fcda8-151">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="fcda8-152">This feature is on by default for newly created Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="fcda8-152">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="fcda8-153">You can see if this feature is enabled for you by running:</span><span class="sxs-lookup"><span data-stu-id="fcda8-153">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="fcda8-154">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span><span class="sxs-lookup"><span data-stu-id="fcda8-154">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="fcda8-155">Synchronize userPrincipalName updates</span><span class="sxs-lookup"><span data-stu-id="fcda8-155">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="fcda8-156">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span><span class="sxs-lookup"><span data-stu-id="fcda8-156">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="fcda8-157">The user is managed (non-federated).</span><span class="sxs-lookup"><span data-stu-id="fcda8-157">The user is managed (non-federated).</span></span>
* <span data-ttu-id="fcda8-158">The user has not been assigned a license.</span><span class="sxs-lookup"><span data-stu-id="fcda8-158">The user has not been assigned a license.</span></span>

<span data-ttu-id="fcda8-159">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="fcda8-159">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="fcda8-160">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password hash sync. If you use federation, this feature is not supported.</span><span class="sxs-lookup"><span data-stu-id="fcda8-160">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password hash sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="fcda8-161">This feature is on by default for newly created Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="fcda8-161">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="fcda8-162">You can see if this feature is enabled for you by running:</span><span class="sxs-lookup"><span data-stu-id="fcda8-162">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="fcda8-163">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span><span class="sxs-lookup"><span data-stu-id="fcda8-163">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="fcda8-164">After enabling this feature, existing userPrincipalName values will remain as-is.</span><span class="sxs-lookup"><span data-stu-id="fcda8-164">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="fcda8-165">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span><span class="sxs-lookup"><span data-stu-id="fcda8-165">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="fcda8-166">See also</span><span class="sxs-lookup"><span data-stu-id="fcda8-166">See also</span></span>
* [<span data-ttu-id="fcda8-167">Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="fcda8-167">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="fcda8-168">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="fcda8-168">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

