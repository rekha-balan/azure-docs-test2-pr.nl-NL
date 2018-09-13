---
title: Azure AD Connect and user privacy | Microsoft Docs
description: This document describes how to obtain GDPR compliancy with Azure AD Connect.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/21/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 8e3f81a6480e9de55c8f803e2266c4ac6e33c316
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856025"
---
# <a name="user-privacy-and-azure-ad-connect"></a><span data-ttu-id="bc2e3-103">User privacy and Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="bc2e3-103">User privacy and Azure AD Connect</span></span> 

[!INCLUDE [Privacy](../../../includes/gdpr-intro-sentence.md)]

>[!NOTE] 
><span data-ttu-id="bc2e3-104">This article deals with Azure AD Connect and user privacy.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-104">This article deals with Azure AD Connect and user privacy.</span></span>  <span data-ttu-id="bc2e3-105">For information on Azure AD Connect Health and user privacy see the article [here](../../active-directory/connect-health/active-directory-aadconnect-health-gdpr.md).</span><span class="sxs-lookup"><span data-stu-id="bc2e3-105">For information on Azure AD Connect Health and user privacy see the article [here](../../active-directory/connect-health/active-directory-aadconnect-health-gdpr.md).</span></span>

<span data-ttu-id="bc2e3-106">Improve user privacy for Azure AD Connect installations in two ways:</span><span class="sxs-lookup"><span data-stu-id="bc2e3-106">Improve user privacy for Azure AD Connect installations in two ways:</span></span>

1.  <span data-ttu-id="bc2e3-107">Upon request, extract data for a person and remove data from that person from the installations</span><span class="sxs-lookup"><span data-stu-id="bc2e3-107">Upon request, extract data for a person and remove data from that person from the installations</span></span>
2.  <span data-ttu-id="bc2e3-108">Ensure no data is retained beyond 48 hours.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-108">Ensure no data is retained beyond 48 hours.</span></span>

<span data-ttu-id="bc2e3-109">The Azure AD Connect team recommends the second option since it is much easier to implement and maintain.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-109">The Azure AD Connect team recommends the second option since it is much easier to implement and maintain.</span></span>

<span data-ttu-id="bc2e3-110">An Azure AD Connect sync server stores the following user privacy data:</span><span class="sxs-lookup"><span data-stu-id="bc2e3-110">An Azure AD Connect sync server stores the following user privacy data:</span></span>
1.  <span data-ttu-id="bc2e3-111">Data about a person in the **Azure AD Connect database**</span><span class="sxs-lookup"><span data-stu-id="bc2e3-111">Data about a person in the **Azure AD Connect database**</span></span>
2.  <span data-ttu-id="bc2e3-112">Data in the **Windows Event log** files that may contain information about a person</span><span class="sxs-lookup"><span data-stu-id="bc2e3-112">Data in the **Windows Event log** files that may contain information about a person</span></span>
3.  <span data-ttu-id="bc2e3-113">Data in the **Azure AD Connect installation log files** that may contain about a person</span><span class="sxs-lookup"><span data-stu-id="bc2e3-113">Data in the **Azure AD Connect installation log files** that may contain about a person</span></span>

<span data-ttu-id="bc2e3-114">Azure AD Connect customers should use the following guidelines when removing user data:</span><span class="sxs-lookup"><span data-stu-id="bc2e3-114">Azure AD Connect customers should use the following guidelines when removing user data:</span></span>
1.  <span data-ttu-id="bc2e3-115">Delete the contents of the folder that contains the Azure AD Connect installation log files on a regular basis – at least every 48 hours</span><span class="sxs-lookup"><span data-stu-id="bc2e3-115">Delete the contents of the folder that contains the Azure AD Connect installation log files on a regular basis – at least every 48 hours</span></span>
2.  <span data-ttu-id="bc2e3-116">This product may also create Event Logs.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-116">This product may also create Event Logs.</span></span>  <span data-ttu-id="bc2e3-117">To learn more about Event Logs logs, please see the [documentation here](https://msdn.microsoft.com/library/windows/desktop/aa385780.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc2e3-117">To learn more about Event Logs logs, please see the [documentation here](https://msdn.microsoft.com/library/windows/desktop/aa385780.aspx).</span></span>

<span data-ttu-id="bc2e3-118">Data about a person is automatically removed from the Azure AD Connect database when that person’s data is removed from the source system where it originated from.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-118">Data about a person is automatically removed from the Azure AD Connect database when that person’s data is removed from the source system where it originated from.</span></span> <span data-ttu-id="bc2e3-119">No specific action from administrators is required to be GDPR compliant.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-119">No specific action from administrators is required to be GDPR compliant.</span></span>  <span data-ttu-id="bc2e3-120">However, it does require that the Azure AD Connect data is synced with your data source at least every two days.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-120">However, it does require that the Azure AD Connect data is synced with your data source at least every two days.</span></span>

## <a name="delete-the-azure-ad-connect-installation-log-file-folder-contents"></a><span data-ttu-id="bc2e3-121">Delete the Azure AD Connect installation log file folder contents</span><span class="sxs-lookup"><span data-stu-id="bc2e3-121">Delete the Azure AD Connect installation log file folder contents</span></span>
<span data-ttu-id="bc2e3-122">Regularly check and delete the contents of **c:\programdata\aadconnect** folder – except for the **PersistedState.Xml** file.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-122">Regularly check and delete the contents of **c:\programdata\aadconnect** folder – except for the **PersistedState.Xml** file.</span></span> <span data-ttu-id="bc2e3-123">This file maintains the state of the previous installation of Azure A Connect and is used when an upgrade installation is performed.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-123">This file maintains the state of the previous installation of Azure A Connect and is used when an upgrade installation is performed.</span></span> <span data-ttu-id="bc2e3-124">This file doesn't contain any data about a person and shouldn't be deleted.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-124">This file doesn't contain any data about a person and shouldn't be deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="bc2e3-125">Do not delete the PersistedState.xml file.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-125">Do not delete the PersistedState.xml file.</span></span>  <span data-ttu-id="bc2e3-126">This file contains no user information and maintains the state of the previous installation.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-126">This file contains no user information and maintains the state of the previous installation.</span></span>

<span data-ttu-id="bc2e3-127">You can either review and delete these files using Windows Explorer or you can use a script like the following to perform the necessary actions:</span><span class="sxs-lookup"><span data-stu-id="bc2e3-127">You can either review and delete these files using Windows Explorer or you can use a script like the following to perform the necessary actions:</span></span>


```
$Files = ((Get-childitem -Path "$env:programdata\aadconnect" -Recurse).VersionInfo).FileName
Foreach ($file in $files) {
If ($File.ToUpper() -ne "$env:programdata\aadconnect\PERSISTEDSTATE.XML".toupper()) # Do not delete this file
    {Remove-Item -Path $File -Force}
    } 
```

### <a name="schedule-this-script-to-run-every-48-hours"></a><span data-ttu-id="bc2e3-128">Schedule this script to run every 48 hours</span><span class="sxs-lookup"><span data-stu-id="bc2e3-128">Schedule this script to run every 48 hours</span></span>
<span data-ttu-id="bc2e3-129">Use the following steps to schedule the script to run every 48 hours.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-129">Use the following steps to schedule the script to run every 48 hours.</span></span>

1.  <span data-ttu-id="bc2e3-130">Save the script in a file with the extension **&#46;PS1**, then open the Control Panel and click on **Systems and Security**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-130">Save the script in a file with the extension **&#46;PS1**, then open the Control Panel and click on **Systems and Security**.</span></span>
    <span data-ttu-id="bc2e3-131">![System](media\active-directory-aadconnect-gdpr\gdpr2.png)</span><span class="sxs-lookup"><span data-stu-id="bc2e3-131">![System](media\active-directory-aadconnect-gdpr\gdpr2.png)</span></span>

2.  <span data-ttu-id="bc2e3-132">Under the Administrative Tools heading, click on **Schedule Tasks**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-132">Under the Administrative Tools heading, click on **Schedule Tasks**.</span></span>
    <span data-ttu-id="bc2e3-133">![Task](media\active-directory-aadconnect-gdpr\gdpr3.png)</span><span class="sxs-lookup"><span data-stu-id="bc2e3-133">![Task](media\active-directory-aadconnect-gdpr\gdpr3.png)</span></span>
3.  <span data-ttu-id="bc2e3-134">In Task Scheduler, right click on **Task Schedule Library** and click on **Create Basic task…**</span><span class="sxs-lookup"><span data-stu-id="bc2e3-134">In Task Scheduler, right click on **Task Schedule Library** and click on **Create Basic task…**</span></span>
4.  <span data-ttu-id="bc2e3-135">Enter the name for the new task and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-135">Enter the name for the new task and click **Next**.</span></span>
5.  <span data-ttu-id="bc2e3-136">Select **Daily** for the task trigger and click on **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-136">Select **Daily** for the task trigger and click on **Next**.</span></span>
6.  <span data-ttu-id="bc2e3-137">Set the recurrence to **2 days** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-137">Set the recurrence to **2 days** and click **Next**.</span></span>
7.  <span data-ttu-id="bc2e3-138">Select **Start a program** as the action and click on **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-138">Select **Start a program** as the action and click on **Next**.</span></span>
8.  <span data-ttu-id="bc2e3-139">Type **PowerShell** in the box for the Program/script, and in box labeled **Add arguments (optional)**, enter the full path to the script that you created earlier, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-139">Type **PowerShell** in the box for the Program/script, and in box labeled **Add arguments (optional)**, enter the full path to the script that you created earlier, then click **Next**.</span></span>
9.  <span data-ttu-id="bc2e3-140">The next screen shows a summary of the task you are about to create.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-140">The next screen shows a summary of the task you are about to create.</span></span> <span data-ttu-id="bc2e3-141">Verify the values and click **Finish** to create the task.</span><span class="sxs-lookup"><span data-stu-id="bc2e3-141">Verify the values and click **Finish** to create the task.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bc2e3-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc2e3-142">Next steps</span></span>
* [<span data-ttu-id="bc2e3-143">Review the Microsoft Privacy policy on Trust Center</span><span class="sxs-lookup"><span data-stu-id="bc2e3-143">Review the Microsoft Privacy policy on Trust Center</span></span>](https://www.microsoft.com/trustcenter)
- [<span data-ttu-id="bc2e3-144">Azure AD Connect Health and User Privacy</span><span class="sxs-lookup"><span data-stu-id="bc2e3-144">Azure AD Connect Health and User Privacy</span></span>](../../active-directory/connect-health/active-directory-aadconnect-health-gdpr.md)
