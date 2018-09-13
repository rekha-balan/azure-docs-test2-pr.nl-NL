---
title: Azure AD Connect in Microsoft Cloud Germany
description: Azure AD Connect will integrate your on-premises directories with Azure Active Directory. This allows you to provide a common identity for Office 365, Azure, and SaaS applications integrated with Azure AD.
keywords: introduction to Azure AD Connect, Azure AD Connect overview, what is Azure AD Connect, install active directory, Germany, Black Forest
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/07/2017
ms.author: billmath
ms.openlocfilehash: 36ed7347fb2baa01e1c6c2083344b78c6ee803fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556531"
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Azure AD Connect in Microsoft Cloud Germany - Public Preview
## <a name="introduction"></a>Introduction
Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.
Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator. When using Microsoft Cloud Germany, you must be aware of the following:

* The following URLs must be opened on a proxy server for synchronization to occur successfully:
  
  * *.microsoftonline.de
  * *.windows.net
  * * Certificate Revocation Lists
* When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.
* The following features are not available:
  * Azure AD Connect Health
  * Automatic updates
  * Password writeback

## <a name="download"></a>Download
You can download Azure AD Connect from the Azure AD Connect blade within the portal.  Use the instructions below to locate the Azure AD Connect blade.

### <a name="the-azure-ad-connect-blade"></a>The Azure AD Connect Blade
Once you have signed in to the Azure portal, do the following:

1. Go to Browse
2. Select Azure Active Directory
3. Then select Azure AD Connect

You should see the following:

![Azure AD Connect Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-germany/germany1.png)

The following table describes the features shown in the blade.

| Title | Description |
| --- | --- |
| SYNC STATUS |Let's you know whether synchronization is enabled or disabled. |
| LAST SYNC |The last time a successful sync completed. |
| FEDERATED DOMAINS |Shows the number of federated domains currently configured. |

## <a name="installation"></a>Installation
To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Advanced features and Additional Information
For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).  This page provides information and links to additional guidance.


