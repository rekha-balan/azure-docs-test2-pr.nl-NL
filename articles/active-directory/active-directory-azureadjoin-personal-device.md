---
title: Join a personal device to your organization| Microsoft Docs
description: Explains how users can register their personal Windows 10 devices to their corporate network, and provides deployment steps for a BYOD scenario.
services: active-directory
documentationcenter: ''
author: femila
manager: femila
editor: ''
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 6effe246eeb4e4a48f1a695de47047c78f9e509e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552913"
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="edf01-103">Join a personal device to your organization</span><span class="sxs-lookup"><span data-stu-id="edf01-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="edf01-104">To join a Windows 10 device to your organization</span><span class="sxs-lookup"><span data-stu-id="edf01-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="edf01-105">From the **Start** menu, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="edf01-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="edf01-106">Select **Accounts**, and then click **Your account**.</span><span class="sxs-lookup"><span data-stu-id="edf01-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="edf01-107">Click **Add Work or School account**, and then type in your organizational account.</span><span class="sxs-lookup"><span data-stu-id="edf01-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="edf01-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="edf01-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="edf01-109">You will be prompted for a multi-factor authentication challenge.</span><span class="sxs-lookup"><span data-stu-id="edf01-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="edf01-110">(This challenge is configurable by an IT administrator.)</span><span class="sxs-lookup"><span data-stu-id="edf01-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="edf01-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span><span class="sxs-lookup"><span data-stu-id="edf01-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="edf01-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span><span class="sxs-lookup"><span data-stu-id="edf01-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="edf01-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span><span class="sxs-lookup"><span data-stu-id="edf01-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="edf01-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="edf01-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="edf01-115">Additional information</span><span class="sxs-lookup"><span data-stu-id="edf01-115">Additional information</span></span>
* [<span data-ttu-id="edf01-116">Windows 10 for the enterprise: Ways to use devices for work</span><span class="sxs-lookup"><span data-stu-id="edf01-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="edf01-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="edf01-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="edf01-118">Authenticating identities without passwords through Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="edf01-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="edf01-119">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="edf01-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="edf01-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="edf01-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="edf01-121">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="edf01-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

