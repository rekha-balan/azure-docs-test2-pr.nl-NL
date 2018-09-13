---
title: Get Azure Blockchain Workbench database details
description: Learn how to get Azure Blockchain Workbench database and database server information.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/4/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: 63b718bcb8722c5fd501891d162eadfae9fb8ec2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869728"
---
# <a name="get-information-about-your-azure-blockchain-workbench-database"></a><span data-ttu-id="afaa7-103">Get information about your Azure Blockchain Workbench database</span><span class="sxs-lookup"><span data-stu-id="afaa7-103">Get information about your Azure Blockchain Workbench database</span></span>

<span data-ttu-id="afaa7-104">This article shows how to get detailed information about your Azure Blockchain Workbench database.</span><span class="sxs-lookup"><span data-stu-id="afaa7-104">This article shows how to get detailed information about your Azure Blockchain Workbench database.</span></span>

## <a name="overview"></a><span data-ttu-id="afaa7-105">Overview</span><span class="sxs-lookup"><span data-stu-id="afaa7-105">Overview</span></span>

<span data-ttu-id="afaa7-106">Information about applications, workflows, and smart contract execution is provided using database views in the Blockchain Workbench SQL DB.</span><span class="sxs-lookup"><span data-stu-id="afaa7-106">Information about applications, workflows, and smart contract execution is provided using database views in the Blockchain Workbench SQL DB.</span></span> <span data-ttu-id="afaa7-107">Developers can use this information when using tools such as Microsoft Excel, PowerBI, Visual Studio, and SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="afaa7-107">Developers can use this information when using tools such as Microsoft Excel, PowerBI, Visual Studio, and SQL Server Management Studio.</span></span>

<span data-ttu-id="afaa7-108">Before a developer can connect to the database, they need:</span><span class="sxs-lookup"><span data-stu-id="afaa7-108">Before a developer can connect to the database, they need:</span></span>

* <span data-ttu-id="afaa7-109">External client access allowed in the database firewall.</span><span class="sxs-lookup"><span data-stu-id="afaa7-109">External client access allowed in the database firewall.</span></span> <span data-ttu-id="afaa7-110">This article about configuring a database firewall article explains how to allow access.</span><span class="sxs-lookup"><span data-stu-id="afaa7-110">This article about configuring a database firewall article explains how to allow access.</span></span>
* <span data-ttu-id="afaa7-111">The database server name and database name.</span><span class="sxs-lookup"><span data-stu-id="afaa7-111">The database server name and database name.</span></span>

## <a name="connect-to-the-blockchain-workbench-database"></a><span data-ttu-id="afaa7-112">Connect to the Blockchain Workbench database</span><span class="sxs-lookup"><span data-stu-id="afaa7-112">Connect to the Blockchain Workbench database</span></span>

<span data-ttu-id="afaa7-113">To connect to the database:</span><span class="sxs-lookup"><span data-stu-id="afaa7-113">To connect to the database:</span></span>

1. <span data-ttu-id="afaa7-114">Sign in to the Azure Portal with an account that has **Owner** permissions for the Azure Blockchain Workbench resources.</span><span class="sxs-lookup"><span data-stu-id="afaa7-114">Sign in to the Azure Portal with an account that has **Owner** permissions for the Azure Blockchain Workbench resources.</span></span>
2. <span data-ttu-id="afaa7-115">In the left navigation pane, choose **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="afaa7-115">In the left navigation pane, choose **Resource groups**.</span></span>
3. <span data-ttu-id="afaa7-116">Choose the name of the resource group for your Blockchain Workbench deployment.</span><span class="sxs-lookup"><span data-stu-id="afaa7-116">Choose the name of the resource group for your Blockchain Workbench deployment.</span></span>
4. <span data-ttu-id="afaa7-117">Select **Type** to sort the resource list, and then choose your **SQL server**.</span><span class="sxs-lookup"><span data-stu-id="afaa7-117">Select **Type** to sort the resource list, and then choose your **SQL server**.</span></span> <span data-ttu-id="afaa7-118">The sorted list in the next screen capture shows two SQL databases, "master" and one that uses "lhgn" as the **Resource prefix**.</span><span class="sxs-lookup"><span data-stu-id="afaa7-118">The sorted list in the next screen capture shows two SQL databases, "master" and one that uses "lhgn" as the **Resource prefix**.</span></span>

   ![Sorted Blockchain Workbench resource list](media/blockchain-workbench-getdb-details/sorted-workbench-resource-list.png)

5. <span data-ttu-id="afaa7-120">To see detailed information about the Blockchain Workbench database, select the link for the database with the **Resource prefix** you provided for deploying Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="afaa7-120">To see detailed information about the Blockchain Workbench database, select the link for the database with the **Resource prefix** you provided for deploying Blockchain Workbench.</span></span>

   ![Database details](media/blockchain-workbench-getdb-details/workbench-db-details.png)

<span data-ttu-id="afaa7-122">The database server name and database name let you connect to the Blockchain Workbench database using your development or reporting tool.</span><span class="sxs-lookup"><span data-stu-id="afaa7-122">The database server name and database name let you connect to the Blockchain Workbench database using your development or reporting tool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afaa7-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="afaa7-123">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="afaa7-124">Database views in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="afaa7-124">Database views in Azure Blockchain Workbench</span></span>](blockchain-workbench-database-views.md)