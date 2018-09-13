---
title: Configure the Azure Blockchain Workbench SQL DB firewall
description: Learn how to configure the Azure Blockchain Workbench SQL DB firewall.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/4/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: afeea143f73fa4f7d3e373535007846a668616ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866995"
---
# <a name="configure-the-azure-blockchain-workbench-database-firewall"></a><span data-ttu-id="ca1eb-103">Configure the Azure Blockchain Workbench database firewall</span><span class="sxs-lookup"><span data-stu-id="ca1eb-103">Configure the Azure Blockchain Workbench database firewall</span></span>

<span data-ttu-id="ca1eb-104">This article shows how to configure a firewall rule using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-104">This article shows how to configure a firewall rule using the Azure portal.</span></span> <span data-ttu-id="ca1eb-105">Firewall rules let external clients or applications connect to your Azure Blockchain Workbench database.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-105">Firewall rules let external clients or applications connect to your Azure Blockchain Workbench database.</span></span>

## <a name="connect-to-the-blockchain-workbench-database"></a><span data-ttu-id="ca1eb-106">Connect to the Blockchain Workbench database</span><span class="sxs-lookup"><span data-stu-id="ca1eb-106">Connect to the Blockchain Workbench database</span></span>

<span data-ttu-id="ca1eb-107">To connect to the database where you want to configure a rule:</span><span class="sxs-lookup"><span data-stu-id="ca1eb-107">To connect to the database where you want to configure a rule:</span></span>

1. <span data-ttu-id="ca1eb-108">Sign in to the Azure Portal with an account that has **Owner**     permissions for the Azure Blockchain Workbench resources.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-108">Sign in to the Azure Portal with an account that has **Owner**     permissions for the Azure Blockchain Workbench resources.</span></span>
2. <span data-ttu-id="ca1eb-109">In the left navigation pane, choose **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-109">In the left navigation pane, choose **Resource groups**.</span></span>
3. <span data-ttu-id="ca1eb-110">Choose the name of the resource group for your Blockchain Workbench deployment.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-110">Choose the name of the resource group for your Blockchain Workbench deployment.</span></span>
4. <span data-ttu-id="ca1eb-111">Select **Type** to sort the list of resources, and then choose your **SQL server**.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-111">Select **Type** to sort the list of resources, and then choose your **SQL server**.</span></span>
5. <span data-ttu-id="ca1eb-112">The resource list example in the following screen capture shows two databases: *master* and *lsgn-sdk*.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-112">The resource list example in the following screen capture shows two databases: *master* and *lsgn-sdk*.</span></span> <span data-ttu-id="ca1eb-113">You configure the firewall rule on  *lsgn-sdk*.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-113">You configure the firewall rule on  *lsgn-sdk*.</span></span>

![List Blockchain Workbench resources](media/blockchain-workbench-database-firewall/list-database-resources.png)

## <a name="create-a-database-firewall-rule"></a><span data-ttu-id="ca1eb-115">Create a database firewall rule</span><span class="sxs-lookup"><span data-stu-id="ca1eb-115">Create a database firewall rule</span></span>

<span data-ttu-id="ca1eb-116">To create a firewall rule:</span><span class="sxs-lookup"><span data-stu-id="ca1eb-116">To create a firewall rule:</span></span>

1. <span data-ttu-id="ca1eb-117">Choose the link to the "lsgn-sdk" database.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-117">Choose the link to the "lsgn-sdk" database.</span></span>
2. <span data-ttu-id="ca1eb-118">On the menu bar, select **Set server firewall**.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-118">On the menu bar, select **Set server firewall**.</span></span>

   ![Set server firewall](media/blockchain-workbench-database-firewall/configure-server-firewall.png)

3. <span data-ttu-id="ca1eb-120">To create a rule for your organization:</span><span class="sxs-lookup"><span data-stu-id="ca1eb-120">To create a rule for your organization:</span></span>

   * <span data-ttu-id="ca1eb-121">Enter a **RULE NAME**</span><span class="sxs-lookup"><span data-stu-id="ca1eb-121">Enter a **RULE NAME**</span></span>
   * <span data-ttu-id="ca1eb-122">Enter an IP address for the **START IP** of the address range</span><span class="sxs-lookup"><span data-stu-id="ca1eb-122">Enter an IP address for the **START IP** of the address range</span></span>
   * <span data-ttu-id="ca1eb-123">Enter an IP address for the **END IP** of the address range</span><span class="sxs-lookup"><span data-stu-id="ca1eb-123">Enter an IP address for the **END IP** of the address range</span></span>

   ![Create firewall rule](media/blockchain-workbench-database-firewall/create-firewall-rule.png)

    > [!NOTE]
    > <span data-ttu-id="ca1eb-125">If you only want to add the IP address of your computer, choose **+ Add client IP**.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-125">If you only want to add the IP address of your computer, choose **+ Add client IP**.</span></span>
        
1. <span data-ttu-id="ca1eb-126">To save your firewall configuration, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-126">To save your firewall configuration, select **Save**.</span></span>
2. <span data-ttu-id="ca1eb-127">Test the IP address range you configured for the database by connecting from an application or tool.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-127">Test the IP address range you configured for the database by connecting from an application or tool.</span></span> <span data-ttu-id="ca1eb-128">For example, SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="ca1eb-128">For example, SQL Server Management Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca1eb-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="ca1eb-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca1eb-130">Database views in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="ca1eb-130">Database views in Azure Blockchain Workbench</span></span>](blockchain-workbench-database-views.md)