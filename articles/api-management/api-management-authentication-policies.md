---
title: Azure API Management authentication policies | Microsoft Docs
description: Learn about the authentication policies available for use in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564447"
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="f2042-103">API Management authentication policies</span><span class="sxs-lookup"><span data-stu-id="f2042-103">API Management authentication policies</span></span>
<span data-ttu-id="f2042-104">This topic provides a reference for the following API Management policies.</span><span class="sxs-lookup"><span data-stu-id="f2042-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="f2042-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="f2042-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <a name="AuthenticationPolicies"></a> <span data-ttu-id="f2042-106">Authentication policies</span><span class="sxs-lookup"><span data-stu-id="f2042-106">Authentication policies</span></span>  
  
-   <span data-ttu-id="f2042-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="f2042-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="f2042-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span><span class="sxs-lookup"><span data-stu-id="f2042-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <a name="Basic"></a> <span data-ttu-id="f2042-109">Authenticate with Basic</span><span class="sxs-lookup"><span data-stu-id="f2042-109">Authenticate with Basic</span></span>  
 <span data-ttu-id="f2042-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="f2042-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="f2042-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span><span class="sxs-lookup"><span data-stu-id="f2042-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f2042-112">Policy statement</span><span class="sxs-lookup"><span data-stu-id="f2042-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="f2042-113">Example</span><span class="sxs-lookup"><span data-stu-id="f2042-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="f2042-114">Elements</span><span class="sxs-lookup"><span data-stu-id="f2042-114">Elements</span></span>  
  
|<span data-ttu-id="f2042-115">Name</span><span class="sxs-lookup"><span data-stu-id="f2042-115">Name</span></span>|<span data-ttu-id="f2042-116">Description</span><span class="sxs-lookup"><span data-stu-id="f2042-116">Description</span></span>|<span data-ttu-id="f2042-117">Required</span><span class="sxs-lookup"><span data-stu-id="f2042-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f2042-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="f2042-118">authentication-basic</span></span>|<span data-ttu-id="f2042-119">Root element.</span><span class="sxs-lookup"><span data-stu-id="f2042-119">Root element.</span></span>|<span data-ttu-id="f2042-120">Yes</span><span class="sxs-lookup"><span data-stu-id="f2042-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f2042-121">Attributes</span><span class="sxs-lookup"><span data-stu-id="f2042-121">Attributes</span></span>  
  
|<span data-ttu-id="f2042-122">Name</span><span class="sxs-lookup"><span data-stu-id="f2042-122">Name</span></span>|<span data-ttu-id="f2042-123">Description</span><span class="sxs-lookup"><span data-stu-id="f2042-123">Description</span></span>|<span data-ttu-id="f2042-124">Required</span><span class="sxs-lookup"><span data-stu-id="f2042-124">Required</span></span>|<span data-ttu-id="f2042-125">Default</span><span class="sxs-lookup"><span data-stu-id="f2042-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f2042-126">username</span><span class="sxs-lookup"><span data-stu-id="f2042-126">username</span></span>|<span data-ttu-id="f2042-127">Specifies the username of the Basic credential.</span><span class="sxs-lookup"><span data-stu-id="f2042-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="f2042-128">Yes</span><span class="sxs-lookup"><span data-stu-id="f2042-128">Yes</span></span>|<span data-ttu-id="f2042-129">N/A</span><span class="sxs-lookup"><span data-stu-id="f2042-129">N/A</span></span>|  
|<span data-ttu-id="f2042-130">password</span><span class="sxs-lookup"><span data-stu-id="f2042-130">password</span></span>|<span data-ttu-id="f2042-131">Specifies the password of the Basic credential.</span><span class="sxs-lookup"><span data-stu-id="f2042-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="f2042-132">Yes</span><span class="sxs-lookup"><span data-stu-id="f2042-132">Yes</span></span>|<span data-ttu-id="f2042-133">N/A</span><span class="sxs-lookup"><span data-stu-id="f2042-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f2042-134">Usage</span><span class="sxs-lookup"><span data-stu-id="f2042-134">Usage</span></span>  
 <span data-ttu-id="f2042-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="f2042-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f2042-136">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="f2042-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f2042-137">**Policy scopes:** API</span><span class="sxs-lookup"><span data-stu-id="f2042-137">**Policy scopes:** API</span></span>  
  
##  <a name="ClientCertificate"></a> <span data-ttu-id="f2042-138">Authenticate with client certificate</span><span class="sxs-lookup"><span data-stu-id="f2042-138">Authenticate with client certificate</span></span>  
 <span data-ttu-id="f2042-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span><span class="sxs-lookup"><span data-stu-id="f2042-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="f2042-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span><span class="sxs-lookup"><span data-stu-id="f2042-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f2042-141">Policy statement</span><span class="sxs-lookup"><span data-stu-id="f2042-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="f2042-142">Example</span><span class="sxs-lookup"><span data-stu-id="f2042-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="f2042-143">Elements</span><span class="sxs-lookup"><span data-stu-id="f2042-143">Elements</span></span>  
  
|<span data-ttu-id="f2042-144">Name</span><span class="sxs-lookup"><span data-stu-id="f2042-144">Name</span></span>|<span data-ttu-id="f2042-145">Description</span><span class="sxs-lookup"><span data-stu-id="f2042-145">Description</span></span>|<span data-ttu-id="f2042-146">Required</span><span class="sxs-lookup"><span data-stu-id="f2042-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f2042-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="f2042-147">authentication-certificate</span></span>|<span data-ttu-id="f2042-148">Root element.</span><span class="sxs-lookup"><span data-stu-id="f2042-148">Root element.</span></span>|<span data-ttu-id="f2042-149">Yes</span><span class="sxs-lookup"><span data-stu-id="f2042-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f2042-150">Attributes</span><span class="sxs-lookup"><span data-stu-id="f2042-150">Attributes</span></span>  
  
|<span data-ttu-id="f2042-151">Name</span><span class="sxs-lookup"><span data-stu-id="f2042-151">Name</span></span>|<span data-ttu-id="f2042-152">Description</span><span class="sxs-lookup"><span data-stu-id="f2042-152">Description</span></span>|<span data-ttu-id="f2042-153">Required</span><span class="sxs-lookup"><span data-stu-id="f2042-153">Required</span></span>|<span data-ttu-id="f2042-154">Default</span><span class="sxs-lookup"><span data-stu-id="f2042-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f2042-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="f2042-155">thumbprint</span></span>|<span data-ttu-id="f2042-156">The thumbprint for the client certificate.</span><span class="sxs-lookup"><span data-stu-id="f2042-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="f2042-157">Yes</span><span class="sxs-lookup"><span data-stu-id="f2042-157">Yes</span></span>|<span data-ttu-id="f2042-158">N/A</span><span class="sxs-lookup"><span data-stu-id="f2042-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f2042-159">Usage</span><span class="sxs-lookup"><span data-stu-id="f2042-159">Usage</span></span>  
 <span data-ttu-id="f2042-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="f2042-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f2042-161">**Policy sections:** inbound</span><span class="sxs-lookup"><span data-stu-id="f2042-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f2042-162">**Policy scopes:** API</span><span class="sxs-lookup"><span data-stu-id="f2042-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="f2042-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2042-163">Next steps</span></span>
<span data-ttu-id="f2042-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f2042-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  