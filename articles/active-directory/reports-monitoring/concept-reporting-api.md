---
title: Get started with the Azure AD reporting API | Microsoft Docs
description: How to get started with the Azure Active Directory reporting API
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 05/07/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 7de7c87e5cf1747f4899f33d9e6b9cbf0bb430e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856551"
---
# <a name="get-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="50a64-103">Get started with the Azure Active Directory reporting API</span><span class="sxs-lookup"><span data-stu-id="50a64-103">Get started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="50a64-104">Azure Active Directory provides you with a variety of [reports](overview-reports.md).</span><span class="sxs-lookup"><span data-stu-id="50a64-104">Azure Active Directory provides you with a variety of [reports](overview-reports.md).</span></span> <span data-ttu-id="50a64-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span><span class="sxs-lookup"><span data-stu-id="50a64-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> 

<span data-ttu-id="50a64-106">By using the Azure AD reporting API, you can gain programmatic access to the data through a set of REST-based APIs.</span><span class="sxs-lookup"><span data-stu-id="50a64-106">By using the Azure AD reporting API, you can gain programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="50a64-107">You can call these APIs from a variety of programming languages and tools.</span><span class="sxs-lookup"><span data-stu-id="50a64-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="50a64-108">This article provides you with a roadmap for accessing the reporting data using the related API.</span><span class="sxs-lookup"><span data-stu-id="50a64-108">This article provides you with a roadmap for accessing the reporting data using the related API.</span></span>

<span data-ttu-id="50a64-109">If you run into issues, see [how to get support for Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="50a64-109">If you run into issues, see [how to get support for Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="50a64-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50a64-110">Prerequisites</span></span>

<span data-ttu-id="50a64-111">To access the reporting API, even if you are planning on accessing the API using a script, you need to:</span><span class="sxs-lookup"><span data-stu-id="50a64-111">To access the reporting API, even if you are planning on accessing the API using a script, you need to:</span></span>

1. <span data-ttu-id="50a64-112">Assign roles (Security Reader, Security Admin, Global Admin)</span><span class="sxs-lookup"><span data-stu-id="50a64-112">Assign roles (Security Reader, Security Admin, Global Admin)</span></span>
2. <span data-ttu-id="50a64-113">Register an application</span><span class="sxs-lookup"><span data-stu-id="50a64-113">Register an application</span></span>
3. <span data-ttu-id="50a64-114">Grant permissions</span><span class="sxs-lookup"><span data-stu-id="50a64-114">Grant permissions</span></span>
4. <span data-ttu-id="50a64-115">Gather configuration settings</span><span class="sxs-lookup"><span data-stu-id="50a64-115">Gather configuration settings</span></span>

<span data-ttu-id="50a64-116">For detailed instructions, see the [prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md).</span><span class="sxs-lookup"><span data-stu-id="50a64-116">For detailed instructions, see the [prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md).</span></span>

## <a name="apis-with-graph-explorer"></a><span data-ttu-id="50a64-117">APIs with Graph Explorer</span><span class="sxs-lookup"><span data-stu-id="50a64-117">APIs with Graph Explorer</span></span>

<span data-ttu-id="50a64-118">You can use the [MSGraph explorer](https://developer.microsoft.com/graph/graph-explorer) to verify your sign-in and audit API data.</span><span class="sxs-lookup"><span data-stu-id="50a64-118">You can use the [MSGraph explorer](https://developer.microsoft.com/graph/graph-explorer) to verify your sign-in and audit API data.</span></span> <span data-ttu-id="50a64-119">Make sure to sign in to your account using both of the sign-in buttons in the Graph Explorer UI, and set **AuditLog.Read.All** and **Directory.Read.All** permissions for your tenant as shown.</span><span class="sxs-lookup"><span data-stu-id="50a64-119">Make sure to sign in to your account using both of the sign-in buttons in the Graph Explorer UI, and set **AuditLog.Read.All** and **Directory.Read.All** permissions for your tenant as shown.</span></span>   

![Graph Explorer](./media/concept-reporting-api/graph-explorer.png)

![Modify permissions UI](./media/concept-reporting-api/modify-permissions.png)

## <a name="use-certificates-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="50a64-122">Use certificates to access the Azure AD reporting API</span><span class="sxs-lookup"><span data-stu-id="50a64-122">Use certificates to access the Azure AD reporting API</span></span> 

<span data-ttu-id="50a64-123">Use the Azure AD Reporting API with certificates if you plan to retrieve reporting data without user intervention.</span><span class="sxs-lookup"><span data-stu-id="50a64-123">Use the Azure AD Reporting API with certificates if you plan to retrieve reporting data without user intervention.</span></span>

<span data-ttu-id="50a64-124">For detailed instructions, see [Get data using the Azure AD Reporting API with certificates](tutorial-access-api-with-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="50a64-124">For detailed instructions, see [Get data using the Azure AD Reporting API with certificates](tutorial-access-api-with-certificates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="50a64-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="50a64-125">Next steps</span></span>

 * [<span data-ttu-id="50a64-126">Audit API reference</span><span class="sxs-lookup"><span data-stu-id="50a64-126">Audit API reference</span></span>](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/directoryaudit) 
 * [<span data-ttu-id="50a64-127">Sign-in activity report API reference</span><span class="sxs-lookup"><span data-stu-id="50a64-127">Sign-in activity report API reference</span></span>](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin)
 * [<span data-ttu-id="50a64-128">Troubleshoot errors in Azure AD reporting API</span><span class="sxs-lookup"><span data-stu-id="50a64-128">Troubleshoot errors in Azure AD reporting API</span></span>](troubleshoot-graph-api.md)


