---
title: User Privacy and Azure Active Directory Pass-through Authentication | Microsoft Docs
description: This article deals with Azure Active Directory (Azure AD) Pass-through Authentication and GDPR compliance.
services: active-directory
keywords: Azure AD Connect Pass-through Authentication, GDPR, required components for Azure AD, SSO, Single Sign-on
documentationcenter: ''
author: billmath
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2018
ms.component: hybrid
ms.author: billmath
ms.custom: seohack1
ms.openlocfilehash: b785b23b41981efeb7fe160a18dc0c3c38f3772f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866886"
---
# <a name="user-privacy-and-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="78c6e-104">User Privacy and Azure Active Directory Pass-through Authentication</span><span class="sxs-lookup"><span data-stu-id="78c6e-104">User Privacy and Azure Active Directory Pass-through Authentication</span></span>


[!INCLUDE [Privacy](../../../includes/gdpr-intro-sentence.md)]

## <a name="overview"></a><span data-ttu-id="78c6e-105">Overview</span><span class="sxs-lookup"><span data-stu-id="78c6e-105">Overview</span></span>

<span data-ttu-id="78c6e-106">Azure AD Pass-through Authentication creates the following log type, which can contain Personal Data:</span><span class="sxs-lookup"><span data-stu-id="78c6e-106">Azure AD Pass-through Authentication creates the following log type, which can contain Personal Data:</span></span>

- <span data-ttu-id="78c6e-107">Azure AD Connect trace log files.</span><span class="sxs-lookup"><span data-stu-id="78c6e-107">Azure AD Connect trace log files.</span></span>
- <span data-ttu-id="78c6e-108">Authentication Agent trace log files.</span><span class="sxs-lookup"><span data-stu-id="78c6e-108">Authentication Agent trace log files.</span></span>
- <span data-ttu-id="78c6e-109">Windows Event log files.</span><span class="sxs-lookup"><span data-stu-id="78c6e-109">Windows Event log files.</span></span>

<span data-ttu-id="78c6e-110">Improve user privacy for Pass-through Authentication in two ways:</span><span class="sxs-lookup"><span data-stu-id="78c6e-110">Improve user privacy for Pass-through Authentication in two ways:</span></span>

1.  <span data-ttu-id="78c6e-111">Upon request, extract data for a person and remove data from that person from the installations.</span><span class="sxs-lookup"><span data-stu-id="78c6e-111">Upon request, extract data for a person and remove data from that person from the installations.</span></span>
2.  <span data-ttu-id="78c6e-112">Ensure no data is retained beyond 48 hours.</span><span class="sxs-lookup"><span data-stu-id="78c6e-112">Ensure no data is retained beyond 48 hours.</span></span>

<span data-ttu-id="78c6e-113">We strongly recommend the second option as it is easier to implement and maintain.</span><span class="sxs-lookup"><span data-stu-id="78c6e-113">We strongly recommend the second option as it is easier to implement and maintain.</span></span> <span data-ttu-id="78c6e-114">Following are the instructions for each log type:</span><span class="sxs-lookup"><span data-stu-id="78c6e-114">Following are the instructions for each log type:</span></span>

### <a name="delete-azure-ad-connect-trace-log-files"></a><span data-ttu-id="78c6e-115">Delete Azure AD Connect trace log files</span><span class="sxs-lookup"><span data-stu-id="78c6e-115">Delete Azure AD Connect trace log files</span></span>

<span data-ttu-id="78c6e-116">Check the contents of **%ProgramData%\AADConnect** folder and delete the trace log contents (**trace-\*.log** files) of this folder within 48 hours of installing or upgrading Azure AD Connect or modifying Pass-through Authentication configuration, as this action may create data covered by GDPR.</span><span class="sxs-lookup"><span data-stu-id="78c6e-116">Check the contents of **%ProgramData%\AADConnect** folder and delete the trace log contents (**trace-\*.log** files) of this folder within 48 hours of installing or upgrading Azure AD Connect or modifying Pass-through Authentication configuration, as this action may create data covered by GDPR.</span></span>

>[!IMPORTANT]
><span data-ttu-id="78c6e-117">Don’t delete the **PersistedState.xml** file in this folder, as this file is used to maintain the state of the previous installation of Azure AD Connect and is used when an upgrade installation is done.</span><span class="sxs-lookup"><span data-stu-id="78c6e-117">Don’t delete the **PersistedState.xml** file in this folder, as this file is used to maintain the state of the previous installation of Azure AD Connect and is used when an upgrade installation is done.</span></span> <span data-ttu-id="78c6e-118">This file will never contain any data about a person and should never be deleted.</span><span class="sxs-lookup"><span data-stu-id="78c6e-118">This file will never contain any data about a person and should never be deleted.</span></span>

<span data-ttu-id="78c6e-119">You can either review and delete these trace log files using Windows Explorer or you can use the following PowerShell script to perform the necessary actions:</span><span class="sxs-lookup"><span data-stu-id="78c6e-119">You can either review and delete these trace log files using Windows Explorer or you can use the following PowerShell script to perform the necessary actions:</span></span>

```
$Files = ((Get-Item -Path "$env:programdata\aadconnect\trace-*.log").VersionInfo).FileName 
 
Foreach ($file in $Files) { 
    {Remove-Item -Path $File -Force} 
}
```

<span data-ttu-id="78c6e-120">Save the script in a file with the ".PS1" extension.</span><span class="sxs-lookup"><span data-stu-id="78c6e-120">Save the script in a file with the ".PS1" extension.</span></span> <span data-ttu-id="78c6e-121">Run this script as needed.</span><span class="sxs-lookup"><span data-stu-id="78c6e-121">Run this script as needed.</span></span>

<span data-ttu-id="78c6e-122">To learn more about related Azure AD Connect GDPR requirements, see [this article](active-directory-aadconnect-gdpr.md).</span><span class="sxs-lookup"><span data-stu-id="78c6e-122">To learn more about related Azure AD Connect GDPR requirements, see [this article](active-directory-aadconnect-gdpr.md).</span></span>

### <a name="delete-authentication-agent-event-logs"></a><span data-ttu-id="78c6e-123">Delete Authentication Agent event logs</span><span class="sxs-lookup"><span data-stu-id="78c6e-123">Delete Authentication Agent event logs</span></span>

<span data-ttu-id="78c6e-124">This product may also create **Windows Event Logs**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-124">This product may also create **Windows Event Logs**.</span></span> <span data-ttu-id="78c6e-125">To learn more, please read [this article](https://msdn.microsoft.com/library/windows/desktop/aa385780(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="78c6e-125">To learn more, please read [this article](https://msdn.microsoft.com/library/windows/desktop/aa385780(v=vs.85).aspx).</span></span>

<span data-ttu-id="78c6e-126">To view logs related to the Pass-through Authentication Agent, open the **Event Viewer** application on the server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-126">To view logs related to the Pass-through Authentication Agent, open the **Event Viewer** application on the server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.</span></span>

### <a name="delete-authentication-agent-trace-log-files"></a><span data-ttu-id="78c6e-127">Delete Authentication Agent trace log files</span><span class="sxs-lookup"><span data-stu-id="78c6e-127">Delete Authentication Agent trace log files</span></span>

<span data-ttu-id="78c6e-128">You should regularly check the contents of \**%ProgramData%\Microsoft\Azure AD Connect Authentication Agent\Trace\** and delete the contents of this folder every 48 hours.</span><span class="sxs-lookup"><span data-stu-id="78c6e-128">You should regularly check the contents of \**%ProgramData%\Microsoft\Azure AD Connect Authentication Agent\Trace\** and delete the contents of this folder every 48 hours.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="78c6e-129">If the Authentication Agent service is running, you'll not be able to delete the current log file in the folder.</span><span class="sxs-lookup"><span data-stu-id="78c6e-129">If the Authentication Agent service is running, you'll not be able to delete the current log file in the folder.</span></span> <span data-ttu-id="78c6e-130">Stop the service before trying again.</span><span class="sxs-lookup"><span data-stu-id="78c6e-130">Stop the service before trying again.</span></span> <span data-ttu-id="78c6e-131">To avoid user sign-in failures, you should have already configured Pass-through Authentication for [high availability](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-4-ensure-high-availability).</span><span class="sxs-lookup"><span data-stu-id="78c6e-131">To avoid user sign-in failures, you should have already configured Pass-through Authentication for [high availability](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-4-ensure-high-availability).</span></span>

<span data-ttu-id="78c6e-132">You can either review and delete these files using Windows Explorer or you can use the following script to perform the necessary actions:</span><span class="sxs-lookup"><span data-stu-id="78c6e-132">You can either review and delete these files using Windows Explorer or you can use the following script to perform the necessary actions:</span></span>

```
$Files = ((Get-childitem -Path "$env:programdata\microsoft\azure ad connect authentication agent\trace" -Recurse).VersionInfo).FileName 
 
Foreach ($file in $files) { 
    {Remove-Item -Path $File -Force} 
}
```

<span data-ttu-id="78c6e-133">To schedule this script to run every 48 hours follow these steps:</span><span class="sxs-lookup"><span data-stu-id="78c6e-133">To schedule this script to run every 48 hours follow these steps:</span></span>

1.  <span data-ttu-id="78c6e-134">Save the script in a file with the ".PS1" extension.</span><span class="sxs-lookup"><span data-stu-id="78c6e-134">Save the script in a file with the ".PS1" extension.</span></span>
2.  <span data-ttu-id="78c6e-135">Open **Control Panel** and click on **System and Security**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-135">Open **Control Panel** and click on **System and Security**.</span></span>
3.  <span data-ttu-id="78c6e-136">Under the **Administrative Tools** heading, click on “**Schedule Tasks**”.</span><span class="sxs-lookup"><span data-stu-id="78c6e-136">Under the **Administrative Tools** heading, click on “**Schedule Tasks**”.</span></span>
4.  <span data-ttu-id="78c6e-137">In **Task Scheduler**, right-click on “**Task Schedule Library**” and click on “**Create Basic task…**”.</span><span class="sxs-lookup"><span data-stu-id="78c6e-137">In **Task Scheduler**, right-click on “**Task Schedule Library**” and click on “**Create Basic task…**”.</span></span>
5.  <span data-ttu-id="78c6e-138">Enter the name for the new task and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-138">Enter the name for the new task and click **Next**.</span></span>
6.  <span data-ttu-id="78c6e-139">Select “**Daily**” for the **Task Trigger** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-139">Select “**Daily**” for the **Task Trigger** and click **Next**.</span></span>
7.  <span data-ttu-id="78c6e-140">Set the recurrence to two days and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-140">Set the recurrence to two days and click **Next**.</span></span>
8.  <span data-ttu-id="78c6e-141">Select “**Start a program**” as the action and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-141">Select “**Start a program**” as the action and click **Next**.</span></span>
9.  <span data-ttu-id="78c6e-142">Type “**PowerShell**” in the box for the Program/script, and in box labeled “**Add arguments (optional)**”, enter the full path to the script that you created earlier, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="78c6e-142">Type “**PowerShell**” in the box for the Program/script, and in box labeled “**Add arguments (optional)**”, enter the full path to the script that you created earlier, then click **Next**.</span></span>
10. <span data-ttu-id="78c6e-143">The next screen shows a summary of the task you are about to create.</span><span class="sxs-lookup"><span data-stu-id="78c6e-143">The next screen shows a summary of the task you are about to create.</span></span> <span data-ttu-id="78c6e-144">Verify the values and click **Finish** to create the task:</span><span class="sxs-lookup"><span data-stu-id="78c6e-144">Verify the values and click **Finish** to create the task:</span></span>
 
### <a name="note-about-domain-controller-logs"></a><span data-ttu-id="78c6e-145">Note about Domain controller logs</span><span class="sxs-lookup"><span data-stu-id="78c6e-145">Note about Domain controller logs</span></span>

<span data-ttu-id="78c6e-146">If audit logging is enabled, this product may generate security logs for your Domain Controllers.</span><span class="sxs-lookup"><span data-stu-id="78c6e-146">If audit logging is enabled, this product may generate security logs for your Domain Controllers.</span></span> <span data-ttu-id="78c6e-147">To learn more about configuring audit policies, read this [article](https://technet.microsoft.com/library/dd277403.aspx).</span><span class="sxs-lookup"><span data-stu-id="78c6e-147">To learn more about configuring audit policies, read this [article](https://technet.microsoft.com/library/dd277403.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78c6e-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="78c6e-148">Next steps</span></span>
* [<span data-ttu-id="78c6e-149">Review the Microsoft Privacy policy on Trust Center</span><span class="sxs-lookup"><span data-stu-id="78c6e-149">Review the Microsoft Privacy policy on Trust Center</span></span>](https://www.microsoft.com/trustcenter)
- <span data-ttu-id="78c6e-150">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span><span class="sxs-lookup"><span data-stu-id="78c6e-150">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
