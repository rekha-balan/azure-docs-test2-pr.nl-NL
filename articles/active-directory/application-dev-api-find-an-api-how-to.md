---
title: How to find a specific API needed for a custom-developed application | Microsoft Docs
description: How to configure the permissions you need to access a particular API in your custom developed Azure AD application
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
ms.openlocfilehash: adf6b3cdf8dee3d85dc93406bad5a701af796f00
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553731"
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="625e2-103">How to find a specific API needed for a custom-developed application</span><span class="sxs-lookup"><span data-stu-id="625e2-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="625e2-104">Access to APIs require configuration of access scopes and roles.</span><span class="sxs-lookup"><span data-stu-id="625e2-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="625e2-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span><span class="sxs-lookup"><span data-stu-id="625e2-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="625e2-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span><span class="sxs-lookup"><span data-stu-id="625e2-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="625e2-107">Configuring a resource application to expose web APIs</span><span class="sxs-lookup"><span data-stu-id="625e2-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="625e2-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span><span class="sxs-lookup"><span data-stu-id="625e2-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="625e2-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="625e2-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="625e2-110">Configuring a client application to access web APIs</span><span class="sxs-lookup"><span data-stu-id="625e2-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="625e2-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span><span class="sxs-lookup"><span data-stu-id="625e2-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="625e2-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="625e2-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="625e2-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="625e2-113">Next steps</span></span>

-   [<span data-ttu-id="625e2-114">Integrating applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="625e2-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="625e2-115">Understanding the Azure Active Directory application manifest</span><span class="sxs-lookup"><span data-stu-id="625e2-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


