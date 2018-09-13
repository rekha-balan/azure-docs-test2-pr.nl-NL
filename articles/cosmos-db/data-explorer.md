---
title: Use Azure Cosmos DB explorer to manage your data  | Microsoft Docs
description: Azure Cosmos DB explorer is a standalone web-based interface that allows you to view and manage the data stored in Azure Cosmos DB.
services: cosmos-db
author: deborahc
manager: kfile
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 07/16/2018
ms.author: dech
ms.openlocfilehash: 8d1bd0d4331937e37307140e17e5aed1a6e3b0ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866080"
---
# <a name="use-azure-cosmos-db-explorer-to-manage-your-data"></a><span data-ttu-id="9c5cb-103">Use Azure Cosmos DB explorer to manage your data</span><span class="sxs-lookup"><span data-stu-id="9c5cb-103">Use Azure Cosmos DB explorer to manage your data</span></span> 

<span data-ttu-id="9c5cb-104">Azure Cosmos DB explorer is a standalone web-based interface that allows you to view and manage the data stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-104">Azure Cosmos DB explorer is a standalone web-based interface that allows you to view and manage the data stored in Azure Cosmos DB.</span></span> <span data-ttu-id="9c5cb-105">Azure Cosmos DB explorer is equivalent to the existing **Data Explorer** tab that is available in Azure portal when you create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-105">Azure Cosmos DB explorer is equivalent to the existing **Data Explorer** tab that is available in Azure portal when you create an Azure Cosmos DB account.</span></span> <span data-ttu-id="9c5cb-106">The key advantages of Azure Cosmos DB explorer over the existing Data explorer are:</span><span class="sxs-lookup"><span data-stu-id="9c5cb-106">The key advantages of Azure Cosmos DB explorer over the existing Data explorer are:</span></span>

* <span data-ttu-id="9c5cb-107">You have a full screen real-estate to view your data, run queries, stored procedures, triggers, and view their results.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-107">You have a full screen real-estate to view your data, run queries, stored procedures, triggers, and view their results.</span></span>  

* <span data-ttu-id="9c5cb-108">You can provide temporary or permanent read or read-write access to your database account and its collections to other users who do not have access to Azure portal or subscription.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-108">You can provide temporary or permanent read or read-write access to your database account and its collections to other users who do not have access to Azure portal or subscription.</span></span>  

* <span data-ttu-id="9c5cb-109">You can share the query results with other users who do not have access to Azure portal or subscription.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-109">You can share the query results with other users who do not have access to Azure portal or subscription.</span></span>  

## <a name="access-azure-cosmos-db-explorer"></a><span data-ttu-id="9c5cb-110">Access Azure Cosmos DB explorer</span><span class="sxs-lookup"><span data-stu-id="9c5cb-110">Access Azure Cosmos DB explorer</span></span>

1. <span data-ttu-id="9c5cb-111">Sign in to [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c5cb-111">Sign in to [Azure Portal](https://portal.azure.com/).</span></span> 

2. <span data-ttu-id="9c5cb-112">From **All resources**, find and navigate to your Azure Cosmos DB account, select Keys, and copy the **Primary Connection String**.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-112">From **All resources**, find and navigate to your Azure Cosmos DB account, select Keys, and copy the **Primary Connection String**.</span></span>  

3. <span data-ttu-id="9c5cb-113">Go to https://cosmos.azure.com/, paste the connection string and select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-113">Go to https://cosmos.azure.com/, paste the connection string and select **Connect**.</span></span> <span data-ttu-id="9c5cb-114">By using the connection string, you can access the Azure Cosmos DB explorer without any time limits.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-114">By using the connection string, you can access the Azure Cosmos DB explorer without any time limits.</span></span>  

   <span data-ttu-id="9c5cb-115">If you want to provide other users temporary access to your Azure Cosmos DB account, you can do so by using the read-write and read access URLs.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-115">If you want to provide other users temporary access to your Azure Cosmos DB account, you can do so by using the read-write and read access URLs.</span></span> 

4. <span data-ttu-id="9c5cb-116">Open the **Data Explorer** blade, select **Open Full Screen**.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-116">Open the **Data Explorer** blade, select **Open Full Screen**.</span></span> <span data-ttu-id="9c5cb-117">From the pop-up dialog, you can view two access URLs – **Read-Write** and **Read**.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-117">From the pop-up dialog, you can view two access URLs – **Read-Write** and **Read**.</span></span> <span data-ttu-id="9c5cb-118">These URLs allow you to share your Azure Cosmos DB account temporarily with other users.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-118">These URLs allow you to share your Azure Cosmos DB account temporarily with other users.</span></span> <span data-ttu-id="9c5cb-119">Access to the account expires in 24 hours after which you can reconnect by using a new access URL or the connection string.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-119">Access to the account expires in 24 hours after which you can reconnect by using a new access URL or the connection string.</span></span> 

   <span data-ttu-id="9c5cb-120">**Read-Write** – When you share the Read-Write URL with other users, they can view and modify the databases, collections, queries, and other resources associated with that specific account.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-120">**Read-Write** – When you share the Read-Write URL with other users, they can view and modify the databases, collections, queries, and other resources associated with that specific account.</span></span>

   <span data-ttu-id="9c5cb-121">**Read** - When you share the read-only URL with other users, they can view the databases, collections, queries, and other resources associated with that specific account.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-121">**Read** - When you share the read-only URL with other users, they can view the databases, collections, queries, and other resources associated with that specific account.</span></span> <span data-ttu-id="9c5cb-122">For example, if you want to share results of a query with your teammates who don't have access to Azure portal or your Azure Cosmos DB account, you can provide them with this URL.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-122">For example, if you want to share results of a query with your teammates who don't have access to Azure portal or your Azure Cosmos DB account, you can provide them with this URL.</span></span>

   <span data-ttu-id="9c5cb-123">Choose the type of access you'd like to open the account with and click **Open**.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-123">Choose the type of access you'd like to open the account with and click **Open**.</span></span> <span data-ttu-id="9c5cb-124">After you open the explorer, the experience is same as you had with the Data Explorer tab in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-124">After you open the explorer, the experience is same as you had with the Data Explorer tab in Azure portal.</span></span>   

   ![Open Azure Cosmos DB explorer](./media/data-explorer/open-data-explorer-with-access-url.png)

## <a name="known-issues"></a><span data-ttu-id="9c5cb-126">Known issues</span><span class="sxs-lookup"><span data-stu-id="9c5cb-126">Known issues</span></span>

<span data-ttu-id="9c5cb-127">Currently the **Open Full Screen** experience that allows you to share temporary read-write or read access is not yet supported for Azure Cosmos DB Gremlin and Table API accounts.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-127">Currently the **Open Full Screen** experience that allows you to share temporary read-write or read access is not yet supported for Azure Cosmos DB Gremlin and Table API accounts.</span></span> <span data-ttu-id="9c5cb-128">You can still view your Gremlin and Table API accounts by passing the connection string to Azure Cosmos DB Explorer.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-128">You can still view your Gremlin and Table API accounts by passing the connection string to Azure Cosmos DB Explorer.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c5cb-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c5cb-129">Next steps</span></span>
<span data-ttu-id="9c5cb-130">Now that you have learned how to get started with Azure Cosmos DB explorer to manage your data, next you can:</span><span class="sxs-lookup"><span data-stu-id="9c5cb-130">Now that you have learned how to get started with Azure Cosmos DB explorer to manage your data, next you can:</span></span>

* <span data-ttu-id="9c5cb-131">Start defining [queries](sql-api-sql-query-reference.md) using SQL syntax and perform [server side programming](programming.md) by using stored procedures, UDFs, triggers.</span><span class="sxs-lookup"><span data-stu-id="9c5cb-131">Start defining [queries](sql-api-sql-query-reference.md) using SQL syntax and perform [server side programming](programming.md) by using stored procedures, UDFs, triggers.</span></span> 