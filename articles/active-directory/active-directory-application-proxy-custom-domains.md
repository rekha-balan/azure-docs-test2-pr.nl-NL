---
title: Custom domains in Azure AD Application Proxy | Microsoft Docs
description: Manage custom domains in Azure AD Application Proxy so that the URL for the app is the same regardless of where your users access it.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: harshja
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: kgremban
ms.openlocfilehash: b8edebd4e7dfdbf85a9beb6d126acaf7ec66dd01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564474"
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="7b5d1-103">Working with custom domains in Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="7b5d1-103">Working with custom domains in Azure AD Application Proxy</span></span>
<span data-ttu-id="7b5d1-104">Using a default domain enables you to set the same URL as the internal and external URL for accessing the application so that your users only have one URL to remember to access the app, no matter where they are accessing from.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-104">Using a default domain enables you to set the same URL as the internal and external URL for accessing the application so that your users only have one URL to remember to access the app, no matter where they are accessing from.</span></span> <span data-ttu-id="7b5d1-105">This also lets you create a single shortcut in the Access Panel for the application.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-105">This also lets you create a single shortcut in the Access Panel for the application.</span></span> <span data-ttu-id="7b5d1-106">If you use the default domain provided by Azure AD Application Proxy, there’s no additional configuration you need to enable your domain.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-106">If you use the default domain provided by Azure AD Application Proxy, there’s no additional configuration you need to enable your domain.</span></span> <span data-ttu-id="7b5d1-107">If you use a custom domain, there are a few things you need to do to make sure that Application Proxy recognizes your domain and validates its certificates.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-107">If you use a custom domain, there are a few things you need to do to make sure that Application Proxy recognizes your domain and validates its certificates.</span></span>

## <a name="selecting-your-custom-domain"></a><span data-ttu-id="7b5d1-108">Selecting your custom domain</span><span class="sxs-lookup"><span data-stu-id="7b5d1-108">Selecting your custom domain</span></span>
1. <span data-ttu-id="7b5d1-109">Publish your application according to the instructions in [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="7b5d1-109">Publish your application according to the instructions in [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>
2. <span data-ttu-id="7b5d1-110">After the application appears in the list of applications, select it and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-110">After the application appears in the list of applications, select it and click **Configure**.</span></span>
3. <span data-ttu-id="7b5d1-111">Under **External URL**, enter your custom domain.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-111">Under **External URL**, enter your custom domain.</span></span>
4. <span data-ttu-id="7b5d1-112">If your external URL is https, you will be prompted to upload a certificate so that Azure can validate the URL of the application.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-112">If your external URL is https, you will be prompted to upload a certificate so that Azure can validate the URL of the application.</span></span> <span data-ttu-id="7b5d1-113">You can also upload a wildcard certificate that matches the External URL of the application.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-113">You can also upload a wildcard certificate that matches the External URL of the application.</span></span> <span data-ttu-id="7b5d1-114">This domain must be within the list of your [Azure verified domains](https://msdn.microsoft.com/library/azure/jj151788.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b5d1-114">This domain must be within the list of your [Azure verified domains](https://msdn.microsoft.com/library/azure/jj151788.aspx).</span></span> <span data-ttu-id="7b5d1-115">Azure must have a certificate for the domain URL of the application or a wildcard certificate that matches the External URL for the application.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-115">Azure must have a certificate for the domain URL of the application or a wildcard certificate that matches the External URL for the application.</span></span>
5. <span data-ttu-id="7b5d1-116">Add a DNS record that routes the internal URL to the application.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-116">Add a DNS record that routes the internal URL to the application.</span></span> <span data-ttu-id="7b5d1-117">This record enables you to have the same URL for internal and external access to the app, and a single shortcut in the user’s applications list.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-117">This record enables you to have the same URL for internal and external access to the app, and a single shortcut in the user’s applications list.</span></span>

## <a name="frequently-asked-questions-about-working-with-custom-domains"></a><span data-ttu-id="7b5d1-118">Frequently asked questions about working with custom domains</span><span class="sxs-lookup"><span data-stu-id="7b5d1-118">Frequently asked questions about working with custom domains</span></span>
<span data-ttu-id="7b5d1-119">Q: Can I select an already-uploaded certificate without uploading it again?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-119">Q: Can I select an already-uploaded certificate without uploading it again?</span></span>  
<span data-ttu-id="7b5d1-120">A: Previously uploaded certificates are automatically bound to an application, and there is exactly one certificate matching the application’s host name.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-120">A: Previously uploaded certificates are automatically bound to an application, and there is exactly one certificate matching the application’s host name.</span></span>  

<span data-ttu-id="7b5d1-121">Q: How do I add a certificate and what format should the exported certificate be uploaded in?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-121">Q: How do I add a certificate and what format should the exported certificate be uploaded in?</span></span>  
<span data-ttu-id="7b5d1-122">A: The certificate should be uploaded from the application configuration page.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-122">A: The certificate should be uploaded from the application configuration page.</span></span> <span data-ttu-id="7b5d1-123">The certificate should be a PFX file.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-123">The certificate should be a PFX file.</span></span>  

<span data-ttu-id="7b5d1-124">Q: Can ECC certs be used?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-124">Q: Can ECC certs be used?</span></span>  
<span data-ttu-id="7b5d1-125">A: There is no explicit limitation on signature methods.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-125">A: There is no explicit limitation on signature methods.</span></span>  

<span data-ttu-id="7b5d1-126">Q: Can SAN certs be used?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-126">Q: Can SAN certs be used?</span></span>  
<span data-ttu-id="7b5d1-127">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-127">A: Yes.</span></span>  

<span data-ttu-id="7b5d1-128">Q: Can wildcard certs be used?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-128">Q: Can wildcard certs be used?</span></span>  
<span data-ttu-id="7b5d1-129">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-129">A: Yes.</span></span>  

<span data-ttu-id="7b5d1-130">Q: Can a different certificate be used on each application?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-130">Q: Can a different certificate be used on each application?</span></span>  
<span data-ttu-id="7b5d1-131">A: Yes, unless the two applications share the same external host.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-131">A: Yes, unless the two applications share the same external host.</span></span>  

<span data-ttu-id="7b5d1-132">Q: If I register a new domain, can I use that domain?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-132">Q: If I register a new domain, can I use that domain?</span></span>  
<span data-ttu-id="7b5d1-133">A: Yes, the list of domains is fed from the tenant’s verified domain list.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-133">A: Yes, the list of domains is fed from the tenant’s verified domain list.</span></span>  

<span data-ttu-id="7b5d1-134">Q: What happens when a cert expires?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-134">Q: What happens when a cert expires?</span></span>  
<span data-ttu-id="7b5d1-135">A: You will get a warning in the certificate section in the application configuration page.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-135">A: You will get a warning in the certificate section in the application configuration page.</span></span> <span data-ttu-id="7b5d1-136">When a user tries to access the application, a security warning will pop up.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-136">When a user tries to access the application, a security warning will pop up.</span></span>  

<span data-ttu-id="7b5d1-137">Q: What should I do if I want to replace a cert for a given app?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-137">Q: What should I do if I want to replace a cert for a given app?</span></span>  
<span data-ttu-id="7b5d1-138">A: Upload a new certificate from the application configuration page.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-138">A: Upload a new certificate from the application configuration page.</span></span>  

<span data-ttu-id="7b5d1-139">Q: Can I delete a cert and replace it?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-139">Q: Can I delete a cert and replace it?</span></span>  
<span data-ttu-id="7b5d1-140">A: When you upload a new certificate, if the old certificate is not in use by another application, it will be automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-140">A: When you upload a new certificate, if the old certificate is not in use by another application, it will be automatically deleted.</span></span>  

<span data-ttu-id="7b5d1-141">Q: What happens when a cert is revoked?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-141">Q: What happens when a cert is revoked?</span></span>  
<span data-ttu-id="7b5d1-142">A: Revocation checks are not performed for certificates.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-142">A: Revocation checks are not performed for certificates.</span></span> <span data-ttu-id="7b5d1-143">When a user tries to access the application, depending on the browser, a security warning might appear.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-143">When a user tries to access the application, depending on the browser, a security warning might appear.</span></span>  

<span data-ttu-id="7b5d1-144">Q: Can I use a self-signed certificate?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-144">Q: Can I use a self-signed certificate?</span></span>  
<span data-ttu-id="7b5d1-145">A: Yes, self-signed certificates are allowed.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-145">A: Yes, self-signed certificates are allowed.</span></span> <span data-ttu-id="7b5d1-146">Note that if you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-146">Note that if you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>  

<span data-ttu-id="7b5d1-147">Q: Is there a place to see all the certificates for my tenant?</span><span class="sxs-lookup"><span data-stu-id="7b5d1-147">Q: Is there a place to see all the certificates for my tenant?</span></span>  
<span data-ttu-id="7b5d1-148">A: This is not supported in the current version.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-148">A: This is not supported in the current version.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7b5d1-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b5d1-149">Next steps</span></span>
* <span data-ttu-id="7b5d1-150">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-150">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="7b5d1-151">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span><span class="sxs-lookup"><span data-stu-id="7b5d1-151">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="7b5d1-152">Add your custom domain name to Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b5d1-152">Add your custom domain name to Azure AD</span></span>](active-directory-add-domain.md)


