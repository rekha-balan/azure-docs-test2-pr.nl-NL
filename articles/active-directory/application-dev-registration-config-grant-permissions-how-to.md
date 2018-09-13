---
title: How to grant permissions to a custom-developed application | Microsoft Docs
description: How to grant permissions to your custom-developed application using the Azure AD portal or a URL parameter
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
ms.openlocfilehash: 922774c2482737537b64787ae473231ec1fbb68e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671519"
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="d77eb-103">How to grant permissions to a custom-developed application</span><span class="sxs-lookup"><span data-stu-id="d77eb-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="d77eb-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span><span class="sxs-lookup"><span data-stu-id="d77eb-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="d77eb-105">How to perform Admin Consent for your application</span><span class="sxs-lookup"><span data-stu-id="d77eb-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="d77eb-106">This has the effect of granting consent to the application for all users in your organization.</span><span class="sxs-lookup"><span data-stu-id="d77eb-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="d77eb-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span><span class="sxs-lookup"><span data-stu-id="d77eb-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="d77eb-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="d77eb-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="d77eb-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span><span class="sxs-lookup"><span data-stu-id="d77eb-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="d77eb-110">After signing in with admin credentials, the app has been granted consent for all users.</span><span class="sxs-lookup"><span data-stu-id="d77eb-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="d77eb-111">How to force User Consent for your application</span><span class="sxs-lookup"><span data-stu-id="d77eb-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="d77eb-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span><span class="sxs-lookup"><span data-stu-id="d77eb-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d77eb-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="d77eb-113">Next steps</span></span>

[<span data-ttu-id="d77eb-114">Consent and Integrating Apps to AzureAD</span><span class="sxs-lookup"><span data-stu-id="d77eb-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="d77eb-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span><span class="sxs-lookup"><span data-stu-id="d77eb-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d77eb-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="d77eb-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
