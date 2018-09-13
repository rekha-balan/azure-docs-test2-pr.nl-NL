---
title: Secure back-end services using client certificate authentication - Azure API Management | Microsoft Docs
description: Learn how to secure back-end services using client certificate authentication in Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: fe30c103245c9cb6b5c2a52cd38fc54f45831b67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564321"
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="5ed41-103">How to secure back-end services using client certificate authentication in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5ed41-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="5ed41-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span><span class="sxs-lookup"><span data-stu-id="5ed41-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="5ed41-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span><span class="sxs-lookup"><span data-stu-id="5ed41-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="5ed41-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="5ed41-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="5ed41-107"><a name="prerequisites"> </a>Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ed41-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="5ed41-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span><span class="sxs-lookup"><span data-stu-id="5ed41-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="5ed41-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="5ed41-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="5ed41-110"><a name="step1"> </a>Upload a client certificate</span><span class="sxs-lookup"><span data-stu-id="5ed41-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="5ed41-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="5ed41-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="5ed41-112">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="5ed41-112">This takes you to the API Management publisher portal.</span></span>

![API Publisher portal][api-management-management-console]

> <span data-ttu-id="5ed41-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ed41-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="5ed41-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span><span class="sxs-lookup"><span data-stu-id="5ed41-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Client certificates][api-management-security-client-certificates]

<span data-ttu-id="5ed41-117">To upload a new certificate, click **Upload certificate**.</span><span class="sxs-lookup"><span data-stu-id="5ed41-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Upload certificate][api-management-upload-certificate]

<span data-ttu-id="5ed41-119">Browse to your certificate, and then enter the password for the certificate.</span><span class="sxs-lookup"><span data-stu-id="5ed41-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="5ed41-120">The certificate must be in **.pfx** format.</span><span class="sxs-lookup"><span data-stu-id="5ed41-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="5ed41-121">Self-signed certificates are allowed.</span><span class="sxs-lookup"><span data-stu-id="5ed41-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Upload certificate][api-management-upload-certificate-form]

<span data-ttu-id="5ed41-123">Click **Upload** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="5ed41-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="5ed41-124">The certificate password is validated at this time.</span><span class="sxs-lookup"><span data-stu-id="5ed41-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="5ed41-125">If it is incorrect an error message is displayed.</span><span class="sxs-lookup"><span data-stu-id="5ed41-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificate uploaded][api-management-certificate-uploaded]

<span data-ttu-id="5ed41-127">Once the certificate is uploaded, it appears on the **Client certificates** tab. If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span><span class="sxs-lookup"><span data-stu-id="5ed41-127">Once the certificate is uploaded, it appears on the **Client certificates** tab. If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="5ed41-128">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="5ed41-128">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="5ed41-129"><a name="step1a"> </a>Delete a client certificate</span><span class="sxs-lookup"><span data-stu-id="5ed41-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="5ed41-130">To delete a certificate, click **Delete** beside the desired certificate.</span><span class="sxs-lookup"><span data-stu-id="5ed41-130">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Delete certificate][api-management-certificate-delete]

<span data-ttu-id="5ed41-132">Click **Yes, delete it** to confirm.</span><span class="sxs-lookup"><span data-stu-id="5ed41-132">Click **Yes, delete it** to confirm.</span></span>

![Confirm delete][api-management-confirm-delete]

<span data-ttu-id="5ed41-134">If the certificate is in use by an API, then a warning screen is displayed.</span><span class="sxs-lookup"><span data-stu-id="5ed41-134">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="5ed41-135">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span><span class="sxs-lookup"><span data-stu-id="5ed41-135">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Confirm delete][api-management-confirm-delete-policy]

## <span data-ttu-id="5ed41-137"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span><span class="sxs-lookup"><span data-stu-id="5ed41-137"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="5ed41-138">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="5ed41-138">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![API security][api-management-api-security]

<span data-ttu-id="5ed41-140">Select **Client certificates** from the **With credentials** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="5ed41-140">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Client certificates][api-management-mutual-certificates]

<span data-ttu-id="5ed41-142">Select the desired certificate from the **Client certificate** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="5ed41-142">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="5ed41-143">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span><span class="sxs-lookup"><span data-stu-id="5ed41-143">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Select certificate][api-management-select-certificate]

<span data-ttu-id="5ed41-145">Click **Save** to save the configuration change to the API.</span><span class="sxs-lookup"><span data-stu-id="5ed41-145">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="5ed41-146">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span><span class="sxs-lookup"><span data-stu-id="5ed41-146">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Save API changes][api-management-save-api]

> <span data-ttu-id="5ed41-148">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span><span class="sxs-lookup"><span data-stu-id="5ed41-148">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Certificate policy][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="5ed41-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ed41-150">Next steps</span></span>
<span data-ttu-id="5ed41-151">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span><span class="sxs-lookup"><span data-stu-id="5ed41-151">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps
















