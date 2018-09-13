---
title: 'Azure AD Connect sync: Prevent accidental deletes | Microsoft Docs'
description: This topic describes the prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: ed679254edbb934bc5197821e07cf963c6b90376
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555281"
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a><span data-ttu-id="c4bda-103">Azure AD Connect sync: Prevent accidental deletes</span><span class="sxs-lookup"><span data-stu-id="c4bda-103">Azure AD Connect sync: Prevent accidental deletes</span></span>
<span data-ttu-id="c4bda-104">This topic describes the prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c4bda-104">This topic describes the prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.</span></span>

<span data-ttu-id="c4bda-105">When installing Azure AD Connect, prevent accidental deletes is enabled by default and configured to not allow an export with more than 500 deletes.</span><span class="sxs-lookup"><span data-stu-id="c4bda-105">When installing Azure AD Connect, prevent accidental deletes is enabled by default and configured to not allow an export with more than 500 deletes.</span></span> <span data-ttu-id="c4bda-106">This feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and other objects.</span><span class="sxs-lookup"><span data-stu-id="c4bda-106">This feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and other objects.</span></span>

## <a name="what-is-prevent-accidental-deletes"></a><span data-ttu-id="c4bda-107">What is prevent accidental deletes</span><span class="sxs-lookup"><span data-stu-id="c4bda-107">What is prevent accidental deletes</span></span>
<span data-ttu-id="c4bda-108">Common scenarios when you see many deletes include:</span><span class="sxs-lookup"><span data-stu-id="c4bda-108">Common scenarios when you see many deletes include:</span></span>

* <span data-ttu-id="c4bda-109">Changes to [filtering](active-directory-aadconnectsync-configure-filtering.md) where an entire [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) or [domain](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is unselected.</span><span class="sxs-lookup"><span data-stu-id="c4bda-109">Changes to [filtering](active-directory-aadconnectsync-configure-filtering.md) where an entire [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) or [domain](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is unselected.</span></span>
* <span data-ttu-id="c4bda-110">All objects in an OU are deleted.</span><span class="sxs-lookup"><span data-stu-id="c4bda-110">All objects in an OU are deleted.</span></span>
* <span data-ttu-id="c4bda-111">An OU is renamed so all objects in it are considered to be out of scope for synchronization.</span><span class="sxs-lookup"><span data-stu-id="c4bda-111">An OU is renamed so all objects in it are considered to be out of scope for synchronization.</span></span>

<span data-ttu-id="c4bda-112">The default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`.</span><span class="sxs-lookup"><span data-stu-id="c4bda-112">The default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="c4bda-113">You should configure this value to fit the size of your organization.</span><span class="sxs-lookup"><span data-stu-id="c4bda-113">You should configure this value to fit the size of your organization.</span></span> <span data-ttu-id="c4bda-114">Since the sync scheduler runs every 30 minutes, the value is the number of deletes seen within 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="c4bda-114">Since the sync scheduler runs every 30 minutes, the value is the number of deletes seen within 30 minutes.</span></span>

<span data-ttu-id="c4bda-115">If there are too many deletes staged to be exported to Azure AD, then the export stops and you receive an email like this:</span><span class="sxs-lookup"><span data-stu-id="c4bda-115">If there are too many deletes staged to be exported to Azure AD, then the export stops and you receive an email like this:</span></span>

![Prevent Accidental deletes email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> <span data-ttu-id="c4bda-117">*Hello (technical contact). At (time) the Identity synchronization service detected that the number of deletions exceeded the configured deletion threshold for (organization name). A total of (number) objects were sent for deletion in this Identity synchronization run. This met or exceeded the configured deletion threshold value of (number) objects. We need you to provide confirmation that these deletions should be processed before we will proceed. Please see the preventing accidental deletions for more information about the error listed in this email message.*</span><span class="sxs-lookup"><span data-stu-id="c4bda-117">*Hello (technical contact). At (time) the Identity synchronization service detected that the number of deletions exceeded the configured deletion threshold for (organization name). A total of (number) objects were sent for deletion in this Identity synchronization run. This met or exceeded the configured deletion threshold value of (number) objects. We need you to provide confirmation that these deletions should be processed before we will proceed. Please see the preventing accidental deletions for more information about the error listed in this email message.*</span></span>
>
> 

<span data-ttu-id="c4bda-118">You can also see the status `stopped-deletion-threshold-exceeded` when you look in the **Synchronization Service Manager** UI for the Export profile.</span><span class="sxs-lookup"><span data-stu-id="c4bda-118">You can also see the status `stopped-deletion-threshold-exceeded` when you look in the **Synchronization Service Manager** UI for the Export profile.</span></span>
<span data-ttu-id="c4bda-119">![Prevent Accidental deletes Sync Service Manager UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="c4bda-119">![Prevent Accidental deletes Sync Service Manager UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span></span>

<span data-ttu-id="c4bda-120">If this was unexpected, then investigate and take corrective actions.</span><span class="sxs-lookup"><span data-stu-id="c4bda-120">If this was unexpected, then investigate and take corrective actions.</span></span> <span data-ttu-id="c4bda-121">To see which objects are about to be deleted, do the following:</span><span class="sxs-lookup"><span data-stu-id="c4bda-121">To see which objects are about to be deleted, do the following:</span></span>

1. <span data-ttu-id="c4bda-122">Start **Synchronization Service** from the Start Menu.</span><span class="sxs-lookup"><span data-stu-id="c4bda-122">Start **Synchronization Service** from the Start Menu.</span></span>
2. <span data-ttu-id="c4bda-123">Go to **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="c4bda-123">Go to **Connectors**.</span></span>
3. <span data-ttu-id="c4bda-124">Select the Connector with type **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4bda-124">Select the Connector with type **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c4bda-125">Under **Actions** to the right, select **Search Connector Space**.</span><span class="sxs-lookup"><span data-stu-id="c4bda-125">Under **Actions** to the right, select **Search Connector Space**.</span></span>
5. <span data-ttu-id="c4bda-126">In the pop-up under **Scope**, select **Disconnected Since** and pick a time in the past.</span><span class="sxs-lookup"><span data-stu-id="c4bda-126">In the pop-up under **Scope**, select **Disconnected Since** and pick a time in the past.</span></span> <span data-ttu-id="c4bda-127">Click **Search**.</span><span class="sxs-lookup"><span data-stu-id="c4bda-127">Click **Search**.</span></span> <span data-ttu-id="c4bda-128">This page provides a view of all objects about to be deleted.</span><span class="sxs-lookup"><span data-stu-id="c4bda-128">This page provides a view of all objects about to be deleted.</span></span> <span data-ttu-id="c4bda-129">By clicking each item, you can get additional information about the object.</span><span class="sxs-lookup"><span data-stu-id="c4bda-129">By clicking each item, you can get additional information about the object.</span></span> <span data-ttu-id="c4bda-130">You can also click **Column Setting** to add additional attributes to be visible in the grid.</span><span class="sxs-lookup"><span data-stu-id="c4bda-130">You can also click **Column Setting** to add additional attributes to be visible in the grid.</span></span>

![Search Connector Space](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

<span data-ttu-id="c4bda-132">If all the deletes are desired, then do the following:</span><span class="sxs-lookup"><span data-stu-id="c4bda-132">If all the deletes are desired, then do the following:</span></span>

1. <span data-ttu-id="c4bda-133">To retrieve the current deletion threshold, run the PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`.</span><span class="sxs-lookup"><span data-stu-id="c4bda-133">To retrieve the current deletion threshold, run the PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="c4bda-134">Provide an Azure AD Global Administrator account and password.</span><span class="sxs-lookup"><span data-stu-id="c4bda-134">Provide an Azure AD Global Administrator account and password.</span></span> <span data-ttu-id="c4bda-135">The default value is 500.</span><span class="sxs-lookup"><span data-stu-id="c4bda-135">The default value is 500.</span></span>
2. <span data-ttu-id="c4bda-136">To temporarily disable this protection and let those deletes go through, run the PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`.</span><span class="sxs-lookup"><span data-stu-id="c4bda-136">To temporarily disable this protection and let those deletes go through, run the PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="c4bda-137">Provide an Azure AD Global Administrator account and password.</span><span class="sxs-lookup"><span data-stu-id="c4bda-137">Provide an Azure AD Global Administrator account and password.</span></span>
   <span data-ttu-id="c4bda-138">![Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span><span class="sxs-lookup"><span data-stu-id="c4bda-138">![Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span></span>
3. <span data-ttu-id="c4bda-139">With the Azure Active Directory Connector still selected, select the action **Run** and select **Export**.</span><span class="sxs-lookup"><span data-stu-id="c4bda-139">With the Azure Active Directory Connector still selected, select the action **Run** and select **Export**.</span></span>
4. <span data-ttu-id="c4bda-140">To re-enable the protection, run the PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span><span class="sxs-lookup"><span data-stu-id="c4bda-140">To re-enable the protection, run the PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span></span> <span data-ttu-id="c4bda-141">Replace 500 with the value you noticed when retrieving the current deletion threshold.</span><span class="sxs-lookup"><span data-stu-id="c4bda-141">Replace 500 with the value you noticed when retrieving the current deletion threshold.</span></span> <span data-ttu-id="c4bda-142">Provide an Azure AD Global Administrator account and password.</span><span class="sxs-lookup"><span data-stu-id="c4bda-142">Provide an Azure AD Global Administrator account and password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4bda-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4bda-143">Next steps</span></span>
<span data-ttu-id="c4bda-144">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="c4bda-144">**Overview topics**</span></span>

* [<span data-ttu-id="c4bda-145">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="c4bda-145">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="c4bda-146">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4bda-146">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)




