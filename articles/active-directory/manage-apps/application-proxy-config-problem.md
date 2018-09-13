---
title: Problem creating an Application Proxy application | Microsoft Docs
description: How to troubleshoot issues creating Application Proxy applications in the Azure AD Admin portal
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
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 2344d35827cf541f0230f74917be3ae0ea39e074
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868754"
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="cfa35-103">Problem creating an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="cfa35-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="cfa35-104">Below are some of the common issues people face when creating a new application proxy application.</span><span class="sxs-lookup"><span data-stu-id="cfa35-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="cfa35-105">Recommended documents</span><span class="sxs-lookup"><span data-stu-id="cfa35-105">Recommended documents</span></span> 

<span data-ttu-id="cfa35-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cfa35-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

<span data-ttu-id="cfa35-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span><span class="sxs-lookup"><span data-stu-id="cfa35-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="cfa35-108">Most error messages include a suggested fix.</span><span class="sxs-lookup"><span data-stu-id="cfa35-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="cfa35-109">Specific things to check</span><span class="sxs-lookup"><span data-stu-id="cfa35-109">Specific things to check</span></span>

<span data-ttu-id="cfa35-110">To avoid common errors, verify:</span><span class="sxs-lookup"><span data-stu-id="cfa35-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="cfa35-111">You are an administrator with permission to create an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="cfa35-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="cfa35-112">The internal URL is unique</span><span class="sxs-lookup"><span data-stu-id="cfa35-112">The internal URL is unique</span></span>

-   <span data-ttu-id="cfa35-113">The external URL is unique</span><span class="sxs-lookup"><span data-stu-id="cfa35-113">The external URL is unique</span></span>

-   <span data-ttu-id="cfa35-114">The URLs start with http or https, and end with a “/”</span><span class="sxs-lookup"><span data-stu-id="cfa35-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="cfa35-115">The URL should be a domain name and not an IP address</span><span class="sxs-lookup"><span data-stu-id="cfa35-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="cfa35-116">The error message should display in the top right corner when you create the application.</span><span class="sxs-lookup"><span data-stu-id="cfa35-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="cfa35-117">You can also select the notification icon to see the error messages.</span><span class="sxs-lookup"><span data-stu-id="cfa35-117">You can also select the notification icon to see the error messages.</span></span>

   ![Notification prompt](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="cfa35-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="cfa35-119">Next steps</span></span>
[<span data-ttu-id="cfa35-120">Enable Application Proxy in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cfa35-120">Enable Application Proxy in the Azure portal</span></span>](application-proxy-enable.md)
