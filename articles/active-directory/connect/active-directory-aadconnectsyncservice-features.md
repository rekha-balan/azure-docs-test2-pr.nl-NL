---
title: Azure AD Connect sync service features and configuration | Microsoft Docs
description: Describes service side features for Azure AD Connect sync service.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: 07bd2eaba717fb51ca67ee81a25faad2dda0f59a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554502"
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="b1d18-103">Azure AD Connect sync service features</span><span class="sxs-lookup"><span data-stu-id="b1d18-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="b1d18-104">The synchronization feature of Azure AD Connect has two components:</span><span class="sxs-lookup"><span data-stu-id="b1d18-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="b1d18-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span><span class="sxs-lookup"><span data-stu-id="b1d18-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="b1d18-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span><span class="sxs-lookup"><span data-stu-id="b1d18-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="b1d18-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1d18-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="b1d18-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="b1d18-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="b1d18-109">Download and install it separately from Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b1d18-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="b1d18-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="b1d18-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="b1d18-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span><span class="sxs-lookup"><span data-stu-id="b1d18-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="b1d18-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="b1d18-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="b1d18-113">![Get-MsolDirSyncFeatures result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="b1d18-113">![Get-MsolDirSyncFeatures result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="b1d18-114">Many of these settings can only be changed by Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b1d18-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="b1d18-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="b1d18-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="b1d18-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="b1d18-116">DirSyncFeature</span></span> | <span data-ttu-id="b1d18-117">Comment</span><span class="sxs-lookup"><span data-stu-id="b1d18-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="b1d18-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="b1d18-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="b1d18-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span><span class="sxs-lookup"><span data-stu-id="b1d18-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="b1d18-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="b1d18-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="b1d18-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span><span class="sxs-lookup"><span data-stu-id="b1d18-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="b1d18-122">After you have enabled a feature, it cannot be disabled again.</span><span class="sxs-lookup"><span data-stu-id="b1d18-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d18-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="b1d18-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="b1d18-124">This feature will also be rolled out and enabled on directories created before this date.</span><span class="sxs-lookup"><span data-stu-id="b1d18-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="b1d18-125">You will receive an email notification when your directory is about to get this feature enabled.</span><span class="sxs-lookup"><span data-stu-id="b1d18-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="b1d18-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="b1d18-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="b1d18-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="b1d18-127">DirSyncFeature</span></span> | <span data-ttu-id="b1d18-128">Comment</span><span class="sxs-lookup"><span data-stu-id="b1d18-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="b1d18-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="b1d18-129">DeviceWriteback</span></span> |[<span data-ttu-id="b1d18-130">Azure AD Connect: Enabling device writeback</span><span class="sxs-lookup"><span data-stu-id="b1d18-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="b1d18-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="b1d18-131">DirectoryExtensions</span></span> |[<span data-ttu-id="b1d18-132">Azure AD Connect sync: Directory extensions</span><span class="sxs-lookup"><span data-stu-id="b1d18-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="b1d18-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="b1d18-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="b1d18-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span><span class="sxs-lookup"><span data-stu-id="b1d18-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="b1d18-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="b1d18-135">PasswordSync</span></span> |[<span data-ttu-id="b1d18-136">Implementing password synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="b1d18-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="b1d18-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="b1d18-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="b1d18-138">Preview: Group writeback</span><span class="sxs-lookup"><span data-stu-id="b1d18-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="b1d18-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="b1d18-139">UserWriteback</span></span> |<span data-ttu-id="b1d18-140">Not currently supported.</span><span class="sxs-lookup"><span data-stu-id="b1d18-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="b1d18-141">Duplicate attribute resiliency</span><span class="sxs-lookup"><span data-stu-id="b1d18-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="b1d18-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span><span class="sxs-lookup"><span data-stu-id="b1d18-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="b1d18-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span><span class="sxs-lookup"><span data-stu-id="b1d18-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="b1d18-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="b1d18-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="b1d18-145">UserPrincipalName soft match</span><span class="sxs-lookup"><span data-stu-id="b1d18-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="b1d18-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span><span class="sxs-lookup"><span data-stu-id="b1d18-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="b1d18-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span><span class="sxs-lookup"><span data-stu-id="b1d18-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="b1d18-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span><span class="sxs-lookup"><span data-stu-id="b1d18-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="b1d18-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span><span class="sxs-lookup"><span data-stu-id="b1d18-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="b1d18-150">This feature is on by default for newly created Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="b1d18-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="b1d18-151">You can see if this feature is enabled for you by running:</span><span class="sxs-lookup"><span data-stu-id="b1d18-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="b1d18-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span><span class="sxs-lookup"><span data-stu-id="b1d18-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="b1d18-153">Synchronize userPrincipalName updates</span><span class="sxs-lookup"><span data-stu-id="b1d18-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="b1d18-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span><span class="sxs-lookup"><span data-stu-id="b1d18-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="b1d18-155">The user is managed (non-federated).</span><span class="sxs-lookup"><span data-stu-id="b1d18-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="b1d18-156">The user has not been assigned a license.</span><span class="sxs-lookup"><span data-stu-id="b1d18-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="b1d18-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="b1d18-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="b1d18-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span><span class="sxs-lookup"><span data-stu-id="b1d18-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="b1d18-159">This feature is on by default for newly created Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="b1d18-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="b1d18-160">You can see if this feature is enabled for you by running:</span><span class="sxs-lookup"><span data-stu-id="b1d18-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="b1d18-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span><span class="sxs-lookup"><span data-stu-id="b1d18-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="b1d18-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span><span class="sxs-lookup"><span data-stu-id="b1d18-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="b1d18-163">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span><span class="sxs-lookup"><span data-stu-id="b1d18-163">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="b1d18-164">See also</span><span class="sxs-lookup"><span data-stu-id="b1d18-164">See also</span></span>
* [<span data-ttu-id="b1d18-165">Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="b1d18-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="b1d18-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b1d18-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>


