---
title: Upgrade to the latest elastic database client library | Microsoft Docs
description: Upgrade apps and libraries using Nuget
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: 09d0ea1037370c61b98e0aa6f6ec4aecdd982443
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550207"
---
# <a name="upgrade-an-app-to-use-the-latest-elastic-database-client-library"></a><span data-ttu-id="446c2-103">Upgrade an app to use the latest elastic database client library</span><span class="sxs-lookup"><span data-stu-id="446c2-103">Upgrade an app to use the latest elastic database client library</span></span>
<span data-ttu-id="446c2-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="446c2-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="446c2-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span><span class="sxs-lookup"><span data-stu-id="446c2-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span></span>

<span data-ttu-id="446c2-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="446c2-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="446c2-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span><span class="sxs-lookup"><span data-stu-id="446c2-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span></span>

<span data-ttu-id="446c2-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span><span class="sxs-lookup"><span data-stu-id="446c2-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="446c2-109">Upgrade steps</span><span class="sxs-lookup"><span data-stu-id="446c2-109">Upgrade steps</span></span>
<span data-ttu-id="446c2-110">**1. Upgrade your applications.**</span><span class="sxs-lookup"><span data-stu-id="446c2-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="446c2-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span><span class="sxs-lookup"><span data-stu-id="446c2-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="446c2-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="446c2-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="446c2-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span><span class="sxs-lookup"><span data-stu-id="446c2-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span></span>
* <span data-ttu-id="446c2-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span><span class="sxs-lookup"><span data-stu-id="446c2-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span></span> <span data-ttu-id="446c2-115">Select the package to update, and click the **Update** button.</span><span class="sxs-lookup"><span data-stu-id="446c2-115">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="446c2-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span><span class="sxs-lookup"><span data-stu-id="446c2-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span></span> <span data-ttu-id="446c2-117">Select the package to update, and click the **Update** button.</span><span class="sxs-lookup"><span data-stu-id="446c2-117">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="446c2-118">Build and Deploy.</span><span class="sxs-lookup"><span data-stu-id="446c2-118">Build and Deploy.</span></span> 

<span data-ttu-id="446c2-119">**2. Upgrade your scripts.**</span><span class="sxs-lookup"><span data-stu-id="446c2-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="446c2-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span><span class="sxs-lookup"><span data-stu-id="446c2-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span></span> 

<span data-ttu-id="446c2-121">**3. Upgrade your split-merge service.**</span><span class="sxs-lookup"><span data-stu-id="446c2-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="446c2-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span><span class="sxs-lookup"><span data-stu-id="446c2-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="446c2-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="446c2-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="446c2-124">**4. Upgrade your Shard Map Manager databases**.</span><span class="sxs-lookup"><span data-stu-id="446c2-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="446c2-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="446c2-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="446c2-126">There are two ways you can accomplish this, using PowerShell or C#.</span><span class="sxs-lookup"><span data-stu-id="446c2-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="446c2-127">Both options are shown below.</span><span class="sxs-lookup"><span data-stu-id="446c2-127">Both options are shown below.</span></span>

<span data-ttu-id="446c2-128">***Option 1: Upgrade metadata using PowerShell***</span><span class="sxs-lookup"><span data-stu-id="446c2-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="446c2-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span><span class="sxs-lookup"><span data-stu-id="446c2-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span></span> 
2. <span data-ttu-id="446c2-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="446c2-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="446c2-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="446c2-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="446c2-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span><span class="sxs-lookup"><span data-stu-id="446c2-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span></span>
5. <span data-ttu-id="446c2-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span><span class="sxs-lookup"><span data-stu-id="446c2-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span></span>

<span data-ttu-id="446c2-134">***Option 2: Upgrade metadata using C#***</span><span class="sxs-lookup"><span data-stu-id="446c2-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="446c2-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span><span class="sxs-lookup"><span data-stu-id="446c2-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="446c2-136">These techniques for metadata upgrades can be applied multiple times without harm.</span><span class="sxs-lookup"><span data-stu-id="446c2-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="446c2-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="446c2-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="446c2-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="446c2-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="446c2-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span><span class="sxs-lookup"><span data-stu-id="446c2-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span></span>   <span data-ttu-id="446c2-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span><span class="sxs-lookup"><span data-stu-id="446c2-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span></span>  <span data-ttu-id="446c2-141">And applications continue to operate through the upgrade sequence described above.</span><span class="sxs-lookup"><span data-stu-id="446c2-141">And applications continue to operate through the upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="446c2-142">Elastic database client version history</span><span class="sxs-lookup"><span data-stu-id="446c2-142">Elastic database client version history</span></span>
<span data-ttu-id="446c2-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="446c2-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png


