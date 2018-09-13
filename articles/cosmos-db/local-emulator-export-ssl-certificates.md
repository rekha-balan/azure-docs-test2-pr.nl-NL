---
title: Export the Azure Cosmos DB Emulator certificates | Microsoft Docs
description: When developing in languages and runtimes that do not use the Windows Certificate Store you will need to export and manage the SSL certificates. This post gives step by step instructions.
services: cosmos-db
keywords: Azure Cosmos DB Emulator
author: David-Noble-at-work
manager: kfile
editor: ''
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.date: 06/06/2017
ms.author: danoble
ms.openlocfilehash: 45a909b910fe45d87833b0f3c6ba652503a1d212
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857364"
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="eb764-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span><span class="sxs-lookup"><span data-stu-id="eb764-105">Export the Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="eb764-106">**Download the Emulator**</span><span class="sxs-lookup"><span data-stu-id="eb764-106">**Download the Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="eb764-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span><span class="sxs-lookup"><span data-stu-id="eb764-107">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="eb764-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="eb764-108">This post demonstrates how to export the SSL certificates for use in languages and runtimes that do not integrate with the Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="eb764-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="eb764-109">You can read more about the emulator in [Use the Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="eb764-110">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="eb764-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb764-111">Rotating certificates</span><span class="sxs-lookup"><span data-stu-id="eb764-111">Rotating certificates</span></span>
> * <span data-ttu-id="eb764-112">Exporting SSL certificate</span><span class="sxs-lookup"><span data-stu-id="eb764-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="eb764-113">Learning how to use the certificate in Java, Python, and Node.js</span><span class="sxs-lookup"><span data-stu-id="eb764-113">Learning how to use the certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="eb764-114">Certification rotation</span><span class="sxs-lookup"><span data-stu-id="eb764-114">Certification rotation</span></span>

<span data-ttu-id="eb764-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span><span class="sxs-lookup"><span data-stu-id="eb764-115">Certificates in the Azure Cosmos DB Local Emulator are generated the first time the emulator is run.</span></span> <span data-ttu-id="eb764-116">There are two certificates.</span><span class="sxs-lookup"><span data-stu-id="eb764-116">There are two certificates.</span></span> <span data-ttu-id="eb764-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span><span class="sxs-lookup"><span data-stu-id="eb764-117">One used for connecting to the local emulator and one for managing secrets within the emulator.</span></span> <span data-ttu-id="eb764-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span><span class="sxs-lookup"><span data-stu-id="eb764-118">The certificate you want to export is the connection certificate with the friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="eb764-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span><span class="sxs-lookup"><span data-stu-id="eb764-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in the Windows Tray.</span></span> <span data-ttu-id="eb764-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span><span class="sxs-lookup"><span data-stu-id="eb764-120">If you regenerate the certificates and have installed them into the Java certificate store or used them elsewhere you will need to update them, otherwise your application will no longer connect to the local emulator.</span></span>

![Azure Cosmos DB local emulator reset data](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="eb764-122">How to export the Azure Cosmos DB SSL certificate</span><span class="sxs-lookup"><span data-stu-id="eb764-122">How to export the Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="eb764-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="eb764-123">Start the Windows Certificate manager by running certlm.msc and navigate to the Personal->Certificates folder and open the certificate with the friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Azure Cosmos DB local emulator export step 1](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="eb764-125">Click on **Details** then **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb764-125">Click on **Details** then **OK**.</span></span>

    ![Azure Cosmos DB local emulator export step 2](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="eb764-127">Click **Copy to File...**.</span><span class="sxs-lookup"><span data-stu-id="eb764-127">Click **Copy to File...**.</span></span>

    ![Azure Cosmos DB local emulator export step 3](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="eb764-129">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb764-129">Click **Next**.</span></span>

    ![Azure Cosmos DB local emulator export step 4](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="eb764-131">Click **No, do not export private key**, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb764-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Azure Cosmos DB local emulator export step 5](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="eb764-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb764-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Azure Cosmos DB local emulator export step 6](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="eb764-135">Give the certificate a name.</span><span class="sxs-lookup"><span data-stu-id="eb764-135">Give the certificate a name.</span></span> <span data-ttu-id="eb764-136">In this case **documentdbemulatorcert** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb764-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Azure Cosmos DB local emulator export step 7](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="eb764-138">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="eb764-138">Click **Finish**.</span></span>

    ![Azure Cosmos DB local emulator export step 8](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a><span data-ttu-id="eb764-140">How to use the certificate in Java</span><span class="sxs-lookup"><span data-stu-id="eb764-140">How to use the certificate in Java</span></span>

<span data-ttu-id="eb764-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span><span class="sxs-lookup"><span data-stu-id="eb764-141">When running Java applications or MongoDB applications that use the Java client it is easier to install the certificate into the Java default certificate store than passing the "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="eb764-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span><span class="sxs-lookup"><span data-stu-id="eb764-142">For example the included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on the default certificate store.</span></span>

<span data-ttu-id="eb764-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span><span class="sxs-lookup"><span data-stu-id="eb764-143">Follow the instructions in the [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) to import the X.509 certificate into the default Java certificate store.</span></span> <span data-ttu-id="eb764-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span><span class="sxs-lookup"><span data-stu-id="eb764-144">Keep in mind you will be working in the %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="eb764-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="eb764-145">Once the "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able to connect and use the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="eb764-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span><span class="sxs-lookup"><span data-stu-id="eb764-146">If you continue to have trouble you may want to follow the [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="eb764-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span><span class="sxs-lookup"><span data-stu-id="eb764-147">It is very likely the certificate is not installed into the %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="eb764-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span><span class="sxs-lookup"><span data-stu-id="eb764-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than the one you updated.</span></span>

## <a name="how-to-use-the-certificate-in-python"></a><span data-ttu-id="eb764-149">How to use the certificate in Python</span><span class="sxs-lookup"><span data-stu-id="eb764-149">How to use the certificate in Python</span></span>

<span data-ttu-id="eb764-150">By default the [Python SDK(version 2.0.0 or higher)](sql-api-sdk-python.md) for the SQL API will not try and use the SSL certificate when connecting to the local emulator.</span><span class="sxs-lookup"><span data-stu-id="eb764-150">By default the [Python SDK(version 2.0.0 or higher)](sql-api-sdk-python.md) for the SQL API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="eb764-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span><span class="sxs-lookup"><span data-stu-id="eb764-151">If however you want to use SSL validation you can follow the examples in the [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-to-use-the-certificate-in-nodejs"></a><span data-ttu-id="eb764-152">How to use the certificate in Node.js</span><span class="sxs-lookup"><span data-stu-id="eb764-152">How to use the certificate in Node.js</span></span>

<span data-ttu-id="eb764-153">By default the [Node.js SDK(version 1.10.1 or higher)](sql-api-sdk-node.md) for the SQL API will not try and use the SSL certificate when connecting to the local emulator.</span><span class="sxs-lookup"><span data-stu-id="eb764-153">By default the [Node.js SDK(version 1.10.1 or higher)](sql-api-sdk-node.md) for the SQL API will not try and use the SSL certificate when connecting to the local emulator.</span></span> <span data-ttu-id="eb764-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="eb764-154">If however you want to use SSL validation you can follow the examples in the [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb764-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb764-155">Next steps</span></span>

<span data-ttu-id="eb764-156">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="eb764-156">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb764-157">Rotated certificates</span><span class="sxs-lookup"><span data-stu-id="eb764-157">Rotated certificates</span></span>
> * <span data-ttu-id="eb764-158">Exported the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="eb764-158">Exported the SSL certificate</span></span>
> * <span data-ttu-id="eb764-159">Learned how to use the certificate in Java, Python and Node.js</span><span class="sxs-lookup"><span data-stu-id="eb764-159">Learned how to use the certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="eb764-160">You can now proceed to the concepts section for more information about Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eb764-160">You can now proceed to the concepts section for more information about Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="eb764-161">Tunable data consistency levels in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eb764-161">Tunable data consistency levels in Azure Cosmos DB</span></span>](../cosmos-db/consistency-levels.md)
