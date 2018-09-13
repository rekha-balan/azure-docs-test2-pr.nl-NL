---
title: Use Robomongo for Azure Cosmos DB | Microsoft Docs
description: 'Learn how to use Robomongo with an Azure Cosmos DB: API for MongoDB account'
keywords: robomongo
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: conceptual
ms.date: 05/23/2017
ms.author: sngun
ms.openlocfilehash: b6d64d7d7b30d4175fb8c8bf6c98127465427d4e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857674"
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="6f35e-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span><span class="sxs-lookup"><span data-stu-id="6f35e-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="6f35e-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span><span class="sxs-lookup"><span data-stu-id="6f35e-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="6f35e-106">Download and install [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="6f35e-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="6f35e-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span><span class="sxs-lookup"><span data-stu-id="6f35e-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="6f35e-108">Connect using Robomongo</span><span class="sxs-lookup"><span data-stu-id="6f35e-108">Connect using Robomongo</span></span>
<span data-ttu-id="6f35e-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="6f35e-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="6f35e-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="6f35e-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Screen shot of the connection string blade](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="6f35e-112">Run *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="6f35e-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="6f35e-113">Click the connection button under **File** to manage your connections.</span><span class="sxs-lookup"><span data-stu-id="6f35e-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="6f35e-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span><span class="sxs-lookup"><span data-stu-id="6f35e-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="6f35e-115">In the **Connection Settings** window, choose a name.</span><span class="sxs-lookup"><span data-stu-id="6f35e-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="6f35e-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span><span class="sxs-lookup"><span data-stu-id="6f35e-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Screen shot of the Robomongo Manage Connections](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="6f35e-118">On the **Authentication** tab, click **Perform authentication**.</span><span class="sxs-lookup"><span data-stu-id="6f35e-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="6f35e-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="6f35e-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="6f35e-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span><span class="sxs-lookup"><span data-stu-id="6f35e-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Screen shot of the Robomongo Authentication Tab](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="6f35e-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span><span class="sxs-lookup"><span data-stu-id="6f35e-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Screen shot of the Robomongo SSL Tab](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="6f35e-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span><span class="sxs-lookup"><span data-stu-id="6f35e-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f35e-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f35e-125">Next steps</span></span>
* <span data-ttu-id="6f35e-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6f35e-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
