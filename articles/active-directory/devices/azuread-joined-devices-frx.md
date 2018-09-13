---
title: Join a new Windows 10 device with Azure AD during a first run | Microsoft Docs
description: A topic that explains how users can set up Azure AD Join during the first run experience.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/25/2018
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eaf0b3e3b607145598660dbb64cadd5a277360cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865781"
---
# <a name="tutorial-join-a-new-windows-10-device-with-azure-ad-during-a-first-run"></a><span data-ttu-id="c93fd-103">Tutorial: Join a new Windows 10 device with Azure AD during a first run</span><span class="sxs-lookup"><span data-stu-id="c93fd-103">Tutorial: Join a new Windows 10 device with Azure AD during a first run</span></span>

<span data-ttu-id="c93fd-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span><span class="sxs-lookup"><span data-stu-id="c93fd-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="c93fd-105">For more information, see the [introduction to device management in Azure Active Directory](overview.md).</span><span class="sxs-lookup"><span data-stu-id="c93fd-105">For more information, see the [introduction to device management in Azure Active Directory](overview.md).</span></span>

<span data-ttu-id="c93fd-106">With Windows 10, You can join a new device to Azure AD during the first-run experience (FRX).</span><span class="sxs-lookup"><span data-stu-id="c93fd-106">With Windows 10, You can join a new device to Azure AD during the first-run experience (FRX).</span></span>  
<span data-ttu-id="c93fd-107">This enables you to distribute shrink-wrapped devices to your employees or students.</span><span class="sxs-lookup"><span data-stu-id="c93fd-107">This enables you to distribute shrink-wrapped devices to your employees or students.</span></span>

<span data-ttu-id="c93fd-108">If you have either Windows 10 Professional or Windows 10 Enterprise installed on a device, the experience defaults to the setup process for company-owned devices.</span><span class="sxs-lookup"><span data-stu-id="c93fd-108">If you have either Windows 10 Professional or Windows 10 Enterprise installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

<span data-ttu-id="c93fd-109">In the Windows *out-of-box experience*, joining an on-premises Active Directory (AD) domain is not supported.</span><span class="sxs-lookup"><span data-stu-id="c93fd-109">In the Windows *out-of-box experience*, joining an on-premises Active Directory (AD) domain is not supported.</span></span> <span data-ttu-id="c93fd-110">If you plan to join a computer to an AD domain, during setup, you should select the link **Set up Windows with a local account**.</span><span class="sxs-lookup"><span data-stu-id="c93fd-110">If you plan to join a computer to an AD domain, during setup, you should select the link **Set up Windows with a local account**.</span></span> <span data-ttu-id="c93fd-111">You can then join the domain from the settings on your computer.</span><span class="sxs-lookup"><span data-stu-id="c93fd-111">You can then join the domain from the settings on your computer.</span></span>
 
<span data-ttu-id="c93fd-112">In this tutorial, you learn how to join a device to Azure AD during FRX:</span><span class="sxs-lookup"><span data-stu-id="c93fd-112">In this tutorial, you learn how to join a device to Azure AD during FRX:</span></span>
 > [!div class="checklist"]
> * <span data-ttu-id="c93fd-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c93fd-113">Prerequisites</span></span>
> * <span data-ttu-id="c93fd-114">Joining a device</span><span class="sxs-lookup"><span data-stu-id="c93fd-114">Joining a device</span></span>
> * <span data-ttu-id="c93fd-115">Verification</span><span class="sxs-lookup"><span data-stu-id="c93fd-115">Verification</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c93fd-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c93fd-116">Prerequisites</span></span>

<span data-ttu-id="c93fd-117">To join a Windows 10 device, the device registration service must be configured to enable you to register devices.</span><span class="sxs-lookup"><span data-stu-id="c93fd-117">To join a Windows 10 device, the device registration service must be configured to enable you to register devices.</span></span> <span data-ttu-id="c93fd-118">In addition to having permission to joining devices in your Azure AD tenant, you must have fewer devices registered than the configured maximum.</span><span class="sxs-lookup"><span data-stu-id="c93fd-118">In addition to having permission to joining devices in your Azure AD tenant, you must have fewer devices registered than the configured maximum.</span></span> <span data-ttu-id="c93fd-119">For more information, see [configure device settings](device-management-azure-portal.md#configure-device-settings).</span><span class="sxs-lookup"><span data-stu-id="c93fd-119">For more information, see [configure device settings](device-management-azure-portal.md#configure-device-settings).</span></span>

<span data-ttu-id="c93fd-120">In addition, if your tenant is federated, your Identity provider MUST support WS-Fed and WS-Trust username/password endpoint.</span><span class="sxs-lookup"><span data-stu-id="c93fd-120">In addition, if your tenant is federated, your Identity provider MUST support WS-Fed and WS-Trust username/password endpoint.</span></span> <span data-ttu-id="c93fd-121">This can be version 1.3 or 2005.</span><span class="sxs-lookup"><span data-stu-id="c93fd-121">This can be version 1.3 or 2005.</span></span> <span data-ttu-id="c93fd-122">This protocol support is required to both join the device to Azure AD and log on to the device with a password.</span><span class="sxs-lookup"><span data-stu-id="c93fd-122">This protocol support is required to both join the device to Azure AD and log on to the device with a password.</span></span>

## <a name="joining-a-device"></a><span data-ttu-id="c93fd-123">Joining a device</span><span class="sxs-lookup"><span data-stu-id="c93fd-123">Joining a device</span></span>

<span data-ttu-id="c93fd-124">**To join a Windows 10 device to Azure AD during FRX:**</span><span class="sxs-lookup"><span data-stu-id="c93fd-124">**To join a Windows 10 device to Azure AD during FRX:**</span></span>


1. <span data-ttu-id="c93fd-125">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span><span class="sxs-lookup"><span data-stu-id="c93fd-125">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="c93fd-126">Follow the prompts to set up your device.</span><span class="sxs-lookup"><span data-stu-id="c93fd-126">Follow the prompts to set up your device.</span></span>

2. <span data-ttu-id="c93fd-127">Start by customizing your region and language.</span><span class="sxs-lookup"><span data-stu-id="c93fd-127">Start by customizing your region and language.</span></span> <span data-ttu-id="c93fd-128">Then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="c93fd-128">Then accept the Microsoft Software License Terms.</span></span>
 
    ![Customize for your region](./media/azuread-joined-devices-frx/01.png)

3. <span data-ttu-id="c93fd-130">Select the network you want to use for connecting to the Internet.</span><span class="sxs-lookup"><span data-stu-id="c93fd-130">Select the network you want to use for connecting to the Internet.</span></span>

4. <span data-ttu-id="c93fd-131">Click **This device belongs to my organization**.</span><span class="sxs-lookup"><span data-stu-id="c93fd-131">Click **This device belongs to my organization**.</span></span> 

    ![Who owns this PC screen](./media/azuread-joined-devices-frx/02.png)

5. <span data-ttu-id="c93fd-133">Enter the credentials that were provided to you by your organization, and then click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="c93fd-133">Enter the credentials that were provided to you by your organization, and then click **Sign in**.</span></span>

    ![Sign-in screen](./media/azuread-joined-devices-frx/03.png)

6. <span data-ttu-id="c93fd-135">You device locates a matching tenant in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c93fd-135">You device locates a matching tenant in Azure AD.</span></span> <span data-ttu-id="c93fd-136">If you are in a federated domain, you are redirected to your on-premises Secure Token Service (STS) server, for example, Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="c93fd-136">If you are in a federated domain, you are redirected to your on-premises Secure Token Service (STS) server, for example, Active Directory Federation Services (AD FS).</span></span>

7. <span data-ttu-id="c93fd-137">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span><span class="sxs-lookup"><span data-stu-id="c93fd-137">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> 

8. <span data-ttu-id="c93fd-138">You are prompted for a multi-factor authentication challenge.</span><span class="sxs-lookup"><span data-stu-id="c93fd-138">You are prompted for a multi-factor authentication challenge.</span></span> 
 
9. <span data-ttu-id="c93fd-139">Azure AD checks whether an enrollment in mobile device management is required.</span><span class="sxs-lookup"><span data-stu-id="c93fd-139">Azure AD checks whether an enrollment in mobile device management is required.</span></span>

10. <span data-ttu-id="c93fd-140">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if applicable.</span><span class="sxs-lookup"><span data-stu-id="c93fd-140">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if applicable.</span></span>

11. <span data-ttu-id="c93fd-141">If you are:</span><span class="sxs-lookup"><span data-stu-id="c93fd-141">If you are:</span></span>
    - <span data-ttu-id="c93fd-142">A managed user, Windows takes you to the desktop through the automatic sign-in process.</span><span class="sxs-lookup"><span data-stu-id="c93fd-142">A managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>

    - <span data-ttu-id="c93fd-143">A federated user, you are directed to the Windows sign-in screen to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="c93fd-143">A federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

## <a name="verification"></a><span data-ttu-id="c93fd-144">Verification</span><span class="sxs-lookup"><span data-stu-id="c93fd-144">Verification</span></span>

<span data-ttu-id="c93fd-145">To verify whether a device is joined to your Azure AD, review the **Access work or school** dialog on your Windows device.</span><span class="sxs-lookup"><span data-stu-id="c93fd-145">To verify whether a device is joined to your Azure AD, review the **Access work or school** dialog on your Windows device.</span></span> <span data-ttu-id="c93fd-146">The dialog should indicate that you are connected to your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="c93fd-146">The dialog should indicate that you are connected to your Azure AD directory.</span></span>

![Access work or school](./media/azuread-joined-devices-frx/13.png)


## <a name="next-steps"></a><span data-ttu-id="c93fd-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="c93fd-148">Next steps</span></span>

- <span data-ttu-id="c93fd-149">For more information, see the [introduction to device management in Azure Active Directory](overview.md).</span><span class="sxs-lookup"><span data-stu-id="c93fd-149">For more information, see the [introduction to device management in Azure Active Directory](overview.md).</span></span>

- <span data-ttu-id="c93fd-150">For more information about managing devices in the Azure AD portal, see [managing devices using the Azure portal](device-management-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c93fd-150">For more information about managing devices in the Azure AD portal, see [managing devices using the Azure portal](device-management-azure-portal.md).</span></span>
