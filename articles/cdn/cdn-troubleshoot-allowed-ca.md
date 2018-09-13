---
title: Allowed certificate authorities for enabling custom HTTPS on Azure CDN | Microsoft Docs
description: If you are using your own certificate to enable HTTPS on a custom domain, you must use an allowed certificate authority (CA) to create it.
services: cdn
documentationcenter: ''
author: KumudD
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 28d6d24266c11b1295c57c8ec46c2bd5ec690b28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869211"
---
# <a name="allowed-certificate-authorities-for-enabling-custom-https-on-azure-cdn"></a><span data-ttu-id="18a2a-103">Allowed certificate authorities for enabling custom HTTPS on Azure CDN</span><span class="sxs-lookup"><span data-stu-id="18a2a-103">Allowed certificate authorities for enabling custom HTTPS on Azure CDN</span></span>

<span data-ttu-id="18a2a-104">For an Azure Content Delivery Network (CDN) custom domain on an **Azure CDN Standard from Microsoft** endpoint, when you [enable the HTTPS feature by using your own certificate](cdn-custom-ssl.md?tabs=option-2-enable-https-with-your-own-certificate#ssl-certificates), you must use an allowed certificate authority (CA) to create your SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="18a2a-104">For an Azure Content Delivery Network (CDN) custom domain on an **Azure CDN Standard from Microsoft** endpoint, when you [enable the HTTPS feature by using your own certificate](cdn-custom-ssl.md?tabs=option-2-enable-https-with-your-own-certificate#ssl-certificates), you must use an allowed certificate authority (CA) to create your SSL certificate.</span></span> <span data-ttu-id="18a2a-105">Otherwise, if you use a non-allowed CA or a self-signed certificate, your request will be rejected.</span><span class="sxs-lookup"><span data-stu-id="18a2a-105">Otherwise, if you use a non-allowed CA or a self-signed certificate, your request will be rejected.</span></span>

> [!NOTE]
> <span data-ttu-id="18a2a-106">The option of using your own certificate to enable custom HTTPS is available only with **Azure CDN Standard from Microsoft** profiles.</span><span class="sxs-lookup"><span data-stu-id="18a2a-106">The option of using your own certificate to enable custom HTTPS is available only with **Azure CDN Standard from Microsoft** profiles.</span></span> 
>

<span data-ttu-id="18a2a-107">The following CAs are allowed when you create your own certificate:</span><span class="sxs-lookup"><span data-stu-id="18a2a-107">The following CAs are allowed when you create your own certificate:</span></span>

- <span data-ttu-id="18a2a-108">AddTrust External CA Root</span><span class="sxs-lookup"><span data-stu-id="18a2a-108">AddTrust External CA Root</span></span>
- <span data-ttu-id="18a2a-109">AP Root CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-109">AP Root CA</span></span>
- <span data-ttu-id="18a2a-110">AP Root Certificate Authority 2013</span><span class="sxs-lookup"><span data-stu-id="18a2a-110">AP Root Certificate Authority 2013</span></span>
- <span data-ttu-id="18a2a-111">AP Root Certificate Authority 2014</span><span class="sxs-lookup"><span data-stu-id="18a2a-111">AP Root Certificate Authority 2014</span></span>
- <span data-ttu-id="18a2a-112">APCA-DM3P</span><span class="sxs-lookup"><span data-stu-id="18a2a-112">APCA-DM3P</span></span>
- <span data-ttu-id="18a2a-113">Autopilot Root CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-113">Autopilot Root CA</span></span>
- <span data-ttu-id="18a2a-114">Baltimore CyberTrust Root</span><span class="sxs-lookup"><span data-stu-id="18a2a-114">Baltimore CyberTrust Root</span></span>
- <span data-ttu-id="18a2a-115">Class 3 Public Primary Certification Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-115">Class 3 Public Primary Certification Authority</span></span>
- <span data-ttu-id="18a2a-116">COMODO RSA Certification Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-116">COMODO RSA Certification Authority</span></span>
- <span data-ttu-id="18a2a-117">COMODO RSA Domain Validation Secure Server CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-117">COMODO RSA Domain Validation Secure Server CA</span></span>
- <span data-ttu-id="18a2a-118">D-TRUST Root Class 3 CA 2 2009</span><span class="sxs-lookup"><span data-stu-id="18a2a-118">D-TRUST Root Class 3 CA 2 2009</span></span>
- <span data-ttu-id="18a2a-119">DigiCert Cloud Services CA-1</span><span class="sxs-lookup"><span data-stu-id="18a2a-119">DigiCert Cloud Services CA-1</span></span>
- <span data-ttu-id="18a2a-120">DigiCert Global Root CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-120">DigiCert Global Root CA</span></span>
- <span data-ttu-id="18a2a-121">DigiCert High Assurance CA-3</span><span class="sxs-lookup"><span data-stu-id="18a2a-121">DigiCert High Assurance CA-3</span></span>
- <span data-ttu-id="18a2a-122">DigiCert High Assurance EV Root CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-122">DigiCert High Assurance EV Root CA</span></span>
- <span data-ttu-id="18a2a-123">DigiCert SHA2 High Assurance Server CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-123">DigiCert SHA2 High Assurance Server CA</span></span>
- <span data-ttu-id="18a2a-124">DigiCert SHA2 Secure Server CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-124">DigiCert SHA2 Secure Server CA</span></span>
- <span data-ttu-id="18a2a-125">GeoTrust Global CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-125">GeoTrust Global CA</span></span>
- <span data-ttu-id="18a2a-126">GeoTrust Primary Certification Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-126">GeoTrust Primary Certification Authority</span></span>
- <span data-ttu-id="18a2a-127">GeoTrust Primary Certification Authority - G2</span><span class="sxs-lookup"><span data-stu-id="18a2a-127">GeoTrust Primary Certification Authority - G2</span></span>
- <span data-ttu-id="18a2a-128">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="18a2a-128">GlobalSign</span></span>
- <span data-ttu-id="18a2a-129">GlobalSign Extended Validation CA - SHA256 - G2</span><span class="sxs-lookup"><span data-stu-id="18a2a-129">GlobalSign Extended Validation CA - SHA256 - G2</span></span>
- <span data-ttu-id="18a2a-130">GlobalSign Organization Validation CA - G2</span><span class="sxs-lookup"><span data-stu-id="18a2a-130">GlobalSign Organization Validation CA - G2</span></span>
- <span data-ttu-id="18a2a-131">GlobalSign Root CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-131">GlobalSign Root CA</span></span>
- <span data-ttu-id="18a2a-132">Go Daddy Root Certificate Authority - G2</span><span class="sxs-lookup"><span data-stu-id="18a2a-132">Go Daddy Root Certificate Authority - G2</span></span>
- <span data-ttu-id="18a2a-133">Microsoft Authenticode(tm) Root Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-133">Microsoft Authenticode(tm) Root Authority</span></span>
- <span data-ttu-id="18a2a-134">Microsoft Exchange Services CA 2015</span><span class="sxs-lookup"><span data-stu-id="18a2a-134">Microsoft Exchange Services CA 2015</span></span>
- <span data-ttu-id="18a2a-135">Microsoft Internal Corporate Root</span><span class="sxs-lookup"><span data-stu-id="18a2a-135">Microsoft Internal Corporate Root</span></span>
- <span data-ttu-id="18a2a-136">Microsoft IT ITO SSL CA 1</span><span class="sxs-lookup"><span data-stu-id="18a2a-136">Microsoft IT ITO SSL CA 1</span></span>
- <span data-ttu-id="18a2a-137">Microsoft IT SSL SHA1</span><span class="sxs-lookup"><span data-stu-id="18a2a-137">Microsoft IT SSL SHA1</span></span>
- <span data-ttu-id="18a2a-138">Microsoft IT SSL SHA2</span><span class="sxs-lookup"><span data-stu-id="18a2a-138">Microsoft IT SSL SHA2</span></span>
- <span data-ttu-id="18a2a-139">Microsoft IT TLS CA 1</span><span class="sxs-lookup"><span data-stu-id="18a2a-139">Microsoft IT TLS CA 1</span></span>
- <span data-ttu-id="18a2a-140">Microsoft IT TLS CA 2</span><span class="sxs-lookup"><span data-stu-id="18a2a-140">Microsoft IT TLS CA 2</span></span>
- <span data-ttu-id="18a2a-141">Microsoft IT TLS CA 4</span><span class="sxs-lookup"><span data-stu-id="18a2a-141">Microsoft IT TLS CA 4</span></span>
- <span data-ttu-id="18a2a-142">Microsoft IT TLS CA 5</span><span class="sxs-lookup"><span data-stu-id="18a2a-142">Microsoft IT TLS CA 5</span></span>
- <span data-ttu-id="18a2a-143">Microsoft Root Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-143">Microsoft Root Authority</span></span>
- <span data-ttu-id="18a2a-144">Microsoft Root Certificate Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-144">Microsoft Root Certificate Authority</span></span>
- <span data-ttu-id="18a2a-145">Microsoft Root Certificate Authority 2010</span><span class="sxs-lookup"><span data-stu-id="18a2a-145">Microsoft Root Certificate Authority 2010</span></span>
- <span data-ttu-id="18a2a-146">Microsoft Root Certificate Authority 2011</span><span class="sxs-lookup"><span data-stu-id="18a2a-146">Microsoft Root Certificate Authority 2011</span></span>
- <span data-ttu-id="18a2a-147">Microsoft Secure Server CA 2011</span><span class="sxs-lookup"><span data-stu-id="18a2a-147">Microsoft Secure Server CA 2011</span></span>
- <span data-ttu-id="18a2a-148">Microsoft Services Partner Root</span><span class="sxs-lookup"><span data-stu-id="18a2a-148">Microsoft Services Partner Root</span></span>
- <span data-ttu-id="18a2a-149">Microsoft Time Stamping Service Root</span><span class="sxs-lookup"><span data-stu-id="18a2a-149">Microsoft Time Stamping Service Root</span></span>
- <span data-ttu-id="18a2a-150">Microsoft Windows Hardware Compatibility</span><span class="sxs-lookup"><span data-stu-id="18a2a-150">Microsoft Windows Hardware Compatibility</span></span>
- <span data-ttu-id="18a2a-151">MSIT CA Z2</span><span class="sxs-lookup"><span data-stu-id="18a2a-151">MSIT CA Z2</span></span>
- <span data-ttu-id="18a2a-152">MSIT Enterprise CA 1</span><span class="sxs-lookup"><span data-stu-id="18a2a-152">MSIT Enterprise CA 1</span></span>
- <span data-ttu-id="18a2a-153">MSIT Enterprise CA 3</span><span class="sxs-lookup"><span data-stu-id="18a2a-153">MSIT Enterprise CA 3</span></span>
- <span data-ttu-id="18a2a-154">Root Agency</span><span class="sxs-lookup"><span data-stu-id="18a2a-154">Root Agency</span></span>
- <span data-ttu-id="18a2a-155">Symantec Class 3 EV SSL CA - G3</span><span class="sxs-lookup"><span data-stu-id="18a2a-155">Symantec Class 3 EV SSL CA - G3</span></span>
- <span data-ttu-id="18a2a-156">Symantec Class 3 Secure Server CA - G4</span><span class="sxs-lookup"><span data-stu-id="18a2a-156">Symantec Class 3 Secure Server CA - G4</span></span>
- <span data-ttu-id="18a2a-157">Symantec Enterprise Mobile Root for Microsoft</span><span class="sxs-lookup"><span data-stu-id="18a2a-157">Symantec Enterprise Mobile Root for Microsoft</span></span>
- <span data-ttu-id="18a2a-158">Thawte Primary Root CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-158">Thawte Primary Root CA</span></span>
- <span data-ttu-id="18a2a-159">Thawte Primary Root CA - G2</span><span class="sxs-lookup"><span data-stu-id="18a2a-159">Thawte Primary Root CA - G2</span></span>
- <span data-ttu-id="18a2a-160">Thawte Primary Root CA - G3</span><span class="sxs-lookup"><span data-stu-id="18a2a-160">Thawte Primary Root CA - G3</span></span>
- <span data-ttu-id="18a2a-161">Thawte Timestamping CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-161">Thawte Timestamping CA</span></span>
- <span data-ttu-id="18a2a-162">UTN-USERFirst-Object</span><span class="sxs-lookup"><span data-stu-id="18a2a-162">UTN-USERFirst-Object</span></span>
- <span data-ttu-id="18a2a-163">VeriSign Class 3 Extended Validation SSL CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-163">VeriSign Class 3 Extended Validation SSL CA</span></span>
- <span data-ttu-id="18a2a-164">VeriSign Class 3 Extended Validation SSL SGC CA</span><span class="sxs-lookup"><span data-stu-id="18a2a-164">VeriSign Class 3 Extended Validation SSL SGC CA</span></span>
- <span data-ttu-id="18a2a-165">VeriSign Class 3 Public Primary Certification Authority - G5</span><span class="sxs-lookup"><span data-stu-id="18a2a-165">VeriSign Class 3 Public Primary Certification Authority - G5</span></span>
- <span data-ttu-id="18a2a-166">VeriSign International Server CA - Class 3</span><span class="sxs-lookup"><span data-stu-id="18a2a-166">VeriSign International Server CA - Class 3</span></span>
- <span data-ttu-id="18a2a-167">VeriSign Time Stamping Service Root</span><span class="sxs-lookup"><span data-stu-id="18a2a-167">VeriSign Time Stamping Service Root</span></span>
- <span data-ttu-id="18a2a-168">VeriSign Universal Root Certification Authority</span><span class="sxs-lookup"><span data-stu-id="18a2a-168">VeriSign Universal Root Certification Authority</span></span>
- <span data-ttu-id="18a2a-169">WMSvc-SHA2-DALEDGE1008</span><span class="sxs-lookup"><span data-stu-id="18a2a-169">WMSvc-SHA2-DALEDGE1008</span></span>

