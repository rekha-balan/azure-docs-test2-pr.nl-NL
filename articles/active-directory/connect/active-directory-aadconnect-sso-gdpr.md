---
title: User Privacy and Azure AD Seamless Single Sign-On | Microsoft Docs
description: This article deals with Azure Active Directory (Azure AD) Seamless SSO and GDPR compliance.
services: active-directory
keywords: what is Azure AD Connect, GDPR, required components for Azure AD, SSO, Single Sign-on
documentationcenter: ''
author: billmath
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/21/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 50c97ce7a492c934e15634622d86bf587ffb3fb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869174"
---
# <a name="user-privacy-and-azure-ad-seamless-single-sign-on"></a><span data-ttu-id="d5bb6-104">User Privacy and Azure AD Seamless Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5bb6-104">User Privacy and Azure AD Seamless Single Sign-On</span></span>

[!INCLUDE [Privacy](../../../includes/gdpr-intro-sentence.md)]

## <a name="overview"></a><span data-ttu-id="d5bb6-105">Overview</span><span class="sxs-lookup"><span data-stu-id="d5bb6-105">Overview</span></span>


<span data-ttu-id="d5bb6-106">Azure AD Seamless SSO creates the following log type, which can contain Personal Data:</span><span class="sxs-lookup"><span data-stu-id="d5bb6-106">Azure AD Seamless SSO creates the following log type, which can contain Personal Data:</span></span> 

- <span data-ttu-id="d5bb6-107">Azure AD Connect trace log files.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-107">Azure AD Connect trace log files.</span></span>

<span data-ttu-id="d5bb6-108">Improve user privacy for Seamless SSO in two ways:</span><span class="sxs-lookup"><span data-stu-id="d5bb6-108">Improve user privacy for Seamless SSO in two ways:</span></span>

1.  <span data-ttu-id="d5bb6-109">Upon request, extract data for a person and remove data from that person from the installations.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-109">Upon request, extract data for a person and remove data from that person from the installations.</span></span>
2.  <span data-ttu-id="d5bb6-110">Ensure no data is retained beyond 48 hours.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-110">Ensure no data is retained beyond 48 hours.</span></span>

<span data-ttu-id="d5bb6-111">We strongly recommend the second option as it is easier to implement and maintain.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-111">We strongly recommend the second option as it is easier to implement and maintain.</span></span> <span data-ttu-id="d5bb6-112">See following instructions for each log type:</span><span class="sxs-lookup"><span data-stu-id="d5bb6-112">See following instructions for each log type:</span></span>

### <a name="delete-azure-ad-connect-trace-log-files"></a><span data-ttu-id="d5bb6-113">Delete Azure AD Connect trace log files</span><span class="sxs-lookup"><span data-stu-id="d5bb6-113">Delete Azure AD Connect trace log files</span></span>

<span data-ttu-id="d5bb6-114">Check the contents of **%ProgramData%\AADConnect** folder and delete the trace log contents (**trace-\*.log** files) of this folder within 48 hours of installing or upgrading Azure AD Connect or modifying Seamless SSO configuration, as this action may create data covered by GDPR.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-114">Check the contents of **%ProgramData%\AADConnect** folder and delete the trace log contents (**trace-\*.log** files) of this folder within 48 hours of installing or upgrading Azure AD Connect or modifying Seamless SSO configuration, as this action may create data covered by GDPR.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d5bb6-115">Don’t delete the **PersistedState.xml** file in this folder, as this file is used to maintain the state of the previous installation of Azure AD Connect and is used when an upgrade installation is done.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-115">Don’t delete the **PersistedState.xml** file in this folder, as this file is used to maintain the state of the previous installation of Azure AD Connect and is used when an upgrade installation is done.</span></span> <span data-ttu-id="d5bb6-116">This file will never contain any data about a person and should never be deleted.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-116">This file will never contain any data about a person and should never be deleted.</span></span>

<span data-ttu-id="d5bb6-117">You can either review and delete these trace log files using Windows Explorer or you can use the following PowerShell script to perform the necessary actions:</span><span class="sxs-lookup"><span data-stu-id="d5bb6-117">You can either review and delete these trace log files using Windows Explorer or you can use the following PowerShell script to perform the necessary actions:</span></span>

```
$Files = ((Get-Item -Path "$env:programdata\aadconnect\trace-*.log").VersionInfo).FileName 
 
Foreach ($file in $Files) { 
    {Remove-Item -Path $File -Force} 
}
```

<span data-ttu-id="d5bb6-118">Save the script in a file with the ".PS1" extension.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-118">Save the script in a file with the ".PS1" extension.</span></span> <span data-ttu-id="d5bb6-119">Run this script as needed.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-119">Run this script as needed.</span></span>

<span data-ttu-id="d5bb6-120">To learn more about related Azure AD Connect GDPR requirements, see [this article](active-directory-aadconnect-gdpr.md).</span><span class="sxs-lookup"><span data-stu-id="d5bb6-120">To learn more about related Azure AD Connect GDPR requirements, see [this article](active-directory-aadconnect-gdpr.md).</span></span>

### <a name="note-about-domain-controller-logs"></a><span data-ttu-id="d5bb6-121">Note about Domain controller logs</span><span class="sxs-lookup"><span data-stu-id="d5bb6-121">Note about Domain controller logs</span></span>

<span data-ttu-id="d5bb6-122">If audit logging is enabled, this product may generate security logs for your Domain Controllers.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-122">If audit logging is enabled, this product may generate security logs for your Domain Controllers.</span></span> <span data-ttu-id="d5bb6-123">To learn more about configuring audit policies, read this [article](https://technet.microsoft.com/library/dd277403.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5bb6-123">To learn more about configuring audit policies, read this [article](https://technet.microsoft.com/library/dd277403.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5bb6-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5bb6-124">Next steps</span></span>
* [<span data-ttu-id="d5bb6-125">Review the Microsoft Privacy policy on Trust Center</span><span class="sxs-lookup"><span data-stu-id="d5bb6-125">Review the Microsoft Privacy policy on Trust Center</span></span>](https://www.microsoft.com/trustcenter)
- <span data-ttu-id="d5bb6-126">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-126">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="d5bb6-127">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span><span class="sxs-lookup"><span data-stu-id="d5bb6-127">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
