---
title: Problem creating an Application Proxy application | Microsoft Docs
description: How to troubleshoot issues creating Application Proxy applications in the Azure AD Admin portal
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
ms.openlocfilehash: 5e120f2e18e9b3a92328c6fd5073d66346f2d2b2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662691"
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="c87dc-103">Problem creating an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="c87dc-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="c87dc-104">Below are some of the common issues people face when creating a new application proxy application.</span><span class="sxs-lookup"><span data-stu-id="c87dc-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="c87dc-105">Recommended documents</span><span class="sxs-lookup"><span data-stu-id="c87dc-105">Recommended documents</span></span> 

<span data-ttu-id="c87dc-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c87dc-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="c87dc-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span><span class="sxs-lookup"><span data-stu-id="c87dc-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="c87dc-108">Most error messages include a suggested fix.</span><span class="sxs-lookup"><span data-stu-id="c87dc-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="c87dc-109">Specific things to check</span><span class="sxs-lookup"><span data-stu-id="c87dc-109">Specific things to check</span></span>

<span data-ttu-id="c87dc-110">To avoid common errors, verify:</span><span class="sxs-lookup"><span data-stu-id="c87dc-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="c87dc-111">You are an administrator with permission to create an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="c87dc-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="c87dc-112">The internal URL is unique</span><span class="sxs-lookup"><span data-stu-id="c87dc-112">The internal URL is unique</span></span>

-   <span data-ttu-id="c87dc-113">The external URL is unique</span><span class="sxs-lookup"><span data-stu-id="c87dc-113">The external URL is unique</span></span>

-   <span data-ttu-id="c87dc-114">The URLs start with http or https, and end with a “/”</span><span class="sxs-lookup"><span data-stu-id="c87dc-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="c87dc-115">The URL should be a domain name and not an IP address</span><span class="sxs-lookup"><span data-stu-id="c87dc-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="c87dc-116">The error message should display in the top right corner when you create the application.</span><span class="sxs-lookup"><span data-stu-id="c87dc-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="c87dc-117">You can also select the notification icon to see the error messages.</span><span class="sxs-lookup"><span data-stu-id="c87dc-117">You can also select the notification icon to see the error messages.</span></span>

   ![Notification prompt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="c87dc-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="c87dc-119">Next steps</span></span>
[<span data-ttu-id="c87dc-120">Enable Application Proxy in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c87dc-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)

