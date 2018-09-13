---
title: Unlicensed Usage Report | Microsoft Docs
description: The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: ee6106b43f2b90d5033c474896f07a3bab86bf98
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563132"
---
# <a name="unlicensed-usage-report"></a>Unlicensed usage report
The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features. This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses. 

The report shows active usage of the paid features in the last 30 days. 

## <a name="report-structure"></a>Report structure
| Column name | Description |
|:--- |:--- |
| Unlicensed User |Name of the user |
| Feature |The feature name. For example: conditional access |
| Application Accessed |The name of the application that is being accessed with the feature. For example: Office 365 SharePoint Online |

> [!NOTE]
> If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Conditional access feature
Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license. 

This applies to MFA / Location policies as well as device polices that use Intune.

## <a name="see-also"></a>See also
* [Using Conditional Access with Office 365 and other Azure Active Directory connected apps](active-directory-conditional-access.md)
* [Getting started with conditional access to Azure AD](active-directory-conditional-access-azuread-connected-apps.md) 

