---
title: Use Azure Blockchain Workbench data in Microsoft Power BI
description: Learn how to load and view Azure Blockchain Workbench SQL DB data in Microsoft Power BI.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/3/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: 321a34589277d62290c2fde680bb461de34b4568
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856878"
---
# <a name="using-azure-blockchain-workbench-data-with-microsoft-power-bi"></a><span data-ttu-id="51a78-103">Using Azure Blockchain Workbench data with Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="51a78-103">Using Azure Blockchain Workbench data with Microsoft Power BI</span></span>

<span data-ttu-id="51a78-104">Microsoft Power BI provides the ability to easily generate powerful reports from SQL DB databases using Power BI Desktop and then publish them to [https://www.powerbi.com](http://www.powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="51a78-104">Microsoft Power BI provides the ability to easily generate powerful reports from SQL DB databases using Power BI Desktop and then publish them to [https://www.powerbi.com](http://www.powerbi.com).</span></span>

<span data-ttu-id="51a78-105">This article contains a step by step walkthrough of how to connect to Azure Blockchain Workbench's SQL Database from within PowerBI desktop, create a report, and deploy the report to powerbi.com.</span><span class="sxs-lookup"><span data-stu-id="51a78-105">This article contains a step by step walkthrough of how to connect to Azure Blockchain Workbench's SQL Database from within PowerBI desktop, create a report, and deploy the report to powerbi.com.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51a78-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="51a78-106">Prerequisites</span></span>

* <span data-ttu-id="51a78-107">Download [PowerBI Desktop](https://aka.ms/pbidesktopstore).</span><span class="sxs-lookup"><span data-stu-id="51a78-107">Download [PowerBI Desktop](https://aka.ms/pbidesktopstore).</span></span>

## <a name="connecting-powerbi-to-data-in-azure-blockchain-workbench"></a><span data-ttu-id="51a78-108">Connecting PowerBI to data in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="51a78-108">Connecting PowerBI to data in Azure Blockchain Workbench</span></span>

1.  <span data-ttu-id="51a78-109">Open Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="51a78-109">Open Power BI Desktop.</span></span>
2.  <span data-ttu-id="51a78-110">Select **Get Data**.</span><span class="sxs-lookup"><span data-stu-id="51a78-110">Select **Get Data**.</span></span>

    ![Get data](media/blockchain-workbench-data-powerbi/get-data.png)
3.  <span data-ttu-id="51a78-112">Select **SQL Server** from the list of data source types.</span><span class="sxs-lookup"><span data-stu-id="51a78-112">Select **SQL Server** from the list of data source types.</span></span>

4.  <span data-ttu-id="51a78-113">Provide the server and database name in the dialog.</span><span class="sxs-lookup"><span data-stu-id="51a78-113">Provide the server and database name in the dialog.</span></span> <span data-ttu-id="51a78-114">Specify if you want to import the data or perform a **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="51a78-114">Specify if you want to import the data or perform a **DirectQuery**.</span></span> <span data-ttu-id="51a78-115">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="51a78-115">Select **OK**.</span></span>

    ![Select SQL Server](media/blockchain-workbench-data-powerbi/select-sql.png)

5.  <span data-ttu-id="51a78-117">Provide the database credentials to access Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="51a78-117">Provide the database credentials to access Azure Blockchain Workbench.</span></span> <span data-ttu-id="51a78-118">Select **Database** and enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="51a78-118">Select **Database** and enter your credentials.</span></span>

    <span data-ttu-id="51a78-119">If you are using the credentials created by the Azure Blockchain Workbench deployment process, the username is **dbadmin** and the password is the one you provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="51a78-119">If you are using the credentials created by the Azure Blockchain Workbench deployment process, the username is **dbadmin** and the password is the one you provided during deployment.</span></span>

    ![SQL DB settings](media/blockchain-workbench-data-powerbi/db-settings.png)

6.  <span data-ttu-id="51a78-121">Once connected to the database, the **Navigator** dialog displays the tables and views available within the database.</span><span class="sxs-lookup"><span data-stu-id="51a78-121">Once connected to the database, the **Navigator** dialog displays the tables and views available within the database.</span></span> <span data-ttu-id="51a78-122">The views are designed for reporting and are all prefixed **vw**.</span><span class="sxs-lookup"><span data-stu-id="51a78-122">The views are designed for reporting and are all prefixed **vw**.</span></span>

    ![Navigator](media/blockchain-workbench-data-powerbi/navigator.png)

7.  <span data-ttu-id="51a78-124">Select the views you wish to include.</span><span class="sxs-lookup"><span data-stu-id="51a78-124">Select the views you wish to include.</span></span> <span data-ttu-id="51a78-125">For demonstration purposes, we include **vwContractAction**, which provides details on all of the actions that have taken place on a contract.</span><span class="sxs-lookup"><span data-stu-id="51a78-125">For demonstration purposes, we include **vwContractAction**, which provides details on all of the actions that have taken place on a contract.</span></span>

    ![Select views](media/blockchain-workbench-data-powerbi/select-views.png)

<span data-ttu-id="51a78-127">You can now create and publish reports as you normally would with Power BI.</span><span class="sxs-lookup"><span data-stu-id="51a78-127">You can now create and publish reports as you normally would with Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51a78-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="51a78-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51a78-129">Database views in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="51a78-129">Database views in Azure Blockchain Workbench</span></span>](blockchain-workbench-database-views.md)