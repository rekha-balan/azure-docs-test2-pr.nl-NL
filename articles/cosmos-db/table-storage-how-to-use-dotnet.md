---
title: Get started with Azure Table storage and Azure Cosmos DB Table API using .NET | Microsoft Docs
description: Store structured data in the cloud using Azure Table storage or the Azure Cosmos DB Table API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: dotnet
ms.topic: sample
ms.date: 08/17/2018
ms.author: sngun
ms.openlocfilehash: c084a08ffef868af751d065c5857a9b67a12485f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871172"
---
# <a name="get-started-with-azure-table-storage-and-the-azure-cosmos-db-table-api-using-net"></a><span data-ttu-id="aee96-103">Get started with Azure Table storage and the Azure Cosmos DB Table API using .NET</span><span class="sxs-lookup"><span data-stu-id="aee96-103">Get started with Azure Table storage and the Azure Cosmos DB Table API using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-applies-to-storagetable-and-cosmos](../../includes/storage-table-applies-to-storagetable-and-cosmos.md)]

<span data-ttu-id="aee96-104">You can use Azure Table storage or the Azure Cosmos DB Table API to store structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span><span class="sxs-lookup"><span data-stu-id="aee96-104">You can use Azure Table storage or the Azure Cosmos DB Table API to store structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="aee96-105">Because Table storage and the Azure Cosmos DB Table API are schemaless, it's easy to adapt your data as the needs of your application evolve.</span><span class="sxs-lookup"><span data-stu-id="aee96-105">Because Table storage and the Azure Cosmos DB Table API are schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="aee96-106">Access to Table storage data and the Azure Cosmos DB Table API is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span><span class="sxs-lookup"><span data-stu-id="aee96-106">Access to Table storage data and the Azure Cosmos DB Table API is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="aee96-107">You can use Table storage or the Azure Cosmos DB Table API to store flexible datasets such as user data for web applications, address books, device information, or other types of metadata your service requires.</span><span class="sxs-lookup"><span data-stu-id="aee96-107">You can use Table storage or the Azure Cosmos DB Table API to store flexible datasets such as user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="aee96-108">You can store any number of entities in a table, and a storage account or Table API account may contain any number of tables, up to the capacity limit of the storage account or Table API account.</span><span class="sxs-lookup"><span data-stu-id="aee96-108">You can store any number of entities in a table, and a storage account or Table API account may contain any number of tables, up to the capacity limit of the storage account or Table API account.</span></span>

### <a name="about-this-sample"></a><span data-ttu-id="aee96-109">About this sample</span><span class="sxs-lookup"><span data-stu-id="aee96-109">About this sample</span></span>
<span data-ttu-id="aee96-110">This sample shows you how to use the [Microsoft Azure CosmosDB Table Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) in common Azure Table storage and Table API scenarios.</span><span class="sxs-lookup"><span data-stu-id="aee96-110">This sample shows you how to use the [Microsoft Azure CosmosDB Table Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) in common Azure Table storage and Table API scenarios.</span></span> <span data-ttu-id="aee96-111">The name of the package indicates it is for use with Azure Cosmos DB, but the package works with both the Azure Cosmos DB Table API and Azure Tables storage, each service just has a unique endpoint.</span><span class="sxs-lookup"><span data-stu-id="aee96-111">The name of the package indicates it is for use with Azure Cosmos DB, but the package works with both the Azure Cosmos DB Table API and Azure Tables storage, each service just has a unique endpoint.</span></span> <span data-ttu-id="aee96-112">These scenarios are explored using C# examples that illustrate how to:</span><span class="sxs-lookup"><span data-stu-id="aee96-112">These scenarios are explored using C# examples that illustrate how to:</span></span>
* <span data-ttu-id="aee96-113">Create and delete tables</span><span class="sxs-lookup"><span data-stu-id="aee96-113">Create and delete tables</span></span>
* <span data-ttu-id="aee96-114">Insert, update and delete rows</span><span class="sxs-lookup"><span data-stu-id="aee96-114">Insert, update and delete rows</span></span>
* <span data-ttu-id="aee96-115">Query tables</span><span class="sxs-lookup"><span data-stu-id="aee96-115">Query tables</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aee96-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aee96-116">Prerequisites</span></span>

<span data-ttu-id="aee96-117">You need the following to complete this sample successfully:</span><span class="sxs-lookup"><span data-stu-id="aee96-117">You need the following to complete this sample successfully:</span></span>

* [<span data-ttu-id="aee96-118">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aee96-118">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="aee96-119">[Azure Storage Common Library for .NET (Preview)](https://www.nuget.org/packages/Microsoft.Azure.Storage.Common/).</span><span class="sxs-lookup"><span data-stu-id="aee96-119">[Azure Storage Common Library for .NET (Preview)](https://www.nuget.org/packages/Microsoft.Azure.Storage.Common/).</span></span> <span data-ttu-id="aee96-120">- A required preview package that is supported in production environments.</span><span class="sxs-lookup"><span data-stu-id="aee96-120">- A required preview package that is supported in production environments.</span></span> 
* <span data-ttu-id="aee96-121">[Microsoft Azure CosmosDB Table Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) - This library is currently available for .NET Standard only, it's not yet available for .NET Core.</span><span class="sxs-lookup"><span data-stu-id="aee96-121">[Microsoft Azure CosmosDB Table Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) - This library is currently available for .NET Standard only, it's not yet available for .NET Core.</span></span>
* [<span data-ttu-id="aee96-122">Azure Configuration Manager for .NET</span><span class="sxs-lookup"><span data-stu-id="aee96-122">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="aee96-123">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="aee96-123">Azure storage account</span></span>](../storage/common/storage-quickstart-create-account.md)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="aee96-124">More samples</span><span class="sxs-lookup"><span data-stu-id="aee96-124">More samples</span></span>
<span data-ttu-id="aee96-125">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="aee96-125">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="aee96-126">You can download the sample application and run it, or browse the code on GitHub.</span><span class="sxs-lookup"><span data-stu-id="aee96-126">You can download the sample application and run it, or browse the code on GitHub.</span></span>

## <a name="create-an-azure-service-account"></a><span data-ttu-id="aee96-127">Create an Azure service account</span><span class="sxs-lookup"><span data-stu-id="aee96-127">Create an Azure service account</span></span>
[!INCLUDE [cosmos-db-create-azure-service-account](../../includes/cosmos-db-create-azure-service-account.md)]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="aee96-128">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="aee96-128">Create an Azure storage account</span></span>
* <span data-ttu-id="aee96-129">The easiest way to create your first Azure storage account is by using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aee96-129">The easiest way to create your first Azure storage account is by using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="aee96-130">To learn more, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="aee96-130">To learn more, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span>

* <span data-ttu-id="aee96-131">You can also create an Azure storage account by using [Azure PowerShell](../storage/common/storage-powershell-guide-full.md), [Azure CLI](../storage/common/storage-azure-cli.md), or the [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage).</span><span class="sxs-lookup"><span data-stu-id="aee96-131">You can also create an Azure storage account by using [Azure PowerShell](../storage/common/storage-powershell-guide-full.md), [Azure CLI](../storage/common/storage-azure-cli.md), or the [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage).</span></span>

* <span data-ttu-id="aee96-132">If you prefer not to create a storage account at this time, you can also use the Azure storage emulator to run and test your code in a local environment.</span><span class="sxs-lookup"><span data-stu-id="aee96-132">If you prefer not to create a storage account at this time, you can also use the Azure storage emulator to run and test your code in a local environment.</span></span> <span data-ttu-id="aee96-133">For more information, see [Use the Azure Storage Emulator for Development and Testing](../storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="aee96-133">For more information, see [Use the Azure Storage Emulator for Development and Testing](../storage/common/storage-use-emulator.md).</span></span>

### <a name="create-an-azure-cosmos-db-table-api-account"></a><span data-ttu-id="aee96-134">Create an Azure Cosmos DB Table API account</span><span class="sxs-lookup"><span data-stu-id="aee96-134">Create an Azure Cosmos DB Table API account</span></span>
[!INCLUDE [cosmos-db-create-tableapi-account](../../includes/cosmos-db-create-tableapi-account.md)]

### <a name="create-a-windows-console-application-project"></a><span data-ttu-id="aee96-135">Create a Windows console application project</span><span class="sxs-lookup"><span data-stu-id="aee96-135">Create a Windows console application project</span></span>
<span data-ttu-id="aee96-136">In Visual Studio, create a new Windows console application.</span><span class="sxs-lookup"><span data-stu-id="aee96-136">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="aee96-137">The following steps show you how to create a console application in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="aee96-137">The following steps show you how to create a console application in Visual Studio 2017.</span></span> <span data-ttu-id="aee96-138">The steps are similar in other versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aee96-138">The steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="aee96-139">Select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="aee96-139">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="aee96-140">Select **Installed** > **Visual C#** > **Windows Classic Desktop**.</span><span class="sxs-lookup"><span data-stu-id="aee96-140">Select **Installed** > **Visual C#** > **Windows Classic Desktop**.</span></span>
3. <span data-ttu-id="aee96-141">Select **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="aee96-141">Select **Console App (.NET Framework)**.</span></span>
4. <span data-ttu-id="aee96-142">In the **Name** field, enter a name for your application.</span><span class="sxs-lookup"><span data-stu-id="aee96-142">In the **Name** field, enter a name for your application.</span></span>
5. <span data-ttu-id="aee96-143">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="aee96-143">Select **OK**.</span></span>

<span data-ttu-id="aee96-144">All code examples in this sample can be added to the `Main()` method of your console application's `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="aee96-144">All code examples in this sample can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="aee96-145">You can use the Azure CosmosDB Table Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span><span class="sxs-lookup"><span data-stu-id="aee96-145">You can use the Azure CosmosDB Table Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="aee96-146">In this guide, we use a console application for simplicity.</span><span class="sxs-lookup"><span data-stu-id="aee96-146">In this guide, we use a console application for simplicity.</span></span>

### <a name="install-the-required-nuget-packages"></a><span data-ttu-id="aee96-147">Install the required NuGet packages</span><span class="sxs-lookup"><span data-stu-id="aee96-147">Install the required NuGet packages</span></span>
<span data-ttu-id="aee96-148">There are three recommended packages you need to reference in your project to complete this sample:</span><span class="sxs-lookup"><span data-stu-id="aee96-148">There are three recommended packages you need to reference in your project to complete this sample:</span></span>

* <span data-ttu-id="aee96-149">[Azure Storage Common Library for .NET (preview)](https://www.nuget.org/packages/Microsoft.Azure.Storage.Common).</span><span class="sxs-lookup"><span data-stu-id="aee96-149">[Azure Storage Common Library for .NET (preview)](https://www.nuget.org/packages/Microsoft.Azure.Storage.Common).</span></span> <span data-ttu-id="aee96-150">- Use a version which is less than or equal to 9.0.0.1 (<= 9.0.0.1).</span><span class="sxs-lookup"><span data-stu-id="aee96-150">- Use a version which is less than or equal to 9.0.0.1 (<= 9.0.0.1).</span></span>

* <span data-ttu-id="aee96-151">[Microsoft Azure Cosmos DB Table Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table).</span><span class="sxs-lookup"><span data-stu-id="aee96-151">[Microsoft Azure Cosmos DB Table Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table).</span></span> <span data-ttu-id="aee96-152">This package provides programmatic access to data resources in your Azure Table storage account or Azure Cosmos DB Table API account.</span><span class="sxs-lookup"><span data-stu-id="aee96-152">This package provides programmatic access to data resources in your Azure Table storage account or Azure Cosmos DB Table API account.</span></span> <span data-ttu-id="aee96-153">This library is currently available for .NET Standard only, it's not yet available for .NET Core.</span><span class="sxs-lookup"><span data-stu-id="aee96-153">This library is currently available for .NET Standard only, it's not yet available for .NET Core.</span></span>

* <span data-ttu-id="aee96-154">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span><span class="sxs-lookup"><span data-stu-id="aee96-154">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="aee96-155">To obtain the NuGet packages, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="aee96-155">To obtain the NuGet packages, follow these steps:</span></span>

1. <span data-ttu-id="aee96-156">Right-click your project in **Solution Explorer**, and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="aee96-156">Right-click your project in **Solution Explorer**, and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="aee96-157">Search online for "Microsoft.Azure.Storage.Common", choose version <= 9.0.0.1 and select **Install** to install the Azure Storage Common Library for .NET (Preview) and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="aee96-157">Search online for "Microsoft.Azure.Storage.Common", choose version <= 9.0.0.1 and select **Install** to install the Azure Storage Common Library for .NET (Preview) and its dependencies.</span></span> <span data-ttu-id="aee96-158">Ensure the **Include prerelease** box is checked as this is a preview package.</span><span class="sxs-lookup"><span data-stu-id="aee96-158">Ensure the **Include prerelease** box is checked as this is a preview package.</span></span>
3. <span data-ttu-id="aee96-159">Search online for "Microsoft.Azure.CosmosDB.Table", and select **Install** to install the Microsoft Azure CosmosDB Table Library.</span><span class="sxs-lookup"><span data-stu-id="aee96-159">Search online for "Microsoft.Azure.CosmosDB.Table", and select **Install** to install the Microsoft Azure CosmosDB Table Library.</span></span>
4. <span data-ttu-id="aee96-160">Search online for "WindowsAzure.ConfigurationManager", and select **Install** to install the Microsoft Azure Configuration Manager Library.</span><span class="sxs-lookup"><span data-stu-id="aee96-160">Search online for "WindowsAzure.ConfigurationManager", and select **Install** to install the Microsoft Azure Configuration Manager Library.</span></span>

> [!NOTE]
> <span data-ttu-id="aee96-161">The ODataLib dependencies in the Storage Common Library for .NET are resolved by the ODataLib packages available on NuGet, not from WCF Data Services.</span><span class="sxs-lookup"><span data-stu-id="aee96-161">The ODataLib dependencies in the Storage Common Library for .NET are resolved by the ODataLib packages available on NuGet, not from WCF Data Services.</span></span> <span data-ttu-id="aee96-162">The ODataLib libraries can be downloaded directly, or referenced by your code project through NuGet.</span><span class="sxs-lookup"><span data-stu-id="aee96-162">The ODataLib libraries can be downloaded directly, or referenced by your code project through NuGet.</span></span> <span data-ttu-id="aee96-163">The specific ODataLib packages used by the Storage Client Library are [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), and [Spatial](http://nuget.org/packages/System.Spatial/).</span><span class="sxs-lookup"><span data-stu-id="aee96-163">The specific ODataLib packages used by the Storage Client Library are [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), and [Spatial](http://nuget.org/packages/System.Spatial/).</span></span> <span data-ttu-id="aee96-164">While these libraries are used by the Azure Table storage classes, they are required dependencies for programming with the Storage Common Library.</span><span class="sxs-lookup"><span data-stu-id="aee96-164">While these libraries are used by the Azure Table storage classes, they are required dependencies for programming with the Storage Common Library.</span></span>
> 
> 

> [!TIP]
> <span data-ttu-id="aee96-165">Developers already familiar with Azure Table storage may have used the [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) package in the past.</span><span class="sxs-lookup"><span data-stu-id="aee96-165">Developers already familiar with Azure Table storage may have used the [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) package in the past.</span></span> <span data-ttu-id="aee96-166">It is recommended that all new table applications use the [Azure Storage Common Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.Common) and the [Azure Cosmos DB Table Library](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table), however the WindowsAzure.Storage package is still supported.</span><span class="sxs-lookup"><span data-stu-id="aee96-166">It is recommended that all new table applications use the [Azure Storage Common Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.Common) and the [Azure Cosmos DB Table Library](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table), however the WindowsAzure.Storage package is still supported.</span></span> <span data-ttu-id="aee96-167">If you use the WindowsAzure.Storage library, include Microsoft.WindowsAzure.Storage.Table in your using statements.</span><span class="sxs-lookup"><span data-stu-id="aee96-167">If you use the WindowsAzure.Storage library, include Microsoft.WindowsAzure.Storage.Table in your using statements.</span></span>
>
>

### <a name="determine-your-target-environment"></a><span data-ttu-id="aee96-168">Determine your target environment</span><span class="sxs-lookup"><span data-stu-id="aee96-168">Determine your target environment</span></span>
<span data-ttu-id="aee96-169">You have three environment options for running the examples in this guide:</span><span class="sxs-lookup"><span data-stu-id="aee96-169">You have three environment options for running the examples in this guide:</span></span>

* <span data-ttu-id="aee96-170">You can run your code against an Azure Storage account in the cloud.</span><span class="sxs-lookup"><span data-stu-id="aee96-170">You can run your code against an Azure Storage account in the cloud.</span></span> 
* <span data-ttu-id="aee96-171">You can run your code against an Azure Cosmos DB account in the cloud.</span><span class="sxs-lookup"><span data-stu-id="aee96-171">You can run your code against an Azure Cosmos DB account in the cloud.</span></span>
* <span data-ttu-id="aee96-172">You can run your code against the Azure storage emulator.</span><span class="sxs-lookup"><span data-stu-id="aee96-172">You can run your code against the Azure storage emulator.</span></span> <span data-ttu-id="aee96-173">The storage emulator is a local environment that emulates an Azure Storage account in the cloud.</span><span class="sxs-lookup"><span data-stu-id="aee96-173">The storage emulator is a local environment that emulates an Azure Storage account in the cloud.</span></span> <span data-ttu-id="aee96-174">The emulator is a free option for testing and debugging your code while your application is under development.</span><span class="sxs-lookup"><span data-stu-id="aee96-174">The emulator is a free option for testing and debugging your code while your application is under development.</span></span> <span data-ttu-id="aee96-175">The emulator uses a well-known account and key.</span><span class="sxs-lookup"><span data-stu-id="aee96-175">The emulator uses a well-known account and key.</span></span> <span data-ttu-id="aee96-176">For more information, see [Use the Azure storage emulator for development and testing](../storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="aee96-176">For more information, see [Use the Azure storage emulator for development and testing](../storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="aee96-177">If you are targeting a storage account in the cloud, copy the primary access key for your storage account from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aee96-177">If you are targeting a storage account in the cloud, copy the primary access key for your storage account from the Azure portal.</span></span> <span data-ttu-id="aee96-178">For more information, see [View and copy storage access keys](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="aee96-178">For more information, see [View and copy storage access keys](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

> [!NOTE]
> <span data-ttu-id="aee96-179">You can target the storage emulator to avoid incurring any costs associated with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aee96-179">You can target the storage emulator to avoid incurring any costs associated with Azure Storage.</span></span> <span data-ttu-id="aee96-180">However, if you do choose to target an Azure storage account in the cloud, costs for performing this sample will be negligible.</span><span class="sxs-lookup"><span data-stu-id="aee96-180">However, if you do choose to target an Azure storage account in the cloud, costs for performing this sample will be negligible.</span></span>
> 
> 

<span data-ttu-id="aee96-181">If you are targeting an Azure Cosmos DB account, copy the primary access key for your Table API account from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aee96-181">If you are targeting an Azure Cosmos DB account, copy the primary access key for your Table API account from the Azure portal.</span></span> <span data-ttu-id="aee96-182">For more information, see [Update your connection string](create-table-dotnet.md#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="aee96-182">For more information, see [Update your connection string](create-table-dotnet.md#update-your-connection-string).</span></span>

### <a name="configure-your-storage-connection-string"></a><span data-ttu-id="aee96-183">Configure your storage connection string</span><span class="sxs-lookup"><span data-stu-id="aee96-183">Configure your storage connection string</span></span>
<span data-ttu-id="aee96-184">The Azure Storage Common Library for .NET supports using a storage connection string to configure endpoints and credentials for accessing storage services.</span><span class="sxs-lookup"><span data-stu-id="aee96-184">The Azure Storage Common Library for .NET supports using a storage connection string to configure endpoints and credentials for accessing storage services.</span></span> <span data-ttu-id="aee96-185">The best way to maintain your storage connection string is in a configuration file.</span><span class="sxs-lookup"><span data-stu-id="aee96-185">The best way to maintain your storage connection string is in a configuration file.</span></span> 

<span data-ttu-id="aee96-186">For more information about connection strings, see [Configure a connection string to Azure Storage](../storage/common/storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="aee96-186">For more information about connection strings, see [Configure a connection string to Azure Storage](../storage/common/storage-configure-connection-string.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aee96-187">Your account key is similar to the root password for your storage account.</span><span class="sxs-lookup"><span data-stu-id="aee96-187">Your account key is similar to the root password for your storage account.</span></span> <span data-ttu-id="aee96-188">Always be careful to protect your storage account key.</span><span class="sxs-lookup"><span data-stu-id="aee96-188">Always be careful to protect your storage account key.</span></span> <span data-ttu-id="aee96-189">Avoid distributing it to other users, hard-coding it, or saving it in a plain-text file that is accessible to others.</span><span class="sxs-lookup"><span data-stu-id="aee96-189">Avoid distributing it to other users, hard-coding it, or saving it in a plain-text file that is accessible to others.</span></span> <span data-ttu-id="aee96-190">Regenerate your key by using the Azure portal if you believe it may have been compromised.</span><span class="sxs-lookup"><span data-stu-id="aee96-190">Regenerate your key by using the Azure portal if you believe it may have been compromised.</span></span>
> 
> 

<span data-ttu-id="aee96-191">To configure your connection string, open the `app.config` file from Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aee96-191">To configure your connection string, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="aee96-192">Add the contents of the `<appSettings>` element shown below.</span><span class="sxs-lookup"><span data-stu-id="aee96-192">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="aee96-193">Replace `account-name` with the name of your account, and `account-key` with your account access key:</span><span class="sxs-lookup"><span data-stu-id="aee96-193">Replace `account-name` with the name of your account, and `account-key` with your account access key:</span></span>

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

<span data-ttu-id="aee96-194">For example, if you're using an Azure Storage account, your configuration settings appear similar to:</span><span class="sxs-lookup"><span data-stu-id="aee96-194">For example, if you're using an Azure Storage account, your configuration settings appear similar to:</span></span>

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>" />
```

<span data-ttu-id="aee96-195">If you're using an Azure Cosmos DB account, your configuration settings appear similar to:</span><span class="sxs-lookup"><span data-stu-id="aee96-195">If you're using an Azure Cosmos DB account, your configuration settings appear similar to:</span></span>

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=tableapiacct;AccountKey=<account-key>;TableEndpoint=https://tableapiacct.table.cosmosdb.azure.com:443/;" />
```

<span data-ttu-id="aee96-196">To target the storage emulator, you can use a shortcut that maps to the well-known account name and key.</span><span class="sxs-lookup"><span data-stu-id="aee96-196">To target the storage emulator, you can use a shortcut that maps to the well-known account name and key.</span></span> <span data-ttu-id="aee96-197">In that case, your connection string setting is:</span><span class="sxs-lookup"><span data-stu-id="aee96-197">In that case, your connection string setting is:</span></span>

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

### <a name="add-using-directives"></a><span data-ttu-id="aee96-198">Add using directives</span><span class="sxs-lookup"><span data-stu-id="aee96-198">Add using directives</span></span>
<span data-ttu-id="aee96-199">Add the following **using** directives to the top of the `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="aee96-199">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.Azure.Storage; // Namespace for StorageAccounts
using Microsoft.Azure.CosmosDB.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="aee96-200">Parse the connection string</span><span class="sxs-lookup"><span data-stu-id="aee96-200">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="aee96-201">Create the Table service client</span><span class="sxs-lookup"><span data-stu-id="aee96-201">Create the Table service client</span></span>
<span data-ttu-id="aee96-202">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span><span class="sxs-lookup"><span data-stu-id="aee96-202">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="aee96-203">Here's one way to create the Table service client:</span><span class="sxs-lookup"><span data-stu-id="aee96-203">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="aee96-204">Now you are ready to write code that reads data from and writes data to Table storage.</span><span class="sxs-lookup"><span data-stu-id="aee96-204">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="aee96-205">Create a table</span><span class="sxs-lookup"><span data-stu-id="aee96-205">Create a table</span></span>
<span data-ttu-id="aee96-206">This example shows how to create a table if it does not already exist:</span><span class="sxs-lookup"><span data-stu-id="aee96-206">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="aee96-207">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="aee96-207">Add an entity to a table</span></span>
<span data-ttu-id="aee96-208">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="aee96-208">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="aee96-209">To add an entity to a table, create a class that defines the properties of your entity.</span><span class="sxs-lookup"><span data-stu-id="aee96-209">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="aee96-210">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span><span class="sxs-lookup"><span data-stu-id="aee96-210">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="aee96-211">Together, an entity's partition and row key uniquely identify it in the table.</span><span class="sxs-lookup"><span data-stu-id="aee96-211">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="aee96-212">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span><span class="sxs-lookup"><span data-stu-id="aee96-212">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="aee96-213">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span><span class="sxs-lookup"><span data-stu-id="aee96-213">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="aee96-214">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span><span class="sxs-lookup"><span data-stu-id="aee96-214">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="aee96-215">Also, your entity type *must* expose a parameter-less constructor.</span><span class="sxs-lookup"><span data-stu-id="aee96-215">Also, your entity type *must* expose a parameter-less constructor.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="aee96-216">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span><span class="sxs-lookup"><span data-stu-id="aee96-216">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="aee96-217">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span><span class="sxs-lookup"><span data-stu-id="aee96-217">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="aee96-218">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="aee96-218">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="aee96-219">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span><span class="sxs-lookup"><span data-stu-id="aee96-219">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="aee96-220">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="aee96-220">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="aee96-221">Insert a batch of entities</span><span class="sxs-lookup"><span data-stu-id="aee96-221">Insert a batch of entities</span></span>
<span data-ttu-id="aee96-222">You can insert a batch of entities into a table in one write operation.</span><span class="sxs-lookup"><span data-stu-id="aee96-222">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="aee96-223">Some other notes on batch operations:</span><span class="sxs-lookup"><span data-stu-id="aee96-223">Some other notes on batch operations:</span></span>

* <span data-ttu-id="aee96-224">You can perform updates, deletes, and inserts in the same single batch operation.</span><span class="sxs-lookup"><span data-stu-id="aee96-224">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="aee96-225">A single batch operation can include up to 100 entities.</span><span class="sxs-lookup"><span data-stu-id="aee96-225">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="aee96-226">All entities in a single batch operation must have the same partition key.</span><span class="sxs-lookup"><span data-stu-id="aee96-226">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="aee96-227">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span><span class="sxs-lookup"><span data-stu-id="aee96-227">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="aee96-228">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span><span class="sxs-lookup"><span data-stu-id="aee96-228">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="aee96-229">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span><span class="sxs-lookup"><span data-stu-id="aee96-229">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="aee96-230">Retrieve all entities in a partition</span><span class="sxs-lookup"><span data-stu-id="aee96-230">Retrieve all entities in a partition</span></span>
<span data-ttu-id="aee96-231">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span><span class="sxs-lookup"><span data-stu-id="aee96-231">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="aee96-232">The following code example specifies a filter for entities where 'Smith' is the partition key.</span><span class="sxs-lookup"><span data-stu-id="aee96-232">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="aee96-233">This example prints the fields of each entity in the query results to the console.</span><span class="sxs-lookup"><span data-stu-id="aee96-233">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="aee96-234">Retrieve a range of entities in a partition</span><span class="sxs-lookup"><span data-stu-id="aee96-234">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="aee96-235">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span><span class="sxs-lookup"><span data-stu-id="aee96-235">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="aee96-236">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span><span class="sxs-lookup"><span data-stu-id="aee96-236">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="aee96-237">Retrieve a single entity</span><span class="sxs-lookup"><span data-stu-id="aee96-237">Retrieve a single entity</span></span>
<span data-ttu-id="aee96-238">You can write a query to retrieve a single, specific entity.</span><span class="sxs-lookup"><span data-stu-id="aee96-238">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="aee96-239">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="aee96-239">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="aee96-240">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="aee96-240">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="aee96-241">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span><span class="sxs-lookup"><span data-stu-id="aee96-241">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="aee96-242">Replace an entity</span><span class="sxs-lookup"><span data-stu-id="aee96-242">Replace an entity</span></span>
<span data-ttu-id="aee96-243">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span><span class="sxs-lookup"><span data-stu-id="aee96-243">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="aee96-244">The following code changes an existing customer's phone number.</span><span class="sxs-lookup"><span data-stu-id="aee96-244">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="aee96-245">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="aee96-245">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="aee96-246">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span><span class="sxs-lookup"><span data-stu-id="aee96-246">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="aee96-247">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span><span class="sxs-lookup"><span data-stu-id="aee96-247">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="aee96-248">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span><span class="sxs-lookup"><span data-stu-id="aee96-248">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="aee96-249">The next section will show you how to override this behavior.</span><span class="sxs-lookup"><span data-stu-id="aee96-249">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="aee96-250">Insert-or-replace an entity</span><span class="sxs-lookup"><span data-stu-id="aee96-250">Insert-or-replace an entity</span></span>
<span data-ttu-id="aee96-251">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span><span class="sxs-lookup"><span data-stu-id="aee96-251">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="aee96-252">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span><span class="sxs-lookup"><span data-stu-id="aee96-252">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="aee96-253">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span><span class="sxs-lookup"><span data-stu-id="aee96-253">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="aee96-254">Your update should overwrite them all.</span><span class="sxs-lookup"><span data-stu-id="aee96-254">Your update should overwrite them all.</span></span> <span data-ttu-id="aee96-255">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span><span class="sxs-lookup"><span data-stu-id="aee96-255">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="aee96-256">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span><span class="sxs-lookup"><span data-stu-id="aee96-256">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="aee96-257">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span><span class="sxs-lookup"><span data-stu-id="aee96-257">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="aee96-258">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span><span class="sxs-lookup"><span data-stu-id="aee96-258">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="aee96-259">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span><span class="sxs-lookup"><span data-stu-id="aee96-259">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="aee96-260">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span><span class="sxs-lookup"><span data-stu-id="aee96-260">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="aee96-261">Query a subset of entity properties</span><span class="sxs-lookup"><span data-stu-id="aee96-261">Query a subset of entity properties</span></span>
<span data-ttu-id="aee96-262">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span><span class="sxs-lookup"><span data-stu-id="aee96-262">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="aee96-263">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span><span class="sxs-lookup"><span data-stu-id="aee96-263">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="aee96-264">The query in the following code returns only the email addresses of entities in the table.</span><span class="sxs-lookup"><span data-stu-id="aee96-264">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="aee96-265">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="aee96-265">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="aee96-266">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="aee96-266">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="aee96-267">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span><span class="sxs-lookup"><span data-stu-id="aee96-267">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="aee96-268">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="aee96-268">Delete an entity</span></span>
<span data-ttu-id="aee96-269">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span><span class="sxs-lookup"><span data-stu-id="aee96-269">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="aee96-270">The following code retrieves and deletes a customer entity.</span><span class="sxs-lookup"><span data-stu-id="aee96-270">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="aee96-271">Delete a table</span><span class="sxs-lookup"><span data-stu-id="aee96-271">Delete a table</span></span>
<span data-ttu-id="aee96-272">Finally, the following code example deletes a table from a storage account.</span><span class="sxs-lookup"><span data-stu-id="aee96-272">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="aee96-273">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span><span class="sxs-lookup"><span data-stu-id="aee96-273">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="aee96-274">Retrieve entities in pages asynchronously</span><span class="sxs-lookup"><span data-stu-id="aee96-274">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="aee96-275">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span><span class="sxs-lookup"><span data-stu-id="aee96-275">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="aee96-276">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span><span class="sxs-lookup"><span data-stu-id="aee96-276">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="aee96-277">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="aee96-277">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="aee96-278">Next steps</span><span class="sxs-lookup"><span data-stu-id="aee96-278">Next steps</span></span>
<span data-ttu-id="aee96-279">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span><span class="sxs-lookup"><span data-stu-id="aee96-279">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="aee96-280">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="aee96-280">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="aee96-281">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="aee96-281">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="aee96-282">View the Table service reference documentation for complete details about available APIs:</span><span class="sxs-lookup"><span data-stu-id="aee96-282">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="aee96-283">Storage Client Library for .NET reference</span><span class="sxs-lookup"><span data-stu-id="aee96-283">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="aee96-284">REST API reference</span><span class="sxs-lookup"><span data-stu-id="aee96-284">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="aee96-285">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki)</span><span class="sxs-lookup"><span data-stu-id="aee96-285">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki)</span></span>
* <span data-ttu-id="aee96-286">View more feature guides to learn about additional options for storing data in Azure.</span><span class="sxs-lookup"><span data-stu-id="aee96-286">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="aee96-287">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span><span class="sxs-lookup"><span data-stu-id="aee96-287">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="aee96-288">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span><span class="sxs-lookup"><span data-stu-id="aee96-288">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
