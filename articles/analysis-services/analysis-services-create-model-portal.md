---
title: Create a tabular model by using the Azure Analysis Services Web designer | Microsoft Docs
description: Learn how to create an Azure Analysis Services tabular model by using the Web designer in Azure portal.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: dcfcfb24d2b47a8272c576856fc3accc547f354a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870711"
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="ee2a8-103">Create a model in Azure portal</span><span class="sxs-lookup"><span data-stu-id="ee2a8-103">Create a model in Azure portal</span></span>

<span data-ttu-id="ee2a8-104">The Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way to create and edit tabular models and query model data right in your browser.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-104">The Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way to create and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="ee2a8-105">Keep in mind, the web designer is **preview**.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-105">Keep in mind, the web designer is **preview**.</span></span> <span data-ttu-id="ee2a8-106">Functionality is limited.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-106">Functionality is limited.</span></span> <span data-ttu-id="ee2a8-107">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ee2a8-107">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ee2a8-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ee2a8-108">Before you begin</span></span>

- <span data-ttu-id="ee2a8-109">Your Azure Analysis Services server must be at the Standard or Developer tier.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-109">Your Azure Analysis Services server must be at the Standard or Developer tier.</span></span> <span data-ttu-id="ee2a8-110">New models created by using the Web designer are DirectQuery, supported only by these tiers.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-110">New models created by using the Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="ee2a8-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="ee2a8-112">New models created from Power BI Desktop files support Azure SQL Database and Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-112">New models created from Power BI Desktop files support Azure SQL Database and Azure SQL Data Warehouse.</span></span>
- <span data-ttu-id="ee2a8-113">A SQL Server account and password for connecting to Azure SQL Database or Azure SQL Data Warehouse data sources.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-113">A SQL Server account and password for connecting to Azure SQL Database or Azure SQL Data Warehouse data sources.</span></span>
- <span data-ttu-id="ee2a8-114">You must have server admin privileges to create a new model.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-114">You must have server admin privileges to create a new model.</span></span> <span data-ttu-id="ee2a8-115">Database admin privileges are required to edit and query a model by using the designer.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-115">Database admin privileges are required to edit and query a model by using the designer.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="ee2a8-116">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ee2a8-116">Sign in to the Azure portal</span></span>

<span data-ttu-id="ee2a8-117">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ee2a8-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="to-create-a-new-tabular-model"></a><span data-ttu-id="ee2a8-118">To create a new tabular model</span><span class="sxs-lookup"><span data-stu-id="ee2a8-118">To create a new tabular model</span></span>

1. <span data-ttu-id="ee2a8-119">In your server **Overview** > **Web designer**, click **Open**.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-119">In your server **Overview** > **Web designer**, click **Open**.</span></span>

    ![Create a model in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="ee2a8-121">In **Web designer** > **Models**, click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-121">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Create a model in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="ee2a8-123">In **New model**, type a model name, and then select a data source.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-123">In **New model**, type a model name, and then select a data source.</span></span>

    ![New model dialog in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="ee2a8-125">In **Connect**, enter the connection properties.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-125">In **Connect**, enter the connection properties.</span></span> <span data-ttu-id="ee2a8-126">Username and password must be a SQL Server account.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-126">Username and password must be a SQL Server account.</span></span>

     ![Connect dialog in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="ee2a8-128">In **Tables and views**, select the tables to include in your model, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-128">In **Tables and views**, select the tables to include in your model, and then click **Create**.</span></span> <span data-ttu-id="ee2a8-129">Relationships are created automatically between tables with a key pair.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-129">Relationships are created automatically between tables with a key pair.</span></span>

     ![Select tables and views](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="ee2a8-131">Your new model appears in your browser.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-131">Your new model appears in your browser.</span></span> <span data-ttu-id="ee2a8-132">From here, you can:</span><span class="sxs-lookup"><span data-stu-id="ee2a8-132">From here, you can:</span></span>   

- <span data-ttu-id="ee2a8-133">Query model data by dragging fields to the query designer and adding filters.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-133">Query model data by dragging fields to the query designer and adding filters.</span></span>
- <span data-ttu-id="ee2a8-134">Create new measures in tables.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-134">Create new measures in tables.</span></span>
- <span data-ttu-id="ee2a8-135">Edit model metadata by using the json editor.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-135">Edit model metadata by using the json editor.</span></span>
- <span data-ttu-id="ee2a8-136">Open the model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-136">Open the model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Select tables and views](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="ee2a8-138">When you edit model metadata or create new measures in your browser, you're saving those changes to your model in Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-138">When you edit model metadata or create new measures in your browser, you're saving those changes to your model in Azure.</span></span> <span data-ttu-id="ee2a8-139">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span><span class="sxs-lookup"><span data-stu-id="ee2a8-139">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ee2a8-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee2a8-140">Next steps</span></span> 
[<span data-ttu-id="ee2a8-141">Manage database roles and users</span><span class="sxs-lookup"><span data-stu-id="ee2a8-141">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="ee2a8-142">Connect with Excel</span><span class="sxs-lookup"><span data-stu-id="ee2a8-142">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


