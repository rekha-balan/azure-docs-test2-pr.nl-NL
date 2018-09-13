---
title: Azure API Management authentication policies | Microsoft Docs
description: Learn about the authentication policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: apimpm
ms.openlocfilehash: 4d13d9dbea9da9db5bfe9a9af85fdbf9eab1ae84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804926"
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="cc01e-103">API Management authentication policies</span><span class="sxs-lookup"><span data-stu-id="cc01e-103">API Management authentication policies</span></span>
<span data-ttu-id="cc01e-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="cc01e-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="cc01e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="cc01e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  

##  <a name="AuthenticationPolicies"></a> <span data-ttu-id="cc01e-106">Authentication policies</span><span class="sxs-lookup"><span data-stu-id="cc01e-106">Authentication policies</span></span>  
  
-   <span data-ttu-id="cc01e-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="cc01e-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="cc01e-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span><span class="sxs-lookup"><span data-stu-id="cc01e-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <a name="Basic"></a> <span data-ttu-id="cc01e-109">Authenticate with Basic</span><span class="sxs-lookup"><span data-stu-id="cc01e-109">Authenticate with Basic</span></span>  
 <span data-ttu-id="cc01e-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="cc01e-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="cc01e-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span><span class="sxs-lookup"><span data-stu-id="cc01e-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cc01e-112">Policy statement</span><span class="sxs-lookup"><span data-stu-id="cc01e-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="cc01e-113">Example</span><span class="sxs-lookup"><span data-stu-id="cc01e-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="cc01e-114">Elements</span><span class="sxs-lookup"><span data-stu-id="cc01e-114">Elements</span></span>  
  
|<span data-ttu-id="cc01e-115">Name</span><span class="sxs-lookup"><span data-stu-id="cc01e-115">Name</span></span>|<span data-ttu-id="cc01e-116">Description</span><span class="sxs-lookup"><span data-stu-id="cc01e-116">Description</span></span>|<span data-ttu-id="cc01e-117">Required</span><span class="sxs-lookup"><span data-stu-id="cc01e-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="cc01e-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="cc01e-118">authentication-basic</span></span>|<span data-ttu-id="cc01e-119">Root element.</span><span class="sxs-lookup"><span data-stu-id="cc01e-119">Root element.</span></span>|<span data-ttu-id="cc01e-120">Yes</span><span class="sxs-lookup"><span data-stu-id="cc01e-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cc01e-121">Attributes</span><span class="sxs-lookup"><span data-stu-id="cc01e-121">Attributes</span></span>  
  
|<span data-ttu-id="cc01e-122">Name</span><span class="sxs-lookup"><span data-stu-id="cc01e-122">Name</span></span>|<span data-ttu-id="cc01e-123">Description</span><span class="sxs-lookup"><span data-stu-id="cc01e-123">Description</span></span>|<span data-ttu-id="cc01e-124">Required</span><span class="sxs-lookup"><span data-stu-id="cc01e-124">Required</span></span>|<span data-ttu-id="cc01e-125">Default</span><span class="sxs-lookup"><span data-stu-id="cc01e-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="cc01e-126">username</span><span class="sxs-lookup"><span data-stu-id="cc01e-126">username</span></span>|<span data-ttu-id="cc01e-127">Specifies the username of the Basic credential.</span><span class="sxs-lookup"><span data-stu-id="cc01e-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="cc01e-128">Yes</span><span class="sxs-lookup"><span data-stu-id="cc01e-128">Yes</span></span>|<span data-ttu-id="cc01e-129">N/A</span><span class="sxs-lookup"><span data-stu-id="cc01e-129">N/A</span></span>|  
|<span data-ttu-id="cc01e-130">password</span><span class="sxs-lookup"><span data-stu-id="cc01e-130">password</span></span>|<span data-ttu-id="cc01e-131">Specifies the password of the Basic credential.</span><span class="sxs-lookup"><span data-stu-id="cc01e-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="cc01e-132">Yes</span><span class="sxs-lookup"><span data-stu-id="cc01e-132">Yes</span></span>|<span data-ttu-id="cc01e-133">N/A</span><span class="sxs-lookup"><span data-stu-id="cc01e-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cc01e-134">Usage</span><span class="sxs-lookup"><span data-stu-id="cc01e-134">Usage</span></span>  
 <span data-ttu-id="cc01e-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="cc01e-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cc01e-136">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="cc01e-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="cc01e-137">**Policy scopes:** API</span><span class="sxs-lookup"><span data-stu-id="cc01e-137">**Policy scopes:** API</span></span>  
  
##  <a name="ClientCertificate"></a> <span data-ttu-id="cc01e-138">Authenticate with client certificate</span><span class="sxs-lookup"><span data-stu-id="cc01e-138">Authenticate with client certificate</span></span>  
 <span data-ttu-id="cc01e-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span><span class="sxs-lookup"><span data-stu-id="cc01e-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="cc01e-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span><span class="sxs-lookup"><span data-stu-id="cc01e-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cc01e-141">Policy statement</span><span class="sxs-lookup"><span data-stu-id="cc01e-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="cc01e-142">Example</span><span class="sxs-lookup"><span data-stu-id="cc01e-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="cc01e-143">Elements</span><span class="sxs-lookup"><span data-stu-id="cc01e-143">Elements</span></span>  
  
|<span data-ttu-id="cc01e-144">Name</span><span class="sxs-lookup"><span data-stu-id="cc01e-144">Name</span></span>|<span data-ttu-id="cc01e-145">Description</span><span class="sxs-lookup"><span data-stu-id="cc01e-145">Description</span></span>|<span data-ttu-id="cc01e-146">Required</span><span class="sxs-lookup"><span data-stu-id="cc01e-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="cc01e-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="cc01e-147">authentication-certificate</span></span>|<span data-ttu-id="cc01e-148">Root element.</span><span class="sxs-lookup"><span data-stu-id="cc01e-148">Root element.</span></span>|<span data-ttu-id="cc01e-149">Yes</span><span class="sxs-lookup"><span data-stu-id="cc01e-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cc01e-150">Attributes</span><span class="sxs-lookup"><span data-stu-id="cc01e-150">Attributes</span></span>  
  
|<span data-ttu-id="cc01e-151">Name</span><span class="sxs-lookup"><span data-stu-id="cc01e-151">Name</span></span>|<span data-ttu-id="cc01e-152">Description</span><span class="sxs-lookup"><span data-stu-id="cc01e-152">Description</span></span>|<span data-ttu-id="cc01e-153">Required</span><span class="sxs-lookup"><span data-stu-id="cc01e-153">Required</span></span>|<span data-ttu-id="cc01e-154">Default</span><span class="sxs-lookup"><span data-stu-id="cc01e-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="cc01e-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="cc01e-155">thumbprint</span></span>|<span data-ttu-id="cc01e-156">The thumbprint for the client certificate.</span><span class="sxs-lookup"><span data-stu-id="cc01e-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="cc01e-157">Yes</span><span class="sxs-lookup"><span data-stu-id="cc01e-157">Yes</span></span>|<span data-ttu-id="cc01e-158">N/A</span><span class="sxs-lookup"><span data-stu-id="cc01e-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cc01e-159">Usage</span><span class="sxs-lookup"><span data-stu-id="cc01e-159">Usage</span></span>  
 <span data-ttu-id="cc01e-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="cc01e-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cc01e-161">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="cc01e-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="cc01e-162">**Policy scopes:** API</span><span class="sxs-lookup"><span data-stu-id="cc01e-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="cc01e-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc01e-163">Next steps</span></span>
<span data-ttu-id="cc01e-164">For more information working with policies, see:</span><span class="sxs-lookup"><span data-stu-id="cc01e-164">For more information working with policies, see:</span></span>

+ [<span data-ttu-id="cc01e-165">Policies in API Management</span><span class="sxs-lookup"><span data-stu-id="cc01e-165">Policies in API Management</span></span>](api-management-howto-policies.md)
+ [<span data-ttu-id="cc01e-166">Transform APIs</span><span class="sxs-lookup"><span data-stu-id="cc01e-166">Transform APIs</span></span>](transform-api.md)
+ <span data-ttu-id="cc01e-167">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span><span class="sxs-lookup"><span data-stu-id="cc01e-167">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span></span>
+ [<span data-ttu-id="cc01e-168">Policy samples</span><span class="sxs-lookup"><span data-stu-id="cc01e-168">Policy samples</span></span>](policy-samples.md)   
