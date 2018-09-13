---
title: Enable HTTPS on an Azure CDN Custom Domain | Microsoft Docs
description: Learn how to enable HTTPS on your Azure CDN endpoint with a custom domain.
services: cdn
documentationcenter: ''
author: camsoper
manager: erikre
editor: ''
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 829934b275fced0806c58e9976867249c4f094c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669623"
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="c82c2-103">Enable HTTPS on an Azure CDN custom domain</span><span class="sxs-lookup"><span data-stu-id="c82c2-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="c82c2-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span><span class="sxs-lookup"><span data-stu-id="c82c2-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="c82c2-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span><span class="sxs-lookup"><span data-stu-id="c82c2-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="c82c2-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span><span class="sxs-lookup"><span data-stu-id="c82c2-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="c82c2-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span><span class="sxs-lookup"><span data-stu-id="c82c2-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="c82c2-108">It provides trust, authentication and protects your web applications from attacks.</span><span class="sxs-lookup"><span data-stu-id="c82c2-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="c82c2-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="c82c2-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="c82c2-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="c82c2-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="c82c2-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span><span class="sxs-lookup"><span data-stu-id="c82c2-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="c82c2-112">Some of the key attributes of HTTPS feature are:</span><span class="sxs-lookup"><span data-stu-id="c82c2-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="c82c2-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="c82c2-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="c82c2-114">You just pay for GB egress from the CDN.</span><span class="sxs-lookup"><span data-stu-id="c82c2-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="c82c2-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c82c2-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c82c2-116">You can also use REST API or other developer tools to enable the feature.</span><span class="sxs-lookup"><span data-stu-id="c82c2-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="c82c2-117">Complete certificate management: All certificate procurement and management is handled for you.</span><span class="sxs-lookup"><span data-stu-id="c82c2-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="c82c2-118">Certificates are automatically provisioned and renewed prior to expiration.</span><span class="sxs-lookup"><span data-stu-id="c82c2-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="c82c2-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span><span class="sxs-lookup"><span data-stu-id="c82c2-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="c82c2-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c82c2-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="c82c2-121">Step 1: Enabling the feature</span><span class="sxs-lookup"><span data-stu-id="c82c2-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="c82c2-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span><span class="sxs-lookup"><span data-stu-id="c82c2-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="c82c2-123">In the list of endpoints, click the endpoint containing your custom domain.</span><span class="sxs-lookup"><span data-stu-id="c82c2-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="c82c2-124">Click the custom domain for which you want to enable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c82c2-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Endpoint blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="c82c2-126">Click **On** to enable HTTPS and save the change.</span><span class="sxs-lookup"><span data-stu-id="c82c2-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Custom HTTPS dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="c82c2-128">Step 2: Domain validation</span><span class="sxs-lookup"><span data-stu-id="c82c2-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c82c2-129">You must complete domain validation before HTTPS will be active on your custom domain.</span><span class="sxs-lookup"><span data-stu-id="c82c2-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="c82c2-130">You have 6 business days to approve the domain.</span><span class="sxs-lookup"><span data-stu-id="c82c2-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="c82c2-131">Request will be canceled with no approval within 6 business days.</span><span class="sxs-lookup"><span data-stu-id="c82c2-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="c82c2-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span><span class="sxs-lookup"><span data-stu-id="c82c2-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="c82c2-133">DigiCert will also send the verification email to the below addresses.</span><span class="sxs-lookup"><span data-stu-id="c82c2-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="c82c2-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span><span class="sxs-lookup"><span data-stu-id="c82c2-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="c82c2-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="c82c2-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="c82c2-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="c82c2-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="c82c2-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="c82c2-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="c82c2-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="c82c2-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="c82c2-139">Upon receiving the email, you have two verification options:</span><span class="sxs-lookup"><span data-stu-id="c82c2-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="c82c2-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span><span class="sxs-lookup"><span data-stu-id="c82c2-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="c82c2-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span><span class="sxs-lookup"><span data-stu-id="c82c2-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="c82c2-142">You can just approve the specific host name used in this request.</span><span class="sxs-lookup"><span data-stu-id="c82c2-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="c82c2-143">Additional approval will be required for subsequent requests.</span><span class="sxs-lookup"><span data-stu-id="c82c2-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="c82c2-144">Example email:</span><span class="sxs-lookup"><span data-stu-id="c82c2-144">Example email:</span></span>
    
    ![Custom HTTPS dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="c82c2-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span><span class="sxs-lookup"><span data-stu-id="c82c2-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="c82c2-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span><span class="sxs-lookup"><span data-stu-id="c82c2-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="c82c2-148">Step 3: Wait for the propagation then start using your feature</span><span class="sxs-lookup"><span data-stu-id="c82c2-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="c82c2-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span><span class="sxs-lookup"><span data-stu-id="c82c2-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="c82c2-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span><span class="sxs-lookup"><span data-stu-id="c82c2-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="c82c2-151">HTTPS with your custom domain is now ready for your use.</span><span class="sxs-lookup"><span data-stu-id="c82c2-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="c82c2-152">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="c82c2-152">Frequently asked questions</span></span>

1. <span data-ttu-id="c82c2-153">*Who is the certificate provider and what type of certificate is used?*</span><span class="sxs-lookup"><span data-stu-id="c82c2-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="c82c2-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c82c2-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="c82c2-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span><span class="sxs-lookup"><span data-stu-id="c82c2-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="c82c2-156">*Can I use my dedicated certificate?*</span><span class="sxs-lookup"><span data-stu-id="c82c2-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="c82c2-157">Not currently, but it's on the roadmap.</span><span class="sxs-lookup"><span data-stu-id="c82c2-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="c82c2-158">*What if I don't receive the domain verification email from DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="c82c2-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="c82c2-159">Please contact Microsoft if you don't receive an email within 24 hours.</span><span class="sxs-lookup"><span data-stu-id="c82c2-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="c82c2-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span><span class="sxs-lookup"><span data-stu-id="c82c2-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="c82c2-161">A SAN cert follows the same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span><span class="sxs-lookup"><span data-stu-id="c82c2-161">A SAN cert follows the same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="c82c2-162">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span><span class="sxs-lookup"><span data-stu-id="c82c2-162">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="c82c2-163">Currently, this feature is only available with Azure CDN from Verizon.</span><span class="sxs-lookup"><span data-stu-id="c82c2-163">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="c82c2-164">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span><span class="sxs-lookup"><span data-stu-id="c82c2-164">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c82c2-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="c82c2-165">Next steps</span></span>

- <span data-ttu-id="c82c2-166">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="c82c2-166">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>





