---
title: Remove personal data - Azure Active Directory Application Proxy | Microsoft Docs
description: Remove personal data from connectors installed on devices for Azure Active Directory Application Proxy.
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: bccda196be82808e7dc369de3f517490f410e26e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865229"
---
# <a name="remove-personal-data-for-azure-active-directory-application-proxy"></a><span data-ttu-id="e6c1f-103">Remove personal data for Azure Active Directory Application Proxy</span><span class="sxs-lookup"><span data-stu-id="e6c1f-103">Remove personal data for Azure Active Directory Application Proxy</span></span>  

<span data-ttu-id="e6c1f-104">Azure Active Directory Application Proxy requires that you install connectors on your devices, which means that there might be personal data on your devices.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-104">Azure Active Directory Application Proxy requires that you install connectors on your devices, which means that there might be personal data on your devices.</span></span> <span data-ttu-id="e6c1f-105">This article provides steps for how to delete that personal data to improve privacy.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-105">This article provides steps for how to delete that personal data to improve privacy.</span></span> 


## <a name="where-is-the-personal-data"></a><span data-ttu-id="e6c1f-106">Where is the personal data?</span><span class="sxs-lookup"><span data-stu-id="e6c1f-106">Where is the personal data?</span></span>
<span data-ttu-id="e6c1f-107">It is possible for Application Proxy to write personal data to the following log types:</span><span class="sxs-lookup"><span data-stu-id="e6c1f-107">It is possible for Application Proxy to write personal data to the following log types:</span></span>

- <span data-ttu-id="e6c1f-108">Connector event logs</span><span class="sxs-lookup"><span data-stu-id="e6c1f-108">Connector event logs</span></span>
- <span data-ttu-id="e6c1f-109">Windows event logs</span><span class="sxs-lookup"><span data-stu-id="e6c1f-109">Windows event logs</span></span>

## <a name="remove-personal-data-from-windows-event-logs"></a><span data-ttu-id="e6c1f-110">Remove personal data from Windows event logs</span><span class="sxs-lookup"><span data-stu-id="e6c1f-110">Remove personal data from Windows event logs</span></span>

<span data-ttu-id="e6c1f-111">For information on how to configure data retention for the Windows event logs, see [Settings for event logs](https://technet.microsoft.com/library/cc952132.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6c1f-111">For information on how to configure data retention for the Windows event logs, see [Settings for event logs](https://technet.microsoft.com/library/cc952132.aspx).</span></span> <span data-ttu-id="e6c1f-112">To learn about Windows event logs, see [Using Windows Event Log](https://msdn.microsoft.com/library/windows/desktop/aa385772.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6c1f-112">To learn about Windows event logs, see [Using Windows Event Log](https://msdn.microsoft.com/library/windows/desktop/aa385772.aspx).</span></span>

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-hybrid-note.md)]

## <a name="remove-personal-data-from-connector-event-logs"></a><span data-ttu-id="e6c1f-113">Remove personal data from Connector event logs</span><span class="sxs-lookup"><span data-stu-id="e6c1f-113">Remove personal data from Connector event logs</span></span>

<span data-ttu-id="e6c1f-114">To ensure the Application Proxy logs do not have personal data, you can either:</span><span class="sxs-lookup"><span data-stu-id="e6c1f-114">To ensure the Application Proxy logs do not have personal data, you can either:</span></span>

- <span data-ttu-id="e6c1f-115">Delete or view data when needed, or</span><span class="sxs-lookup"><span data-stu-id="e6c1f-115">Delete or view data when needed, or</span></span>
- <span data-ttu-id="e6c1f-116">Turn off logging</span><span class="sxs-lookup"><span data-stu-id="e6c1f-116">Turn off logging</span></span>

<span data-ttu-id="e6c1f-117">Use the following sections to remove personal data from connector event logs.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-117">Use the following sections to remove personal data from connector event logs.</span></span> <span data-ttu-id="e6c1f-118">You must complete the removal process for all devices on which the connector is installed.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-118">You must complete the removal process for all devices on which the connector is installed.</span></span>

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

### <a name="view-or-export-specific-data"></a><span data-ttu-id="e6c1f-119">View or export specific data</span><span class="sxs-lookup"><span data-stu-id="e6c1f-119">View or export specific data</span></span>

<span data-ttu-id="e6c1f-120">To view or export specific data, search for related entries in each of the connector event logs.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-120">To view or export specific data, search for related entries in each of the connector event logs.</span></span> <span data-ttu-id="e6c1f-121">The logs are located at `C:\ProgramData\Microsoft\Microsoft AAD Application Proxy Connector\Trace`.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-121">The logs are located at `C:\ProgramData\Microsoft\Microsoft AAD Application Proxy Connector\Trace`.</span></span> 

<span data-ttu-id="e6c1f-122">Since the logs are text files, you can use [findstr](https://docs.microsoft.com/windows-server/administration/windows-commands/findstr) to search for text entries related to a user.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-122">Since the logs are text files, you can use [findstr](https://docs.microsoft.com/windows-server/administration/windows-commands/findstr) to search for text entries related to a user.</span></span>  

<span data-ttu-id="e6c1f-123">To find personal data, search log files for UserID.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-123">To find personal data, search log files for UserID.</span></span> 

<span data-ttu-id="e6c1f-124">To find personal data logged by an application that uses Kerberos Constrained Delegation, search for these components of the username type:</span><span class="sxs-lookup"><span data-stu-id="e6c1f-124">To find personal data logged by an application that uses Kerberos Constrained Delegation, search for these components of the username type:</span></span>

- <span data-ttu-id="e6c1f-125">On-premises user principal name</span><span class="sxs-lookup"><span data-stu-id="e6c1f-125">On-premises user principal name</span></span>
- <span data-ttu-id="e6c1f-126">Username part of user principal name</span><span class="sxs-lookup"><span data-stu-id="e6c1f-126">Username part of user principal name</span></span>
- <span data-ttu-id="e6c1f-127">Username part of on-premises user principal name</span><span class="sxs-lookup"><span data-stu-id="e6c1f-127">Username part of on-premises user principal name</span></span>
- <span data-ttu-id="e6c1f-128">On-premises security accounts manager (SAM) account name</span><span class="sxs-lookup"><span data-stu-id="e6c1f-128">On-premises security accounts manager (SAM) account name</span></span> 


### <a name="delete-specific-data"></a><span data-ttu-id="e6c1f-129">Delete specific data</span><span class="sxs-lookup"><span data-stu-id="e6c1f-129">Delete specific data</span></span>

<span data-ttu-id="e6c1f-130">To delete specific data:</span><span class="sxs-lookup"><span data-stu-id="e6c1f-130">To delete specific data:</span></span>

1. <span data-ttu-id="e6c1f-131">Restart the Microsoft Azure AD Application Proxy Connector service to generate a new log file.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-131">Restart the Microsoft Azure AD Application Proxy Connector service to generate a new log file.</span></span> <span data-ttu-id="e6c1f-132">The new log file enables you to delete or modify the old log files.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-132">The new log file enables you to delete or modify the old log files.</span></span> 
2. <span data-ttu-id="e6c1f-133">Follow the [View or export specific data](#view-or-export-specific-data) process described previously to find information that needs to be deleted.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-133">Follow the [View or export specific data](#view-or-export-specific-data) process described previously to find information that needs to be deleted.</span></span> <span data-ttu-id="e6c1f-134">Search all of the connector logs.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-134">Search all of the connector logs.</span></span>
3. <span data-ttu-id="e6c1f-135">Either delete the relevant log files or selectively delete the fields that contain personal data.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-135">Either delete the relevant log files or selectively delete the fields that contain personal data.</span></span> <span data-ttu-id="e6c1f-136">You can also delete all old log files if you don’t need them anymore.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-136">You can also delete all old log files if you don’t need them anymore.</span></span>

### <a name="turn-off-connector-logs"></a><span data-ttu-id="e6c1f-137">Turn off connector logs</span><span class="sxs-lookup"><span data-stu-id="e6c1f-137">Turn off connector logs</span></span>

<span data-ttu-id="e6c1f-138">One option to ensure the connector logs do not contain personal data is to turn off the log generation.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-138">One option to ensure the connector logs do not contain personal data is to turn off the log generation.</span></span> <span data-ttu-id="e6c1f-139">To stop generating connector logs, remove the following highlighted line from `C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config`.</span><span class="sxs-lookup"><span data-stu-id="e6c1f-139">To stop generating connector logs, remove the following highlighted line from `C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config`.</span></span> 

![Configuration](./media/application-proxy-remove-personal-data/01.png)


## <a name="next-steps"></a><span data-ttu-id="e6c1f-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6c1f-141">Next steps</span></span>

<span data-ttu-id="e6c1f-142">For an overview of Application Proxy, see [How to provide secure remote access to on-premises applications](application-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="e6c1f-142">For an overview of Application Proxy, see [How to provide secure remote access to on-premises applications](application-proxy.md).</span></span>

