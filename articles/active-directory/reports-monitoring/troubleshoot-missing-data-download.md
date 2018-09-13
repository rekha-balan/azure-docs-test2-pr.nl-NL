---
title: 'Troubleshooting: Missing data in the downloaded Azure Active Directory activity logs | Microsoft Docs'
description: Provides you with a resolution to missing data in downloaded Azure Active Directory activity logs.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 01/15/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 9138da42eeb87e45b86be10aff67792ee6de09b4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864657"
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-downloaded"></a><span data-ttu-id="ce0c4-103">I can’t find any data in the Azure Active Directory activity logs I downloaded</span><span class="sxs-lookup"><span data-stu-id="ce0c4-103">I can’t find any data in the Azure Active Directory activity logs I downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="ce0c4-104">Symptoms</span><span class="sxs-lookup"><span data-stu-id="ce0c4-104">Symptoms</span></span>

<span data-ttu-id="ce0c4-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span><span class="sxs-lookup"><span data-stu-id="ce0c4-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span></span> <span data-ttu-id="ce0c4-106">Why?</span><span class="sxs-lookup"><span data-stu-id="ce0c4-106">Why?</span></span> 

 ![Reporting](./media/troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="ce0c4-108">Cause</span><span class="sxs-lookup"><span data-stu-id="ce0c4-108">Cause</span></span>

<span data-ttu-id="ce0c4-109">When you download activity logs in the Azure portal, we limit the scale to 5000 records, sorted by most recent first.</span><span class="sxs-lookup"><span data-stu-id="ce0c4-109">When you download activity logs in the Azure portal, we limit the scale to 5000 records, sorted by most recent first.</span></span> 

## <a name="resolution"></a><span data-ttu-id="ce0c4-110">Resolution</span><span class="sxs-lookup"><span data-stu-id="ce0c4-110">Resolution</span></span>

<span data-ttu-id="ce0c4-111">You can leverage [Azure AD Reporting APIs](concept-reporting-api.md) to fetch up to a million records at any given point.</span><span class="sxs-lookup"><span data-stu-id="ce0c4-111">You can leverage [Azure AD Reporting APIs](concept-reporting-api.md) to fetch up to a million records at any given point.</span></span> <span data-ttu-id="ce0c4-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (for example, daily or weekly).</span><span class="sxs-lookup"><span data-stu-id="ce0c4-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (for example, daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce0c4-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce0c4-113">Next steps</span></span>
<span data-ttu-id="ce0c4-114">See the [Azure Active Directory reporting FAQ](reports-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ce0c4-114">See the [Azure Active Directory reporting FAQ](reports-faq.md).</span></span>

