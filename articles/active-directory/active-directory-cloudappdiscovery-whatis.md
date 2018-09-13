---
title: Finding unmanaged cloud applications with Cloud App Discovery | Microsoft Docs
description: Provides information about finding and managing applications with Cloud App Discovery, what are the benefits and how it works.
services: active-directory
keywords: cloud app discovery, managing applications
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 07c8c1d045bc3635515e5dc423126019a39dfaa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564460"
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="33017-104">Finding unmanaged cloud applications with Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="33017-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="33017-105">Overview</span><span class="sxs-lookup"><span data-stu-id="33017-105">Overview</span></span>
<span data-ttu-id="33017-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span><span class="sxs-lookup"><span data-stu-id="33017-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="33017-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span><span class="sxs-lookup"><span data-stu-id="33017-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="33017-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span><span class="sxs-lookup"><span data-stu-id="33017-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="33017-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span><span class="sxs-lookup"><span data-stu-id="33017-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="33017-110">**With Cloud App Discovery, you can:**</span><span class="sxs-lookup"><span data-stu-id="33017-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="33017-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span><span class="sxs-lookup"><span data-stu-id="33017-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="33017-112">Identify the users that are using an application.</span><span class="sxs-lookup"><span data-stu-id="33017-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="33017-113">Export data for offline analysis.</span><span class="sxs-lookup"><span data-stu-id="33017-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="33017-114">Bring these applications under IT control and enable single sign on for user management.</span><span class="sxs-lookup"><span data-stu-id="33017-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="33017-115">How it works</span><span class="sxs-lookup"><span data-stu-id="33017-115">How it works</span></span>
1. <span data-ttu-id="33017-116">Application usage agents are installed on user's computers.</span><span class="sxs-lookup"><span data-stu-id="33017-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="33017-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span><span class="sxs-lookup"><span data-stu-id="33017-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="33017-118">The Cloud App Discovery service evaluates the data and generates reports.</span><span class="sxs-lookup"><span data-stu-id="33017-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Cloud App Discovery diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="33017-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="33017-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="33017-121">Related articles</span><span class="sxs-lookup"><span data-stu-id="33017-121">Related articles</span></span>
* [<span data-ttu-id="33017-122">Cloud App Discovery Security and Privacy Considerations</span><span class="sxs-lookup"><span data-stu-id="33017-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="33017-123">Cloud App Discovery Group Policy Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="33017-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="33017-124">Cloud App Discovery System Center Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="33017-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="33017-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span><span class="sxs-lookup"><span data-stu-id="33017-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="33017-126">Cloud App Discovery Agent Changelog </span><span class="sxs-lookup"><span data-stu-id="33017-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="33017-127">Cloud App Discovery Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="33017-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="33017-128">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33017-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)


