---
title: Getting started with the Azure AD reporting API | Microsoft Docs
description: How to get started with the Azure Active Directory reporting API
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/25/2016
ms.author: dhanyahk;markvi
ms.openlocfilehash: 3a8e9c802c265dacd1b8c3688855ce6ec0d90bb1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540933"
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="13e15-103">Getting started with the Azure Active Directory reporting API</span><span class="sxs-lookup"><span data-stu-id="13e15-103">Getting started with the Azure Active Directory reporting API</span></span>
<span data-ttu-id="13e15-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="13e15-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="13e15-105">Azure Active Directory provides you with a variety of reports.</span><span class="sxs-lookup"><span data-stu-id="13e15-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="13e15-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span><span class="sxs-lookup"><span data-stu-id="13e15-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="13e15-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span><span class="sxs-lookup"><span data-stu-id="13e15-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="13e15-108">You can call these APIs from a variety of programming languages and tools.</span><span class="sxs-lookup"><span data-stu-id="13e15-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="13e15-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span><span class="sxs-lookup"><span data-stu-id="13e15-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="13e15-110">In the next section, you find more details about using the audit and sign-in APIs.</span><span class="sxs-lookup"><span data-stu-id="13e15-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="13e15-111">For all other APIs, see the [Azure AD reports and events (preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span><span class="sxs-lookup"><span data-stu-id="13e15-111">For all other APIs, see the [Azure AD reports and events (preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="13e15-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="13e15-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="13e15-113">Learning map</span><span class="sxs-lookup"><span data-stu-id="13e15-113">Learning map</span></span>
1. <span data-ttu-id="13e15-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="13e15-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="13e15-115">**Explore** - Get a first impression of the reporting APIs:</span><span class="sxs-lookup"><span data-stu-id="13e15-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="13e15-116">Using the samples for the audit API</span><span class="sxs-lookup"><span data-stu-id="13e15-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="13e15-117">Using the samples for the sign-in activity report API</span><span class="sxs-lookup"><span data-stu-id="13e15-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="13e15-118">**Customize** -  Create your own solution:</span><span class="sxs-lookup"><span data-stu-id="13e15-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="13e15-119">Using the audit API reference</span><span class="sxs-lookup"><span data-stu-id="13e15-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="13e15-120">Using the sign-in activity report API reference</span><span class="sxs-lookup"><span data-stu-id="13e15-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="13e15-121">Next Steps</span><span class="sxs-lookup"><span data-stu-id="13e15-121">Next Steps</span></span>
<span data-ttu-id="13e15-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="13e15-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

