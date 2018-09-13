---
title: Custom domains in Azure AD Application Proxy | Microsoft Docs
description: Manage custom domains in Azure AD Application Proxy so that the URL for the app is the same regardless of where your users access it.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/31/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 090df19861e00a99f0bb63bf20eb2f26dc6761fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968770"
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="aa5d8-103">Working with custom domains in Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="aa5d8-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="aa5d8-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="aa5d8-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="aa5d8-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="aa5d8-107">If you want to use your own domain name, configure a custom domain for your application.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="aa5d8-108">We recommend that you set up custom domains for your applications whenever possible.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="aa5d8-109">Some of the benefits of custom domains include:</span><span class="sxs-lookup"><span data-stu-id="aa5d8-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="aa5d8-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="aa5d8-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="aa5d8-112">You control your branding, and create the URLs you want.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="aa5d8-113">Configure a custom domain</span><span class="sxs-lookup"><span data-stu-id="aa5d8-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aa5d8-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa5d8-114">Prerequisites</span></span>

<span data-ttu-id="aa5d8-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span><span class="sxs-lookup"><span data-stu-id="aa5d8-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="aa5d8-116">A [verified domain added to Azure Active Directory](../fundamentals/add-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aa5d8-116">A [verified domain added to Azure Active Directory](../fundamentals/add-custom-domain.md).</span></span>
- <span data-ttu-id="aa5d8-117">A custom certificate for the domain, in the form of a PFX file.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="aa5d8-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aa5d8-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="aa5d8-119">Configure your custom domain</span><span class="sxs-lookup"><span data-stu-id="aa5d8-119">Configure your custom domain</span></span>

<span data-ttu-id="aa5d8-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span><span class="sxs-lookup"><span data-stu-id="aa5d8-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="aa5d8-121">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa5d8-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aa5d8-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="aa5d8-123">Select **Application Proxy**.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="aa5d8-124">In the External URL field, use the dropdown list to select your custom domain.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="aa5d8-125">If you don't see your domain in the list, then it hasn't been verified yet.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="aa5d8-126">Select **Save**</span><span class="sxs-lookup"><span data-stu-id="aa5d8-126">Select **Save**</span></span>
5. <span data-ttu-id="aa5d8-127">The **Certificate** field that was disabled becomes enabled.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="aa5d8-128">Select this field.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-128">Select this field.</span></span> 

   ![Click to upload a certificate](./media/application-proxy-configure-custom-domain/certificate.png)

   <span data-ttu-id="aa5d8-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="aa5d8-131">Upload the PFX certificate and enter the password for the certificate.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="aa5d8-132">Select **Save** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="aa5d8-133">Add a [DNS record](../../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-133">Add a [DNS record](../../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="aa5d8-134">You only need to upload one certificate per custom domain.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="aa5d8-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="aa5d8-136">Manage certificates</span><span class="sxs-lookup"><span data-stu-id="aa5d8-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="aa5d8-137">Certificate format</span><span class="sxs-lookup"><span data-stu-id="aa5d8-137">Certificate format</span></span>
<span data-ttu-id="aa5d8-138">There is no restriction on the certificate signature methods.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="aa5d8-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="aa5d8-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

### <a name="changing-the-domain"></a><span data-ttu-id="aa5d8-141">Changing the domain</span><span class="sxs-lookup"><span data-stu-id="aa5d8-141">Changing the domain</span></span>
<span data-ttu-id="aa5d8-142">All verified domains appear in the External URL dropdown list for your application.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-142">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="aa5d8-143">To change the domain, just update that field for the application.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-143">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="aa5d8-144">If the domain you want isn't in the list, [add it as a verified domain](../fundamentals/add-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aa5d8-144">If the domain you want isn't in the list, [add it as a verified domain](../fundamentals/add-custom-domain.md).</span></span> <span data-ttu-id="aa5d8-145">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-145">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="aa5d8-146">Then, make sure you update the DNS record to redirect from the new external URL.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-146">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="aa5d8-147">Certificate management</span><span class="sxs-lookup"><span data-stu-id="aa5d8-147">Certificate management</span></span>
<span data-ttu-id="aa5d8-148">You can use the same certificate for multiple applications unless the applications share an external host.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-148">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="aa5d8-149">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-149">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="aa5d8-150">If the certificate is revoked, your users may see a security warning when accessing the application.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-150">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="aa5d8-151">We don’t perform revocation checks for certificates.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-151">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="aa5d8-152">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-152">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="aa5d8-153">If the old certificate is not being used by other applications, it is deleted automatically.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-153">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="aa5d8-154">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-154">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aa5d8-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa5d8-155">Next steps</span></span>
* <span data-ttu-id="aa5d8-156">[Enable single sign-on](application-proxy-configure-single-sign-on-with-kcd.md) to your published apps with Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-156">[Enable single sign-on](application-proxy-configure-single-sign-on-with-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="aa5d8-157">[Enable conditional access](application-proxy-integrate-with-sharepoint-server.md) to your published apps.</span><span class="sxs-lookup"><span data-stu-id="aa5d8-157">[Enable conditional access](application-proxy-integrate-with-sharepoint-server.md) to your published apps.</span></span>
* [<span data-ttu-id="aa5d8-158">Add your custom domain name to Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa5d8-158">Add your custom domain name to Azure AD</span></span>](../fundamentals/add-custom-domain.md)


