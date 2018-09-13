---
title: 'Troubleshooting: Missing data in the downloaded Azure Active Directory activity logs - preview | Microsoft Docs'
description: Provides you with a resolution to missing data in downloaded Azure Active Directory activity logs preview.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/09/2017
ms.author: markvi
ms.openlocfilehash: 133b8147691caea39db31fb9439c28fff718f6f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662171"
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a>I can’t find any data in the Azure Active Directory activity logs I have downloaded


## <a name="symptoms"></a>Symptoms

I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose. Why? 

 ![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Cause

When you download activity logs in the Azure portal, we limit the scale to 120K records, sorted by most recent. 

## <a name="resolution"></a>Resolution

You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) to fetch up to a million records at any given point. Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (e.g., daily or weekly).

## <a name="next-steps"></a>Next steps
See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).


