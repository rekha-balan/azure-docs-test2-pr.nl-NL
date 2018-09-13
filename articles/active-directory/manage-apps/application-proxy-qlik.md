---
title: Azure AD App Proxy and Qlik Sense| Microsoft Docs
description: Turn on Application Proxy in the Azure  portal, and install the Connectors for the reverse proxy.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.topic: article
ms.date: 09/06/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5f103e9fe410374a551eb43d456d5993bdd36627
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855566"
---
# <a name="application-proxy-and-qlik-sense"></a><span data-ttu-id="80b02-103">Application Proxy and Qlik Sense</span><span class="sxs-lookup"><span data-stu-id="80b02-103">Application Proxy and Qlik Sense</span></span> 
<span data-ttu-id="80b02-104">Azure Active Directory Application Proxy and Qlik Sense have partnered together to ensure you are easily able to use Application Proxy to provide remote access for your Qlik Sense deployment.</span><span class="sxs-lookup"><span data-stu-id="80b02-104">Azure Active Directory Application Proxy and Qlik Sense have partnered together to ensure you are easily able to use Application Proxy to provide remote access for your Qlik Sense deployment.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="80b02-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="80b02-105">Prerequisites</span></span> 
<span data-ttu-id="80b02-106">The remainder of this scenario assumes you done the following:</span><span class="sxs-lookup"><span data-stu-id="80b02-106">The remainder of this scenario assumes you done the following:</span></span>
 
- <span data-ttu-id="80b02-107">Configured [Qlik Sense](https://community.qlik.com/docs/DOC-19822).</span><span class="sxs-lookup"><span data-stu-id="80b02-107">Configured [Qlik Sense](https://community.qlik.com/docs/DOC-19822).</span></span> 
- [<span data-ttu-id="80b02-108">Installed an Application Proxy connector</span><span class="sxs-lookup"><span data-stu-id="80b02-108">Installed an Application Proxy connector</span></span>](application-proxy-enable.md#install-and-register-a-connector) 
 
## <a name="publish-your-applications-in-azure"></a><span data-ttu-id="80b02-109">Publish your applications in Azure</span><span class="sxs-lookup"><span data-stu-id="80b02-109">Publish your applications in Azure</span></span> 
<span data-ttu-id="80b02-110">To publish QlikSense, you will need to publish two applications in Azure.</span><span class="sxs-lookup"><span data-stu-id="80b02-110">To publish QlikSense, you will need to publish two applications in Azure.</span></span>  

### <a name="application-1"></a><span data-ttu-id="80b02-111">Application #1:</span><span class="sxs-lookup"><span data-stu-id="80b02-111">Application #1:</span></span> 
<span data-ttu-id="80b02-112">Follow these steps to publish your app.</span><span class="sxs-lookup"><span data-stu-id="80b02-112">Follow these steps to publish your app.</span></span> <span data-ttu-id="80b02-113">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80b02-113">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span> 


1. <span data-ttu-id="80b02-114">Sign in to the Azure portal as a global administrator.</span><span class="sxs-lookup"><span data-stu-id="80b02-114">Sign in to the Azure portal as a global administrator.</span></span> 
2. <span data-ttu-id="80b02-115">Select **Azure Active Directory** > **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="80b02-115">Select **Azure Active Directory** > **Enterprise applications**.</span></span> 
3. <span data-ttu-id="80b02-116">Select **Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="80b02-116">Select **Add** at the top of the blade.</span></span> 
4. <span data-ttu-id="80b02-117">Select **On-premises application**.</span><span class="sxs-lookup"><span data-stu-id="80b02-117">Select **On-premises application**.</span></span> 
5.       <span data-ttu-id="80b02-118">Fill out the required fields with information about your new app.</span><span class="sxs-lookup"><span data-stu-id="80b02-118">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="80b02-119">Use the following guidance for the settings:</span><span class="sxs-lookup"><span data-stu-id="80b02-119">Use the following guidance for the settings:</span></span> 
    - <span data-ttu-id="80b02-120">**Internal URL**: This application should have an internal URL that is the QlikSense URL itself.</span><span class="sxs-lookup"><span data-stu-id="80b02-120">**Internal URL**: This application should have an internal URL that is the QlikSense URL itself.</span></span> <span data-ttu-id="80b02-121">For example, **https&#58;//demo.qlikemm.com:4244**</span><span class="sxs-lookup"><span data-stu-id="80b02-121">For example, **https&#58;//demo.qlikemm.com:4244**</span></span> 
    - <span data-ttu-id="80b02-122">**Pre-authentication method**: Azure Active Directory (Recommended but not required)</span><span class="sxs-lookup"><span data-stu-id="80b02-122">**Pre-authentication method**: Azure Active Directory (Recommended but not required)</span></span> 
1.       <span data-ttu-id="80b02-123">Select **Add** at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="80b02-123">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="80b02-124">Your application is added, and the quick start menu opens.</span><span class="sxs-lookup"><span data-stu-id="80b02-124">Your application is added, and the quick start menu opens.</span></span> 
2.       <span data-ttu-id="80b02-125">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span><span class="sxs-lookup"><span data-stu-id="80b02-125">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="80b02-126">Make sure this test account has access to the on-premises application.</span><span class="sxs-lookup"><span data-stu-id="80b02-126">Make sure this test account has access to the on-premises application.</span></span> 
3.       <span data-ttu-id="80b02-127">Select **Assign** to save the test user assignment.</span><span class="sxs-lookup"><span data-stu-id="80b02-127">Select **Assign** to save the test user assignment.</span></span> 
4.       <span data-ttu-id="80b02-128">(Optional) On the app management blade, select Single sign-on.</span><span class="sxs-lookup"><span data-stu-id="80b02-128">(Optional) On the app management blade, select Single sign-on.</span></span> <span data-ttu-id="80b02-129">Choose **Kerberos Constrained Delegation** from the drop-down menu, and fill out the required fields based on your Qlik configuration.</span><span class="sxs-lookup"><span data-stu-id="80b02-129">Choose **Kerberos Constrained Delegation** from the drop-down menu, and fill out the required fields based on your Qlik configuration.</span></span> <span data-ttu-id="80b02-130">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="80b02-130">Select **Save**.</span></span> 

### <a name="application-2"></a><span data-ttu-id="80b02-131">Application #2:</span><span class="sxs-lookup"><span data-stu-id="80b02-131">Application #2:</span></span> 
<span data-ttu-id="80b02-132">Follow the same steps as for Application #1, with the following exceptions:</span><span class="sxs-lookup"><span data-stu-id="80b02-132">Follow the same steps as for Application #1, with the following exceptions:</span></span> 

<span data-ttu-id="80b02-133">**Step #5**: The Internal URL should now be the QlikSense URL with the authentication port used by the application.</span><span class="sxs-lookup"><span data-stu-id="80b02-133">**Step #5**: The Internal URL should now be the QlikSense URL with the authentication port used by the application.</span></span> <span data-ttu-id="80b02-134">The default is **4244** for HTTPS, and 4248 for HTTP.</span><span class="sxs-lookup"><span data-stu-id="80b02-134">The default is **4244** for HTTPS, and 4248 for HTTP.</span></span> <span data-ttu-id="80b02-135">Ex: **https&#58;//demo.qlik.com:4244**</span><span class="sxs-lookup"><span data-stu-id="80b02-135">Ex: **https&#58;//demo.qlik.com:4244**</span></span></br></br><span data-ttu-id="80b02-136"> 
\*\*Step #10:\*\* Don’t set up SSO, and leave the \*\*Single sign-on disabled**</span><span class="sxs-lookup"><span data-stu-id="80b02-136"> 
\*\*Step #10:\*\* Don’t set up SSO, and leave the \*\*Single sign-on disabled**</span></span>
 
 
## <a name="testing"></a><span data-ttu-id="80b02-137">Testing</span><span class="sxs-lookup"><span data-stu-id="80b02-137">Testing</span></span> 
<span data-ttu-id="80b02-138">Your application is now ready to test.</span><span class="sxs-lookup"><span data-stu-id="80b02-138">Your application is now ready to test.</span></span> <span data-ttu-id="80b02-139">Access the external URL you used to publish QlikSense in Application #1, and login as a user assigned to both applications.</span><span class="sxs-lookup"><span data-stu-id="80b02-139">Access the external URL you used to publish QlikSense in Application #1, and login as a user assigned to both applications.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="80b02-140">Next Steps</span><span class="sxs-lookup"><span data-stu-id="80b02-140">Next Steps</span></span>

- [<span data-ttu-id="80b02-141">Publish applications with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="80b02-141">Publish applications with Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
- <span data-ttu-id="80b02-142">[Working with Application Proxy connectors](application-proxy-connector-groups.md).</span><span class="sxs-lookup"><span data-stu-id="80b02-142">[Working with Application Proxy connectors](application-proxy-connector-groups.md).</span></span>
