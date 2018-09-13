---
title: Links on the page don't work for an Application Proxy application | Microsoft Docs
description: How to troubleshoot issues with broken links on Application Proxy applications you have integrated with Azure AD
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 382b484f5ed1e45863d24635554cd7c3a55176a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865870"
---
# <a name="links-on-the-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="f901b-103">Links on the page don't work for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="f901b-103">Links on the page don't work for an Application Proxy application</span></span>

<span data-ttu-id="f901b-104">This article helps you troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span><span class="sxs-lookup"><span data-stu-id="f901b-104">This article helps you troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="f901b-105">Overview</span><span class="sxs-lookup"><span data-stu-id="f901b-105">Overview</span></span> 
<span data-ttu-id="f901b-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span><span class="sxs-lookup"><span data-stu-id="f901b-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span></span> <span data-ttu-id="f901b-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span><span class="sxs-lookup"><span data-stu-id="f901b-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span></span>

<span data-ttu-id="f901b-108">**Why does this happen?**</span><span class="sxs-lookup"><span data-stu-id="f901b-108">**Why does this happen?**</span></span> <span data-ttu-id="f901b-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span><span class="sxs-lookup"><span data-stu-id="f901b-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span></span> <span data-ttu-id="f901b-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span><span class="sxs-lookup"><span data-stu-id="f901b-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="f901b-111">Ways you can resolve broken links</span><span class="sxs-lookup"><span data-stu-id="f901b-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="f901b-112">There are three ways to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="f901b-112">There are three ways to resolve this issue.</span></span> <span data-ttu-id="f901b-113">The choices below are in listed in increasing complexity.</span><span class="sxs-lookup"><span data-stu-id="f901b-113">The choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="f901b-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span><span class="sxs-lookup"><span data-stu-id="f901b-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span></span> <span data-ttu-id="f901b-115">This allows all links to be resolved as content published within the same application.</span><span class="sxs-lookup"><span data-stu-id="f901b-115">This allows all links to be resolved as content published within the same application.</span></span>

    <span data-ttu-id="f901b-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span><span class="sxs-lookup"><span data-stu-id="f901b-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span></span> <span data-ttu-id="f901b-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span><span class="sxs-lookup"><span data-stu-id="f901b-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span></span> <span data-ttu-id="f901b-118">In this properties tab, you see the field “Home Page URL”, which you can adjust to be the desired landing page.</span><span class="sxs-lookup"><span data-stu-id="f901b-118">In this properties tab, you see the field “Home Page URL”, which you can adjust to be the desired landing page.</span></span>

2.  <span data-ttu-id="f901b-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](application-proxy-configure-custom-domain.md) to publish your applications.</span><span class="sxs-lookup"><span data-stu-id="f901b-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](application-proxy-configure-custom-domain.md) to publish your applications.</span></span> <span data-ttu-id="f901b-120">This feature allows the same URL to be used both internally and externally.</span><span class="sxs-lookup"><span data-stu-id="f901b-120">This feature allows the same URL to be used both internally and externally.</span></span>

    <span data-ttu-id="f901b-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span><span class="sxs-lookup"><span data-stu-id="f901b-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span></span> <span data-ttu-id="f901b-122">All links still need to belong to a published application.</span><span class="sxs-lookup"><span data-stu-id="f901b-122">All links still need to belong to a published application.</span></span> <span data-ttu-id="f901b-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span><span class="sxs-lookup"><span data-stu-id="f901b-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span></span>

3.  <span data-ttu-id="f901b-124">If neither of these options are feasible, there are multiple options for enabling inline link translation.</span><span class="sxs-lookup"><span data-stu-id="f901b-124">If neither of these options are feasible, there are multiple options for enabling inline link translation.</span></span> <span data-ttu-id="f901b-125">These options include using the Intune Managed Browser, My Apps extension, or using the link translation setting on your application.</span><span class="sxs-lookup"><span data-stu-id="f901b-125">These options include using the Intune Managed Browser, My Apps extension, or using the link translation setting on your application.</span></span> <span data-ttu-id="f901b-126">To learn more about each of these options and how to enable them, see [Redirect hardcoded links for apps published with Azure AD Application Proxy](application-proxy-configure-hard-coded-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="f901b-126">To learn more about each of these options and how to enable them, see [Redirect hardcoded links for apps published with Azure AD Application Proxy](application-proxy-configure-hard-coded-link-translation.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f901b-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="f901b-127">Next steps</span></span>
[<span data-ttu-id="f901b-128">Work with existing on-premises proxy servers</span><span class="sxs-lookup"><span data-stu-id="f901b-128">Work with existing on-premises proxy servers</span></span>](application-proxy-configure-connectors-with-proxy-servers.md)

