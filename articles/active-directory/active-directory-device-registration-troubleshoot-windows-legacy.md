---
title: Troubleshooting the auto-registration of Azure AD domain joined computers for Windows down-level clients | Microsoft Docs
description: Troubleshooting the auto-registration of Azure AD domain joined computers for Windows down-level clients.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: markvi
ms.openlocfilehash: 1dc295817d01bb7eaa5df9ec33d20536c49a92cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549624"
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="972ab-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span><span class="sxs-lookup"><span data-stu-id="972ab-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="972ab-104">This topic is applicable only to the following clients:</span><span class="sxs-lookup"><span data-stu-id="972ab-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="972ab-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="972ab-105">Windows 7</span></span> 
- <span data-ttu-id="972ab-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="972ab-106">Windows 8.1</span></span> 
- <span data-ttu-id="972ab-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="972ab-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="972ab-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="972ab-108">Windows Server 2012</span></span> 
- <span data-ttu-id="972ab-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="972ab-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="972ab-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="972ab-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="972ab-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="972ab-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="972ab-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span><span class="sxs-lookup"><span data-stu-id="972ab-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="972ab-113">Some things to note for successful outcomes:</span><span class="sxs-lookup"><span data-stu-id="972ab-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="972ab-114">Registration of these clients on Azure AD is per user/device.</span><span class="sxs-lookup"><span data-stu-id="972ab-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="972ab-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span><span class="sxs-lookup"><span data-stu-id="972ab-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="972ab-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span><span class="sxs-lookup"><span data-stu-id="972ab-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="972ab-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="972ab-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="972ab-118">Step 1: Retrieve the registration status</span><span class="sxs-lookup"><span data-stu-id="972ab-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="972ab-119">**To verify the registration status:**</span><span class="sxs-lookup"><span data-stu-id="972ab-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="972ab-120">Open the command prompt as an administrator</span><span class="sxs-lookup"><span data-stu-id="972ab-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="972ab-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="972ab-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="972ab-122">This command displays a dialog box that provides you with more details about the join status.</span><span class="sxs-lookup"><span data-stu-id="972ab-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join for Windows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="972ab-124">Step 2: Evaluate the registration status</span><span class="sxs-lookup"><span data-stu-id="972ab-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="972ab-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span><span class="sxs-lookup"><span data-stu-id="972ab-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="972ab-126">**The most common issues are:**</span><span class="sxs-lookup"><span data-stu-id="972ab-126">**The most common issues are:**</span></span>

- <span data-ttu-id="972ab-127">A misconfigured AD FS or Azure AD</span><span class="sxs-lookup"><span data-stu-id="972ab-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="972ab-129">You are not signed on as a domain user</span><span class="sxs-lookup"><span data-stu-id="972ab-129">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="972ab-131">A quota has been reached</span><span class="sxs-lookup"><span data-stu-id="972ab-131">A quota has been reached</span></span>

    ![Workplace Join for Windows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="972ab-133">The service is not responding</span><span class="sxs-lookup"><span data-stu-id="972ab-133">The service is not responding</span></span> 

    ![Workplace Join for Windows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="972ab-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="972ab-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="972ab-136">**The most common causes for a failed registration are:**</span><span class="sxs-lookup"><span data-stu-id="972ab-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="972ab-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span><span class="sxs-lookup"><span data-stu-id="972ab-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="972ab-138">You are logged on to your computer with a local computer account.</span><span class="sxs-lookup"><span data-stu-id="972ab-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="972ab-139">Service configuration issues:</span><span class="sxs-lookup"><span data-stu-id="972ab-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="972ab-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="972ab-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="972ab-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span><span class="sxs-lookup"><span data-stu-id="972ab-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="972ab-142">A user has reached the limit of devices.</span><span class="sxs-lookup"><span data-stu-id="972ab-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="972ab-143">Please see Get Started with Azure Active Directory Device Registration.</span><span class="sxs-lookup"><span data-stu-id="972ab-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="972ab-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="972ab-144">Next steps</span></span>

<span data-ttu-id="972ab-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="972ab-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 





