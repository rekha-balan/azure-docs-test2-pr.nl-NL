---
title: Azure Active Directory reporting latencies | Microsoft Docs
description: Learn about the amount of time it takes for reporting events to show up in your Azure portal
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: markvi;dhanyahk
ms.openlocfilehash: 1c6b79c5f67cee5d62c9879bdeec926091253af6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552431"
---
# <a name="azure-active-directory-reporting-latencies---preview"></a>Azure Active Directory reporting latencies - preview

With reporting in the Azure Active Directory [preview](active-directory-preview-explainer.md), you get all the information you need to determine how your environment is doing. The amount of time it takes for reporting data to show up in the Azure portal is also known as latency. 

This topic lists the latency information for the all reporting categories in the Azure portal. 


## <a name="activity-reports"></a>Activity reports

There are two areas of activity reporting:

- **Sign-in activities** – Information about the usage of managed applications and user sign-in activities
- **Audit logs** - System activity information about users and group management, your managed applications and directory activities

The following table lists the latency information for activity reports.

| Report | Minimum | Average | Maximum |
| :-- | --- | --- | --- |
| Audit logs             | 30 minutes  | 45 Minutes | 1 hour     |
| Sign-ins               | 15 minutes  | 15 minutes | 2 hours*   |

>[!NOTE]
> For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up. 


## <a name="security-reports"></a>Security reports

There are two areas of security reporting:

- **Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account. 
- **Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised. 

The following table lists the latency information for security reports.

| Report | Minimum | Average | Maximum |
| :-- | --- | --- | --- |
| Users at risk          | 5 minutes   | 15 minutes  | 2 hours  |
| Risky sign-ins         | 5 minutes   | 15 minutes  | 2 hours  |

## <a name="risk-events"></a>Risk events

Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts. Each detected suspicious action is stored in a record called risk event.

The following table lists the latency information for risk events.

| Report | Minimum | Average | Maximum |
| :-- | --- | --- | --- |
| Sign-ins from anonymous IP addresses |5 minutes |15 Minutes |2 hours |
| Sign-ins from unfamiliar locations |5 minutes |15 Minutes |2 hours |
| Users with leaked credentials |2 hours |4 hours |8 hours |
| Impossible travel to atypical locations |2 hours |4 hours |8 hours  |
| Sign-ins from infected devices |2 hours |4 hours |8 hours  |
| Sign-ins from IP addresses with suspicious activity |2 hours |4 hours |8 hours  |



## <a name="next-steps"></a>Next steps

If you want to know more about the activity reports in the Azure portal, see:

- [Sign-in activity reports in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins.md)
- [Audit activity reports in the Azure Active Directory portal](active-directory-reporting-activity-audit-logs.md)

If you want to know more about the security reports in the Azure portal, see:

- [Users at risk security report in the Azure Active Directory portal](active-directory-reporting-security-user-at-risk.md)
- [Risky sign-ins report in the Azure Active Directory portal](active-directory-reporting-security-risky-sign-ins.md)

If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).