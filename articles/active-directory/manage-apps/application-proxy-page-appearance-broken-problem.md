---
title: Application page does not display correctly for an Application Proxy application | Microsoft Docs
description: Guidance when the page isn’t displaying correctly in an Application Proxy Application you have integrated with Azure AD
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 2ebcf225fb0959b5c72c3cea50f2f1386beb1457
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864918"
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="ec517-103">Application page does not display correctly for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="ec517-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="ec517-104">This article helps you troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span><span class="sxs-lookup"><span data-stu-id="ec517-104">This article helps you troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="ec517-105">Overview</span><span class="sxs-lookup"><span data-stu-id="ec517-105">Overview</span></span>
<span data-ttu-id="ec517-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span><span class="sxs-lookup"><span data-stu-id="ec517-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="ec517-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span><span class="sxs-lookup"><span data-stu-id="ec517-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="ec517-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span><span class="sxs-lookup"><span data-stu-id="ec517-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="ec517-109">You can verify if missing resources is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span><span class="sxs-lookup"><span data-stu-id="ec517-109">You can verify if missing resources is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="ec517-110">That indicates the pages currently cannot be found and that you need to publish them.</span><span class="sxs-lookup"><span data-stu-id="ec517-110">That indicates the pages currently cannot be found and that you need to publish them.</span></span>

<span data-ttu-id="ec517-111">As an example of this case, assume you have published an expenses application using the internal URL http://myapps/expenses, but the app uses the stylesheet http://myapps/style.css.</span><span class="sxs-lookup"><span data-stu-id="ec517-111">As an example of this case, assume you have published an expenses application using the internal URL http://myapps/expenses, but the app uses the stylesheet http://myapps/style.css.</span></span> <span data-ttu-id="ec517-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span><span class="sxs-lookup"><span data-stu-id="ec517-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="ec517-113">In this example, the problem is resolved by publishing the application with an internal URL http://myapp/.</span><span class="sxs-lookup"><span data-stu-id="ec517-113">In this example, the problem is resolved by publishing the application with an internal URL http://myapp/.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="ec517-114">Problems with publishing as one application</span><span class="sxs-lookup"><span data-stu-id="ec517-114">Problems with publishing as one application</span></span>

<span data-ttu-id="ec517-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span><span class="sxs-lookup"><span data-stu-id="ec517-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="ec517-116">To do so, we recommend using the [custom domains](application-proxy-configure-custom-domain.md) solution.</span><span class="sxs-lookup"><span data-stu-id="ec517-116">To do so, we recommend using the [custom domains](application-proxy-configure-custom-domain.md) solution.</span></span> <span data-ttu-id="ec517-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span><span class="sxs-lookup"><span data-stu-id="ec517-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="ec517-118">For other options, see the [troubleshoot broken links documentation](application-proxy-page-links-broken-problem.md).</span><span class="sxs-lookup"><span data-stu-id="ec517-118">For other options, see the [troubleshoot broken links documentation](application-proxy-page-links-broken-problem.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec517-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec517-119">Next steps</span></span>
[<span data-ttu-id="ec517-120">Publish applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="ec517-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
