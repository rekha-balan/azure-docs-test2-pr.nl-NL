---
title: Use Azure Blockchain Workbench data in Microsoft Excel
description: Learn how to load and view Azure Blockchain Workbench SQL DB data in Microsoft Excel.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/3/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: e8c20f4b8e39615e2a8c486130d7c8bec655a936
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865824"
---
# <a name="view-azure-blockchain-workbench-data-with-microsoft-excel"></a><span data-ttu-id="b5d1c-103">View Azure Blockchain Workbench data with Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="b5d1c-103">View Azure Blockchain Workbench data with Microsoft Excel</span></span>

<span data-ttu-id="b5d1c-104">You can use Microsoft Excel to view data in Azure Blockchain Workbench's SQL DB.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-104">You can use Microsoft Excel to view data in Azure Blockchain Workbench's SQL DB.</span></span> <span data-ttu-id="b5d1c-105">This article provides the steps you need to:</span><span class="sxs-lookup"><span data-stu-id="b5d1c-105">This article provides the steps you need to:</span></span>

* <span data-ttu-id="b5d1c-106">Connect to the Blockchain Workbench database from Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="b5d1c-106">Connect to the Blockchain Workbench database from Microsoft Excel</span></span>
* <span data-ttu-id="b5d1c-107">Look at Blockchain Workbench database tables and views</span><span class="sxs-lookup"><span data-stu-id="b5d1c-107">Look at Blockchain Workbench database tables and views</span></span>
* <span data-ttu-id="b5d1c-108">Load Blockchain Workbench view data into Excel</span><span class="sxs-lookup"><span data-stu-id="b5d1c-108">Load Blockchain Workbench view data into Excel</span></span>

## <a name="connect-to-the-blockchain-workbench-database"></a><span data-ttu-id="b5d1c-109">Connect to the Blockchain Workbench database</span><span class="sxs-lookup"><span data-stu-id="b5d1c-109">Connect to the Blockchain Workbench database</span></span>

<span data-ttu-id="b5d1c-110">To connect to a Blockchain Workbench database:</span><span class="sxs-lookup"><span data-stu-id="b5d1c-110">To connect to a Blockchain Workbench database:</span></span>

1. <span data-ttu-id="b5d1c-111">Open Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-111">Open Microsoft Excel.</span></span>
2. <span data-ttu-id="b5d1c-112">On the **Data** tab, choose **Get Data**.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-112">On the **Data** tab, choose **Get Data**.</span></span>
3. <span data-ttu-id="b5d1c-113">Select **From Azure** and then select **From Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-113">Select **From Azure** and then select **From Azure SQL Database**.</span></span>

   ![Connect to Azure SQL database](media/blockchain-workbench-data-excel/connect-sql-db.png)

4. <span data-ttu-id="b5d1c-115">In the **SQL Server database** dialog box:</span><span class="sxs-lookup"><span data-stu-id="b5d1c-115">In the **SQL Server database** dialog box:</span></span>

    * <span data-ttu-id="b5d1c-116">For **Server**, enter the name of the Blockchain Workbench server.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-116">For **Server**, enter the name of the Blockchain Workbench server.</span></span>
    * <span data-ttu-id="b5d1c-117">For **Database (optional)**, enter the name of the database.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-117">For **Database (optional)**, enter the name of the database.</span></span>

   ![Provide database server and database](media/blockchain-workbench-data-excel/provide-server-db.png)

5. <span data-ttu-id="b5d1c-119">In the **SQL Server database** dialog navigation bar, select     **Database**.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-119">In the **SQL Server database** dialog navigation bar, select     **Database**.</span></span> <span data-ttu-id="b5d1c-120">Enter your **Username** and **Password**, and then    select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-120">Enter your **Username** and **Password**, and then    select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5d1c-121">If you're using the credentials created during the Azure Blockchain Workbench deployment process, the **User name** is `dbadmin`.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-121">If you're using the credentials created during the Azure Blockchain Workbench deployment process, the **User name** is `dbadmin`.</span></span> <span data-ttu-id="b5d1c-122">The **Password** is the one you created when you deployed the Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-122">The **Password** is the one you created when you deployed the Blockchain Workbench.</span></span>
    
   ![Provide credentials to access database](media/blockchain-workbench-data-excel/provide-credentials.png)

## <a name="look-at-database-tables-and-views"></a><span data-ttu-id="b5d1c-124">Look at database tables and views</span><span class="sxs-lookup"><span data-stu-id="b5d1c-124">Look at database tables and views</span></span>

<span data-ttu-id="b5d1c-125">The Excel Navigator dialog opens after you connect to the database.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-125">The Excel Navigator dialog opens after you connect to the database.</span></span> <span data-ttu-id="b5d1c-126">You can use the Navigator to look at the tables and views in the database.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-126">You can use the Navigator to look at the tables and views in the database.</span></span> <span data-ttu-id="b5d1c-127">The views are designed for reporting and their names are prefixed with **vw**.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-127">The views are designed for reporting and their names are prefixed with **vw**.</span></span>

   ![Excel Navigator preview of a view](media/blockchain-workbench-data-excel/excel-navigator.png)

## <a name="load-view-data-into-an-excel-workbook"></a><span data-ttu-id="b5d1c-129">Load view data into an Excel workbook</span><span class="sxs-lookup"><span data-stu-id="b5d1c-129">Load view data into an Excel workbook</span></span>

<span data-ttu-id="b5d1c-130">The next example shows how you can load data from a view into an Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-130">The next example shows how you can load data from a view into an Excel workbook.</span></span>

1. <span data-ttu-id="b5d1c-131">In the **Navigator** scroll bar, select the **vwContractAction** view.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-131">In the **Navigator** scroll bar, select the **vwContractAction** view.</span></span> <span data-ttu-id="b5d1c-132">The **vwContractAction** preview shows all the actions related to a contract in the Blockchain Workbench database.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-132">The **vwContractAction** preview shows all the actions related to a contract in the Blockchain Workbench database.</span></span>
2. <span data-ttu-id="b5d1c-133">Select **Load** to retrieve all the data in the view and put it in your Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-133">Select **Load** to retrieve all the data in the view and put it in your Excel workbook.</span></span>

   ![Data loaded from a view](media/blockchain-workbench-data-excel/view-data.png)

<span data-ttu-id="b5d1c-135">Now that you have the data loaded, you can use Excel features to create your own reports using the metadata and transaction data from the Azure Blockchain Workbench database.</span><span class="sxs-lookup"><span data-stu-id="b5d1c-135">Now that you have the data loaded, you can use Excel features to create your own reports using the metadata and transaction data from the Azure Blockchain Workbench database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5d1c-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5d1c-136">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5d1c-137">Database views in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="b5d1c-137">Database views in Azure Blockchain Workbench</span></span>](blockchain-workbench-database-views.md)