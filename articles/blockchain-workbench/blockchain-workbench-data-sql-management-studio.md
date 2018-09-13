---
title: Use Azure Blockchain Workbench Data with SQL Server Management Studio
description: Learn how to connect to Azure Blockchain Workbench's SQL Database from within SQL Server Management Studio.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/3/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: 5c5a2e2b42cd9c19810e6579159b228369ee8f7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856625"
---
# <a name="using-azure-blockchain-workbench-data-with-sql-server-management-studio"></a><span data-ttu-id="bfc53-103">Using Azure Blockchain Workbench data with SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="bfc53-103">Using Azure Blockchain Workbench data with SQL Server Management Studio</span></span>

<span data-ttu-id="bfc53-104">Microsoft SQL Server Management Studio provides the ability to rapidly write and test queries against Azure Blockhain Workbench's SQL DB.</span><span class="sxs-lookup"><span data-stu-id="bfc53-104">Microsoft SQL Server Management Studio provides the ability to rapidly write and test queries against Azure Blockhain Workbench's SQL DB.</span></span> <span data-ttu-id="bfc53-105">This section contains a step by step walkthrough of how to connect to Azure Blockchain Workbench's SQL Database from within SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="bfc53-105">This section contains a step by step walkthrough of how to connect to Azure Blockchain Workbench's SQL Database from within SQL Server Management Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfc53-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bfc53-106">Prerequisites</span></span>

* <span data-ttu-id="bfc53-107">Download [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="bfc53-107">Download [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017).</span></span>

## <a name="connecting-sql-server-management-studio-to-data-in-azure-blockchain-workbench"></a><span data-ttu-id="bfc53-108">Connecting SQL Server Management Studio to data in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="bfc53-108">Connecting SQL Server Management Studio to data in Azure Blockchain Workbench</span></span>

1. <span data-ttu-id="bfc53-109">Open the SQL Server Management Studio and select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="bfc53-109">Open the SQL Server Management Studio and select **Connect**.</span></span>
2. <span data-ttu-id="bfc53-110">Select **Database Engine**.</span><span class="sxs-lookup"><span data-stu-id="bfc53-110">Select **Database Engine**.</span></span>

    ![Database engine](media/blockchain-workbench-data-sql-management-studio/database-engine.png)

3. <span data-ttu-id="bfc53-112">In the **Connect to Server** dialog, enter the server name and your database credentials.</span><span class="sxs-lookup"><span data-stu-id="bfc53-112">In the **Connect to Server** dialog, enter the server name and your database credentials.</span></span>

    <span data-ttu-id="bfc53-113">If you are using the credentials created by the Azure Blockchain Workbench deployment process, the username will be **dbadmin** and the password will be the one you provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="bfc53-113">If you are using the credentials created by the Azure Blockchain Workbench deployment process, the username will be **dbadmin** and the password will be the one you provided during deployment.</span></span>

    ![Enter SQL credentials](media/blockchain-workbench-data-sql-management-studio/sql-creds.png)

 4. <span data-ttu-id="bfc53-115">SQL Server Management Studio displays the list of databases, database views, and stored procedures in the Azure Blockchain Workbench database.</span><span class="sxs-lookup"><span data-stu-id="bfc53-115">SQL Server Management Studio displays the list of databases, database views, and stored procedures in the Azure Blockchain Workbench database.</span></span>

    ![Database list](media/blockchain-workbench-data-sql-management-studio/db-list.png)

5. <span data-ttu-id="bfc53-117">To view the data associated with any of the database views, you can automatically generate a select statement using the following steps.</span><span class="sxs-lookup"><span data-stu-id="bfc53-117">To view the data associated with any of the database views, you can automatically generate a select statement using the following steps.</span></span>
6. <span data-ttu-id="bfc53-118">Right click on any of the database views in the Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="bfc53-118">Right click on any of the database views in the Object Explorer.</span></span>
7. <span data-ttu-id="bfc53-119">Select **Script View as**.</span><span class="sxs-lookup"><span data-stu-id="bfc53-119">Select **Script View as**.</span></span>
8. <span data-ttu-id="bfc53-120">Choose **SELECT to**.</span><span class="sxs-lookup"><span data-stu-id="bfc53-120">Choose **SELECT to**.</span></span>
9. <span data-ttu-id="bfc53-121">Select **New Query Editor Window**.</span><span class="sxs-lookup"><span data-stu-id="bfc53-121">Select **New Query Editor Window**.</span></span>
10. <span data-ttu-id="bfc53-122">A new query can be created by selecting **New Query**.</span><span class="sxs-lookup"><span data-stu-id="bfc53-122">A new query can be created by selecting **New Query**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfc53-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfc53-123">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfc53-124">Database views in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="bfc53-124">Database views in Azure Blockchain Workbench</span></span>](blockchain-workbench-database-views.md)