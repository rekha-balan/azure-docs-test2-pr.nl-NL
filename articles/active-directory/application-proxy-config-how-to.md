---
title: How to configure an Application Proxy application | Microsoft Docs
description: Learn how to create an configure an APplication Proxy application in a few simple steps
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: c1c026347d6b72ee255bb46b43566bcb9d266007
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556619"
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="8f9ed-103">How to configure an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="8f9ed-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="8f9ed-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="8f9ed-105">Recommended documents</span><span class="sxs-lookup"><span data-stu-id="8f9ed-105">Recommended documents</span></span> 

<span data-ttu-id="8f9ed-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="8f9ed-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="8f9ed-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="8f9ed-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="8f9ed-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="8f9ed-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="8f9ed-109">Create the Application/Setting the URLs</span><span class="sxs-lookup"><span data-stu-id="8f9ed-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="8f9ed-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="8f9ed-111">Most error messages include a suggested fix.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="8f9ed-112">To avoid common errors, verify:</span><span class="sxs-lookup"><span data-stu-id="8f9ed-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="8f9ed-113">You are an administrator with permission to create an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="8f9ed-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="8f9ed-114">The internal URL is unique</span><span class="sxs-lookup"><span data-stu-id="8f9ed-114">The internal URL is unique</span></span>

-   <span data-ttu-id="8f9ed-115">The external URL is unique</span><span class="sxs-lookup"><span data-stu-id="8f9ed-115">The external URL is unique</span></span>

-   <span data-ttu-id="8f9ed-116">The URLs start with http or https, and end with a “/”</span><span class="sxs-lookup"><span data-stu-id="8f9ed-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="8f9ed-117">The URL should be a domain name, not an IP address</span><span class="sxs-lookup"><span data-stu-id="8f9ed-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="8f9ed-118">The error message should display in the top right corner when you create the application.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="8f9ed-119">You can also select the notification icon to see the error messages.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-119">You can also select the notification icon to see the error messages.</span></span>

   ![Notification prompt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="8f9ed-121">Configure connectors/connector groups</span><span class="sxs-lookup"><span data-stu-id="8f9ed-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="8f9ed-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="8f9ed-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="8f9ed-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="8f9ed-124">If your connectors are inactive, this means that they are unable to reach the service.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="8f9ed-125">This is often because all the required ports are not open.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="8f9ed-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="8f9ed-127">Upload certificates for custom domains</span><span class="sxs-lookup"><span data-stu-id="8f9ed-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="8f9ed-128">Custom Domains allow you to specify the domain of your external URLs.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="8f9ed-129">To use custom domains, you need to upload the certificate for that domain.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="8f9ed-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="8f9ed-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="8f9ed-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="8f9ed-132">Common certificate problems include:</span><span class="sxs-lookup"><span data-stu-id="8f9ed-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="8f9ed-133">Expired certificate</span><span class="sxs-lookup"><span data-stu-id="8f9ed-133">Expired certificate</span></span>

-   <span data-ttu-id="8f9ed-134">Certificate is self-signed</span><span class="sxs-lookup"><span data-stu-id="8f9ed-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="8f9ed-135">Certificate is missing the private key</span><span class="sxs-lookup"><span data-stu-id="8f9ed-135">Certificate is missing the private key</span></span>

<span data-ttu-id="8f9ed-136">The error message display in the top right corner as you try to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="8f9ed-137">You can also select the notification icon to see the error messages.</span><span class="sxs-lookup"><span data-stu-id="8f9ed-137">You can also select the notification icon to see the error messages.</span></span>

   ![Notification prompt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="8f9ed-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f9ed-139">Next steps</span></span>
[<span data-ttu-id="8f9ed-140">Publish applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="8f9ed-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)


