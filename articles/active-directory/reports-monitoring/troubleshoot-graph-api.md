---
title: Troubleshoot errors in Azure Active Directory reporting API | Microsoft Docs
description: Provides you with a resolution to errors while calling Azure Active Directory Reporting APIs.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 0030c5a4-16f0-46f4-ad30-782e7fea7e40
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 01/15/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: a333e72312b3916b2f6ffb0703de0ff1655d6685
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857231"
---
# <a name="troubleshoot-errors-in-azure-active-directory-reporting-api"></a><span data-ttu-id="a150f-103">Troubleshoot errors in Azure Active Directory reporting API</span><span class="sxs-lookup"><span data-stu-id="a150f-103">Troubleshoot errors in Azure Active Directory reporting API</span></span>

<span data-ttu-id="a150f-104">This article lists the common error messages you may run into while accessing activity reports using the MS Graph API and steps for their resolution.</span><span class="sxs-lookup"><span data-stu-id="a150f-104">This article lists the common error messages you may run into while accessing activity reports using the MS Graph API and steps for their resolution.</span></span>

### <a name="500-http-internal-server-error-while-accessing-microsoft-graph-v2-endpoint"></a><span data-ttu-id="a150f-105">500 HTTP internal server error while accessing Microsoft Graph V2 endpoint</span><span class="sxs-lookup"><span data-stu-id="a150f-105">500 HTTP internal server error while accessing Microsoft Graph V2 endpoint</span></span>

<span data-ttu-id="a150f-106">We do not currently support the Microsoft Graph v2 endpoint - make sure to access the activity logs using the Microsoft Graph v1 endpoint.</span><span class="sxs-lookup"><span data-stu-id="a150f-106">We do not currently support the Microsoft Graph v2 endpoint - make sure to access the activity logs using the Microsoft Graph v1 endpoint.</span></span>

### <a name="error-failed-to-get-user-roles-from-ad-graph"></a><span data-ttu-id="a150f-107">Error: Failed to get user roles from AD Graph</span><span class="sxs-lookup"><span data-stu-id="a150f-107">Error: Failed to get user roles from AD Graph</span></span>

<span data-ttu-id="a150f-108">You may get this error message when trying to access sign-ins using Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="a150f-108">You may get this error message when trying to access sign-ins using Graph Explorer.</span></span> <span data-ttu-id="a150f-109">Make sure you are signed in to your account using both of the sign-in buttons in the Graph Explorer UI, as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="a150f-109">Make sure you are signed in to your account using both of the sign-in buttons in the Graph Explorer UI, as shown in the following image.</span></span> 

![Graph Explorer](./media/troubleshoot-graph-api/graph-explorer.png)

### <a name="error-failed-to-do-premium-license-check-from-ad-graph"></a><span data-ttu-id="a150f-111">Error: Failed to do premium license check from AD Graph</span><span class="sxs-lookup"><span data-stu-id="a150f-111">Error: Failed to do premium license check from AD Graph</span></span> 

<span data-ttu-id="a150f-112">If you run into this error message while trying to access sign-ins using Graph Explorer, choose **Modify Permissions** underneath your account on the left nav, and select **Tasks.ReadWrite** and **Directory.Read.All**.</span><span class="sxs-lookup"><span data-stu-id="a150f-112">If you run into this error message while trying to access sign-ins using Graph Explorer, choose **Modify Permissions** underneath your account on the left nav, and select **Tasks.ReadWrite** and **Directory.Read.All**.</span></span> 

![Modify permissions UI](./media/troubleshoot-graph-api/modify-permissions.png)


### <a name="error-neither-tenant-is-b2c-or-tenant-doesnt-have-premium-license"></a><span data-ttu-id="a150f-114">Error: Neither tenant is B2C or tenant doesn't have premium license</span><span class="sxs-lookup"><span data-stu-id="a150f-114">Error: Neither tenant is B2C or tenant doesn't have premium license</span></span>

<span data-ttu-id="a150f-115">Accessing sign-in reports requires an Azure Active Directory premium 1 (P1) license.</span><span class="sxs-lookup"><span data-stu-id="a150f-115">Accessing sign-in reports requires an Azure Active Directory premium 1 (P1) license.</span></span> <span data-ttu-id="a150f-116">If you see this error message while accessing sign-ins, make sure that your tenant is licensed with an Azure AD P1 license.</span><span class="sxs-lookup"><span data-stu-id="a150f-116">If you see this error message while accessing sign-ins, make sure that your tenant is licensed with an Azure AD P1 license.</span></span>

### <a name="error-user-is-not-in-the-allowed-roles"></a><span data-ttu-id="a150f-117">Error: User is not in the allowed roles</span><span class="sxs-lookup"><span data-stu-id="a150f-117">Error: User is not in the allowed roles</span></span> 

<span data-ttu-id="a150f-118">If you see this error message while trying to access audit logs or sign-ins using the API, make sure that your account is part of the **Security Reader** or **Report Reader** role in your Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="a150f-118">If you see this error message while trying to access audit logs or sign-ins using the API, make sure that your account is part of the **Security Reader** or **Report Reader** role in your Azure Active Directory tenant.</span></span> 

### <a name="error-application-missing-aad-read-directory-data-permission"></a><span data-ttu-id="a150f-119">Error: Application missing AAD 'Read directory data' permission</span><span class="sxs-lookup"><span data-stu-id="a150f-119">Error: Application missing AAD 'Read directory data' permission</span></span> 

<span data-ttu-id="a150f-120">Please follow the steps in the [Prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md) to ensure your application is running with the right set of permissions.</span><span class="sxs-lookup"><span data-stu-id="a150f-120">Please follow the steps in the [Prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md) to ensure your application is running with the right set of permissions.</span></span> 

### <a name="error-application-missing-msgraph-api-read-all-audit-log-data-permission"></a><span data-ttu-id="a150f-121">Error: Application missing MSGraph API 'Read all audit log data' permission</span><span class="sxs-lookup"><span data-stu-id="a150f-121">Error: Application missing MSGraph API 'Read all audit log data' permission</span></span>

<span data-ttu-id="a150f-122">Please follow the steps in the [Prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md) to ensure your application is running with the right set of permissions.</span><span class="sxs-lookup"><span data-stu-id="a150f-122">Please follow the steps in the [Prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md) to ensure your application is running with the right set of permissions.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a150f-123">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a150f-123">Next Steps</span></span>

<span data-ttu-id="a150f-124">[Use the audit API reference](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/directoryaudit)
[Use the sign-in activity report API reference](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin)</span><span class="sxs-lookup"><span data-stu-id="a150f-124">[Use the audit API reference](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/directoryaudit)
[Use the sign-in activity report API reference](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin)</span></span>