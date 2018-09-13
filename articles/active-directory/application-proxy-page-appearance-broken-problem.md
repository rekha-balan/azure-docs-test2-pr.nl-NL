---
title: Application page does not display correctly for an Application Proxy application | Microsoft Docs
description: Guidance when the page isn’t displaying correctly in an Application Proxy Application you have integrated with Azure AD
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
ms.openlocfilehash: cbd8fc1d37851fd5e9317ca92f5c32a6fbd7709c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549847"
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="c27ce-103">Application page does not display correctly for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="c27ce-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="c27ce-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span><span class="sxs-lookup"><span data-stu-id="c27ce-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="c27ce-105">Overview</span><span class="sxs-lookup"><span data-stu-id="c27ce-105">Overview</span></span>
<span data-ttu-id="c27ce-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span><span class="sxs-lookup"><span data-stu-id="c27ce-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="c27ce-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span><span class="sxs-lookup"><span data-stu-id="c27ce-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="c27ce-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span><span class="sxs-lookup"><span data-stu-id="c27ce-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="c27ce-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span><span class="sxs-lookup"><span data-stu-id="c27ce-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="c27ce-110">That indicates the pages that currently cannot be found and may still need to be published.</span><span class="sxs-lookup"><span data-stu-id="c27ce-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="c27ce-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="c27ce-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="c27ce-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span><span class="sxs-lookup"><span data-stu-id="c27ce-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="c27ce-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span><span class="sxs-lookup"><span data-stu-id="c27ce-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="c27ce-114">Problems with publishing as one application</span><span class="sxs-lookup"><span data-stu-id="c27ce-114">Problems with publishing as one application</span></span>

<span data-ttu-id="c27ce-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span><span class="sxs-lookup"><span data-stu-id="c27ce-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="c27ce-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span><span class="sxs-lookup"><span data-stu-id="c27ce-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="c27ce-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span><span class="sxs-lookup"><span data-stu-id="c27ce-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="c27ce-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="c27ce-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c27ce-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="c27ce-119">Next steps</span></span>
[<span data-ttu-id="c27ce-120">Publish applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="c27ce-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
