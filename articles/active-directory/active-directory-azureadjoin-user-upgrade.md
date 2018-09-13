---
title: Set up a Windows 10 device with Azure AD from Settings| Microsoft Docs
description: Explains how users can join to Azure AD through the Settings menu.
services: active-directory
documentationcenter: ''
author: femila
manager: swadhwa
editor: ''
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 57e8b16122d857921d6f3106cd7dd64fa1ebdb02
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552433"
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="773ee-103">Set up a Windows 10 device with Azure AD from Settings</span><span class="sxs-lookup"><span data-stu-id="773ee-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="773ee-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span><span class="sxs-lookup"><span data-stu-id="773ee-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="773ee-105">To join to Azure AD from the Settings menu</span><span class="sxs-lookup"><span data-stu-id="773ee-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="773ee-106">From the **Start** menu, click the **Settings** charm.</span><span class="sxs-lookup"><span data-stu-id="773ee-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="773ee-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="773ee-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="773ee-108"><center>
   ![Join Azure AD from the Settings menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="773ee-108"><center>
![Join Azure AD from the Settings menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="773ee-109">Click **Continue** in the Azure AD Join message window.</span><span class="sxs-lookup"><span data-stu-id="773ee-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="773ee-110"><center>
   ![Join Azure AD message window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="773ee-110"><center>
![Join Azure AD message window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="773ee-111">Provide your sign-in credentials.</span><span class="sxs-lookup"><span data-stu-id="773ee-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="773ee-112">This sign-in experience will include all the steps that are required to complete authentication.</span><span class="sxs-lookup"><span data-stu-id="773ee-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="773ee-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span><span class="sxs-lookup"><span data-stu-id="773ee-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="773ee-114"><center>
   ![Provide sign-in credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="773ee-114"><center>
![Provide sign-in credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="773ee-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span><span class="sxs-lookup"><span data-stu-id="773ee-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="773ee-116">Click **Accept** on the **Allow this device to be managed** screen.</span><span class="sxs-lookup"><span data-stu-id="773ee-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="773ee-117">You should see the message "Your device is now joined to your organization in Azure AD".</span><span class="sxs-lookup"><span data-stu-id="773ee-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="773ee-118">Additional information</span><span class="sxs-lookup"><span data-stu-id="773ee-118">Additional information</span></span>
* [<span data-ttu-id="773ee-119">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="773ee-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="773ee-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="773ee-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="773ee-121">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="773ee-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="773ee-122">Authenticating identities without passwords through Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="773ee-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)




