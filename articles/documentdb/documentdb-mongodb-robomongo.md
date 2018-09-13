---
title: Use Robomongo for MongoDB with Azure DocumentDB | Microsoft Docs
description: 'Learn how to use Robomongo with a DocumentDB: API for MongoDB account'
keywords: robomongo
services: documentdb
author: AndrewHoh
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: anhoh
ms.openlocfilehash: 060ad7d47541f5a8a9a23cbe67146112dad66fc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554056"
---
# <a name="use-robomongo-with-a-documentdb-api-for-mongodb-account"></a><span data-ttu-id="59c70-104">Use Robomongo with a DocumentDB: API for MongoDB account</span><span class="sxs-lookup"><span data-stu-id="59c70-104">Use Robomongo with a DocumentDB: API for MongoDB account</span></span>
<span data-ttu-id="59c70-105">To connect to an Azure DocumentDB: API for MongoDB account using Robomongo, you must:</span><span class="sxs-lookup"><span data-stu-id="59c70-105">To connect to an Azure DocumentDB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="59c70-106">Download and install [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="59c70-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="59c70-107">Have your DocumentDB: API for MongoDB account [connection string](documentdb-connect-mongodb-account.md) information</span><span class="sxs-lookup"><span data-stu-id="59c70-107">Have your DocumentDB: API for MongoDB account [connection string](documentdb-connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="59c70-108">Connect using Robomongo</span><span class="sxs-lookup"><span data-stu-id="59c70-108">Connect using Robomongo</span></span>
<span data-ttu-id="59c70-109">To add your DocumentDB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="59c70-109">To add your DocumentDB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="59c70-110">Retrieve your DocumentDB: API for MongoDB account connection information using the instructions [here](documentdb-connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="59c70-110">Retrieve your DocumentDB: API for MongoDB account connection information using the instructions [here](documentdb-connect-mongodb-account.md).</span></span>

    ![Screen shot of the connection string blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="59c70-112">Run *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="59c70-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="59c70-113">Click the connection button under **File** to manage your connections.</span><span class="sxs-lookup"><span data-stu-id="59c70-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="59c70-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span><span class="sxs-lookup"><span data-stu-id="59c70-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="59c70-115">In the **Connection Settings** window, choose a name.</span><span class="sxs-lookup"><span data-stu-id="59c70-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="59c70-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span><span class="sxs-lookup"><span data-stu-id="59c70-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Screen shot of the Robomongo Manage Connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="59c70-118">On the **Authentication** tab, click **Perform authentication**.</span><span class="sxs-lookup"><span data-stu-id="59c70-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="59c70-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="59c70-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="59c70-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span><span class="sxs-lookup"><span data-stu-id="59c70-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Screen shot of the Robomongo Authentication Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/authentication.png)
6. <span data-ttu-id="59c70-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span><span class="sxs-lookup"><span data-stu-id="59c70-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Screen shot of the Robomongo SSL Tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-mongodb-robomongo/SSL.png)
7. <span data-ttu-id="59c70-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span><span class="sxs-lookup"><span data-stu-id="59c70-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59c70-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="59c70-125">Next steps</span></span>
* <span data-ttu-id="59c70-126">Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="59c70-126">Explore DocumentDB: API for MongoDB [samples](documentdb-mongodb-samples.md).</span></span>




