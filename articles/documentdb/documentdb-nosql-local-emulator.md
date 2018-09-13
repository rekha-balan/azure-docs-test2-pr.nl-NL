---
title: Develop locally with the DocumentDB Emulator | Microsoft Docs
description: Using the DocumentDB Emulator, you can develop and test your application locally for free, without creating an Azure subscription.
services: documentdb
documentationcenter: ''
keywords: DocumentDB Emulator
author: arramac
manager: jhubbard
editor: ''
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: documentdb
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: arramac
ms.openlocfilehash: c9912af568e302fc896085e59991d1ed01b54a1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550459"
---
# <a name="use-the-azure-documentdb-emulator-for-development-and-testing"></a><span data-ttu-id="8f39b-104">Use the Azure DocumentDB Emulator for development and testing</span><span class="sxs-lookup"><span data-stu-id="8f39b-104">Use the Azure DocumentDB Emulator for development and testing</span></span>

[<span data-ttu-id="8f39b-105">**Download the Emulator**</span><span class="sxs-lookup"><span data-stu-id="8f39b-105">**Download the Emulator**</span></span>](https://aka.ms/documentdb-emulator)

<span data-ttu-id="8f39b-106">The Azure DocumentDB Emulator provides a local environment that emulates the Azure DocumentDB service for development purposes.</span><span class="sxs-lookup"><span data-stu-id="8f39b-106">The Azure DocumentDB Emulator provides a local environment that emulates the Azure DocumentDB service for development purposes.</span></span> <span data-ttu-id="8f39b-107">Using the DocumentDB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span><span class="sxs-lookup"><span data-stu-id="8f39b-107">Using the DocumentDB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="8f39b-108">When you're satisfied with how your application is working in the DocumentDB Emulator, you can switch to using an Azure DocumentDB account in the cloud.</span><span class="sxs-lookup"><span data-stu-id="8f39b-108">When you're satisfied with how your application is working in the DocumentDB Emulator, you can switch to using an Azure DocumentDB account in the cloud.</span></span>

<span data-ttu-id="8f39b-109">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-109">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the DocumentDB Emulator.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="system-requirements"></a><span data-ttu-id="8f39b-110">System requirements</span><span class="sxs-lookup"><span data-stu-id="8f39b-110">System requirements</span></span>
<span data-ttu-id="8f39b-111">The DocumentDB Emulator has the following hardware and software requirements:</span><span class="sxs-lookup"><span data-stu-id="8f39b-111">The DocumentDB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="8f39b-112">Software requirements</span><span class="sxs-lookup"><span data-stu-id="8f39b-112">Software requirements</span></span>
  * <span data-ttu-id="8f39b-113">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span><span class="sxs-lookup"><span data-stu-id="8f39b-113">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="8f39b-114">Minimum Hardware requirements</span><span class="sxs-lookup"><span data-stu-id="8f39b-114">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="8f39b-115">2 GB RAM</span><span class="sxs-lookup"><span data-stu-id="8f39b-115">2 GB RAM</span></span>
  * <span data-ttu-id="8f39b-116">10 GB available hard disk space</span><span class="sxs-lookup"><span data-stu-id="8f39b-116">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="8f39b-117">Installation</span><span class="sxs-lookup"><span data-stu-id="8f39b-117">Installation</span></span>
<span data-ttu-id="8f39b-118">You can download and install the DocumentDB Emulator from the [Microsoft Download Center](https://aka.ms/documentdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="8f39b-118">You can download and install the DocumentDB Emulator from the [Microsoft Download Center](https://aka.ms/documentdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="8f39b-119">To install, configure, and run the DocumentDB Emulator, you must have administrative privileges on the computer.</span><span class="sxs-lookup"><span data-stu-id="8f39b-119">To install, configure, and run the DocumentDB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="8f39b-120">Running on Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="8f39b-120">Running on Docker for Windows</span></span>

<span data-ttu-id="8f39b-121">The DocumentDB Emulator can be run on Docker for Windows.</span><span class="sxs-lookup"><span data-stu-id="8f39b-121">The DocumentDB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="8f39b-122">The Emulator does not work on Docker for Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="8f39b-122">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="8f39b-123">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span><span class="sxs-lookup"><span data-stu-id="8f39b-123">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull mominag/documentdb_emulator 
```
<span data-ttu-id="8f39b-124">To start the image, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="8f39b-124">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\DocumentDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\DocumentDBEmulatorCert:c:\DocumentDBEmulator\DocumentDBEmulatorCert -P -t -i mominag/documentdb_emulator
```

<span data-ttu-id="8f39b-125">The response looks similar to the following:</span><span class="sxs-lookup"><span data-stu-id="8f39b-125">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\DocumentDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="8f39b-126">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span><span class="sxs-lookup"><span data-stu-id="8f39b-126">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="8f39b-127">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span><span class="sxs-lookup"><span data-stu-id="8f39b-127">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="8f39b-128">To import the SSL certificate, do the following from an admin command prompt:</span><span class="sxs-lookup"><span data-stu-id="8f39b-128">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\DocumentDBEmulatorCert
powershell .\importcert.ps1
```

## <a name="checking-for-updates"></a><span data-ttu-id="8f39b-129">Checking for updates</span><span class="sxs-lookup"><span data-stu-id="8f39b-129">Checking for updates</span></span>
<span data-ttu-id="8f39b-130">The DocumentDB Emulator includes a built-in Azure DocumentDB Data Explorer to browse data stored within DocumentDB, create new collections, and let you know when a new update is available for download.</span><span class="sxs-lookup"><span data-stu-id="8f39b-130">The DocumentDB Emulator includes a built-in Azure DocumentDB Data Explorer to browse data stored within DocumentDB, create new collections, and let you know when a new update is available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="8f39b-131">Data created in one version of the DocumentDB Emulator is not guaranteed to be accessible when using a different version.</span><span class="sxs-lookup"><span data-stu-id="8f39b-131">Data created in one version of the DocumentDB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="8f39b-132">If you need to persist your data for the long term, it is recommended that you store that data in an Azure DocumentDB account, rather than in the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-132">If you need to persist your data for the long term, it is recommended that you store that data in an Azure DocumentDB account, rather than in the DocumentDB Emulator.</span></span> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="8f39b-133">How the Emulator works</span><span class="sxs-lookup"><span data-stu-id="8f39b-133">How the Emulator works</span></span>
<span data-ttu-id="8f39b-134">The DocumentDB Emulator provides a high-fidelity emulation of the DocumentDB service.</span><span class="sxs-lookup"><span data-stu-id="8f39b-134">The DocumentDB Emulator provides a high-fidelity emulation of the DocumentDB service.</span></span> <span data-ttu-id="8f39b-135">It supports identical functionality as Azure DocumentDB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="8f39b-135">It supports identical functionality as Azure DocumentDB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="8f39b-136">You can develop and test applications using the DocumentDB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8f39b-136">You can develop and test applications using the DocumentDB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for DocumentDB.</span></span>

<span data-ttu-id="8f39b-137">While we created a high-fidelity local emulation of the actual DocumentDB service, the implementation of the DocumentDB Emulator is different than that of the service.</span><span class="sxs-lookup"><span data-stu-id="8f39b-137">While we created a high-fidelity local emulation of the actual DocumentDB service, the implementation of the DocumentDB Emulator is different than that of the service.</span></span> <span data-ttu-id="8f39b-138">For example, the DocumentDB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span><span class="sxs-lookup"><span data-stu-id="8f39b-138">For example, the DocumentDB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="8f39b-139">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-139">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the DocumentDB Emulator.</span></span>


## <a name="authenticating-requests"></a><span data-ttu-id="8f39b-140">Authenticating requests</span><span class="sxs-lookup"><span data-stu-id="8f39b-140">Authenticating requests</span></span>
<span data-ttu-id="8f39b-141">Just as with Azure Document in the cloud, every request that you make against the DocumentDB Emulator must be authenticated.</span><span class="sxs-lookup"><span data-stu-id="8f39b-141">Just as with Azure Document in the cloud, every request that you make against the DocumentDB Emulator must be authenticated.</span></span> <span data-ttu-id="8f39b-142">The DocumentDB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span><span class="sxs-lookup"><span data-stu-id="8f39b-142">The DocumentDB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="8f39b-143">This account and key are the only credentials permitted for use with the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-143">This account and key are the only credentials permitted for use with the DocumentDB Emulator.</span></span> <span data-ttu-id="8f39b-144">They are:</span><span class="sxs-lookup"><span data-stu-id="8f39b-144">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="8f39b-145">The master key supported by the DocumentDB Emulator is intended for use only with the emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-145">The master key supported by the DocumentDB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="8f39b-146">You cannot use your production DocumentDB account and key with the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-146">You cannot use your production DocumentDB account and key with the DocumentDB Emulator.</span></span> 

<span data-ttu-id="8f39b-147">Additionally, just as the Azure DocumentDB service, the DocumentDB Emulator supports only secure communication via SSL.</span><span class="sxs-lookup"><span data-stu-id="8f39b-147">Additionally, just as the Azure DocumentDB service, the DocumentDB Emulator supports only secure communication via SSL.</span></span>

## <a name="start-and-initialize-the-emulator"></a><span data-ttu-id="8f39b-148">Start and initialize the Emulator</span><span class="sxs-lookup"><span data-stu-id="8f39b-148">Start and initialize the Emulator</span></span>

<span data-ttu-id="8f39b-149">To start the Azure DocumentDB Emulator, select the Start button or press the Windows key.</span><span class="sxs-lookup"><span data-stu-id="8f39b-149">To start the Azure DocumentDB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="8f39b-150">Begin typing **DocumentDB Emulator**, and select the emulator from the list of applications.</span><span class="sxs-lookup"><span data-stu-id="8f39b-150">Begin typing **DocumentDB Emulator**, and select the emulator from the list of applications.</span></span> 

![Select the Start button or press the Windows key, begin typing **DocumentDB Emulator**, and select the emulator from the list of applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-start.png)

<span data-ttu-id="8f39b-152">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span><span class="sxs-lookup"><span data-stu-id="8f39b-152">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> <span data-ttu-id="8f39b-153">The DocumentDB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span><span class="sxs-lookup"><span data-stu-id="8f39b-153">The DocumentDB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

![DocumentDB local emulator taskbar notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-taskbar.png)

<span data-ttu-id="8f39b-155">The DocumentDB Emulator is installed by default to the `C:\Program Files\DocumentDB Emulator` directory.</span><span class="sxs-lookup"><span data-stu-id="8f39b-155">The DocumentDB Emulator is installed by default to the `C:\Program Files\DocumentDB Emulator` directory.</span></span> <span data-ttu-id="8f39b-156">You can also start and stop the emulator from the command-line.</span><span class="sxs-lookup"><span data-stu-id="8f39b-156">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="8f39b-157">See [command-line tool reference](#command-line) for more information.</span><span class="sxs-lookup"><span data-stu-id="8f39b-157">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="8f39b-158">Start Data Explorer</span><span class="sxs-lookup"><span data-stu-id="8f39b-158">Start Data Explorer</span></span>

<span data-ttu-id="8f39b-159">When the DocumentDB emulator launches it will automatically open the DocumentDB Data Explorer in your browser.</span><span class="sxs-lookup"><span data-stu-id="8f39b-159">When the DocumentDB emulator launches it will automatically open the DocumentDB Data Explorer in your browser.</span></span> <span data-ttu-id="8f39b-160">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="8f39b-160">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="8f39b-161">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the DocumentDB Emulator in the Windows Tray Icon as shown below.</span><span class="sxs-lookup"><span data-stu-id="8f39b-161">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the DocumentDB Emulator in the Windows Tray Icon as shown below.</span></span>

![DocumentDB local emulator data explorer launcher](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-data-explorer-launcher.png)

## <a name="developing-with-the-emulator"></a><span data-ttu-id="8f39b-163">Developing with the Emulator</span><span class="sxs-lookup"><span data-stu-id="8f39b-163">Developing with the Emulator</span></span>
<span data-ttu-id="8f39b-164">Once you have the DocumentDB Emulator running on your desktop, you can use any supported [DocumentDB SDK](documentdb-sdk-dotnet.md) or the [DocumentDB REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx) to interact with the Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-164">Once you have the DocumentDB Emulator running on your desktop, you can use any supported [DocumentDB SDK](documentdb-sdk-dotnet.md) or the [DocumentDB REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx) to interact with the Emulator.</span></span> <span data-ttu-id="8f39b-165">The DocumentDB Emulator also includes a built-in Data Explorer that lets you create collections, view and edit documents without writing any code.</span><span class="sxs-lookup"><span data-stu-id="8f39b-165">The DocumentDB Emulator also includes a built-in Data Explorer that lets you create collections, view and edit documents without writing any code.</span></span> 

    // Connect to the DocumentDB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="8f39b-166">If you're using [DocumentDB protocol support for MongoDB](documentdb-protocol-mongodb.md), please use the following connection string:</span><span class="sxs-lookup"><span data-stu-id="8f39b-166">If you're using [DocumentDB protocol support for MongoDB](documentdb-protocol-mongodb.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10250/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="8f39b-167">You can use existing tools like [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-167">You can use existing tools like [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the DocumentDB Emulator.</span></span> <span data-ttu-id="8f39b-168">You can also migrate data between the DocumentDB Emulator and the Azure DocumentDB service using the [DocumentDB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="8f39b-168">You can also migrate data between the DocumentDB Emulator and the Azure DocumentDB service using the [DocumentDB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

<span data-ttu-id="8f39b-169">Using the DocumentDB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span><span class="sxs-lookup"><span data-stu-id="8f39b-169">Using the DocumentDB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="8f39b-170">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="8f39b-170">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="8f39b-171">Export the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="8f39b-171">Export the SSL certificate</span></span>

<span data-ttu-id="8f39b-172">.NET languages and runtime use the Windows Certificate Store to securely connect to the DocumentDB local emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-172">.NET languages and runtime use the Windows Certificate Store to securely connect to the DocumentDB local emulator.</span></span> <span data-ttu-id="8f39b-173">Other languages have their own method of managing and using certificates.</span><span class="sxs-lookup"><span data-stu-id="8f39b-173">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="8f39b-174">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="8f39b-174">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="8f39b-175">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span><span class="sxs-lookup"><span data-stu-id="8f39b-175">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="8f39b-176">You can start it by running certlm.msc or follow the step by step instructions in [Export the DocumentDB Emulator Certificates](./documentdb-nosql-local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="8f39b-176">You can start it by running certlm.msc or follow the step by step instructions in [Export the DocumentDB Emulator Certificates](./documentdb-nosql-local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="8f39b-177">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span><span class="sxs-lookup"><span data-stu-id="8f39b-177">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![DocumentDB local emulator SSL certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-local-emulator/azure-documentdb-database-local-emulator-ssl_certificate.png)

<span data-ttu-id="8f39b-179">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/en-us/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="8f39b-179">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/en-us/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="8f39b-180">Once the certificate is imported into the cacerts store Java and MongoDB applications will be able to connect to the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-180">Once the certificate is imported into the cacerts store Java and MongoDB applications will be able to connect to the DocumentDB Emulator.</span></span>

<span data-ttu-id="8f39b-181">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span><span class="sxs-lookup"><span data-stu-id="8f39b-181">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <a id="command-line"></a><span data-ttu-id="8f39b-182">Command-line tool reference</span><span class="sxs-lookup"><span data-stu-id="8f39b-182">Command-line tool reference</span></span>
<span data-ttu-id="8f39b-183">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span><span class="sxs-lookup"><span data-stu-id="8f39b-183">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="8f39b-184">Command-line Syntax</span><span class="sxs-lookup"><span data-stu-id="8f39b-184">Command-line Syntax</span></span>

    DocumentDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="8f39b-185">To view the list of options, type `DocumentDB.Emulator.exe /?` at the command prompt.</span><span class="sxs-lookup"><span data-stu-id="8f39b-185">To view the list of options, type `DocumentDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="8f39b-186"><strong>Option</strong></span><span class="sxs-lookup"><span data-stu-id="8f39b-186"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="8f39b-187"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="8f39b-187"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="8f39b-188"><strong>Command</strong></span><span class="sxs-lookup"><span data-stu-id="8f39b-188"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="8f39b-189"><strong>Arguments</strong></span><span class="sxs-lookup"><span data-stu-id="8f39b-189"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-190">[No arguments]</span><span class="sxs-lookup"><span data-stu-id="8f39b-190">[No arguments]</span></span></td>
  <td><span data-ttu-id="8f39b-191">Starts up the DocumentDB Emulator with default settings.</span><span class="sxs-lookup"><span data-stu-id="8f39b-191">Starts up the DocumentDB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="8f39b-192">DocumentDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="8f39b-192">DocumentDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-193">[Help]</span><span class="sxs-lookup"><span data-stu-id="8f39b-193">[Help]</span></span></td>
  <td><span data-ttu-id="8f39b-194">Displays the list of supported command-line arguments.</span><span class="sxs-lookup"><span data-stu-id="8f39b-194">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="8f39b-195">DocumentDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="8f39b-195">DocumentDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-196">Shutdown</span><span class="sxs-lookup"><span data-stu-id="8f39b-196">Shutdown</span></span></td>
  <td><span data-ttu-id="8f39b-197">Shuts down the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-197">Shuts down the DocumentDB Emulator.</span></span></td>
  <td><span data-ttu-id="8f39b-198">DocumentDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="8f39b-198">DocumentDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-199">DataPath</span><span class="sxs-lookup"><span data-stu-id="8f39b-199">DataPath</span></span></td>
  <td><span data-ttu-id="8f39b-200">Specifies the path in which to store data files.</span><span class="sxs-lookup"><span data-stu-id="8f39b-200">Specifies the path in which to store data files.</span></span> <span data-ttu-id="8f39b-201">Default is %LocalAppdata%\DocumentDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-201">Default is %LocalAppdata%\DocumentDBEmulator.</span></span></td>
  <td><span data-ttu-id="8f39b-202">DocumentDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="8f39b-202">DocumentDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="8f39b-203">&lt;datapath&gt;: An accessible path</span><span class="sxs-lookup"><span data-stu-id="8f39b-203">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-204">Port</span><span class="sxs-lookup"><span data-stu-id="8f39b-204">Port</span></span></td>
  <td><span data-ttu-id="8f39b-205">Specifies the port number to use for the emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-205">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="8f39b-206">Default is 8081.</span><span class="sxs-lookup"><span data-stu-id="8f39b-206">Default is 8081.</span></span></td>
  <td><span data-ttu-id="8f39b-207">DocumentDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="8f39b-207">DocumentDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="8f39b-208">&lt;port&gt;: Single port number</span><span class="sxs-lookup"><span data-stu-id="8f39b-208">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-209">MongoPort</span><span class="sxs-lookup"><span data-stu-id="8f39b-209">MongoPort</span></span></td>
  <td><span data-ttu-id="8f39b-210">Specifies the port number to use for MongoDB compatibility API.</span><span class="sxs-lookup"><span data-stu-id="8f39b-210">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="8f39b-211">Default is 10250.</span><span class="sxs-lookup"><span data-stu-id="8f39b-211">Default is 10250.</span></span></td>
  <td><span data-ttu-id="8f39b-212">DocumentDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="8f39b-212">DocumentDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="8f39b-213">&lt;mongoport&gt;: Single port number</span><span class="sxs-lookup"><span data-stu-id="8f39b-213">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-214">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="8f39b-214">DirectPorts</span></span></td>
  <td><span data-ttu-id="8f39b-215">Specifies the ports to use for direct connectivity.</span><span class="sxs-lookup"><span data-stu-id="8f39b-215">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="8f39b-216">Defaults are 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="8f39b-216">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="8f39b-217">DocumentDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="8f39b-217">DocumentDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="8f39b-218">&lt;directports&gt;: Comma-delimited list of 4 ports</span><span class="sxs-lookup"><span data-stu-id="8f39b-218">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-219">Key</span><span class="sxs-lookup"><span data-stu-id="8f39b-219">Key</span></span></td>
  <td><span data-ttu-id="8f39b-220">Authorization key for the emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-220">Authorization key for the emulator.</span></span> <span data-ttu-id="8f39b-221">Key must be the base-64 encoding of a 64-byte vector.</span><span class="sxs-lookup"><span data-stu-id="8f39b-221">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="8f39b-222">DocumentDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="8f39b-222">DocumentDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="8f39b-223">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span><span class="sxs-lookup"><span data-stu-id="8f39b-223">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-224">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="8f39b-224">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="8f39b-225">Specifies that request rate limiting behavior is enabled.</span><span class="sxs-lookup"><span data-stu-id="8f39b-225">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="8f39b-226">DocumentDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="8f39b-226">DocumentDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-227">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="8f39b-227">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="8f39b-228">Specifies that request rate limiting behavior is disabled.</span><span class="sxs-lookup"><span data-stu-id="8f39b-228">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="8f39b-229">DocumentDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="8f39b-229">DocumentDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-230">NoUI</span><span class="sxs-lookup"><span data-stu-id="8f39b-230">NoUI</span></span></td>
  <td><span data-ttu-id="8f39b-231">Do not show the emulator user interface.</span><span class="sxs-lookup"><span data-stu-id="8f39b-231">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="8f39b-232">DocumentDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="8f39b-232">DocumentDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-233">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="8f39b-233">NoExplorer</span></span></td>
  <td><span data-ttu-id="8f39b-234">Don't show document explorer on startup.</span><span class="sxs-lookup"><span data-stu-id="8f39b-234">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="8f39b-235">DocumentDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="8f39b-235">DocumentDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="8f39b-236">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="8f39b-236">PartitionCount</span></span></td>
  <td><span data-ttu-id="8f39b-237">Specifies the maximum number of partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="8f39b-237">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="8f39b-238">See [Change the number of collections](#set-partitioncount) for more information.</span><span class="sxs-lookup"><span data-stu-id="8f39b-238">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="8f39b-239">DocumentDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="8f39b-239">DocumentDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="8f39b-240">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span><span class="sxs-lookup"><span data-stu-id="8f39b-240">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="8f39b-241">Default is 25.</span><span class="sxs-lookup"><span data-stu-id="8f39b-241">Default is 25.</span></span> <span data-ttu-id="8f39b-242">Maximum allowed is 250.</span><span class="sxs-lookup"><span data-stu-id="8f39b-242">Maximum allowed is 250.</span></span></td>
</tr>
</table>

## <a name="differences-between-the-documentdb-emulator-and-azure-documentdb"></a><span data-ttu-id="8f39b-243">Differences between the DocumentDB Emulator and Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8f39b-243">Differences between the DocumentDB Emulator and Azure DocumentDB</span></span> 
<span data-ttu-id="8f39b-244">Because the DocumentDB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure DocumentDB account in the cloud:</span><span class="sxs-lookup"><span data-stu-id="8f39b-244">Because the DocumentDB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure DocumentDB account in the cloud:</span></span>

* <span data-ttu-id="8f39b-245">The DocumentDB Emulator supports only a single fixed account and a well-known master key.</span><span class="sxs-lookup"><span data-stu-id="8f39b-245">The DocumentDB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="8f39b-246">Key regeneration is not possible in the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-246">Key regeneration is not possible in the DocumentDB Emulator.</span></span>
* <span data-ttu-id="8f39b-247">The DocumentDB Emulator is not a scalable service and will not support a large number of collections.</span><span class="sxs-lookup"><span data-stu-id="8f39b-247">The DocumentDB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="8f39b-248">The DocumentDB Emulator does not simulate different [DocumentDB consistency levels](documentdb-consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8f39b-248">The DocumentDB Emulator does not simulate different [DocumentDB consistency levels](documentdb-consistency-levels.md).</span></span>
* <span data-ttu-id="8f39b-249">The DocumentDB Emulator does not simulate [multi-region replication](documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="8f39b-249">The DocumentDB Emulator does not simulate [multi-region replication](documentdb-distribute-data-globally.md).</span></span>
* <span data-ttu-id="8f39b-250">The DocumentDB Emulator does not support the service quota overrides that are available in the Azure DocumentDB service (e.g. document size limits, increased partitioned collection storage).</span><span class="sxs-lookup"><span data-stu-id="8f39b-250">The DocumentDB Emulator does not support the service quota overrides that are available in the Azure DocumentDB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="8f39b-251">As your copy of the DocumentDB Emulator might not be up to date with the most recent changes with the Azure DocumentDB service, please [DocumentDB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span><span class="sxs-lookup"><span data-stu-id="8f39b-251">As your copy of the DocumentDB Emulator might not be up to date with the most recent changes with the Azure DocumentDB service, please [DocumentDB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <a id="set-partitioncount"></a><span data-ttu-id="8f39b-252">Change the number of collections</span><span class="sxs-lookup"><span data-stu-id="8f39b-252">Change the number of collections</span></span>

<span data-ttu-id="8f39b-253">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the DocumentDB Emulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-253">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the DocumentDB Emulator.</span></span> <span data-ttu-id="8f39b-254">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span><span class="sxs-lookup"><span data-stu-id="8f39b-254">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="8f39b-255">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span><span class="sxs-lookup"><span data-stu-id="8f39b-255">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="8f39b-256">To change the number of collections available to the DocumentDB Emulator, do the following:</span><span class="sxs-lookup"><span data-stu-id="8f39b-256">To change the number of collections available to the DocumentDB Emulator, do the following:</span></span>

1. <span data-ttu-id="8f39b-257">Delete all local DocumentDB Emulator data by right-clicking the **DocumentDB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span><span class="sxs-lookup"><span data-stu-id="8f39b-257">Delete all local DocumentDB Emulator data by right-clicking the **DocumentDB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="8f39b-258">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\DocumentDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="8f39b-258">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\DocumentDBEmulator.</span></span>
3. <span data-ttu-id="8f39b-259">Exit all open instances by right-clicking the **DocumentDB Emulator** icon on the system tray, and then clicking **Exit**.</span><span class="sxs-lookup"><span data-stu-id="8f39b-259">Exit all open instances by right-clicking the **DocumentDB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="8f39b-260">It may take a minute for all instances to exit.</span><span class="sxs-lookup"><span data-stu-id="8f39b-260">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="8f39b-261">Install the latest version of the [DocumentDB Emulator](https://aka.ms/documentdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="8f39b-261">Install the latest version of the [DocumentDB Emulator](https://aka.ms/documentdb-emulator).</span></span>
5. <span data-ttu-id="8f39b-262">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span><span class="sxs-lookup"><span data-stu-id="8f39b-262">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="8f39b-263">For example: `C:\Program Files\DocumentDB Emulator>DocumentDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="8f39b-263">For example: `C:\Program Files\DocumentDB Emulator>DocumentDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8f39b-264">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="8f39b-264">Troubleshooting</span></span>

<span data-ttu-id="8f39b-265">Use the following tips to help troubleshoot issues you encounter with the DocumentDB emulator:</span><span class="sxs-lookup"><span data-stu-id="8f39b-265">Use the following tips to help troubleshoot issues you encounter with the DocumentDB emulator:</span></span>

- <span data-ttu-id="8f39b-266">If the DocumentDB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8f39b-266">If the DocumentDB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).</span></span>

- <span data-ttu-id="8f39b-267">If you experience crashes in DocumentDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="8f39b-267">If you experience crashes in DocumentDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="8f39b-268">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8f39b-268">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).</span></span>

### <a id="trace-files"></a><span data-ttu-id="8f39b-269">Collect trace files</span><span class="sxs-lookup"><span data-stu-id="8f39b-269">Collect trace files</span></span>

<span data-ttu-id="8f39b-270">To collect debugging traces, run the following commands from an administrative command prompt:</span><span class="sxs-lookup"><span data-stu-id="8f39b-270">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\DocumentDB Emulator"`
2. <span data-ttu-id="8f39b-271">`DocumentDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="8f39b-271">`DocumentDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="8f39b-272">Watch the system tray to make sure the program has shut down, it may take a minute.</span><span class="sxs-lookup"><span data-stu-id="8f39b-272">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="8f39b-273">You can also just click **Exit** in the DocumentDB emulator user interface.</span><span class="sxs-lookup"><span data-stu-id="8f39b-273">You can also just click **Exit** in the DocumentDB emulator user interface.</span></span>
3. `DocumentDB.Emulator.exe /starttraces`
4. `DocumentDB.Emulator.exe`
5. <span data-ttu-id="8f39b-274">Reproduce the problem.</span><span class="sxs-lookup"><span data-stu-id="8f39b-274">Reproduce the problem.</span></span> <span data-ttu-id="8f39b-275">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span><span class="sxs-lookup"><span data-stu-id="8f39b-275">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `DocumentDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="8f39b-276">Navigate to `%ProgramFiles%\DocumentDB Emulator` and find the docdbemulator_000001.etl file.</span><span class="sxs-lookup"><span data-stu-id="8f39b-276">Navigate to `%ProgramFiles%\DocumentDB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="8f39b-277">Send the .etl file along with repro steps to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com) for debugging.</span><span class="sxs-lookup"><span data-stu-id="8f39b-277">Send the .etl file along with repro steps to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com) for debugging.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8f39b-278">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f39b-278">Next steps</span></span>
* <span data-ttu-id="8f39b-279">To learn more about DocumentDB, see [Introduction to Azure DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8f39b-279">To learn more about DocumentDB, see [Introduction to Azure DocumentDB](documentdb-introduction.md)</span></span>
* <span data-ttu-id="8f39b-280">To start developing against the DocumentDB Emulator, download one of the [supported DocumentDB SDKs](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8f39b-280">To start developing against the DocumentDB Emulator, download one of the [supported DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span>




