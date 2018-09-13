---
title: Group Policy and MDM settings | Microsoft Docs
description: Provides information about group policy and mobile device management (MDM) settings that should be used on corporate-owned devices. These policies are applied to the user’s entire device.
services: active-directory
keywords: what are group Policy and MDM settings for Enterprise State Roaming, Enterprise State Roaming, windows cloud
documentationcenter: ''
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 71dd5281a618fe7367eab3e97daac069f77ab491
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662190"
---
# <a name="group-policy-and-mdm-settings"></a><span data-ttu-id="47aec-105">Group Policy and MDM settings</span><span class="sxs-lookup"><span data-stu-id="47aec-105">Group Policy and MDM settings</span></span>
<span data-ttu-id="47aec-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied to the user’s entire device.</span><span class="sxs-lookup"><span data-stu-id="47aec-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied to the user’s entire device.</span></span> <span data-ttu-id="47aec-107">Applying an MDM policy to disable settings sync for a personal, user-owned device will negatively impact the use of that device.</span><span class="sxs-lookup"><span data-stu-id="47aec-107">Applying an MDM policy to disable settings sync for a personal, user-owned device will negatively impact the use of that device.</span></span> <span data-ttu-id="47aec-108">Additionally, other user accounts on the device will also be affected by the policy.</span><span class="sxs-lookup"><span data-stu-id="47aec-108">Additionally, other user accounts on the device will also be affected by the policy.</span></span>

<span data-ttu-id="47aec-109">Enterprises that want to manage roaming for personal (unmanaged) devices can use the Azure portal to enable or disable roaming, rather than using Group Policy or MDM.</span><span class="sxs-lookup"><span data-stu-id="47aec-109">Enterprises that want to manage roaming for personal (unmanaged) devices can use the Azure portal to enable or disable roaming, rather than using Group Policy or MDM.</span></span>
<span data-ttu-id="47aec-110">The following tables describe the policy settings available.</span><span class="sxs-lookup"><span data-stu-id="47aec-110">The following tables describe the policy settings available.</span></span>

## <a name="mdm-settings"></a><span data-ttu-id="47aec-111">MDM settings</span><span class="sxs-lookup"><span data-stu-id="47aec-111">MDM settings</span></span>
<span data-ttu-id="47aec-112">The MDM policy settings apply to both Windows 10 and Windows 10 Mobile.</span><span class="sxs-lookup"><span data-stu-id="47aec-112">The MDM policy settings apply to both Windows 10 and Windows 10 Mobile.</span></span>  <span data-ttu-id="47aec-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span><span class="sxs-lookup"><span data-stu-id="47aec-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span></span>  <span data-ttu-id="47aec-114">Please refer to “Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span><span class="sxs-lookup"><span data-stu-id="47aec-114">Please refer to “Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span></span>

| <span data-ttu-id="47aec-115">Name</span><span class="sxs-lookup"><span data-stu-id="47aec-115">Name</span></span> | <span data-ttu-id="47aec-116">Description</span><span class="sxs-lookup"><span data-stu-id="47aec-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47aec-117">Allow Microsoft Account Connection</span><span class="sxs-lookup"><span data-stu-id="47aec-117">Allow Microsoft Account Connection</span></span> |<span data-ttu-id="47aec-118">Allows users to authenticate using a Microsoft account on the device</span><span class="sxs-lookup"><span data-stu-id="47aec-118">Allows users to authenticate using a Microsoft account on the device</span></span> |
| <span data-ttu-id="47aec-119">Allow Sync My Settings</span><span class="sxs-lookup"><span data-stu-id="47aec-119">Allow Sync My Settings</span></span> |<span data-ttu-id="47aec-120">Allows users to roam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span><span class="sxs-lookup"><span data-stu-id="47aec-120">Allows users to roam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span></span> |

## <a name="group-policy-settings"></a><span data-ttu-id="47aec-121">Group Policy settings</span><span class="sxs-lookup"><span data-stu-id="47aec-121">Group Policy settings</span></span>
<span data-ttu-id="47aec-122">The Group Policy settings apply to Windows 10 devices that are joined to an Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="47aec-122">The Group Policy settings apply to Windows 10 devices that are joined to an Active Directory domain.</span></span> <span data-ttu-id="47aec-123">The table also includes legacy settings that would appear to manage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in the description.</span><span class="sxs-lookup"><span data-stu-id="47aec-123">The table also includes legacy settings that would appear to manage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in the description.</span></span>

| <span data-ttu-id="47aec-124">Name</span><span class="sxs-lookup"><span data-stu-id="47aec-124">Name</span></span> | <span data-ttu-id="47aec-125">Description</span><span class="sxs-lookup"><span data-stu-id="47aec-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47aec-126">Accounts: Block Microsoft Accounts</span><span class="sxs-lookup"><span data-stu-id="47aec-126">Accounts: Block Microsoft Accounts</span></span> |<span data-ttu-id="47aec-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span><span class="sxs-lookup"><span data-stu-id="47aec-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span></span> |
| <span data-ttu-id="47aec-128">Do not sync</span><span class="sxs-lookup"><span data-stu-id="47aec-128">Do not sync</span></span> |<span data-ttu-id="47aec-129">Prevents users to roam Windows settings and app data</span><span class="sxs-lookup"><span data-stu-id="47aec-129">Prevents users to roam Windows settings and app data</span></span> |
| <span data-ttu-id="47aec-130">Do not sync personalize</span><span class="sxs-lookup"><span data-stu-id="47aec-130">Do not sync personalize</span></span> |<span data-ttu-id="47aec-131">Disables syncing of the Themes group</span><span class="sxs-lookup"><span data-stu-id="47aec-131">Disables syncing of the Themes group</span></span> |
| <span data-ttu-id="47aec-132">Do not sync browser settings</span><span class="sxs-lookup"><span data-stu-id="47aec-132">Do not sync browser settings</span></span> |<span data-ttu-id="47aec-133">Disables syncing of the Internet Explorer group</span><span class="sxs-lookup"><span data-stu-id="47aec-133">Disables syncing of the Internet Explorer group</span></span> |
| <span data-ttu-id="47aec-134">Do not sync passwords</span><span class="sxs-lookup"><span data-stu-id="47aec-134">Do not sync passwords</span></span> |<span data-ttu-id="47aec-135">Disables syncing of Passwords group</span><span class="sxs-lookup"><span data-stu-id="47aec-135">Disables syncing of Passwords group</span></span> |
| <span data-ttu-id="47aec-136">Do not sync other Windows settings</span><span class="sxs-lookup"><span data-stu-id="47aec-136">Do not sync other Windows settings</span></span> |<span data-ttu-id="47aec-137">Disables syncing of Other Windows settings group</span><span class="sxs-lookup"><span data-stu-id="47aec-137">Disables syncing of Other Windows settings group</span></span> |
| <span data-ttu-id="47aec-138">Do not sync desktop personalization</span><span class="sxs-lookup"><span data-stu-id="47aec-138">Do not sync desktop personalization</span></span> |<span data-ttu-id="47aec-139">Do not use; has no effect</span><span class="sxs-lookup"><span data-stu-id="47aec-139">Do not use; has no effect</span></span> |
| <span data-ttu-id="47aec-140">Do not sync on metered connections</span><span class="sxs-lookup"><span data-stu-id="47aec-140">Do not sync on metered connections</span></span> |<span data-ttu-id="47aec-141">Disables roaming on metered connections, such as cellular 3G</span><span class="sxs-lookup"><span data-stu-id="47aec-141">Disables roaming on metered connections, such as cellular 3G</span></span> |
| <span data-ttu-id="47aec-142">Do not sync apps</span><span class="sxs-lookup"><span data-stu-id="47aec-142">Do not sync apps</span></span> |<span data-ttu-id="47aec-143">Do not use; has no effect</span><span class="sxs-lookup"><span data-stu-id="47aec-143">Do not use; has no effect</span></span> |
| <span data-ttu-id="47aec-144">Do not sync app settings</span><span class="sxs-lookup"><span data-stu-id="47aec-144">Do not sync app settings</span></span> |<span data-ttu-id="47aec-145">Disables roaming of app data</span><span class="sxs-lookup"><span data-stu-id="47aec-145">Disables roaming of app data</span></span> |
| <span data-ttu-id="47aec-146">Do not sync start settings</span><span class="sxs-lookup"><span data-stu-id="47aec-146">Do not sync start settings</span></span> |<span data-ttu-id="47aec-147">Do not use; has no effect</span><span class="sxs-lookup"><span data-stu-id="47aec-147">Do not use; has no effect</span></span> |

## <a name="related-topics"></a><span data-ttu-id="47aec-148">Related topics</span><span class="sxs-lookup"><span data-stu-id="47aec-148">Related topics</span></span>
* [<span data-ttu-id="47aec-149">Enterprise State Roaming overview</span><span class="sxs-lookup"><span data-stu-id="47aec-149">Enterprise State Roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="47aec-150">Enable enterprise state roaming in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47aec-150">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="47aec-151">Settings and data roaming FAQ</span><span class="sxs-lookup"><span data-stu-id="47aec-151">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="47aec-152">Windows 10 roaming settings reference</span><span class="sxs-lookup"><span data-stu-id="47aec-152">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [<span data-ttu-id="47aec-153">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="47aec-153">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

