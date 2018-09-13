---
title: Links on the page don't work for an Application Proxy application | Microsoft Docs
description: How to troubleshoot issues with broken links on Application Proxy applications you have integrated with Azure AD
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
ms.openlocfilehash: f667fb96055934b8d9ce2d9ee7b9c0dd752c0533
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563754"
---
# <a name="links-on-the-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="93220-103">Links on the page don't work for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="93220-103">Links on the page don't work for an Application Proxy application</span></span>

<span data-ttu-id="93220-104">This article help you to troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span><span class="sxs-lookup"><span data-stu-id="93220-104">This article help you to troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="93220-105">Overview</span><span class="sxs-lookup"><span data-stu-id="93220-105">Overview</span></span> 
<span data-ttu-id="93220-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span><span class="sxs-lookup"><span data-stu-id="93220-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span></span> <span data-ttu-id="93220-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span><span class="sxs-lookup"><span data-stu-id="93220-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span></span>

<span data-ttu-id="93220-108">**Why does this happen?**</span><span class="sxs-lookup"><span data-stu-id="93220-108">**Why does this happen?**</span></span> <span data-ttu-id="93220-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span><span class="sxs-lookup"><span data-stu-id="93220-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span></span> <span data-ttu-id="93220-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span><span class="sxs-lookup"><span data-stu-id="93220-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="93220-111">Ways you can resolve broken links</span><span class="sxs-lookup"><span data-stu-id="93220-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="93220-112">There are three ways to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="93220-112">There are three ways to resolve this issue.</span></span> <span data-ttu-id="93220-113">The choices below are in listed in increasing complexity.</span><span class="sxs-lookup"><span data-stu-id="93220-113">The choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="93220-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span><span class="sxs-lookup"><span data-stu-id="93220-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span></span> <span data-ttu-id="93220-115">This allows all links to be resolved as content published within the same application.</span><span class="sxs-lookup"><span data-stu-id="93220-115">This allows all links to be resolved as content published within the same application.</span></span>

    <span data-ttu-id="93220-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span><span class="sxs-lookup"><span data-stu-id="93220-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span></span> <span data-ttu-id="93220-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span><span class="sxs-lookup"><span data-stu-id="93220-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span></span> <span data-ttu-id="93220-118">In this properties tab, you see the field “Home Page URL” which you can adjust to be the desired landing page.</span><span class="sxs-lookup"><span data-stu-id="93220-118">In this properties tab, you see the field “Home Page URL” which you can adjust to be the desired landing page.</span></span>

2.  <span data-ttu-id="93220-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) to publish your applications.</span><span class="sxs-lookup"><span data-stu-id="93220-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) to publish your applications.</span></span> <span data-ttu-id="93220-120">This feature allows the same URL to be used both internally and externally.</span><span class="sxs-lookup"><span data-stu-id="93220-120">This feature allows the same URL to be used both internally and externally.</span></span>

    <span data-ttu-id="93220-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span><span class="sxs-lookup"><span data-stu-id="93220-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span></span> <span data-ttu-id="93220-122">Note that all links still need to belong to a published application.</span><span class="sxs-lookup"><span data-stu-id="93220-122">Note that all links still need to belong to a published application.</span></span> <span data-ttu-id="93220-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span><span class="sxs-lookup"><span data-stu-id="93220-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span></span>

3.  <span data-ttu-id="93220-124">If neither of these options are feasible, you join the preview for a new feature that do URL translation/rewriting.</span><span class="sxs-lookup"><span data-stu-id="93220-124">If neither of these options are feasible, you join the preview for a new feature that do URL translation/rewriting.</span></span> <span data-ttu-id="93220-125">With this option, internal URLs or links that exist in the HTML body of your applications be translated, or “mapped”, to the published external App Proxy URLs.</span><span class="sxs-lookup"><span data-stu-id="93220-125">With this option, internal URLs or links that exist in the HTML body of your applications be translated, or “mapped”, to the published external App Proxy URLs.</span></span> <span data-ttu-id="93220-126">This only works for links in the HTML or CSS, and this not help if your link is generated through JS.</span><span class="sxs-lookup"><span data-stu-id="93220-126">This only works for links in the HTML or CSS, and this not help if your link is generated through JS.</span></span> 

<span data-ttu-id="93220-127">As a result, we strongly recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span><span class="sxs-lookup"><span data-stu-id="93220-127">As a result, we strongly recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span></span> <span data-ttu-id="93220-128">If you do want to join the preview, email <aadapfeedback@microsoft.com> with the applicationId(s).</span><span class="sxs-lookup"><span data-stu-id="93220-128">If you do want to join the preview, email <aadapfeedback@microsoft.com> with the applicationId(s).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93220-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="93220-129">Next steps</span></span>
[<span data-ttu-id="93220-130">Work with existing on-premises proxy servers</span><span class="sxs-lookup"><span data-stu-id="93220-130">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)

