---
title: 'Azure AD Connect: Select your installation type | Microsoft Docs'
description: This topic walks you through how to select the installation type to use for Azure AD Connect
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: e0ee71d7d32583f81d7fea207c7440f044f3f0fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552711"
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="da084-103">Select which installation type to use for Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="da084-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="da084-104">Azure AD Connect has two installation types for new installation: Express and customized.</span><span class="sxs-lookup"><span data-stu-id="da084-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="da084-105">This topic helps you to decide which option to use during installation.</span><span class="sxs-lookup"><span data-stu-id="da084-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="da084-106">Express</span><span class="sxs-lookup"><span data-stu-id="da084-106">Express</span></span>
<span data-ttu-id="da084-107">Express is the most common option and is used by about 90% of all new installations.</span><span class="sxs-lookup"><span data-stu-id="da084-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="da084-108">It was designed to provide a configuration that works for the most common customer scenarios.</span><span class="sxs-lookup"><span data-stu-id="da084-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="da084-109">It assumes:</span><span class="sxs-lookup"><span data-stu-id="da084-109">It assumes:</span></span>

- <span data-ttu-id="da084-110">You have a single Active Directory forest on-premises.</span><span class="sxs-lookup"><span data-stu-id="da084-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="da084-111">You have an enterprise administrator account you can use for the installation.</span><span class="sxs-lookup"><span data-stu-id="da084-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="da084-112">You have less than 100,000 objects in your on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da084-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="da084-113">You get:</span><span class="sxs-lookup"><span data-stu-id="da084-113">You get:</span></span>

- <span data-ttu-id="da084-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="da084-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="da084-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="da084-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="da084-116">Synchronization of all eligible objects in all domains and all OUs.</span><span class="sxs-lookup"><span data-stu-id="da084-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="da084-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span><span class="sxs-lookup"><span data-stu-id="da084-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="da084-118">Options where you can still use Express:</span><span class="sxs-lookup"><span data-stu-id="da084-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="da084-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect \*\*Start the synchronization process...\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="da084-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect \*\*Start the synchronization process...\*\*\*.</span></span> <span data-ttu-id="da084-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span><span class="sxs-lookup"><span data-stu-id="da084-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="da084-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span><span class="sxs-lookup"><span data-stu-id="da084-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="da084-122">First go through express to get the initial installation completed.</span><span class="sxs-lookup"><span data-stu-id="da084-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="da084-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="da084-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="da084-124">Custom</span><span class="sxs-lookup"><span data-stu-id="da084-124">Custom</span></span>
<span data-ttu-id="da084-125">The customized path allows many more options than express.</span><span class="sxs-lookup"><span data-stu-id="da084-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="da084-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span><span class="sxs-lookup"><span data-stu-id="da084-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="da084-127">Use when:</span><span class="sxs-lookup"><span data-stu-id="da084-127">Use when:</span></span>

- <span data-ttu-id="da084-128">You do not have access to an enterprise admin account in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da084-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="da084-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span><span class="sxs-lookup"><span data-stu-id="da084-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="da084-130">You have domains in your forest not reachable from the Connect server.</span><span class="sxs-lookup"><span data-stu-id="da084-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="da084-131">You plan to use federation or pass-through authentication for user sign-in.</span><span class="sxs-lookup"><span data-stu-id="da084-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="da084-132">You have more than 100,000 objects and need to use a full SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da084-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="da084-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span><span class="sxs-lookup"><span data-stu-id="da084-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="da084-134">Upgrade from DirSync</span><span class="sxs-lookup"><span data-stu-id="da084-134">Upgrade from DirSync</span></span>
<span data-ttu-id="da084-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span><span class="sxs-lookup"><span data-stu-id="da084-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="da084-136">There are two different upgrade options:</span><span class="sxs-lookup"><span data-stu-id="da084-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="da084-137">In-place upgrade to install Connect on the same server.</span><span class="sxs-lookup"><span data-stu-id="da084-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="da084-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span><span class="sxs-lookup"><span data-stu-id="da084-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="da084-139">Upgrade from Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="da084-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="da084-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span><span class="sxs-lookup"><span data-stu-id="da084-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="da084-141">There are two different upgrade options:</span><span class="sxs-lookup"><span data-stu-id="da084-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="da084-142">In-place upgrade to install Connect on the same server.</span><span class="sxs-lookup"><span data-stu-id="da084-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="da084-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span><span class="sxs-lookup"><span data-stu-id="da084-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="da084-144">Migrate from FIM2010 or MIM2016</span><span class="sxs-lookup"><span data-stu-id="da084-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="da084-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span><span class="sxs-lookup"><span data-stu-id="da084-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="da084-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="da084-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="da084-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="da084-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da084-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="da084-148">Next steps</span></span>
<span data-ttu-id="da084-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span><span class="sxs-lookup"><span data-stu-id="da084-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
