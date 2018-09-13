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
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="76443-103">Problems signing in to an custom-developed application</span><span class="sxs-lookup"><span data-stu-id="76443-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="76443-104">There are several errors that could be causing you to not be able to sign into an app.</span><span class="sxs-lookup"><span data-stu-id="76443-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="76443-105">The biggest reason people encounter this problem is misconfigured apps.</span><span class="sxs-lookup"><span data-stu-id="76443-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="76443-106">Errors related to  misconfigured apps</span><span class="sxs-lookup"><span data-stu-id="76443-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="76443-107">Verify both the configurations in the portal match what you have in your app.</span><span class="sxs-lookup"><span data-stu-id="76443-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="76443-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span><span class="sxs-lookup"><span data-stu-id="76443-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="76443-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span><span class="sxs-lookup"><span data-stu-id="76443-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="76443-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span><span class="sxs-lookup"><span data-stu-id="76443-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76443-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="76443-111">Next steps</span></span>

[<span data-ttu-id="76443-112">Azure AD Developer Guide</span><span class="sxs-lookup"><span data-stu-id="76443-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="76443-113">Consent and Integrating Apps to Azure AD</span><span class="sxs-lookup"><span data-stu-id="76443-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="76443-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span><span class="sxs-lookup"><span data-stu-id="76443-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="76443-115">Azure AD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="76443-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
