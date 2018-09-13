---
title: Develop locally with the Azure Cosmos DB Emulator | Microsoft Docs
description: Using the Azure Cosmos DB Emulator, you can develop and test your application locally for free, without creating an Azure subscription.
services: cosmos-db
keywords: Azure Cosmos DB Emulator
author: David-Noble-at-work
manager: kfile
editor: ''
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.date: 04/20/2018
ms.author: danoble
ms.openlocfilehash: 84728b5dd80c8059c17dd46fbe0052bcfba67658
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868163"
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="85f52-104">Use the Azure Cosmos DB Emulator for local development and testing</span><span class="sxs-lookup"><span data-stu-id="85f52-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="85f52-105"><strong>Binaries</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="85f52-106">Download MSI</span><span class="sxs-lookup"><span data-stu-id="85f52-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="85f52-108">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="85f52-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-cosmosdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-109"><strong>Docker source</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="85f52-110">Github</span><span class="sxs-lookup"><span data-stu-id="85f52-110">Github</span></span>](https://github.com/Azure/azure-cosmos-db-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="85f52-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span><span class="sxs-lookup"><span data-stu-id="85f52-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="85f52-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span><span class="sxs-lookup"><span data-stu-id="85f52-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="85f52-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span><span class="sxs-lookup"><span data-stu-id="85f52-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="85f52-114">At this time the Data Explorer in the emulator only fully supports SQL API collections and MongoDB collections.</span><span class="sxs-lookup"><span data-stu-id="85f52-114">At this time the Data Explorer in the emulator only fully supports SQL API collections and MongoDB collections.</span></span> <span data-ttu-id="85f52-115">Table, Graph, and Cassandra containers are not fully supported.</span><span class="sxs-lookup"><span data-stu-id="85f52-115">Table, Graph, and Cassandra containers are not fully supported.</span></span> 

<span data-ttu-id="85f52-116">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="85f52-116">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="85f52-117">Installing the Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-117">Installing the Emulator</span></span>
> * <span data-ttu-id="85f52-118">Authenticating requests</span><span class="sxs-lookup"><span data-stu-id="85f52-118">Authenticating requests</span></span>
> * <span data-ttu-id="85f52-119">Using the Data Explorer in the Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-119">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="85f52-120">Exporting SSL certificates</span><span class="sxs-lookup"><span data-stu-id="85f52-120">Exporting SSL certificates</span></span>
> * <span data-ttu-id="85f52-121">Calling the Emulator from the command-line</span><span class="sxs-lookup"><span data-stu-id="85f52-121">Calling the Emulator from the command-line</span></span>
> * <span data-ttu-id="85f52-122">Running the Emulator on Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="85f52-122">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="85f52-123">Collecting trace files</span><span class="sxs-lookup"><span data-stu-id="85f52-123">Collecting trace files</span></span>
> * <span data-ttu-id="85f52-124">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="85f52-124">Troubleshooting</span></span>

## <a name="how-the-emulator-works"></a><span data-ttu-id="85f52-125">How the Emulator works</span><span class="sxs-lookup"><span data-stu-id="85f52-125">How the Emulator works</span></span>

<span data-ttu-id="85f52-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span><span class="sxs-lookup"><span data-stu-id="85f52-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="85f52-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="85f52-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="85f52-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85f52-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="85f52-129">While emulation of the Azure Cosmos DB service is faithful, the Emulator's implementation is different than the service.</span><span class="sxs-lookup"><span data-stu-id="85f52-129">While emulation of the Azure Cosmos DB service is faithful, the Emulator's implementation is different than the service.</span></span> <span data-ttu-id="85f52-130">For example, the Emulator uses standard OS components such as the local file system for persistence, and the HTTPS protocol stack for connectivity.</span><span class="sxs-lookup"><span data-stu-id="85f52-130">For example, the Emulator uses standard OS components such as the local file system for persistence, and the HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="85f52-131">Functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are unavailable.</span><span class="sxs-lookup"><span data-stu-id="85f52-131">Functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are unavailable.</span></span>

## <a name="differences-between-the-emulator-and-the-service"></a><span data-ttu-id="85f52-132">Differences between the Emulator and the service</span><span class="sxs-lookup"><span data-stu-id="85f52-132">Differences between the Emulator and the service</span></span> 
<span data-ttu-id="85f52-133">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span><span class="sxs-lookup"><span data-stu-id="85f52-133">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="85f52-134">Currently Data Explorer in the emulator supports SQL API collections and MongoDB collections only.</span><span class="sxs-lookup"><span data-stu-id="85f52-134">Currently Data Explorer in the emulator supports SQL API collections and MongoDB collections only.</span></span> <span data-ttu-id="85f52-135">Table, Graph, and Cassandra APIs are not yet supported.</span><span class="sxs-lookup"><span data-stu-id="85f52-135">Table, Graph, and Cassandra APIs are not yet supported.</span></span>  
* <span data-ttu-id="85f52-136">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span><span class="sxs-lookup"><span data-stu-id="85f52-136">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="85f52-137">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-137">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="85f52-138">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span><span class="sxs-lookup"><span data-stu-id="85f52-138">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="85f52-139">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="85f52-139">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="85f52-140">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="85f52-140">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="85f52-141">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (for example, document size limits, increased partitioned collection storage).</span><span class="sxs-lookup"><span data-stu-id="85f52-141">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (for example, document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="85f52-142">As your copy of the Azure Cosmos DB Emulator might not be up-to-date with the most recent changes with the Azure Cosmos DB service, you should use the [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate the production throughput (RUs) needs of your application.</span><span class="sxs-lookup"><span data-stu-id="85f52-142">As your copy of the Azure Cosmos DB Emulator might not be up-to-date with the most recent changes with the Azure Cosmos DB service, you should use the [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate the production throughput (RUs) needs of your application.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="85f52-143">System requirements</span><span class="sxs-lookup"><span data-stu-id="85f52-143">System requirements</span></span>
<span data-ttu-id="85f52-144">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span><span class="sxs-lookup"><span data-stu-id="85f52-144">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="85f52-145">Software requirements</span><span class="sxs-lookup"><span data-stu-id="85f52-145">Software requirements</span></span>
  * <span data-ttu-id="85f52-146">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span><span class="sxs-lookup"><span data-stu-id="85f52-146">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="85f52-147">Minimum Hardware requirements</span><span class="sxs-lookup"><span data-stu-id="85f52-147">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="85f52-148">2-GB RAM</span><span class="sxs-lookup"><span data-stu-id="85f52-148">2-GB RAM</span></span>
  * <span data-ttu-id="85f52-149">10-GB available hard disk space</span><span class="sxs-lookup"><span data-stu-id="85f52-149">10-GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="85f52-150">Installation</span><span class="sxs-lookup"><span data-stu-id="85f52-150">Installation</span></span>
<span data-ttu-id="85f52-151">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator) or you can run the emulator on Docker for Windows.</span><span class="sxs-lookup"><span data-stu-id="85f52-151">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator) or you can run the emulator on Docker for Windows.</span></span> <span data-ttu-id="85f52-152">For instructions on using the Emulator on Docker for Windows, see [Running on Docker](#running-on-docker).</span><span class="sxs-lookup"><span data-stu-id="85f52-152">For instructions on using the Emulator on Docker for Windows, see [Running on Docker](#running-on-docker).</span></span> 

> [!NOTE]
> <span data-ttu-id="85f52-153">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span><span class="sxs-lookup"><span data-stu-id="85f52-153">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-windows"></a><span data-ttu-id="85f52-154">Running on Windows</span><span class="sxs-lookup"><span data-stu-id="85f52-154">Running on Windows</span></span>

<span data-ttu-id="85f52-155">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span><span class="sxs-lookup"><span data-stu-id="85f52-155">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="85f52-156">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span><span class="sxs-lookup"><span data-stu-id="85f52-156">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Select the Start button or press the Windows key, begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="85f52-158">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span><span class="sxs-lookup"><span data-stu-id="85f52-158">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Azure Cosmos DB local emulator taskbar notification](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="85f52-160">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span><span class="sxs-lookup"><span data-stu-id="85f52-160">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="85f52-161">The Azure Cosmos DB Emulator is installed to `C:\Program Files\Azure Cosmos DB Emulator` by default.</span><span class="sxs-lookup"><span data-stu-id="85f52-161">The Azure Cosmos DB Emulator is installed to `C:\Program Files\Azure Cosmos DB Emulator` by default.</span></span> <span data-ttu-id="85f52-162">You can also start and stop the emulator from the command-line.</span><span class="sxs-lookup"><span data-stu-id="85f52-162">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="85f52-163">For more information, see the [command-line tool reference](#command-line).</span><span class="sxs-lookup"><span data-stu-id="85f52-163">For more information, see the [command-line tool reference](#command-line).</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="85f52-164">Start Data Explorer</span><span class="sxs-lookup"><span data-stu-id="85f52-164">Start Data Explorer</span></span>

<span data-ttu-id="85f52-165">When the Azure Cosmos DB emulator launches, it automatically opens the Azure Cosmos DB Data Explorer in your browser.</span><span class="sxs-lookup"><span data-stu-id="85f52-165">When the Azure Cosmos DB emulator launches, it automatically opens the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="85f52-166">The address appears as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="85f52-166">The address appears as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="85f52-167">If you close the explorer and would like to reopen it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span><span class="sxs-lookup"><span data-stu-id="85f52-167">If you close the explorer and would like to reopen it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Azure Cosmos DB local emulator data explorer launcher](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="85f52-169">Checking for updates</span><span class="sxs-lookup"><span data-stu-id="85f52-169">Checking for updates</span></span>
<span data-ttu-id="85f52-170">Data Explorer indicates if there is a new update available for download.</span><span class="sxs-lookup"><span data-stu-id="85f52-170">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="85f52-171">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span><span class="sxs-lookup"><span data-stu-id="85f52-171">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="85f52-172">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-172">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="85f52-173">Authenticating requests</span><span class="sxs-lookup"><span data-stu-id="85f52-173">Authenticating requests</span></span>
<span data-ttu-id="85f52-174">As with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span><span class="sxs-lookup"><span data-stu-id="85f52-174">As with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="85f52-175">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span><span class="sxs-lookup"><span data-stu-id="85f52-175">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="85f52-176">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-176">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="85f52-177">They are:</span><span class="sxs-lookup"><span data-stu-id="85f52-177">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="85f52-178">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-178">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="85f52-179">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-179">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="85f52-180">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="85f52-180">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="85f52-181">As with the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span><span class="sxs-lookup"><span data-stu-id="85f52-181">As with the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-on-a-local-network"></a><span data-ttu-id="85f52-182">Running on a local network</span><span class="sxs-lookup"><span data-stu-id="85f52-182">Running on a local network</span></span>

<span data-ttu-id="85f52-183">You can run the emulator on a local network.</span><span class="sxs-lookup"><span data-stu-id="85f52-183">You can run the emulator on a local network.</span></span> <span data-ttu-id="85f52-184">To enable network access, specify the /AllowNetworkAccess option at the [command-line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span><span class="sxs-lookup"><span data-stu-id="85f52-184">To enable network access, specify the /AllowNetworkAccess option at the [command-line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="85f52-185">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span><span class="sxs-lookup"><span data-stu-id="85f52-185">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="85f52-186">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="85f52-186">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="85f52-187">To enable network access for the first time the user should shut down the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="85f52-187">To enable network access for the first time the user should shut down the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="85f52-188">Developing with the Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-188">Developing with the Emulator</span></span>
<span data-ttu-id="85f52-189">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](sql-api-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/cosmos-db/) to interact with the Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-189">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](sql-api-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/cosmos-db/) to interact with the Emulator.</span></span> <span data-ttu-id="85f52-190">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the SQL and MongoDB APIs, and view and edit documents without writing any code.</span><span class="sxs-lookup"><span data-stu-id="85f52-190">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the SQL and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="85f52-191">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), use the following connection string:</span><span class="sxs-lookup"><span data-stu-id="85f52-191">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true

<span data-ttu-id="85f52-192">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-192">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="85f52-193">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="85f52-193">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="85f52-194">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="85f52-194">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="85f52-195">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span><span class="sxs-lookup"><span data-stu-id="85f52-195">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="85f52-196">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="85f52-196">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="85f52-197">Export the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="85f52-197">Export the SSL certificate</span></span>

<span data-ttu-id="85f52-198">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-198">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="85f52-199">Other languages have their own method of managing and using certificates.</span><span class="sxs-lookup"><span data-stu-id="85f52-199">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="85f52-200">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="85f52-200">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="85f52-201">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store, you will need to export it using the Windows Certificate Manager.</span><span class="sxs-lookup"><span data-stu-id="85f52-201">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store, you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="85f52-202">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="85f52-202">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="85f52-203">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span><span class="sxs-lookup"><span data-stu-id="85f52-203">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure Cosmos DB local emulator SSL certificate](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="85f52-205">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="85f52-205">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="85f52-206">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-206">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="85f52-207">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span><span class="sxs-lookup"><span data-stu-id="85f52-207">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <a id="command-line"></a><span data-ttu-id="85f52-208">Command-line tool reference</span><span class="sxs-lookup"><span data-stu-id="85f52-208">Command-line tool reference</span></span>
<span data-ttu-id="85f52-209">From the installation location, you can use the command line to start and stop the emulator, configure options, and perform other operations.</span><span class="sxs-lookup"><span data-stu-id="85f52-209">From the installation location, you can use the command line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="85f52-210">Command-line syntax</span><span class="sxs-lookup"><span data-stu-id="85f52-210">Command-line syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="85f52-211">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span><span class="sxs-lookup"><span data-stu-id="85f52-211">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="85f52-212"><strong>Option</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-212"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="85f52-213"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-213"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="85f52-214"><strong>Command</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-214"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="85f52-215"><strong>Arguments</strong></span><span class="sxs-lookup"><span data-stu-id="85f52-215"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-216">[No arguments]</span><span class="sxs-lookup"><span data-stu-id="85f52-216">[No arguments]</span></span></td>
  <td><span data-ttu-id="85f52-217">Starts up the Azure Cosmos DB Emulator with default settings.</span><span class="sxs-lookup"><span data-stu-id="85f52-217">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="85f52-218">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="85f52-218">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-219">[Help]</span><span class="sxs-lookup"><span data-stu-id="85f52-219">[Help]</span></span></td>
  <td><span data-ttu-id="85f52-220">Displays the list of supported command-line arguments.</span><span class="sxs-lookup"><span data-stu-id="85f52-220">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="85f52-221">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="85f52-221">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-222">GetStatus</span><span class="sxs-lookup"><span data-stu-id="85f52-222">GetStatus</span></span></td>
  <td><span data-ttu-id="85f52-223">Gets the status of the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-223">Gets the status of the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="85f52-224">The status is indicated by the exit code: 1 = Starting, 2 = Running, 3 = Stopped.</span><span class="sxs-lookup"><span data-stu-id="85f52-224">The status is indicated by the exit code: 1 = Starting, 2 = Running, 3 = Stopped.</span></span> <span data-ttu-id="85f52-225">A negative exit code indicates that an error occurred.</span><span class="sxs-lookup"><span data-stu-id="85f52-225">A negative exit code indicates that an error occurred.</span></span> <span data-ttu-id="85f52-226">No other output is produced.</span><span class="sxs-lookup"><span data-stu-id="85f52-226">No other output is produced.</span></span></td>
  <td><span data-ttu-id="85f52-227">CosmosDB.Emulator.exe /GetStatus</span><span class="sxs-lookup"><span data-stu-id="85f52-227">CosmosDB.Emulator.exe /GetStatus</span></span></td>
  <td></td>
<tr>
  <td><span data-ttu-id="85f52-228">Shutdown</span><span class="sxs-lookup"><span data-stu-id="85f52-228">Shutdown</span></span></td>
  <td><span data-ttu-id="85f52-229">Shuts down the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-229">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="85f52-230">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="85f52-230">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-231">DataPath</span><span class="sxs-lookup"><span data-stu-id="85f52-231">DataPath</span></span></td>
  <td><span data-ttu-id="85f52-232">Specifies the path in which to store data files.</span><span class="sxs-lookup"><span data-stu-id="85f52-232">Specifies the path in which to store data files.</span></span> <span data-ttu-id="85f52-233">Default is %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-233">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="85f52-234">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-234">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="85f52-235">&lt;datapath&gt;: An accessible path</span><span class="sxs-lookup"><span data-stu-id="85f52-235">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-236">Port</span><span class="sxs-lookup"><span data-stu-id="85f52-236">Port</span></span></td>
  <td><span data-ttu-id="85f52-237">Specifies the port number to use for the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-237">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="85f52-238">Default is 8081.</span><span class="sxs-lookup"><span data-stu-id="85f52-238">Default is 8081.</span></span></td>
  <td><span data-ttu-id="85f52-239">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-239">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="85f52-240">&lt;port&gt;: Single port number</span><span class="sxs-lookup"><span data-stu-id="85f52-240">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-241">MongoPort</span><span class="sxs-lookup"><span data-stu-id="85f52-241">MongoPort</span></span></td>
  <td><span data-ttu-id="85f52-242">Specifies the port number to use for MongoDB compatibility API.</span><span class="sxs-lookup"><span data-stu-id="85f52-242">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="85f52-243">Default is 10255.</span><span class="sxs-lookup"><span data-stu-id="85f52-243">Default is 10255.</span></span></td>
  <td><span data-ttu-id="85f52-244">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-244">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="85f52-245">&lt;mongoport&gt;: Single port number</span><span class="sxs-lookup"><span data-stu-id="85f52-245">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-246">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="85f52-246">DirectPorts</span></span></td>
  <td><span data-ttu-id="85f52-247">Specifies the ports to use for direct connectivity.</span><span class="sxs-lookup"><span data-stu-id="85f52-247">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="85f52-248">Defaults are 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="85f52-248">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="85f52-249">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-249">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="85f52-250">&lt;directports&gt;: Comma-delimited list of 4 ports</span><span class="sxs-lookup"><span data-stu-id="85f52-250">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-251">Key</span><span class="sxs-lookup"><span data-stu-id="85f52-251">Key</span></span></td>
  <td><span data-ttu-id="85f52-252">Authorization key for the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-252">Authorization key for the emulator.</span></span> <span data-ttu-id="85f52-253">Key must be the base-64 encoding of a 64-byte vector.</span><span class="sxs-lookup"><span data-stu-id="85f52-253">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="85f52-254">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-254">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="85f52-255">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span><span class="sxs-lookup"><span data-stu-id="85f52-255">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-256">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="85f52-256">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="85f52-257">Specifies that request rate limiting behavior is enabled.</span><span class="sxs-lookup"><span data-stu-id="85f52-257">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="85f52-258">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="85f52-258">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-259">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="85f52-259">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="85f52-260">Specifies that request rate limiting behavior is disabled.</span><span class="sxs-lookup"><span data-stu-id="85f52-260">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="85f52-261">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="85f52-261">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-262">NoUI</span><span class="sxs-lookup"><span data-stu-id="85f52-262">NoUI</span></span></td>
  <td><span data-ttu-id="85f52-263">Do not show the emulator user interface.</span><span class="sxs-lookup"><span data-stu-id="85f52-263">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="85f52-264">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="85f52-264">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-265">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="85f52-265">NoExplorer</span></span></td>
  <td><span data-ttu-id="85f52-266">Don't show data explorer on startup.</span><span class="sxs-lookup"><span data-stu-id="85f52-266">Don't show data explorer on startup.</span></span></td>
  <td><span data-ttu-id="85f52-267">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="85f52-267">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-268">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="85f52-268">PartitionCount</span></span></td>
  <td><span data-ttu-id="85f52-269">Specifies the maximum number of partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="85f52-269">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="85f52-270">See [Change the number of collections](#set-partitioncount) for more information.</span><span class="sxs-lookup"><span data-stu-id="85f52-270">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="85f52-271">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-271">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="85f52-272">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span><span class="sxs-lookup"><span data-stu-id="85f52-272">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="85f52-273">Default is 25.</span><span class="sxs-lookup"><span data-stu-id="85f52-273">Default is 25.</span></span> <span data-ttu-id="85f52-274">Maximum allowed is 250.</span><span class="sxs-lookup"><span data-stu-id="85f52-274">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-275">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="85f52-275">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="85f52-276">Specifies the default number of partitions for a partitioned collection.</span><span class="sxs-lookup"><span data-stu-id="85f52-276">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="85f52-277">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-277">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="85f52-278">&lt;defaultpartitioncount&gt; Default is 25.</span><span class="sxs-lookup"><span data-stu-id="85f52-278">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-279">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="85f52-279">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="85f52-280">Enables access to the emulator over a network.</span><span class="sxs-lookup"><span data-stu-id="85f52-280">Enables access to the emulator over a network.</span></span> <span data-ttu-id="85f52-281">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span><span class="sxs-lookup"><span data-stu-id="85f52-281">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="85f52-282">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-282">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="85f52-283">or</span><span class="sxs-lookup"><span data-stu-id="85f52-283">or</span></span><br><br><span data-ttu-id="85f52-284">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-284">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-285">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="85f52-285">NoFirewall</span></span></td>
  <td><span data-ttu-id="85f52-286">Don't adjust firewall rules when /AllowNetworkAccess is used.</span><span class="sxs-lookup"><span data-stu-id="85f52-286">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="85f52-287">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="85f52-287">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-288">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="85f52-288">GenKeyFile</span></span></td>
  <td><span data-ttu-id="85f52-289">Generate a new authorization key and save to the specified file.</span><span class="sxs-lookup"><span data-stu-id="85f52-289">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="85f52-290">The generated key can be used with the /Key or /KeyFile options.</span><span class="sxs-lookup"><span data-stu-id="85f52-290">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="85f52-291">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-291">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-292">Consistency</span><span class="sxs-lookup"><span data-stu-id="85f52-292">Consistency</span></span></td>
  <td><span data-ttu-id="85f52-293">Set the default consistency level for the account.</span><span class="sxs-lookup"><span data-stu-id="85f52-293">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="85f52-294">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="85f52-294">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="85f52-295">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="85f52-295">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="85f52-296">The default value is Session.</span><span class="sxs-lookup"><span data-stu-id="85f52-296">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="85f52-297">?</span><span class="sxs-lookup"><span data-stu-id="85f52-297">?</span></span></td>
  <td><span data-ttu-id="85f52-298">Show the help message.</span><span class="sxs-lookup"><span data-stu-id="85f52-298">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a id="set-partitioncount"></a><span data-ttu-id="85f52-299">Change the number of collections</span><span class="sxs-lookup"><span data-stu-id="85f52-299">Change the number of collections</span></span>

<span data-ttu-id="85f52-300">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-300">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="85f52-301">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where one partitioned collection = 25 single partition collection).</span><span class="sxs-lookup"><span data-stu-id="85f52-301">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where one partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="85f52-302">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span><span class="sxs-lookup"><span data-stu-id="85f52-302">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email askcosmosdb@microsoft.com at any time or
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="85f52-303">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span><span class="sxs-lookup"><span data-stu-id="85f52-303">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="85f52-304">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span><span class="sxs-lookup"><span data-stu-id="85f52-304">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="85f52-305">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-305">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="85f52-306">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span><span class="sxs-lookup"><span data-stu-id="85f52-306">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="85f52-307">It may take a minute for all instances to exit.</span><span class="sxs-lookup"><span data-stu-id="85f52-307">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="85f52-308">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="85f52-308">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="85f52-309">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span><span class="sxs-lookup"><span data-stu-id="85f52-309">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="85f52-310">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="85f52-310">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="controlling-the-emulator"></a><span data-ttu-id="85f52-311">Controlling the Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-311">Controlling the Emulator</span></span>

<span data-ttu-id="85f52-312">The Emulator comes with a PowerShell module for starting, stopping, uninstalling, and retrieving the status of the service.</span><span class="sxs-lookup"><span data-stu-id="85f52-312">The Emulator comes with a PowerShell module for starting, stopping, uninstalling, and retrieving the status of the service.</span></span> <span data-ttu-id="85f52-313">To use it:</span><span class="sxs-lookup"><span data-stu-id="85f52-313">To use it:</span></span>

```powershell
Import-Module "$env:ProgramFiles\Azure Cosmos DB Emulator\PSModules\Microsoft.Azure.CosmosDB.Emulator"
```

<span data-ttu-id="85f52-314">or put the `PSModules` directory on your `PSModulesPath` and import it like this:</span><span class="sxs-lookup"><span data-stu-id="85f52-314">or put the `PSModules` directory on your `PSModulesPath` and import it like this:</span></span>

```powershell
$env:PSModulesPath += "$env:ProgramFiles\Azure Cosmos DB Emulator\PSModules"
Import-Module Microsoft.Azure.CosmosDB.Emulator
```

<span data-ttu-id="85f52-315">Here is a summary of the commands for controlling the emulator from PowerShell:</span><span class="sxs-lookup"><span data-stu-id="85f52-315">Here is a summary of the commands for controlling the emulator from PowerShell:</span></span>

### `Get-CosmosDbEmulatorStatus`

#### <a name="syntax"></a><span data-ttu-id="85f52-316">Syntax</span><span class="sxs-lookup"><span data-stu-id="85f52-316">Syntax</span></span>

`Get-CosmosDbEmulatorStatus`

#### <a name="remarks"></a><span data-ttu-id="85f52-317">Remarks</span><span class="sxs-lookup"><span data-stu-id="85f52-317">Remarks</span></span>

<span data-ttu-id="85f52-318">Returns one of these ServiceControllerStatus values: ServiceControllerStatus.StartPending, ServiceControllerStatus.Running, or ServiceControllerStatus.Stopped.</span><span class="sxs-lookup"><span data-stu-id="85f52-318">Returns one of these ServiceControllerStatus values: ServiceControllerStatus.StartPending, ServiceControllerStatus.Running, or ServiceControllerStatus.Stopped.</span></span>

### `Start-CosmosDbEmulator`

#### <a name="syntax"></a><span data-ttu-id="85f52-319">Syntax</span><span class="sxs-lookup"><span data-stu-id="85f52-319">Syntax</span></span>

`Start-CosmosDbEmulator [-DataPath <string>] [-DefaultPartitionCount <uint16>] [-DirectPort <uint16[]>] [-MongoPort <uint16>] [-NoUI] [-NoWait] [-PartitionCount <uint16>] [-Port <uint16>]  [<CommonParameters>]`

#### <a name="remarks"></a><span data-ttu-id="85f52-320">Remarks</span><span class="sxs-lookup"><span data-stu-id="85f52-320">Remarks</span></span>

<span data-ttu-id="85f52-321">Starts the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-321">Starts the emulator.</span></span> <span data-ttu-id="85f52-322">By default, the command waits until the emulator is ready to accept requests.</span><span class="sxs-lookup"><span data-stu-id="85f52-322">By default, the command waits until the emulator is ready to accept requests.</span></span> <span data-ttu-id="85f52-323">Use the -NoWait option, if you wish the cmdlet to return as soon as it starts the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-323">Use the -NoWait option, if you wish the cmdlet to return as soon as it starts the emulator.</span></span>

### `Stop-CosmosDbEmulator`

#### <a name="syntax"></a><span data-ttu-id="85f52-324">Syntax</span><span class="sxs-lookup"><span data-stu-id="85f52-324">Syntax</span></span>

 `Stop-CosmosDbEmulator [-NoWait]`

#### <a name="remarks"></a><span data-ttu-id="85f52-325">Remarks</span><span class="sxs-lookup"><span data-stu-id="85f52-325">Remarks</span></span>

<span data-ttu-id="85f52-326">Stops the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-326">Stops the emulator.</span></span> <span data-ttu-id="85f52-327">By default, this command waits until the emulator is fully shut down.</span><span class="sxs-lookup"><span data-stu-id="85f52-327">By default, this command waits until the emulator is fully shut down.</span></span> <span data-ttu-id="85f52-328">Use the -NoWait option, if you wish the cmdlet to return as soon as the emulator begins to shut down.</span><span class="sxs-lookup"><span data-stu-id="85f52-328">Use the -NoWait option, if you wish the cmdlet to return as soon as the emulator begins to shut down.</span></span>

### `Uninstall-CosmosDbEmulator`

#### <a name="syntax"></a><span data-ttu-id="85f52-329">Syntax</span><span class="sxs-lookup"><span data-stu-id="85f52-329">Syntax</span></span>

`Uninstall-CosmosDbEmulator [-RemoveData]`

#### <a name="remarks"></a><span data-ttu-id="85f52-330">Remarks</span><span class="sxs-lookup"><span data-stu-id="85f52-330">Remarks</span></span>

<span data-ttu-id="85f52-331">Uninstalls the emulator and optionally removes the full contents of $env:LOCALAPPDATA\CosmosDbEmulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-331">Uninstalls the emulator and optionally removes the full contents of $env:LOCALAPPDATA\CosmosDbEmulator.</span></span>
<span data-ttu-id="85f52-332">The cmdlet ensures the emulator is stopped before uninstalling it.</span><span class="sxs-lookup"><span data-stu-id="85f52-332">The cmdlet ensures the emulator is stopped before uninstalling it.</span></span>

## <a name="running-on-docker"></a><span data-ttu-id="85f52-333">Running on Docker</span><span class="sxs-lookup"><span data-stu-id="85f52-333">Running on Docker</span></span>

<span data-ttu-id="85f52-334">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span><span class="sxs-lookup"><span data-stu-id="85f52-334">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="85f52-335">The Emulator does not work on Docker for Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="85f52-335">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="85f52-336">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, switch to Windows containers by right-clicking the Docker icon on the toolbar and selecting **Switch to Windows containers**.</span><span class="sxs-lookup"><span data-stu-id="85f52-336">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, switch to Windows containers by right-clicking the Docker icon on the toolbar and selecting **Switch to Windows containers**.</span></span>

<span data-ttu-id="85f52-337">Next, pull the Emulator image from Docker Hub by running the following command from your favorite shell.</span><span class="sxs-lookup"><span data-stu-id="85f52-337">Next, pull the Emulator image from Docker Hub by running the following command from your favorite shell.</span></span>

```     
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="85f52-338">To start the image, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="85f52-338">To start the image, run the following commands.</span></span>

<span data-ttu-id="85f52-339">From the command-line:</span><span class="sxs-lookup"><span data-stu-id="85f52-339">From the command-line:</span></span>
```cmd 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>null
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:C:\CosmosDB.Emulator\CosmosDBEmulatorCert -P -t -i -m 2GB microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="85f52-340">From PowerShell:</span><span class="sxs-lookup"><span data-stu-id="85f52-340">From PowerShell:</span></span>
```powershell
md $env:LOCALAPPDATA\CosmosDBEmulatorCert 2>null
docker run -v $env:LOCALAPPDATA\CosmosDBEmulatorCert:C:\CosmosDB.Emulator\CosmosDBEmulatorCert -P -t -i -m 2GB microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="85f52-341">The response looks similar to the following:</span><span class="sxs-lookup"><span data-stu-id="85f52-341">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="85f52-342">Now use the endpoint and master key-in from the response in your client and import the SSL certificate into your host.</span><span class="sxs-lookup"><span data-stu-id="85f52-342">Now use the endpoint and master key-in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="85f52-343">To import the SSL certificate, do the following from an admin command prompt:</span><span class="sxs-lookup"><span data-stu-id="85f52-343">To import the SSL certificate, do the following from an admin command prompt:</span></span>

<span data-ttu-id="85f52-344">From the command-line:</span><span class="sxs-lookup"><span data-stu-id="85f52-344">From the command-line:</span></span>
```cmd 
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```

<span data-ttu-id="85f52-345">From PowerShell:</span><span class="sxs-lookup"><span data-stu-id="85f52-345">From PowerShell:</span></span>
```powershell
cd $env:LOCALAPPDATA\CosmosDBEmulatorCert
.\importcert.ps1
```

<span data-ttu-id="85f52-346">Closing the interactive shell once the Emulator has been started will shut down the Emulator’s container.</span><span class="sxs-lookup"><span data-stu-id="85f52-346">Closing the interactive shell once the Emulator has been started will shut down the Emulator’s container.</span></span>

<span data-ttu-id="85f52-347">To open the Data Explorer, navigate to the following URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="85f52-347">To open the Data Explorer, navigate to the following URL in your browser.</span></span> <span data-ttu-id="85f52-348">The emulator endpoint is provided in the response message shown above.</span><span class="sxs-lookup"><span data-stu-id="85f52-348">The emulator endpoint is provided in the response message shown above.</span></span>

    https://<emulator endpoint provided in response>/_explorer/index.html


## <a name="troubleshooting"></a><span data-ttu-id="85f52-349">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="85f52-349">Troubleshooting</span></span>

<span data-ttu-id="85f52-350">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span><span class="sxs-lookup"><span data-stu-id="85f52-350">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="85f52-351">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span><span class="sxs-lookup"><span data-stu-id="85f52-351">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="85f52-352">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span><span class="sxs-lookup"><span data-stu-id="85f52-352">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="85f52-353">If that does not fix the errors, you can uninstall and reinstall the app.</span><span class="sxs-lookup"><span data-stu-id="85f52-353">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="85f52-354">See [Uninstall the local emulator](#uninstall) for instructions.</span><span class="sxs-lookup"><span data-stu-id="85f52-354">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="85f52-355">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="85f52-355">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="85f52-356">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="85f52-356">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="85f52-357">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="85f52-357">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="85f52-358">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span><span class="sxs-lookup"><span data-stu-id="85f52-358">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="85f52-359">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span><span class="sxs-lookup"><span data-stu-id="85f52-359">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="85f52-360">Uninstalling third-party network filter drivers typically fixes the issue.</span><span class="sxs-lookup"><span data-stu-id="85f52-360">Uninstalling third-party network filter drivers typically fixes the issue.</span></span>

### <a id="trace-files"></a><span data-ttu-id="85f52-361">Collect trace files</span><span class="sxs-lookup"><span data-stu-id="85f52-361">Collect trace files</span></span>

<span data-ttu-id="85f52-362">To collect debugging traces, run the following commands from an administrative command prompt:</span><span class="sxs-lookup"><span data-stu-id="85f52-362">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="85f52-363">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="85f52-363">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="85f52-364">Watch the system tray to make sure the program has shut down, it may take a minute.</span><span class="sxs-lookup"><span data-stu-id="85f52-364">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="85f52-365">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span><span class="sxs-lookup"><span data-stu-id="85f52-365">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="85f52-366">Reproduce the problem.</span><span class="sxs-lookup"><span data-stu-id="85f52-366">Reproduce the problem.</span></span> <span data-ttu-id="85f52-367">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span><span class="sxs-lookup"><span data-stu-id="85f52-367">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="85f52-368">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span><span class="sxs-lookup"><span data-stu-id="85f52-368">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="85f52-369">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span><span class="sxs-lookup"><span data-stu-id="85f52-369">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <a id="uninstall"></a><span data-ttu-id="85f52-370">Uninstall the local Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-370">Uninstall the local Emulator</span></span>

1. <span data-ttu-id="85f52-371">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span><span class="sxs-lookup"><span data-stu-id="85f52-371">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="85f52-372">It may take a minute for all instances to exit.</span><span class="sxs-lookup"><span data-stu-id="85f52-372">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="85f52-373">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span><span class="sxs-lookup"><span data-stu-id="85f52-373">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="85f52-374">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span><span class="sxs-lookup"><span data-stu-id="85f52-374">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="85f52-375">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span><span class="sxs-lookup"><span data-stu-id="85f52-375">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="change-list"></a><span data-ttu-id="85f52-376">Change list</span><span class="sxs-lookup"><span data-stu-id="85f52-376">Change list</span></span>

<span data-ttu-id="85f52-377">You can check the version number by right-clicking the local emulator icon on the task bar and clicking the about menu item.</span><span class="sxs-lookup"><span data-stu-id="85f52-377">You can check the version number by right-clicking the local emulator icon on the task bar and clicking the about menu item.</span></span>

### <a name="1220-released-on-april-20-2018"></a><span data-ttu-id="85f52-378">1.22.0.</span><span class="sxs-lookup"><span data-stu-id="85f52-378">1.22.0.</span></span> <span data-ttu-id="85f52-379">Released on April 20, 2018</span><span class="sxs-lookup"><span data-stu-id="85f52-379">Released on April 20, 2018</span></span>

<span data-ttu-id="85f52-380">In addition to updating Emulator services for parity with Cosmos DB cloud services, we've included improved PowerShell documentation and some miscellaneous bug fixes.</span><span class="sxs-lookup"><span data-stu-id="85f52-380">In addition to updating Emulator services for parity with Cosmos DB cloud services, we've included improved PowerShell documentation and some miscellaneous bug fixes.</span></span>

### <a name="12106-released-on-march-27-2018"></a><span data-ttu-id="85f52-381">1.21.0.6 Released on March 27, 2018</span><span class="sxs-lookup"><span data-stu-id="85f52-381">1.21.0.6 Released on March 27, 2018</span></span>

<span data-ttu-id="85f52-382">In addition to updating Emulator services for parity with Cosmos DB cloud services, we've included one new feature and two bug fixes in this release.</span><span class="sxs-lookup"><span data-stu-id="85f52-382">In addition to updating Emulator services for parity with Cosmos DB cloud services, we've included one new feature and two bug fixes in this release.</span></span>

#### <a name="features"></a><span data-ttu-id="85f52-383">Features</span><span class="sxs-lookup"><span data-stu-id="85f52-383">Features</span></span>

1. <span data-ttu-id="85f52-384">The Start-CosmosDbEmulator command now includes startup options.</span><span class="sxs-lookup"><span data-stu-id="85f52-384">The Start-CosmosDbEmulator command now includes startup options.</span></span>

#### <a name="bug-fixes"></a><span data-ttu-id="85f52-385">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="85f52-385">Bug fixes</span></span>

1. <span data-ttu-id="85f52-386">The Microsoft.Azure.CosmosDB.Emulator PowerShell module now ensures that the `ServiceControllerStatus` enumeration is loaded.</span><span class="sxs-lookup"><span data-stu-id="85f52-386">The Microsoft.Azure.CosmosDB.Emulator PowerShell module now ensures that the `ServiceControllerStatus` enumeration is loaded.</span></span>

2. <span data-ttu-id="85f52-387">The Microsoft.Azure.CosmosDB.Emulator PowerShell module now includes a manifest; an omission from the first release.</span><span class="sxs-lookup"><span data-stu-id="85f52-387">The Microsoft.Azure.CosmosDB.Emulator PowerShell module now includes a manifest; an omission from the first release.</span></span>

### <a name="1201084-released-on-february-14-2018"></a><span data-ttu-id="85f52-388">1.20.108.4 Released on February 14, 2018</span><span class="sxs-lookup"><span data-stu-id="85f52-388">1.20.108.4 Released on February 14, 2018</span></span>

<span data-ttu-id="85f52-389">There is one new feature and two bug fixes in this release.</span><span class="sxs-lookup"><span data-stu-id="85f52-389">There is one new feature and two bug fixes in this release.</span></span> <span data-ttu-id="85f52-390">Thanks to the customers who helped us to find and fix these issues.</span><span class="sxs-lookup"><span data-stu-id="85f52-390">Thanks to the customers who helped us to find and fix these issues.</span></span>

#### <a name="bug-fixes"></a><span data-ttu-id="85f52-391">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="85f52-391">Bug fixes</span></span>

1. <span data-ttu-id="85f52-392">The emulator now works on computers with 1 or 2 cores (or virtual CPUs)</span><span class="sxs-lookup"><span data-stu-id="85f52-392">The emulator now works on computers with 1 or 2 cores (or virtual CPUs)</span></span>

   <span data-ttu-id="85f52-393">Cosmos DB allocates tasks to perform various services.</span><span class="sxs-lookup"><span data-stu-id="85f52-393">Cosmos DB allocates tasks to perform various services.</span></span> <span data-ttu-id="85f52-394">The number of tasks allocated is a multiple of the number of cores on a host.</span><span class="sxs-lookup"><span data-stu-id="85f52-394">The number of tasks allocated is a multiple of the number of cores on a host.</span></span> <span data-ttu-id="85f52-395">The default multiple works well in production environments where the number of cores is large.</span><span class="sxs-lookup"><span data-stu-id="85f52-395">The default multiple works well in production environments where the number of cores is large.</span></span> <span data-ttu-id="85f52-396">However, on machines with 1 or 2 processors, no tasks are allocated to perform these services when this multiple is applied.</span><span class="sxs-lookup"><span data-stu-id="85f52-396">However, on machines with 1 or 2 processors, no tasks are allocated to perform these services when this multiple is applied.</span></span>

   <span data-ttu-id="85f52-397">We corrected this by adding a configuration override to the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-397">We corrected this by adding a configuration override to the emulator.</span></span> <span data-ttu-id="85f52-398">We now apply a multiple of 1.</span><span class="sxs-lookup"><span data-stu-id="85f52-398">We now apply a multiple of 1.</span></span> <span data-ttu-id="85f52-399">The number of tasks allocated to perform various services is now equal to the number of cores on a host.</span><span class="sxs-lookup"><span data-stu-id="85f52-399">The number of tasks allocated to perform various services is now equal to the number of cores on a host.</span></span>

   <span data-ttu-id="85f52-400">If we did nothing else for this release, it would have been to address this issue.</span><span class="sxs-lookup"><span data-stu-id="85f52-400">If we did nothing else for this release, it would have been to address this issue.</span></span> <span data-ttu-id="85f52-401">We find that many dev/test environments hosting the emulator have 1 or 2 cores.</span><span class="sxs-lookup"><span data-stu-id="85f52-401">We find that many dev/test environments hosting the emulator have 1 or 2 cores.</span></span>

2. <span data-ttu-id="85f52-402">The emulator no longer requires the Microsoft Visual C++ 2015 redistributable to be installed.</span><span class="sxs-lookup"><span data-stu-id="85f52-402">The emulator no longer requires the Microsoft Visual C++ 2015 redistributable to be installed.</span></span>

   <span data-ttu-id="85f52-403">We found that fresh installs of Windows (desktop and server editions) do not include this redistributable package.</span><span class="sxs-lookup"><span data-stu-id="85f52-403">We found that fresh installs of Windows (desktop and server editions) do not include this redistributable package.</span></span> <span data-ttu-id="85f52-404">Hence, we now bundle the redistributable binaries with the emulator.</span><span class="sxs-lookup"><span data-stu-id="85f52-404">Hence, we now bundle the redistributable binaries with the emulator.</span></span>

#### <a name="features"></a><span data-ttu-id="85f52-405">Features</span><span class="sxs-lookup"><span data-stu-id="85f52-405">Features</span></span>

<span data-ttu-id="85f52-406">Many of the customers we've talked to have said: It would be nice if the Emulator was scriptable.</span><span class="sxs-lookup"><span data-stu-id="85f52-406">Many of the customers we've talked to have said: It would be nice if the Emulator was scriptable.</span></span> <span data-ttu-id="85f52-407">Hence, in this release we've added some script ability.</span><span class="sxs-lookup"><span data-stu-id="85f52-407">Hence, in this release we've added some script ability.</span></span> <span data-ttu-id="85f52-408">The Emulator now includes a PowerShell module for starting, stopping, getting status, and uninstalling itself: `Microsoft.Azure.CosmosDB.Emulator`.</span><span class="sxs-lookup"><span data-stu-id="85f52-408">The Emulator now includes a PowerShell module for starting, stopping, getting status, and uninstalling itself: `Microsoft.Azure.CosmosDB.Emulator`.</span></span> 

### <a name="120911-released-on-january-26-2018"></a><span data-ttu-id="85f52-409">1.20.91.1 Released on January 26, 2018</span><span class="sxs-lookup"><span data-stu-id="85f52-409">1.20.91.1 Released on January 26, 2018</span></span>

* <span data-ttu-id="85f52-410">Enabled the MongoDB aggregation pipeline by default.</span><span class="sxs-lookup"><span data-stu-id="85f52-410">Enabled the MongoDB aggregation pipeline by default.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85f52-411">Next steps</span><span class="sxs-lookup"><span data-stu-id="85f52-411">Next steps</span></span>

<span data-ttu-id="85f52-412">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="85f52-412">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85f52-413">Installed the local Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-413">Installed the local Emulator</span></span>
> * <span data-ttu-id="85f52-414">Ran the Emulator on Docker for Windows</span><span class="sxs-lookup"><span data-stu-id="85f52-414">Ran the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="85f52-415">Authenticated requests</span><span class="sxs-lookup"><span data-stu-id="85f52-415">Authenticated requests</span></span>
> * <span data-ttu-id="85f52-416">Used the Data Explorer in the Emulator</span><span class="sxs-lookup"><span data-stu-id="85f52-416">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="85f52-417">Exported SSL certificates</span><span class="sxs-lookup"><span data-stu-id="85f52-417">Exported SSL certificates</span></span>
> * <span data-ttu-id="85f52-418">Called the Emulator from the command-line</span><span class="sxs-lookup"><span data-stu-id="85f52-418">Called the Emulator from the command-line</span></span>
> * <span data-ttu-id="85f52-419">Collected trace files</span><span class="sxs-lookup"><span data-stu-id="85f52-419">Collected trace files</span></span>

<span data-ttu-id="85f52-420">In this tutorial, you've learned how to use the local Emulator for free local development.</span><span class="sxs-lookup"><span data-stu-id="85f52-420">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="85f52-421">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="85f52-421">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="85f52-422">Export the Azure Cosmos DB Emulator certificates</span><span class="sxs-lookup"><span data-stu-id="85f52-422">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
