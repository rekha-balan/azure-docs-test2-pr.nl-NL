---
title: Azure Active Directory Application Proxy and Tableau | Microsoft Docs
description: Learn how to use Azure Active Directory (Azure AD) Application Proxy to provide remote access for your Tableau deployment.
services: active-directory
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 08/20/2018
ms.author: barbkess
ms.reviewer: japere
ms.custom: it-pro
ms.openlocfilehash: a68b0465acdb416cd953e22d7f024eb399c94493
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871704"
---
# <a name="azure-active-directory-application-proxy-and-tableau"></a><span data-ttu-id="56c98-103">Azure Active Directory Application Proxy and Tableau</span><span class="sxs-lookup"><span data-stu-id="56c98-103">Azure Active Directory Application Proxy and Tableau</span></span> 

<span data-ttu-id="56c98-104">Azure Active Directory Application Proxy and Tableau have partnered to ensure you are easily able to use Application Proxy to provide remote access for your Tableau deployment.</span><span class="sxs-lookup"><span data-stu-id="56c98-104">Azure Active Directory Application Proxy and Tableau have partnered to ensure you are easily able to use Application Proxy to provide remote access for your Tableau deployment.</span></span> <span data-ttu-id="56c98-105">This article explains how to configure this scenario.</span><span class="sxs-lookup"><span data-stu-id="56c98-105">This article explains how to configure this scenario.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="56c98-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="56c98-106">Prerequisites</span></span> 

<span data-ttu-id="56c98-107">The scenario in this article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="56c98-107">The scenario in this article assumes that you have:</span></span>

- <span data-ttu-id="56c98-108">[Tableau](https://onlinehelp.tableau.com/current/server/en-us/proxy.htm#azure) configured.</span><span class="sxs-lookup"><span data-stu-id="56c98-108">[Tableau](https://onlinehelp.tableau.com/current/server/en-us/proxy.htm#azure) configured.</span></span> 

- <span data-ttu-id="56c98-109">An [Application Proxy connector](application-proxy-enable.md) installed.</span><span class="sxs-lookup"><span data-stu-id="56c98-109">An [Application Proxy connector](application-proxy-enable.md) installed.</span></span> 

 
## <a name="enabling-application-proxy-for-tableau"></a><span data-ttu-id="56c98-110">Enabling Application Proxy for Tableau</span><span class="sxs-lookup"><span data-stu-id="56c98-110">Enabling Application Proxy for Tableau</span></span> 

<span data-ttu-id="56c98-111">Application Proxy supports the OAuth 2.0 Grant Flow, which is required for Tableau to work properly.</span><span class="sxs-lookup"><span data-stu-id="56c98-111">Application Proxy supports the OAuth 2.0 Grant Flow, which is required for Tableau to work properly.</span></span> <span data-ttu-id="56c98-112">This means that there are no longer any special steps required to enable this application, other than configuring it by following the publishing steps below.</span><span class="sxs-lookup"><span data-stu-id="56c98-112">This means that there are no longer any special steps required to enable this application, other than configuring it by following the publishing steps below.</span></span>


## <a name="publish-your-applications-in-azure"></a><span data-ttu-id="56c98-113">Publish your applications in Azure</span><span class="sxs-lookup"><span data-stu-id="56c98-113">Publish your applications in Azure</span></span> 

<span data-ttu-id="56c98-114">To publish Tableau, you need to publish an application in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="56c98-114">To publish Tableau, you need to publish an application in the Azure Portal.</span></span>

<span data-ttu-id="56c98-115">For:</span><span class="sxs-lookup"><span data-stu-id="56c98-115">For:</span></span>

- <span data-ttu-id="56c98-116">Detailed instructions of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="56c98-116">Detailed instructions of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span> 
- <span data-ttu-id="56c98-117">Information about how to find Tableau values for the App Proxy fields, please see the Tableau documentation.</span><span class="sxs-lookup"><span data-stu-id="56c98-117">Information about how to find Tableau values for the App Proxy fields, please see the Tableau documentation.</span></span>  

<span data-ttu-id="56c98-118">**To publish your app**:</span><span class="sxs-lookup"><span data-stu-id="56c98-118">**To publish your app**:</span></span> 


1. <span data-ttu-id="56c98-119">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span><span class="sxs-lookup"><span data-stu-id="56c98-119">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span> 

2. <span data-ttu-id="56c98-120">Select **Azure Active Directory > Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="56c98-120">Select **Azure Active Directory > Enterprise applications**.</span></span> 

3. <span data-ttu-id="56c98-121">Select **Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="56c98-121">Select **Add** at the top of the blade.</span></span> 

4. <span data-ttu-id="56c98-122">Select **On-premises application**.</span><span class="sxs-lookup"><span data-stu-id="56c98-122">Select **On-premises application**.</span></span> 

5. <span data-ttu-id="56c98-123">Fill out the required fields with information about your new app.</span><span class="sxs-lookup"><span data-stu-id="56c98-123">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="56c98-124">Use the following guidance for the settings:</span><span class="sxs-lookup"><span data-stu-id="56c98-124">Use the following guidance for the settings:</span></span> 

    - <span data-ttu-id="56c98-125">**Internal URL**: This application should have an internal URL that is the Tableau URL itself.</span><span class="sxs-lookup"><span data-stu-id="56c98-125">**Internal URL**: This application should have an internal URL that is the Tableau URL itself.</span></span> <span data-ttu-id="56c98-126">For example, `https://adventure-works.tableau.com`.</span><span class="sxs-lookup"><span data-stu-id="56c98-126">For example, `https://adventure-works.tableau.com`.</span></span> 

    - <span data-ttu-id="56c98-127">**Pre-authentication method**: Azure Active Directory (recommended but not required).</span><span class="sxs-lookup"><span data-stu-id="56c98-127">**Pre-authentication method**: Azure Active Directory (recommended but not required).</span></span> 

6. <span data-ttu-id="56c98-128">Select **Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="56c98-128">Select **Add** at the top of the blade.</span></span> <span data-ttu-id="56c98-129">Your application is added, and the quick start menu opens.</span><span class="sxs-lookup"><span data-stu-id="56c98-129">Your application is added, and the quick start menu opens.</span></span> 

7. <span data-ttu-id="56c98-130">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span><span class="sxs-lookup"><span data-stu-id="56c98-130">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="56c98-131">Make sure this test account has access to the on-premises application.</span><span class="sxs-lookup"><span data-stu-id="56c98-131">Make sure this test account has access to the on-premises application.</span></span> 

8. <span data-ttu-id="56c98-132">Select **Assign** to save the test user assignment.</span><span class="sxs-lookup"><span data-stu-id="56c98-132">Select **Assign** to save the test user assignment.</span></span> 

9. <span data-ttu-id="56c98-133">(Optional) On the app management page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="56c98-133">(Optional) On the app management page, select **Single sign-on**.</span></span> <span data-ttu-id="56c98-134">Choose **Integrated Windows Authentication** from the drop-down menu, and fill out the required fields based on your Tableau configuration.</span><span class="sxs-lookup"><span data-stu-id="56c98-134">Choose **Integrated Windows Authentication** from the drop-down menu, and fill out the required fields based on your Tableau configuration.</span></span> <span data-ttu-id="56c98-135">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="56c98-135">Select **Save**.</span></span> 

 

## <a name="testing"></a><span data-ttu-id="56c98-136">Testing</span><span class="sxs-lookup"><span data-stu-id="56c98-136">Testing</span></span> 

<span data-ttu-id="56c98-137">Your application is now ready to test.</span><span class="sxs-lookup"><span data-stu-id="56c98-137">Your application is now ready to test.</span></span> <span data-ttu-id="56c98-138">Access the external URL you used to publish Tableau, and login as a user assigned to both applications.</span><span class="sxs-lookup"><span data-stu-id="56c98-138">Access the external URL you used to publish Tableau, and login as a user assigned to both applications.</span></span>



## <a name="next-steps"></a><span data-ttu-id="56c98-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="56c98-139">Next steps</span></span>

<span data-ttu-id="56c98-140">For more information about Azure AD Application Proxy, see [How to provide secure remote access to on-premises applications](application-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="56c98-140">For more information about Azure AD Application Proxy, see [How to provide secure remote access to on-premises applications](application-proxy.md).</span></span>

