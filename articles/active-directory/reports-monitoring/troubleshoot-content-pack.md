---
title: Troubleshooting Azure Active Directory Activity logs content pack errors | Microsoft Docs
description: Provides you with a list of error messages of the Azure Active Directory Activity content pack and steps to fix them.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 01/15/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: bf50dbf942dc7a82afbb60455be45b6c4b287ccd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869110"
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="3227d-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span><span class="sxs-lookup"><span data-stu-id="3227d-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 

|  |
|--|
|<span data-ttu-id="3227d-104">Currently, the Azure AD Power BI content pack uses the Azure AD Graph APIs to retrieve data from your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="3227d-104">Currently, the Azure AD Power BI content pack uses the Azure AD Graph APIs to retrieve data from your Azure AD tenant.</span></span> <span data-ttu-id="3227d-105">As a result, you may see some disparity between the data available in the content pack and the data retrieved using the [Microsoft Graph APIs for reporting](concept-reporting-api.md).</span><span class="sxs-lookup"><span data-stu-id="3227d-105">As a result, you may see some disparity between the data available in the content pack and the data retrieved using the [Microsoft Graph APIs for reporting](concept-reporting-api.md).</span></span> |
|  |

<span data-ttu-id="3227d-106">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span><span class="sxs-lookup"><span data-stu-id="3227d-106">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="3227d-107">Refresh failed</span><span class="sxs-lookup"><span data-stu-id="3227d-107">Refresh failed</span></span>](troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="3227d-108">Failed to update data source credentials</span><span class="sxs-lookup"><span data-stu-id="3227d-108">Failed to update data source credentials</span></span>](troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="3227d-109">Importing of data is taking too long</span><span class="sxs-lookup"><span data-stu-id="3227d-109">Importing of data is taking too long</span></span>](troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="3227d-110">This article provides you with information about the possible causes and how to fix these errors.</span><span class="sxs-lookup"><span data-stu-id="3227d-110">This article provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="3227d-111">Refresh failed</span><span class="sxs-lookup"><span data-stu-id="3227d-111">Refresh failed</span></span> 
 
<span data-ttu-id="3227d-112">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span><span class="sxs-lookup"><span data-stu-id="3227d-112">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="3227d-113">Cause</span><span class="sxs-lookup"><span data-stu-id="3227d-113">Cause</span></span> | <span data-ttu-id="3227d-114">How to fix</span><span class="sxs-lookup"><span data-stu-id="3227d-114">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3227d-115">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the content pack.</span><span class="sxs-lookup"><span data-stu-id="3227d-115">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the content pack.</span></span> | <span data-ttu-id="3227d-116">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="3227d-116">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="3227d-117">A refresh can fail due to data issues in the underlying content pack.</span><span class="sxs-lookup"><span data-stu-id="3227d-117">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="3227d-118">File a support ticket.</span><span class="sxs-lookup"><span data-stu-id="3227d-118">File a support ticket.</span></span> <span data-ttu-id="3227d-119">For more information, see [How to get support for Azure Active Directory](../fundamentals/active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3227d-119">For more information, see [How to get support for Azure Active Directory](../fundamentals/active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="3227d-120">Failed to update data source credentials</span><span class="sxs-lookup"><span data-stu-id="3227d-120">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="3227d-121">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span><span class="sxs-lookup"><span data-stu-id="3227d-121">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="3227d-122">Cause</span><span class="sxs-lookup"><span data-stu-id="3227d-122">Cause</span></span> | <span data-ttu-id="3227d-123">How to fix</span><span class="sxs-lookup"><span data-stu-id="3227d-123">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3227d-124">The connecting user is not a global admin or a security reader or a security admin.</span><span class="sxs-lookup"><span data-stu-id="3227d-124">The connecting user is not a global admin or a security reader or a security admin.</span></span> | <span data-ttu-id="3227d-125">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span><span class="sxs-lookup"><span data-stu-id="3227d-125">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="3227d-126">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span><span class="sxs-lookup"><span data-stu-id="3227d-126">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="3227d-127">File a support ticket.</span><span class="sxs-lookup"><span data-stu-id="3227d-127">File a support ticket.</span></span> <span data-ttu-id="3227d-128">For more information, see [How to get support for Azure Active Directory](../fundamentals/active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3227d-128">For more information, see [How to get support for Azure Active Directory](../fundamentals/active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="3227d-129">Importing of data is taking too long</span><span class="sxs-lookup"><span data-stu-id="3227d-129">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="3227d-130">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span><span class="sxs-lookup"><span data-stu-id="3227d-130">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="3227d-131">You see the message: “*Importing data...*”</span><span class="sxs-lookup"><span data-stu-id="3227d-131">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="3227d-132">Cause</span><span class="sxs-lookup"><span data-stu-id="3227d-132">Cause</span></span> | <span data-ttu-id="3227d-133">How to fix</span><span class="sxs-lookup"><span data-stu-id="3227d-133">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3227d-134">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="3227d-134">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="3227d-135">Just be patient.</span><span class="sxs-lookup"><span data-stu-id="3227d-135">Just be patient.</span></span> <span data-ttu-id="3227d-136">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span><span class="sxs-lookup"><span data-stu-id="3227d-136">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="3227d-137">For more information, see [How to get support for Azure Active Directory](../fundamentals/active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="3227d-137">For more information, see [How to get support for Azure Active Directory](../fundamentals/active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3227d-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="3227d-138">Next steps</span></span>

<span data-ttu-id="3227d-139">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="3227d-139">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/blog/azure-active-directory-meets-power-bi/).</span></span>


