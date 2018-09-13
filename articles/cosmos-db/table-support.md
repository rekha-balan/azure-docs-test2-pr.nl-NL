---
title: Azure Table Storage support in Azure Cosmos DB | Microsoft Docs
description: Learn how Azure Cosmos DB Table API and Azure Storage Tables work together.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: na
ms.topic: overview
ms.date: 11/15/2017
ms.author: sngun
ms.openlocfilehash: 114286b45df5f47e81bd2b990c8b50c8b7b7a482
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965901"
---
# <a name="developing-with-azure-cosmos-db-table-api-and-azure-table-storage"></a><span data-ttu-id="9fb7e-103">Developing with Azure Cosmos DB Table API and Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="9fb7e-103">Developing with Azure Cosmos DB Table API and Azure Table storage</span></span>

<span data-ttu-id="9fb7e-104">Azure Cosmos DB Table API and Azure Table storage share the same table data model and expose the same create, delete, update, and query operations through their SDKs.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-104">Azure Cosmos DB Table API and Azure Table storage share the same table data model and expose the same create, delete, update, and query operations through their SDKs.</span></span> 

[!INCLUDE [storage-table-cosmos-comparison](../../includes/storage-table-cosmos-comparison.md)]

## <a name="developing-with-the-azure-cosmos-db-table-api"></a><span data-ttu-id="9fb7e-105">Developing with the Azure Cosmos DB Table API</span><span class="sxs-lookup"><span data-stu-id="9fb7e-105">Developing with the Azure Cosmos DB Table API</span></span>

<span data-ttu-id="9fb7e-106">At this time, the [Azure Cosmos DB Table API](table-introduction.md) has four SDKs available for development:</span><span class="sxs-lookup"><span data-stu-id="9fb7e-106">At this time, the [Azure Cosmos DB Table API](table-introduction.md) has four SDKs available for development:</span></span> 
- <span data-ttu-id="9fb7e-107">[Microsoft.Azure.CosmosDB.Table](https://aka.ms/tableapinuget) .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-107">[Microsoft.Azure.CosmosDB.Table](https://aka.ms/tableapinuget) .NET SDK.</span></span> <span data-ttu-id="9fb7e-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the Table API.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the Table API.</span></span> <span data-ttu-id="9fb7e-109">Note that the `Microsoft.Azure.CosmosDB.Table` library is currently available for .NET Standard only, it's not yet available for .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-109">Note that the `Microsoft.Azure.CosmosDB.Table` library is currently available for .NET Standard only, it's not yet available for .NET Core.</span></span>
- <span data-ttu-id="9fb7e-110">[Python SDK](table-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-110">[Python SDK](table-sdk-python.md).</span></span> <span data-ttu-id="9fb7e-111">The new Azure Cosmos DB Python SDK is the only SDK that supports Azure Table storage in Python.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-111">The new Azure Cosmos DB Python SDK is the only SDK that supports Azure Table storage in Python.</span></span> <span data-ttu-id="9fb7e-112">This SDK connects with both Azure Table storage and Azure Cosmos DB Table API.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-112">This SDK connects with both Azure Table storage and Azure Cosmos DB Table API.</span></span>
- <span data-ttu-id="9fb7e-113">[Java SDK](table-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-113">[Java SDK](table-sdk-java.md).</span></span> <span data-ttu-id="9fb7e-114">This Azure Storage SDK has the ability to connect to Azure Cosmos DB accounts using the Table API.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-114">This Azure Storage SDK has the ability to connect to Azure Cosmos DB accounts using the Table API.</span></span>
- <span data-ttu-id="9fb7e-115">[Node.js SDK](table-sdk-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-115">[Node.js SDK](table-sdk-nodejs.md).</span></span> <span data-ttu-id="9fb7e-116">This Azure Storage SDK has the ability to connect to Azure Cosmos DB accounts using the Table API.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-116">This Azure Storage SDK has the ability to connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="9fb7e-117">Additional information about working with the Table API is available in the [FAQ: Develop with the Table API](faq.md#table) article.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-117">Additional information about working with the Table API is available in the [FAQ: Develop with the Table API](faq.md#table) article.</span></span>

## <a name="developing-with-azure-table-storage"></a><span data-ttu-id="9fb7e-118">Developing with Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="9fb7e-118">Developing with Azure Table storage</span></span>

<span data-ttu-id="9fb7e-119">Azure Table storage has these SDKs available for development:</span><span class="sxs-lookup"><span data-stu-id="9fb7e-119">Azure Table storage has these SDKs available for development:</span></span>

- <span data-ttu-id="9fb7e-120">[WindowsAzure.Storage .NET SDK](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-120">[WindowsAzure.Storage .NET SDK](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="9fb7e-121">This library enables you to work with the storage Table service.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-121">This library enables you to work with the storage Table service.</span></span>
- <span data-ttu-id="9fb7e-122">[Python SDK](table-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-122">[Python SDK](table-sdk-python.md).</span></span> <span data-ttu-id="9fb7e-123">The Azure Cosmos DB Table SDK for Python also supports the storage Table service.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-123">The Azure Cosmos DB Table SDK for Python also supports the storage Table service.</span></span>
- <span data-ttu-id="9fb7e-124">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-124">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java).</span></span> <span data-ttu-id="9fb7e-125">This Azure Storage SDK provides a client library in Java to consume Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-125">This Azure Storage SDK provides a client library in Java to consume Azure Table storage.</span></span>
- <span data-ttu-id="9fb7e-126">[Node.js SDK](table-sdk-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-126">[Node.js SDK](table-sdk-nodejs.md).</span></span> <span data-ttu-id="9fb7e-127">This SDK provides a Node.js package and a browser-compatible JavaScript client library to consume the storage Table service.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-127">This SDK provides a Node.js package and a browser-compatible JavaScript client library to consume the storage Table service.</span></span>
- <span data-ttu-id="9fb7e-128">[AzureRmStorageTable PowerShell module](https://www.powershellgallery.com/packages/AzureRmStorageTable/1.0.0.7).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-128">[AzureRmStorageTable PowerShell module](https://www.powershellgallery.com/packages/AzureRmStorageTable/1.0.0.7).</span></span> <span data-ttu-id="9fb7e-129">This PowerShell module has cmdlets to work with storage Tables.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-129">This PowerShell module has cmdlets to work with storage Tables.</span></span>
- <span data-ttu-id="9fb7e-130">[Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-130">[Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/).</span></span> <span data-ttu-id="9fb7e-131">This library enables you to build applications against Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-131">This library enables you to build applications against Azure Storage.</span></span>
- <span data-ttu-id="9fb7e-132">[Azure Storage Table Client Library for Ruby](https://github.com/azure/azure-storage-ruby/tree/master/table).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-132">[Azure Storage Table Client Library for Ruby](https://github.com/azure/azure-storage-ruby/tree/master/table).</span></span> <span data-ttu-id="9fb7e-133">This project provides a Ruby package that makes it easy to access Azure storage Table services.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-133">This project provides a Ruby package that makes it easy to access Azure storage Table services.</span></span>
- <span data-ttu-id="9fb7e-134">[Azure Storage Table PHP Client Library](https://github.com/Azure/azure-storage-php/tree/master/azure-storage-table).</span><span class="sxs-lookup"><span data-stu-id="9fb7e-134">[Azure Storage Table PHP Client Library](https://github.com/Azure/azure-storage-php/tree/master/azure-storage-table).</span></span> <span data-ttu-id="9fb7e-135">This project provides a PHP client library that makes it easy to access Azure storage Table services.</span><span class="sxs-lookup"><span data-stu-id="9fb7e-135">This project provides a PHP client library that makes it easy to access Azure storage Table services.</span></span>


   





