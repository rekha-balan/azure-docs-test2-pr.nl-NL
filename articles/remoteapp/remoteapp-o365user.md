---
title: How to use Azure RemoteApp with Office 365 user accounts | Microsoft Docs
description: Learn how to use Azure RemoteApp with my Office 365 user accounts
services: remoteapp
documentationcenter: ''
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d8c6ca1a170329f8fa05cdafcb185c9cb2a1431b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553742"
---
# <a name="how-to-use-azure-remoteapp-with-office-365-user-accounts"></a><span data-ttu-id="91d99-103">How to use Azure RemoteApp with Office 365 user accounts</span><span class="sxs-lookup"><span data-stu-id="91d99-103">How to use Azure RemoteApp with Office 365 user accounts</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91d99-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="91d99-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="91d99-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="91d99-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="91d99-106">If you have an Office 365 subscription you have an Azure Active Directory that stores your user names and passwords used to access Office 365 services.</span><span class="sxs-lookup"><span data-stu-id="91d99-106">If you have an Office 365 subscription you have an Azure Active Directory that stores your user names and passwords used to access Office 365 services.</span></span> <span data-ttu-id="91d99-107">For example, when your users activate Office 365 ProPlus they authenticate against Azure AD to check for licenses.</span><span class="sxs-lookup"><span data-stu-id="91d99-107">For example, when your users activate Office 365 ProPlus they authenticate against Azure AD to check for licenses.</span></span> <span data-ttu-id="91d99-108">Most customers would like to use the same directory with Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="91d99-108">Most customers would like to use the same directory with Azure RemoteApp.</span></span>

<span data-ttu-id="91d99-109">If you are deploying Azure RemoteApp you are most likely using an Azure subscription that is associated with a different Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91d99-109">If you are deploying Azure RemoteApp you are most likely using an Azure subscription that is associated with a different Azure AD.</span></span> <span data-ttu-id="91d99-110">In order to use your Office 365 directory, you will need to move the Azure subscription into that directory.</span><span class="sxs-lookup"><span data-stu-id="91d99-110">In order to use your Office 365 directory, you will need to move the Azure subscription into that directory.</span></span>

<span data-ttu-id="91d99-111">For info on how to deploy Office 365 client applications, see [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-111">For info on how to deploy Office 365 client applications, see [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a><span data-ttu-id="91d99-112">Phase 1: Register your free Office 365 Azure Active Directory subscription</span><span class="sxs-lookup"><span data-stu-id="91d99-112">Phase 1: Register your free Office 365 Azure Active Directory subscription</span></span>
<span data-ttu-id="91d99-113">If you are using the Azure classic portal, use the steps in [Register your free Azure Active Directory subscription](https://technet.microsoft.com/library/dn832618.aspx) to get administrative access to your Azure AD via the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="91d99-113">If you are using the Azure classic portal, use the steps in [Register your free Azure Active Directory subscription](https://technet.microsoft.com/library/dn832618.aspx) to get administrative access to your Azure AD via the Azure Management Portal.</span></span> <span data-ttu-id="91d99-114">As the result of this process you should be able to log into the Azure portal and see your directory there – at this point you won’t see much more since the full Azure subscription you are using with Azure RemoteApp is in a different directory.</span><span class="sxs-lookup"><span data-stu-id="91d99-114">As the result of this process you should be able to log into the Azure portal and see your directory there – at this point you won’t see much more since the full Azure subscription you are using with Azure RemoteApp is in a different directory.</span></span>

<span data-ttu-id="91d99-115">Remember the name and password of the administrator account you created in this step – they will be needed in Phase 2.</span><span class="sxs-lookup"><span data-stu-id="91d99-115">Remember the name and password of the administrator account you created in this step – they will be needed in Phase 2.</span></span>

<span data-ttu-id="91d99-116">If you are using the Azure portal, check out [How to register and activate a free Azure Active Directory using Office 365 portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).</span><span class="sxs-lookup"><span data-stu-id="91d99-116">If you are using the Azure portal, check out [How to register and activate a free Azure Active Directory using Office 365 portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).</span></span>

## <a name="phase-2-change-the-azure-ad-associated-with-your-azure-subscription"></a><span data-ttu-id="91d99-117">Phase 2: Change the Azure AD associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="91d99-117">Phase 2: Change the Azure AD associated with your Azure subscription.</span></span>
<span data-ttu-id="91d99-118">We are going to change your Azure subscription from its current directory into the Office 365 directory we worked with in Phase 1.</span><span class="sxs-lookup"><span data-stu-id="91d99-118">We are going to change your Azure subscription from its current directory into the Office 365 directory we worked with in Phase 1.</span></span>

<span data-ttu-id="91d99-119">Follow the instructions described in [Change the Azure Active Directory tenant in Azure RemoteApp](remoteapp-changetenant.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-119">Follow the instructions described in [Change the Azure Active Directory tenant in Azure RemoteApp](remoteapp-changetenant.md).</span></span> <span data-ttu-id="91d99-120">Pay particular attention to the following steps:</span><span class="sxs-lookup"><span data-stu-id="91d99-120">Pay particular attention to the following steps:</span></span>

* <span data-ttu-id="91d99-121">Step #1: If you have deployed Azure RemoteApp (ARA) in this subscription, make sure you remove all Azure AD user accounts from any ARA collections first, before trying anything else.</span><span class="sxs-lookup"><span data-stu-id="91d99-121">Step #1: If you have deployed Azure RemoteApp (ARA) in this subscription, make sure you remove all Azure AD user accounts from any ARA collections first, before trying anything else.</span></span> <span data-ttu-id="91d99-122">Alternatively, you can consider deleting any existing collections.</span><span class="sxs-lookup"><span data-stu-id="91d99-122">Alternatively, you can consider deleting any existing collections.</span></span>
* <span data-ttu-id="91d99-123">Step #2: This is a critical step.</span><span class="sxs-lookup"><span data-stu-id="91d99-123">Step #2: This is a critical step.</span></span> <span data-ttu-id="91d99-124">You need to use a Microsoft account (e.g. @outlook.com) as a Service Administrator on the subscription; this is because we cannot have any user accounts from the existing Azure AD attached to the subscription – if we do, we won’t be able to move it to a different Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91d99-124">You need to use a Microsoft account (e.g. @outlook.com) as a Service Administrator on the subscription; this is because we cannot have any user accounts from the existing Azure AD attached to the subscription – if we do, we won’t be able to move it to a different Azure AD.</span></span>
* <span data-ttu-id="91d99-125">Step #4: When adding an existing directory, the system will ask you to sign in with the administrator account for that directory.</span><span class="sxs-lookup"><span data-stu-id="91d99-125">Step #4: When adding an existing directory, the system will ask you to sign in with the administrator account for that directory.</span></span> <span data-ttu-id="91d99-126">Make sure to use the administrator account from Phase 1.</span><span class="sxs-lookup"><span data-stu-id="91d99-126">Make sure to use the administrator account from Phase 1.</span></span>
* <span data-ttu-id="91d99-127">Step #5: Change the parent directory of the subscription to your Office 365 directory.</span><span class="sxs-lookup"><span data-stu-id="91d99-127">Step #5: Change the parent directory of the subscription to your Office 365 directory.</span></span> <span data-ttu-id="91d99-128">The end result should be that under Settings -> Subscriptions your subscription lists the Office 365 directory.</span><span class="sxs-lookup"><span data-stu-id="91d99-128">The end result should be that under Settings -> Subscriptions your subscription lists the Office 365 directory.</span></span> 
  <span data-ttu-id="91d99-129">![Change the parent directory of the subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-o365user/settings.png)</span><span class="sxs-lookup"><span data-stu-id="91d99-129">![Change the parent directory of the subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-o365user/settings.png)</span></span>

<span data-ttu-id="91d99-130">At this point your Azure RemoteApp subscription is associated with your Office 365 Azure AD; you can use the existing Office 365 user accounts with Azure RemoteApp!</span><span class="sxs-lookup"><span data-stu-id="91d99-130">At this point your Azure RemoteApp subscription is associated with your Office 365 Azure AD; you can use the existing Office 365 user accounts with Azure RemoteApp!</span></span>


