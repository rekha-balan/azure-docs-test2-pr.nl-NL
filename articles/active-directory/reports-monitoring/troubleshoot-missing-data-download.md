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
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-downloaded"></a>I can’t find any data in the Azure Active Directory activity logs I downloaded


## <a name="symptoms"></a>Symptoms

I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose. Why? 

 ![Reporting](./media/troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Cause

When you download activity logs in the Azure portal, we limit the scale to 5000 records, sorted by most recent first. 

## <a name="resolution"></a>Resolution

You can leverage [Azure AD Reporting APIs](concept-reporting-api.md) to fetch up to a million records at any given point. Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (for example, daily or weekly).

## <a name="next-steps"></a>Next steps
See the [Azure Active Directory reporting FAQ](reports-faq.md).

