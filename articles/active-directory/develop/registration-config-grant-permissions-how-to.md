---
title: How to grant permissions to a custom-developed application | Microsoft Docs
description: How to grant permissions to your custom-developed application using the Azure AD portal or a URL parameter
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2018
ms.author: celested
ms.openlocfilehash: 10cf04fca8379f41587b1ea680c5b52a26193b53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965488"
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a>How to grant permissions to a custom-developed application

If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.

## <a name="how-to-perform-admin-consent-for-your-application"></a>How to perform Admin Consent for your application

This has the effect of granting consent to the application for all users in your organization.

1. Navigate to the **App Registrations** blade as a **global administrator**, then select the app.

2. Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.

Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*. After signing in with admin credentials, the app has been granted consent for all users.

## <a name="how-to-force-user-consent-for-your-application"></a>How to force User Consent for your application

* Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.

## <a name="next-steps"></a>Next steps

[Consent and Integrating Apps to AzureAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
