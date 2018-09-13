---
title: Azure Active Directory Reporting Latencies | Microsoft Docs
description: Amount of time it takes for reporting events to show up in your Azure Active Directory
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/07/2016
ms.author: dhanyahk;markvi
ms.openlocfilehash: 16336e38454d463364f6e46681bc1af42d7f57f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552952"
---
# <a name="azure-active-directory-report-latencies"></a>Azure Active Directory Report Latencies
*This documentation is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*

| Report | Minimum | Average | Maximum |
| --- | --- | --- | --- |
| **Security Reports** | | | |
| Irregular sign-in activity |2 hours |4 hours |8 hours |
| Sign-ins from unknown sources |2 hours |4 hours |8 hours |
| Sign-ins after multiple failures |2 hours |4 hours |8 hours |
| Sign-ins from multiple geographies |2 hours |4 hours |8 hours |
| Sign-ins from IP addresses with suspicious activity |2 hours |4 hours |8 hours |
| Sign-ins from possibly infected devices |2 hours |4 hours |8 hours |
| Users with anomalous sign-in activity |2 hours |4 hours |8 hours |
| Users with leaked credentials |2 hours |4 hours |8 hours |
| **Application Reports** | | | |
| Account provisioning activity |2 hours |4 hours |8 hours |
| Account provisioning errors |2 hours |4 hours |8 hours |
| Application usage |2 hours |4 hours |8 hours |
| Password rollover status |2 hours |4 hours |8 hours |
| **Audit & Activity Reports** | | | |
| Audit report |1 minute |15 minutes |30 minutes |
| Password reset activity (Azure AD) |2 hours |4 hours |8 hours |
| Password reset activity (Identity Manager) |2 hours |4 hours |8 hours |
| Password reset registration activity (Azure AD) |2 hours |4 hours |8 hours |
| Password reset registration activity (Identity Manager) |2 hours |4 hours |8 hours |
| Self service groups activity (Azure AD) |2 hours |4 hours |8 hours |
| Self service groups activity (Identity Manager) |2 hours |4 hours |8 hours |
| **RMS Reports** | | | |
| Most active RMS users |2 hours |4 hours |8 hours |
| RMS usage |2 hours |4 hours |8 hours |
| RMS device usage |2 hours |4 hours |8 hours |
| RMS enabled application usage |2 hours |4 hours |8 hours |
| **Private Preview Reports** | | | |
| All User Sign-in activity |2 hours |4 hours |8 hours |

