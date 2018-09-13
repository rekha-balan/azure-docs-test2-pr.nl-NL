---
title: Set up a new device with Azure AD during Setup| Microsoft Docs
description: A topic that explains how users can set up Azure AD Join during their first run experience.
services: active-directory
documentationcenter: ''
author: femila
manager: swadhwa
editor: ''
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 1b07f807b261b09016cce4f60643b5b2ac6e0776
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540928"
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="4d200-103">Set up a new device with Azure AD during Setup</span><span class="sxs-lookup"><span data-stu-id="4d200-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="4d200-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span><span class="sxs-lookup"><span data-stu-id="4d200-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span></span> <span data-ttu-id="4d200-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span><span class="sxs-lookup"><span data-stu-id="4d200-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="4d200-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span><span class="sxs-lookup"><span data-stu-id="4d200-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

## <a name="to-join-a-device-to-azure-ad"></a><span data-ttu-id="4d200-107">To join a device to Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d200-107">To join a device to Azure AD</span></span>
1. <span data-ttu-id="4d200-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span><span class="sxs-lookup"><span data-stu-id="4d200-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="4d200-109">Follow the prompts to set up your device.</span><span class="sxs-lookup"><span data-stu-id="4d200-109">Follow the prompts to set up your device.</span></span>
2. <span data-ttu-id="4d200-110">Start by customizing your region and language.</span><span class="sxs-lookup"><span data-stu-id="4d200-110">Start by customizing your region and language.</span></span> <span data-ttu-id="4d200-111">Then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="4d200-111">Then accept the Microsoft Software License Terms.</span></span>
   <span data-ttu-id="4d200-112">![Customize for your region](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="4d200-112">![Customize for your region](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="4d200-113">Select the network you want to use for connecting to the Internet.</span><span class="sxs-lookup"><span data-stu-id="4d200-113">Select the network you want to use for connecting to the Internet.</span></span>
4. <span data-ttu-id="4d200-114">Select whether you're using a personal device or a company-owned device.</span><span class="sxs-lookup"><span data-stu-id="4d200-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="4d200-115">If it's company-owned, click **This device belongs to my organization**.</span><span class="sxs-lookup"><span data-stu-id="4d200-115">If it's company-owned, click **This device belongs to my organization**.</span></span> <span data-ttu-id="4d200-116">This starts the Azure AD Join experience.</span><span class="sxs-lookup"><span data-stu-id="4d200-116">This starts the Azure AD Join experience.</span></span> <span data-ttu-id="4d200-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span><span class="sxs-lookup"><span data-stu-id="4d200-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="4d200-118"><center>
   ![Who owns this PC screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="4d200-118"><center>
![Who owns this PC screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="4d200-119">Enter the credentials that were provided to you by your organization.</span><span class="sxs-lookup"><span data-stu-id="4d200-119">Enter the credentials that were provided to you by your organization.</span></span>
   <span data-ttu-id="4d200-120"><center>
   ![Sign-in screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="4d200-120"><center>
![Sign-in screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="4d200-121">After you have entered your user name, a matching tenant is located in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d200-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="4d200-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="4d200-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="4d200-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span><span class="sxs-lookup"><span data-stu-id="4d200-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> <span data-ttu-id="4d200-124">If company branding was configured, you will also see your organization’s logo and support text.</span><span class="sxs-lookup"><span data-stu-id="4d200-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="4d200-125">You're prompted for a multi-factor authentication challenge.</span><span class="sxs-lookup"><span data-stu-id="4d200-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="4d200-126">This challenge is configurable by an IT administrator.</span><span class="sxs-lookup"><span data-stu-id="4d200-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="4d200-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span><span class="sxs-lookup"><span data-stu-id="4d200-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="4d200-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span><span class="sxs-lookup"><span data-stu-id="4d200-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="4d200-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span><span class="sxs-lookup"><span data-stu-id="4d200-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>
12. <span data-ttu-id="4d200-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="4d200-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="4d200-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span><span class="sxs-lookup"><span data-stu-id="4d200-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="4d200-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span><span class="sxs-lookup"><span data-stu-id="4d200-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="4d200-133">You can then join the domain from the settings on your computer as you’ve done before.</span><span class="sxs-lookup"><span data-stu-id="4d200-133">You can then join the domain from the settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="4d200-134">Additional information</span><span class="sxs-lookup"><span data-stu-id="4d200-134">Additional information</span></span>
* [<span data-ttu-id="4d200-135">Windows 10 for the enterprise: Ways to use devices for work</span><span class="sxs-lookup"><span data-stu-id="4d200-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="4d200-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="4d200-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="4d200-137">Authenticating identities without passwords through Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="4d200-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="4d200-138">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="4d200-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="4d200-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="4d200-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="4d200-140">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="4d200-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)




