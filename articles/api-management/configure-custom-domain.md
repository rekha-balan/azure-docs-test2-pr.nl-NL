---
title: Configure a custom domain name for your Azure API Management instance | Microsoft Docs
description: This topic describes how to configure a custom domain name for your Azure API Management instance.
services: api-management
documentationcenter: ''
author: vladvino
manager: anneta
editor: ''
ms.service: api-management
ms.workload: integration
ms.topic: article
ms.date: 12/14/2017
ms.author: apimpm
ms.openlocfilehash: 96e233a26af95d4373323867046ca01fe1304608
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855915"
---
# <a name="configure-a-custom-domain-name"></a><span data-ttu-id="fef8a-103">Configure a custom domain name</span><span class="sxs-lookup"><span data-stu-id="fef8a-103">Configure a custom domain name</span></span> 

<span data-ttu-id="fef8a-104">When you create an API Management (APIM) instance, Azure assigns it to a subdomain of azure-api.net (for example, `apim-service-name.azure-api.net`).</span><span class="sxs-lookup"><span data-stu-id="fef8a-104">When you create an API Management (APIM) instance, Azure assigns it to a subdomain of azure-api.net (for example, `apim-service-name.azure-api.net`).</span></span> <span data-ttu-id="fef8a-105">However, you can expose your APIM endpoints using your own domain name, such as **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fef8a-105">However, you can expose your APIM endpoints using your own domain name, such as **contoso.com**.</span></span> <span data-ttu-id="fef8a-106">This tutorial shows you how to map an existing custom DNS name to endpoints exposed by an Azure API Management instance.</span><span class="sxs-lookup"><span data-stu-id="fef8a-106">This tutorial shows you how to map an existing custom DNS name to endpoints exposed by an Azure API Management instance.</span></span>

> [!WARNING]
> <span data-ttu-id="fef8a-107">Customers who wish to use certificate pinning to improve the security of their applications must use a custom domain name > and certificate which they manage, not the default certificate.</span><span class="sxs-lookup"><span data-stu-id="fef8a-107">Customers who wish to use certificate pinning to improve the security of their applications must use a custom domain name > and certificate which they manage, not the default certificate.</span></span> <span data-ttu-id="fef8a-108">Customers that pin the default certificate instead will be > taking a hard dependency on the properties of the certificate they don't control, which is not a recommended practice.</span><span class="sxs-lookup"><span data-stu-id="fef8a-108">Customers that pin the default certificate instead will be > taking a hard dependency on the properties of the certificate they don't control, which is not a recommended practice.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fef8a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fef8a-109">Prerequisites</span></span>

<span data-ttu-id="fef8a-110">To perform the steps described in this article, you must have:</span><span class="sxs-lookup"><span data-stu-id="fef8a-110">To perform the steps described in this article, you must have:</span></span>

+ <span data-ttu-id="fef8a-111">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fef8a-111">An active Azure subscription.</span></span>

    [!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

+ <span data-ttu-id="fef8a-112">An APIM instance.</span><span class="sxs-lookup"><span data-stu-id="fef8a-112">An APIM instance.</span></span> <span data-ttu-id="fef8a-113">For more information, see [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="fef8a-113">For more information, see [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>
+ <span data-ttu-id="fef8a-114">A custom domain name that is owned by you.</span><span class="sxs-lookup"><span data-stu-id="fef8a-114">A custom domain name that is owned by you.</span></span> <span data-ttu-id="fef8a-115">The custom domain name you want to use, must be procured separately and hosted on a DNS server.</span><span class="sxs-lookup"><span data-stu-id="fef8a-115">The custom domain name you want to use, must be procured separately and hosted on a DNS server.</span></span> <span data-ttu-id="fef8a-116">This topic does not give instructions on how to host a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="fef8a-116">This topic does not give instructions on how to host a custom domain name.</span></span>
+ <span data-ttu-id="fef8a-117">You must have a valid certificate with a public and private key (.PFX).</span><span class="sxs-lookup"><span data-stu-id="fef8a-117">You must have a valid certificate with a public and private key (.PFX).</span></span> <span data-ttu-id="fef8a-118">Subject or subject alternative name (SAN) has to match the domain name (this enables APIM to securely expose URLs over SSL).</span><span class="sxs-lookup"><span data-stu-id="fef8a-118">Subject or subject alternative name (SAN) has to match the domain name (this enables APIM to securely expose URLs over SSL).</span></span>

## <a name="use-the-azure-portal-to-set-a-custom-domain-name"></a><span data-ttu-id="fef8a-119">Use the Azure portal to set a custom domain name</span><span class="sxs-lookup"><span data-stu-id="fef8a-119">Use the Azure portal to set a custom domain name</span></span>

1. <span data-ttu-id="fef8a-120">Navigate to your APIM instance in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fef8a-120">Navigate to your APIM instance in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fef8a-121">Select **Custom domains and SSL**.</span><span class="sxs-lookup"><span data-stu-id="fef8a-121">Select **Custom domains and SSL**.</span></span>
    
    <span data-ttu-id="fef8a-122">There is a number of endpoints to which you can assign a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="fef8a-122">There is a number of endpoints to which you can assign a custom domain name.</span></span> <span data-ttu-id="fef8a-123">Currently, the following endpoints are available:</span><span class="sxs-lookup"><span data-stu-id="fef8a-123">Currently, the following endpoints are available:</span></span> 
    + <span data-ttu-id="fef8a-124">**Proxy** (default is: `<apim-service-name>.azure-api.net`),</span><span class="sxs-lookup"><span data-stu-id="fef8a-124">**Proxy** (default is: `<apim-service-name>.azure-api.net`),</span></span> 
    + <span data-ttu-id="fef8a-125">**Portal** (default is: `<apim-service-name>.portal.azure-api.net`),</span><span class="sxs-lookup"><span data-stu-id="fef8a-125">**Portal** (default is: `<apim-service-name>.portal.azure-api.net`),</span></span>     
    + <span data-ttu-id="fef8a-126">**Management** (default is: `<apim-service-name>.management.azure-api.net`),</span><span class="sxs-lookup"><span data-stu-id="fef8a-126">**Management** (default is: `<apim-service-name>.management.azure-api.net`),</span></span> 
    + <span data-ttu-id="fef8a-127">**SCM** (default is: `<apim-service-name>.scm.azure-api.net`).</span><span class="sxs-lookup"><span data-stu-id="fef8a-127">**SCM** (default is: `<apim-service-name>.scm.azure-api.net`).</span></span>

    >[!NOTE]
    > <span data-ttu-id="fef8a-128">You can update all of the endpoints or some of them.</span><span class="sxs-lookup"><span data-stu-id="fef8a-128">You can update all of the endpoints or some of them.</span></span> <span data-ttu-id="fef8a-129">Commonly, customers update **Proxy** (this URL is used to call the API exposed through API Management) and **Portal** (the developer portal URL).</span><span class="sxs-lookup"><span data-stu-id="fef8a-129">Commonly, customers update **Proxy** (this URL is used to call the API exposed through API Management) and **Portal** (the developer portal URL).</span></span> <span data-ttu-id="fef8a-130">**Management** and **SCM** endpoints are used internally by APIM customers and thus are less frequently assigned a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="fef8a-130">**Management** and **SCM** endpoints are used internally by APIM customers and thus are less frequently assigned a custom domain name.</span></span>
3. <span data-ttu-id="fef8a-131">Select the endpoint that you want to update.</span><span class="sxs-lookup"><span data-stu-id="fef8a-131">Select the endpoint that you want to update.</span></span> 
4. <span data-ttu-id="fef8a-132">In the window on the right, click **Custom**.</span><span class="sxs-lookup"><span data-stu-id="fef8a-132">In the window on the right, click **Custom**.</span></span>

    + <span data-ttu-id="fef8a-133">In the **Custom domain name**, specify the name you want to use.</span><span class="sxs-lookup"><span data-stu-id="fef8a-133">In the **Custom domain name**, specify the name you want to use.</span></span> <span data-ttu-id="fef8a-134">For example, `api.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="fef8a-134">For example, `api.contoso.com`.</span></span> <br/><span data-ttu-id="fef8a-135">Wildcard domain names (for example, \*.domain.com) are also supported.</span><span class="sxs-lookup"><span data-stu-id="fef8a-135">Wildcard domain names (for example, \*.domain.com) are also supported.</span></span>
    + <span data-ttu-id="fef8a-136">In the **Certificate**, specify a valid .PFX file that you want to upload.</span><span class="sxs-lookup"><span data-stu-id="fef8a-136">In the **Certificate**, specify a valid .PFX file that you want to upload.</span></span> 
    + <span data-ttu-id="fef8a-137">If the certificate has a password, enter it in the **Password** field.</span><span class="sxs-lookup"><span data-stu-id="fef8a-137">If the certificate has a password, enter it in the **Password** field.</span></span>
1. <span data-ttu-id="fef8a-138">Click Apply.</span><span class="sxs-lookup"><span data-stu-id="fef8a-138">Click Apply.</span></span>

    >[!NOTE]
    ><span data-ttu-id="fef8a-139">The process of assigning the certificate may take 15 minutes or more depending on size of deployment.</span><span class="sxs-lookup"><span data-stu-id="fef8a-139">The process of assigning the certificate may take 15 minutes or more depending on size of deployment.</span></span> <span data-ttu-id="fef8a-140">Developer SKU has downtime, Basic and higher SKU's do not have downtime.</span><span class="sxs-lookup"><span data-stu-id="fef8a-140">Developer SKU has downtime, Basic and higher SKU's do not have downtime.</span></span>

[!INCLUDE [api-management-custom-domain](../../includes/api-management-custom-domain.md)]

## <a name="next-steps"></a><span data-ttu-id="fef8a-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="fef8a-141">Next steps</span></span>

[<span data-ttu-id="fef8a-142">Upgrade and scale your service</span><span class="sxs-lookup"><span data-stu-id="fef8a-142">Upgrade and scale your service</span></span>](upgrade-and-scale.md)
