---
title: Setting up Azure AD Join for your users| Microsoft Docs
description: Explains how administrators can set up Azure AD Join for on-premises directory and device registration.
services: active-directory
documentationcenter: ''
author: femila
manager: swadhwa
editor: ''
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 0b5a86ef9159571c516ce36923f5cf3f8d0f9722
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670207"
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="520c2-103">Setting up Azure AD Join in your organization</span><span class="sxs-lookup"><span data-stu-id="520c2-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="520c2-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="520c2-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="520c2-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="520c2-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="520c2-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="520c2-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="520c2-107">Set up device registration</span><span class="sxs-lookup"><span data-stu-id="520c2-107">Set up device registration</span></span>
1. <span data-ttu-id="520c2-108">Log on to the Azure portal as an administrator.</span><span class="sxs-lookup"><span data-stu-id="520c2-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="520c2-109">On the left pane, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="520c2-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="520c2-110">On the **Directory** tab, select your directory.</span><span class="sxs-lookup"><span data-stu-id="520c2-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="520c2-111">Select the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="520c2-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="520c2-112">Go to the **Devices** section.</span><span class="sxs-lookup"><span data-stu-id="520c2-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="520c2-113">On the **devices** tab, set the following:</span><span class="sxs-lookup"><span data-stu-id="520c2-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="520c2-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="520c2-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="520c2-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span><span class="sxs-lookup"><span data-stu-id="520c2-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="520c2-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="520c2-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="520c2-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="520c2-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="520c2-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="520c2-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="520c2-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span><span class="sxs-lookup"><span data-stu-id="520c2-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="520c2-120">Global administrators and device owners are granted local administrator rights by default.</span><span class="sxs-lookup"><span data-stu-id="520c2-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="520c2-121"><center>![Set up device regisration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="520c2-121"><center>![Set up device regisration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="520c2-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span><span class="sxs-lookup"><span data-stu-id="520c2-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="520c2-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span><span class="sxs-lookup"><span data-stu-id="520c2-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="520c2-124">Users join a company-owned device directly to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="520c2-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="520c2-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="520c2-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="520c2-126">Users add work or school accounts to Windows on a personal device</span><span class="sxs-lookup"><span data-stu-id="520c2-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="520c2-127">Additional information</span><span class="sxs-lookup"><span data-stu-id="520c2-127">Additional information</span></span>
* [<span data-ttu-id="520c2-128">Windows 10 for the enterprise: Ways to use devices for work</span><span class="sxs-lookup"><span data-stu-id="520c2-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="520c2-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="520c2-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="520c2-130">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="520c2-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="520c2-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="520c2-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="520c2-132">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="520c2-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)


