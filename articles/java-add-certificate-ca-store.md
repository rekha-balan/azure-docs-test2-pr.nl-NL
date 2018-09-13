---
title: Add a certificate to the Java CA store | Microsoft Docs
description: Learn how to add a certificate authority (CA) certificate to the Java CA certificate (cacerts) store for Twilio service or Azure Service Bus.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 3e71e6f7e052d5d19a87d3467e23bc4156f436dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661118"
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="6b0de-103">Adding a Certificate to the Java CA Certificates Store</span><span class="sxs-lookup"><span data-stu-id="6b0de-103">Adding a Certificate to the Java CA Certificates Store</span></span>
<span data-ttu-id="6b0de-104">The following steps show you how to add a certificate authority (CA) certificate to the Java CA certificate (cacerts) store.</span><span class="sxs-lookup"><span data-stu-id="6b0de-104">The following steps show you how to add a certificate authority (CA) certificate to the Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="6b0de-105">The example used is for the CA certificate required by the Twilio service.</span><span class="sxs-lookup"><span data-stu-id="6b0de-105">The example used is for the CA certificate required by the Twilio service.</span></span> <span data-ttu-id="6b0de-106">Information provided later in the topic describes how to install the CA certificate for the Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6b0de-106">Information provided later in the topic describes how to install the CA certificate for the Azure Service Bus.</span></span> 

<span data-ttu-id="6b0de-107">You can use keytool to add the CA certificate prior to zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span><span class="sxs-lookup"><span data-stu-id="6b0de-107">You can use keytool to add the CA certificate prior to zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span> <span data-ttu-id="6b0de-108">This example assumes you will add a CA certificate prior to the JDK being zipped.</span><span class="sxs-lookup"><span data-stu-id="6b0de-108">This example assumes you will add a CA certificate prior to the JDK being zipped.</span></span> <span data-ttu-id="6b0de-109">Also, a specific CA certificate will be used in the example, but the steps of obtaining a different CA certificate and importing it into the cacerts store would be similar.</span><span class="sxs-lookup"><span data-stu-id="6b0de-109">Also, a specific CA certificate will be used in the example, but the steps of obtaining a different CA certificate and importing it into the cacerts store would be similar.</span></span>

## <a name="to-add-a-certificate-to-the-cacerts-store"></a><span data-ttu-id="6b0de-110">To add a certificate to the cacerts store</span><span class="sxs-lookup"><span data-stu-id="6b0de-110">To add a certificate to the cacerts store</span></span>
1. <span data-ttu-id="6b0de-111">At a command prompt that is set to your JDK's **jdk\jre\lib\security** folder, run the following to see what certificates are installed:</span><span class="sxs-lookup"><span data-stu-id="6b0de-111">At a command prompt that is set to your JDK's **jdk\jre\lib\security** folder, run the following to see what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="6b0de-112">You'll be prompted for the store password.</span><span class="sxs-lookup"><span data-stu-id="6b0de-112">You'll be prompted for the store password.</span></span> <span data-ttu-id="6b0de-113">The default password is **changeit**.</span><span class="sxs-lookup"><span data-stu-id="6b0de-113">The default password is **changeit**.</span></span> <span data-ttu-id="6b0de-114">(If you want to change the password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that the certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want to import it (this particular certificate is needed by the Twilio API service).</span><span class="sxs-lookup"><span data-stu-id="6b0de-114">(If you want to change the password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that the certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want to import it (this particular certificate is needed by the Twilio API service).</span></span>
2. <span data-ttu-id="6b0de-115">Obtain the certificate from the list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="6b0de-115">Obtain the certificate from the list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="6b0de-116">Right-click the link for the certificate with serial number 35:DE:F4:CF and save it to the **jdk\jre\lib\security** folder.</span><span class="sxs-lookup"><span data-stu-id="6b0de-116">Right-click the link for the certificate with serial number 35:DE:F4:CF and save it to the **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="6b0de-117">For purposes of this example, it was saved to a file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span><span class="sxs-lookup"><span data-stu-id="6b0de-117">For purposes of this example, it was saved to a file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="6b0de-118">Import the certificate via the following command:</span><span class="sxs-lookup"><span data-stu-id="6b0de-118">Import the certificate via the following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="6b0de-119">When prompted to trust this certificate, if the certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span><span class="sxs-lookup"><span data-stu-id="6b0de-119">When prompted to trust this certificate, if the certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="6b0de-120">Run the following command to ensure the CA certificate has been successfully imported:</span><span class="sxs-lookup"><span data-stu-id="6b0de-120">Run the following command to ensure the CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="6b0de-121">Zip the JDK and add it to your Azure project's **approot** folder.</span><span class="sxs-lookup"><span data-stu-id="6b0de-121">Zip the JDK and add it to your Azure project's **approot** folder.</span></span>

<span data-ttu-id="6b0de-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="6b0de-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="6b0de-123">Azure Root Certificates</span><span class="sxs-lookup"><span data-stu-id="6b0de-123">Azure Root Certificates</span></span>
<span data-ttu-id="6b0de-124">Your applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust Root certificate.</span><span class="sxs-lookup"><span data-stu-id="6b0de-124">Your applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="6b0de-125">(Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global Root to the Baltimore CyberTrust Root.</span><span class="sxs-lookup"><span data-stu-id="6b0de-125">(Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global Root to the Baltimore CyberTrust Root.</span></span> <span data-ttu-id="6b0de-126">This migration took several months to complete.)</span><span class="sxs-lookup"><span data-stu-id="6b0de-126">This migration took several months to complete.)</span></span>

<span data-ttu-id="6b0de-127">The Baltimore certificate might already be installed in your cacerts store, so remember to run the **keytool -list** command first to see if it already exists.</span><span class="sxs-lookup"><span data-stu-id="6b0de-127">The Baltimore certificate might already be installed in your cacerts store, so remember to run the **keytool -list** command first to see if it already exists.</span></span>

<span data-ttu-id="6b0de-128">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span><span class="sxs-lookup"><span data-stu-id="6b0de-128">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="6b0de-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved to a local file with extension **.cer**, and then imported using **keytool** as shown above.</span><span class="sxs-lookup"><span data-stu-id="6b0de-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved to a local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b0de-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b0de-130">Next steps</span></span>
<span data-ttu-id="6b0de-131">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b0de-131">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="6b0de-132">For more information about Java, see the [Java Developer Center](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="6b0de-132">For more information about Java, see the [Java Developer Center](/develop/java/).</span></span>

