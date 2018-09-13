---
title: Problems signing in to an custom-developed application | Microsoft Docs
description: Common rrors that could be causing you to not be able to sign into an application you have developed with Azure AD
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 6e39bef84814aa441d72b50e584332ba8b55993f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552278"
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a>Problems signing in to an custom-developed application

There are several errors that could be causing you to not be able to sign into an app. The biggest reason people encounter this problem is misconfigured apps.

## <a name="errors-related-to--misconfigured-apps"></a>Errors related to  misconfigured apps

* Verify both the configurations in the portal match what you have in your app. Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.

* Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.

* See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.

## <a name="next-steps"></a>Next steps

[Azure AD Developer Guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[Consent and Integrating Apps to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[Consent and Permissioning for Azure AD v2.0 converged Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory>)
