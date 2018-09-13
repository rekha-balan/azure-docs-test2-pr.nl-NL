---
title: How to configure an Application Proxy application | Microsoft Docs
description: Learn how to create an configure an APplication Proxy application in a few simple steps
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/18/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: cf3e367dad528017a98e103962c57cb758da55cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868215"
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="7c8e4-103">How to configure an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="7c8e4-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="7c8e4-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="7c8e4-105">Recommended documents</span><span class="sxs-lookup"><span data-stu-id="7c8e4-105">Recommended documents</span></span> 

<span data-ttu-id="7c8e4-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e4-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

<span data-ttu-id="7c8e4-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e4-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](application-proxy-enable.md).</span></span>

<span data-ttu-id="7c8e4-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e4-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="7c8e4-109">Create the Application/Setting the URLs</span><span class="sxs-lookup"><span data-stu-id="7c8e4-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="7c8e4-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="7c8e4-111">Most error messages include a suggested fix.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="7c8e4-112">To avoid common errors, verify:</span><span class="sxs-lookup"><span data-stu-id="7c8e4-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="7c8e4-113">You are an administrator with permission to create an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="7c8e4-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="7c8e4-114">The internal URL is unique</span><span class="sxs-lookup"><span data-stu-id="7c8e4-114">The internal URL is unique</span></span>

-   <span data-ttu-id="7c8e4-115">The external URL is unique</span><span class="sxs-lookup"><span data-stu-id="7c8e4-115">The external URL is unique</span></span>

-   <span data-ttu-id="7c8e4-116">The URLs start with http or https, and end with a “/”</span><span class="sxs-lookup"><span data-stu-id="7c8e4-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="7c8e4-117">The URL should be a domain name, not an IP address</span><span class="sxs-lookup"><span data-stu-id="7c8e4-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="7c8e4-118">The error message should display in the top right corner when you create the application.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="7c8e4-119">You can also select the notification icon to see the error messages.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-119">You can also select the notification icon to see the error messages.</span></span>

   ![Notification prompt](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="7c8e4-121">Configure connectors/connector groups</span><span class="sxs-lookup"><span data-stu-id="7c8e4-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="7c8e4-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="7c8e4-123">If you want to learn more about connectors, see the [connectors documentation](application-proxy-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e4-123">If you want to learn more about connectors, see the [connectors documentation](application-proxy-connectors.md).</span></span>

<span data-ttu-id="7c8e4-124">If your connectors are inactive, this means that they are unable to reach the service.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="7c8e4-125">This is often because all the required ports are not open.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="7c8e4-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="7c8e4-127">Upload certificates for custom domains</span><span class="sxs-lookup"><span data-stu-id="7c8e4-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="7c8e4-128">Custom Domains allow you to specify the domain of your external URLs.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="7c8e4-129">To use custom domains, you need to upload the certificate for that domain.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="7c8e4-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e4-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span></span> 

<span data-ttu-id="7c8e4-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="7c8e4-132">Common certificate problems include:</span><span class="sxs-lookup"><span data-stu-id="7c8e4-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="7c8e4-133">Expired certificate</span><span class="sxs-lookup"><span data-stu-id="7c8e4-133">Expired certificate</span></span>

-   <span data-ttu-id="7c8e4-134">Certificate is self-signed</span><span class="sxs-lookup"><span data-stu-id="7c8e4-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="7c8e4-135">Certificate is missing the private key</span><span class="sxs-lookup"><span data-stu-id="7c8e4-135">Certificate is missing the private key</span></span>

<span data-ttu-id="7c8e4-136">The error message display in the top right corner as you try to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="7c8e4-137">You can also select the notification icon to see the error messages.</span><span class="sxs-lookup"><span data-stu-id="7c8e4-137">You can also select the notification icon to see the error messages.</span></span>

   ![Notification prompt](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="7c8e4-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c8e4-139">Next steps</span></span>
[<span data-ttu-id="7c8e4-140">Publish applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="7c8e4-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
