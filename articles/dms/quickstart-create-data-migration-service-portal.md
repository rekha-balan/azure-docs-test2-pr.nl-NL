---
title: Create Azure Database Migration Service instance using the Azure portal | Microsoft Docs
description: Use the Azure portal to create an instance of the Azure Database Migration Service
services: database-migration
author: edmacauley
ms.author: jtoland
manager: craigg
ms.reviewer: ''
ms.service: database-migration
ms.workload: data-services
ms.custom: mvc
ms.topic: quickstart
ms.date: 08/13/2018
ms.openlocfilehash: f4dcc659d72edff1d8c2523cce1de059f1cf3fdf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865026"
---
# <a name="create-an-instance-of-the-azure-database-migration-service-by-using-the-azure-portal"></a><span data-ttu-id="98b1c-103">Create an instance of the Azure Database Migration Service by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="98b1c-103">Create an instance of the Azure Database Migration Service by using the Azure portal</span></span>
<span data-ttu-id="98b1c-104">In this Quickstart, you use the Azure portal to create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="98b1c-104">In this Quickstart, you use the Azure portal to create an instance of the Azure Database Migration Service.</span></span>  <span data-ttu-id="98b1c-105">After you create the service, you can use it to migrate data from SQL Server on-premises to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="98b1c-105">After you create the service, you can use it to migrate data from SQL Server on-premises to an Azure SQL database.</span></span>

<span data-ttu-id="98b1c-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="98b1c-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="98b1c-107">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="98b1c-107">Log in to the Azure portal</span></span>
<span data-ttu-id="98b1c-108">Open your web browser, navigate to the [Microsoft Azure portal](https://portal.azure.com/), and then enter your credentials to sign in to the portal.</span><span class="sxs-lookup"><span data-stu-id="98b1c-108">Open your web browser, navigate to the [Microsoft Azure portal](https://portal.azure.com/), and then enter your credentials to sign in to the portal.</span></span>

<span data-ttu-id="98b1c-109">The default view is your service dashboard.</span><span class="sxs-lookup"><span data-stu-id="98b1c-109">The default view is your service dashboard.</span></span>

## <a name="register-the-resource-provider"></a><span data-ttu-id="98b1c-110">Register the resource provider</span><span class="sxs-lookup"><span data-stu-id="98b1c-110">Register the resource provider</span></span>
<span data-ttu-id="98b1c-111">Register the Microsoft.DataMigration resource provider before you create your first instance of the Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="98b1c-111">Register the Microsoft.DataMigration resource provider before you create your first instance of the Database Migration Service.</span></span>

1. <span data-ttu-id="98b1c-112">In the Azure portal, select **All services**, and then select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-112">In the Azure portal, select **All services**, and then select **Subscriptions**.</span></span>

2. <span data-ttu-id="98b1c-113">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-113">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span></span>

3. <span data-ttu-id="98b1c-114">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-114">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span></span>

    ![Register resource provider](media/quickstart-create-data-migration-service-portal/dms-register-provider.png)

## <a name="create-an-instance-of-the-service"></a><span data-ttu-id="98b1c-116">Create an instance of the service</span><span class="sxs-lookup"><span data-stu-id="98b1c-116">Create an instance of the service</span></span>
1. <span data-ttu-id="98b1c-117">Select +**Create a resource** to create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="98b1c-117">Select +**Create a resource** to create an instance of the Azure Database Migration Service.</span></span>

2. <span data-ttu-id="98b1c-118">Search the marketplace for "migration", select **Azure Database Migration Service**, and then on the **Azure Database Migration Service** screen, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-118">Search the marketplace for "migration", select **Azure Database Migration Service**, and then on the **Azure Database Migration Service** screen, select **Create**.</span></span>

3. <span data-ttu-id="98b1c-119">On the **Create Migration Service** screen:</span><span class="sxs-lookup"><span data-stu-id="98b1c-119">On the **Create Migration Service** screen:</span></span> 

    - <span data-ttu-id="98b1c-120">Choose a **Service Name** that is memorable and unique to identify your instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="98b1c-120">Choose a **Service Name** that is memorable and unique to identify your instance of the Azure Database Migration Service.</span></span>
    - <span data-ttu-id="98b1c-121">Select the Azure **Subscription** in which you want to create the instance.</span><span class="sxs-lookup"><span data-stu-id="98b1c-121">Select the Azure **Subscription** in which you want to create the instance.</span></span>
    - <span data-ttu-id="98b1c-122">Select an existing **Resource Group** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="98b1c-122">Select an existing **Resource Group** or create a new one.</span></span>
    - <span data-ttu-id="98b1c-123">Choose the **Location** that is closest to your source or target server.</span><span class="sxs-lookup"><span data-stu-id="98b1c-123">Choose the **Location** that is closest to your source or target server.</span></span>
    - <span data-ttu-id="98b1c-124">Select an existing **Virtual network** (VNET) or create one.</span><span class="sxs-lookup"><span data-stu-id="98b1c-124">Select an existing **Virtual network** (VNET) or create one.</span></span>

        <span data-ttu-id="98b1c-125">The VNET provides the Azure Database Migration Service with access to the source database and target environment.</span><span class="sxs-lookup"><span data-stu-id="98b1c-125">The VNET provides the Azure Database Migration Service with access to the source database and target environment.</span></span>

        <span data-ttu-id="98b1c-126">For more information on how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/vnet).</span><span class="sxs-lookup"><span data-stu-id="98b1c-126">For more information on how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/vnet).</span></span>

    - <span data-ttu-id="98b1c-127">Select Basic: 1 vCore for the **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-127">Select Basic: 1 vCore for the **Pricing tier**.</span></span>

        ![Create migration service](media/quickstart-create-data-migration-service-portal/dms-create-service1.png)

4. <span data-ttu-id="98b1c-129">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-129">Select **Create**.</span></span>

    <span data-ttu-id="98b1c-130">After a few moments, your instance of the Azure Database Migration service is created and ready to use.</span><span class="sxs-lookup"><span data-stu-id="98b1c-130">After a few moments, your instance of the Azure Database Migration service is created and ready to use.</span></span> <span data-ttu-id="98b1c-131">The Database Migration Service displays as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="98b1c-131">The Database Migration Service displays as shown in the following image:</span></span>

    ![Migration service created](media/quickstart-create-data-migration-service-portal/dms-service-created.png)

## <a name="clean-up-resources"></a><span data-ttu-id="98b1c-133">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="98b1c-133">Clean up resources</span></span>
<span data-ttu-id="98b1c-134">You can clean up the resources created in this Quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98b1c-134">You can clean up the resources created in this Quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="98b1c-135">To delete the resource group, navigate to the instance of the Azure Database Migration Service that you created.</span><span class="sxs-lookup"><span data-stu-id="98b1c-135">To delete the resource group, navigate to the instance of the Azure Database Migration Service that you created.</span></span> <span data-ttu-id="98b1c-136">Select the **Resource group** name, and then select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="98b1c-136">Select the **Resource group** name, and then select **Delete resource group**.</span></span> <span data-ttu-id="98b1c-137">This action deletes all assets in the resource group as well as the group itself.</span><span class="sxs-lookup"><span data-stu-id="98b1c-137">This action deletes all assets in the resource group as well as the group itself.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98b1c-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="98b1c-138">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="98b1c-139">Migrate SQL Server on-premises to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="98b1c-139">Migrate SQL Server on-premises to Azure SQL Database</span></span>](tutorial-sql-server-to-azure-sql.md)