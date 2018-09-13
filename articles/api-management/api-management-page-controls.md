---
title: Azure API Management page controls | Microsoft Docs
description: Learn about the page controls available for use in developer portal templates in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 91c5e2af06ac1f9e240b7d6ee2e06281b234a6b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662281"
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="c3b85-103">Azure API Management page controls</span><span class="sxs-lookup"><span data-stu-id="c3b85-103">Azure API Management page controls</span></span>
<span data-ttu-id="c3b85-104">Azure API Management provides the following controls for use in the developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="c3b85-105">To use a control, place it in the desired location in the developer portal template.</span><span class="sxs-lookup"><span data-stu-id="c3b85-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="c3b85-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="c3b85-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="c3b85-107">The values for the parameters are passed in as part of the data model for the template.</span><span class="sxs-lookup"><span data-stu-id="c3b85-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="c3b85-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span><span class="sxs-lookup"><span data-stu-id="c3b85-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="c3b85-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span><span class="sxs-lookup"><span data-stu-id="c3b85-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="c3b85-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="c3b85-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="c3b85-111">Developer portal template page controls</span><span class="sxs-lookup"><span data-stu-id="c3b85-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="c3b85-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="c3b85-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="c3b85-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="c3b85-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="c3b85-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="c3b85-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="c3b85-115">providers</span><span class="sxs-lookup"><span data-stu-id="c3b85-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="c3b85-116">search-control</span><span class="sxs-lookup"><span data-stu-id="c3b85-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="c3b85-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="c3b85-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="c3b85-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="c3b85-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="c3b85-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="c3b85-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <a name="app-actions"></a> <span data-ttu-id="c3b85-120">app-actions</span><span class="sxs-lookup"><span data-stu-id="c3b85-120">app-actions</span></span>  
 <span data-ttu-id="c3b85-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c3b85-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="c3b85-122">![app&#45;actions control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-app-actions-control.png "APIM app-actions control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-122">![app&#45;actions control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-123">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-124">Parameters</span></span>  
  
|<span data-ttu-id="c3b85-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3b85-125">Parameter</span></span>|<span data-ttu-id="c3b85-126">Description</span><span class="sxs-lookup"><span data-stu-id="c3b85-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="c3b85-127">appId</span><span class="sxs-lookup"><span data-stu-id="c3b85-127">appId</span></span>|<span data-ttu-id="c3b85-128">The id of the application.</span><span class="sxs-lookup"><span data-stu-id="c3b85-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-129">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-129">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-130">The `app-actions` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-131">Applications</span><span class="sxs-lookup"><span data-stu-id="c3b85-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> <span data-ttu-id="c3b85-132">basic-signin</span><span class="sxs-lookup"><span data-stu-id="c3b85-132">basic-signin</span></span>  
 <span data-ttu-id="c3b85-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c3b85-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="c3b85-134">![basic&#45;signin control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-basic-signin-control.png "APIM basic-signin control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-134">![basic&#45;signin control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-135">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-136">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-136">Parameters</span></span>  
 <span data-ttu-id="c3b85-137">None.</span><span class="sxs-lookup"><span data-stu-id="c3b85-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-138">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-138">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-139">The `basic-signin` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-140">Sign in</span><span class="sxs-lookup"><span data-stu-id="c3b85-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> <span data-ttu-id="c3b85-141">paging-control</span><span class="sxs-lookup"><span data-stu-id="c3b85-141">paging-control</span></span>  
 <span data-ttu-id="c3b85-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span><span class="sxs-lookup"><span data-stu-id="c3b85-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="c3b85-143">![paging control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-paging-control.png "APIM paging control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-143">![paging control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-144">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-145">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-145">Parameters</span></span>  
 <span data-ttu-id="c3b85-146">None.</span><span class="sxs-lookup"><span data-stu-id="c3b85-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-147">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-147">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-148">The `paging-control` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-149">API list</span><span class="sxs-lookup"><span data-stu-id="c3b85-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="c3b85-150">Issue list</span><span class="sxs-lookup"><span data-stu-id="c3b85-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="c3b85-151">Product list</span><span class="sxs-lookup"><span data-stu-id="c3b85-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> <span data-ttu-id="c3b85-152">providers</span><span class="sxs-lookup"><span data-stu-id="c3b85-152">providers</span></span>  
 <span data-ttu-id="c3b85-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c3b85-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="c3b85-154">![providers control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-providers-control.png "APIM providers control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-154">![providers control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-155">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-156">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-156">Parameters</span></span>  
 <span data-ttu-id="c3b85-157">None.</span><span class="sxs-lookup"><span data-stu-id="c3b85-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-158">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-158">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-159">The `providers` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-160">Sign in</span><span class="sxs-lookup"><span data-stu-id="c3b85-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> <span data-ttu-id="c3b85-161">search-control</span><span class="sxs-lookup"><span data-stu-id="c3b85-161">search-control</span></span>  
 <span data-ttu-id="c3b85-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span><span class="sxs-lookup"><span data-stu-id="c3b85-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="c3b85-163">![search control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-search-control.png "APIM search control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-163">![search control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-164">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-165">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-165">Parameters</span></span>  
 <span data-ttu-id="c3b85-166">None.</span><span class="sxs-lookup"><span data-stu-id="c3b85-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-167">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-167">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-168">The `search-control` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-169">API list</span><span class="sxs-lookup"><span data-stu-id="c3b85-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="c3b85-170">Product list</span><span class="sxs-lookup"><span data-stu-id="c3b85-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> <span data-ttu-id="c3b85-171">sign-up</span><span class="sxs-lookup"><span data-stu-id="c3b85-171">sign-up</span></span>  
 <span data-ttu-id="c3b85-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c3b85-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="c3b85-173">![sign&#45;up control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-sign-up-control.png "APIM sign-up control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-173">![sign&#45;up control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-174">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-175">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-175">Parameters</span></span>  
 <span data-ttu-id="c3b85-176">None.</span><span class="sxs-lookup"><span data-stu-id="c3b85-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-177">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-177">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-178">The `sign-up` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-179">Sign up</span><span class="sxs-lookup"><span data-stu-id="c3b85-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> <span data-ttu-id="c3b85-180">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="c3b85-180">subscribe-button</span></span>  
 <span data-ttu-id="c3b85-181">The `subscribe-button` provides a control for subscribing a user to a product.</span><span class="sxs-lookup"><span data-stu-id="c3b85-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="c3b85-182">![subscribe&#45;button control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-subscribe-button-control.png "APIM subscribe-button control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-182">![subscribe&#45;button control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-183">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-184">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-184">Parameters</span></span>  
 <span data-ttu-id="c3b85-185">None.</span><span class="sxs-lookup"><span data-stu-id="c3b85-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-186">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-186">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-187">The `subscribe-button` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-188">Product</span><span class="sxs-lookup"><span data-stu-id="c3b85-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> <span data-ttu-id="c3b85-189">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="c3b85-189">subscription-cancel</span></span>  
 <span data-ttu-id="c3b85-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c3b85-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="c3b85-191">![subscription&#45;cancel control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-subscription-cancel-control.png "APIM subscription-cancel control")</span><span class="sxs-lookup"><span data-stu-id="c3b85-191">![subscription&#45;cancel control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-controls/apim-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="c3b85-192">Usage</span><span class="sxs-lookup"><span data-stu-id="c3b85-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="c3b85-193">Parameters</span><span class="sxs-lookup"><span data-stu-id="c3b85-193">Parameters</span></span>  
  
|<span data-ttu-id="c3b85-194">Parameter</span><span class="sxs-lookup"><span data-stu-id="c3b85-194">Parameter</span></span>|<span data-ttu-id="c3b85-195">Description</span><span class="sxs-lookup"><span data-stu-id="c3b85-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="c3b85-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c3b85-196">subscriptionId</span></span>|<span data-ttu-id="c3b85-197">The id of the subscription to cancel.</span><span class="sxs-lookup"><span data-stu-id="c3b85-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="c3b85-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="c3b85-198">cancelUrl</span></span>|<span data-ttu-id="c3b85-199">The subscription cancel URL.</span><span class="sxs-lookup"><span data-stu-id="c3b85-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="c3b85-200">Developer portal templates</span><span class="sxs-lookup"><span data-stu-id="c3b85-200">Developer portal templates</span></span>  
 <span data-ttu-id="c3b85-201">The `subscription-cancel` control may be used in the following developer portal templates.</span><span class="sxs-lookup"><span data-stu-id="c3b85-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="c3b85-202">Product</span><span class="sxs-lookup"><span data-stu-id="c3b85-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="c3b85-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3b85-203">Next steps</span></span>
<span data-ttu-id="c3b85-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c3b85-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>







