---
title: 'Troubleshooting: Missing data in the Azure Active Directory activity log - preview | Microsoft Docs'
description: Lists the various available reports for Azure Active Directory preview
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/09/2017
ms.author: markvi
ms.openlocfilehash: 5c8d5c93cabc2243464df56026cc3884fb8a1022
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554400"
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a>I can’t find some actions that I performed in the Azure Active Directory activity log


## <a name="symptoms"></a>Symptoms

I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.

 ![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a>Cause

Actions don’t appear immediately in the Activity Audit log. It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.

## <a name="resolution"></a>Resolution

Wait for 15 minutes to an hour and see if the actions appear in the log. If you still don’t see them, please raise a support ticket with us and we will look into it.


## <a name="next-steps"></a>Next steps
See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).


