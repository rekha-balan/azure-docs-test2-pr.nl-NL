---
title: Using b2clogin.com | Microsoft Docs
description: Learn about using b2clogin.com instead of login.microsoftonline.com.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/29/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 6ad0a5d59b28bf48742c9e1be89b51d2301dd582
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870753"
---
# <a name="using-b2clogincom"></a>Using b2clogin.com

>[!IMPORTANT]
>This feature is public preview 
>

You now have the option to use the Azure AD B2C service with `<YourTenantName>.b2clogin.com` instead of using `login.microsoftonline.com`.  This has many benefits:
* You no longer share the same cookie header size limit with the other Microsoft products.
* You can remove all references to Microsoft in your URL (you can replace `<YourTenantName>.onmicrosoft.com` with your tenant ID). For example: `https://<tenantname>.b2clogin.com/tfp/<tenantID>/<policyname>/v2.0/.well-known/openid-configuration`.

 In order to take advantage of b2clogin.com, you need to set some of the following:

1. For your **Run now endpoint** make sure you are using `<YourTenantName>.b2clogin.com` instead of using `login.microsoftonline.com`.
2. If you are using MSAL, you need to set `validateauthority=false`.  This is because the token issuer becomes`<YourTenantName>.b2clogin.com`.
