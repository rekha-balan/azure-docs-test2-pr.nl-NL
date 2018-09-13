---
title: Tutorial - Add a basic sample model to your Azure Analysis Services server by using the portal | Microsoft Docs
description: In this tutorial lesson, learn how to add a sample model in Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: tutorial
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: c63995a461cee6bc39603a43604b8080942bd88b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856890"
---
# <a name="tutorial-add-a-sample-model-from-the-portal"></a><span data-ttu-id="57505-103">Tutorial: Add a sample model from the portal</span><span class="sxs-lookup"><span data-stu-id="57505-103">Tutorial: Add a sample model from the portal</span></span>

<span data-ttu-id="57505-104">In this tutorial, you add a sample Adventure Works tabular model database to your server.</span><span class="sxs-lookup"><span data-stu-id="57505-104">In this tutorial, you add a sample Adventure Works tabular model database to your server.</span></span> <span data-ttu-id="57505-105">The sample model is a completed version of the Adventure Works Internet Sales (1200) sample data model.</span><span class="sxs-lookup"><span data-stu-id="57505-105">The sample model is a completed version of the Adventure Works Internet Sales (1200) sample data model.</span></span> <span data-ttu-id="57505-106">A sample model is useful for testing model management, connecting with tools and client applications, and querying model data.</span><span class="sxs-lookup"><span data-stu-id="57505-106">A sample model is useful for testing model management, connecting with tools and client applications, and querying model data.</span></span> <span data-ttu-id="57505-107">This tutorial uses the [Azure portal](https://portal.azure.com) and [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) to:</span><span class="sxs-lookup"><span data-stu-id="57505-107">This tutorial uses the [Azure portal](https://portal.azure.com) and [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="57505-108">Add a completed sample tabular data model to a server</span><span class="sxs-lookup"><span data-stu-id="57505-108">Add a completed sample tabular data model to a server</span></span> 
> * <span data-ttu-id="57505-109">Connect to the model with SSMS</span><span class="sxs-lookup"><span data-stu-id="57505-109">Connect to the model with SSMS</span></span>

<span data-ttu-id="57505-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="57505-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="57505-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="57505-111">Before you begin</span></span>

<span data-ttu-id="57505-112">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="57505-112">To complete this tutorial, you need:</span></span>

- <span data-ttu-id="57505-113">An Azure Analysis Services server.</span><span class="sxs-lookup"><span data-stu-id="57505-113">An Azure Analysis Services server.</span></span> <span data-ttu-id="57505-114">To learn more, see [Create a server - portal](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="57505-114">To learn more, see [Create a server - portal](analysis-services-create-server.md).</span></span>
- <span data-ttu-id="57505-115">Server administrator permissions</span><span class="sxs-lookup"><span data-stu-id="57505-115">Server administrator permissions</span></span>
- [<span data-ttu-id="57505-116">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="57505-116">SQL Server Management Studio</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)


## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="57505-117">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="57505-117">Sign in to the Azure portal</span></span>

<span data-ttu-id="57505-118">Sign in to the [portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="57505-118">Sign in to the [portal](https://portal.azure.com/).</span></span>

## <a name="add-a-sample-model"></a><span data-ttu-id="57505-119">Add a sample model</span><span class="sxs-lookup"><span data-stu-id="57505-119">Add a sample model</span></span>

1. <span data-ttu-id="57505-120">In server **Overview**, click **New model**.</span><span class="sxs-lookup"><span data-stu-id="57505-120">In server **Overview**, click **New model**.</span></span>

    ![Create a sample model](./media/analysis-services-create-sample-model/aas-create-sample-new-model.png)

2. <span data-ttu-id="57505-122">In **New model** > **Choose a datasource**,  verify **Sample data** is selected, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="57505-122">In **New model** > **Choose a datasource**,  verify **Sample data** is selected, and then click **Add**.</span></span>

    ![Select sample data](./media/analysis-services-create-sample-model/aas-create-sample-data.png)

3. <span data-ttu-id="57505-124">In **Overview**, verify the `adventureworks` sample model is added.</span><span class="sxs-lookup"><span data-stu-id="57505-124">In **Overview**, verify the `adventureworks` sample model is added.</span></span>

    ![Select sample data](./media/analysis-services-create-sample-model/aas-create-sample-verify.png)


## <a name="clean-up-resources"></a><span data-ttu-id="57505-126">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="57505-126">Clean up resources</span></span>

<span data-ttu-id="57505-127">Your sample model is using cache memory resources.</span><span class="sxs-lookup"><span data-stu-id="57505-127">Your sample model is using cache memory resources.</span></span> <span data-ttu-id="57505-128">If you are not using your sample model for testing, you should remove it from your server.</span><span class="sxs-lookup"><span data-stu-id="57505-128">If you are not using your sample model for testing, you should remove it from your server.</span></span>

<span data-ttu-id="57505-129">These steps describe how to delete a model from a server by using SSMS.</span><span class="sxs-lookup"><span data-stu-id="57505-129">These steps describe how to delete a model from a server by using SSMS.</span></span> <span data-ttu-id="57505-130">You can also delete a model by using the preview Web designer feature.</span><span class="sxs-lookup"><span data-stu-id="57505-130">You can also delete a model by using the preview Web designer feature.</span></span>

1. <span data-ttu-id="57505-131">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="57505-131">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>

2. <span data-ttu-id="57505-132">In **Connect to Server**, paste in the server name, then in **Authentication**, choose **Active Directory - Universal with MFA support**, enter your username, and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="57505-132">In **Connect to Server**, paste in the server name, then in **Authentication**, choose **Active Directory - Universal with MFA support**, enter your username, and then click **Connect**.</span></span>

    ![Sign in](./media/analysis-services-create-sample-model/aas-create-sample-cleanup-signin.png)

3. <span data-ttu-id="57505-134">In **Object Explorer**, right-click the `adventureworks` sample database, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="57505-134">In **Object Explorer**, right-click the `adventureworks` sample database, and then click **Delete**.</span></span>

    ![Delete sample database](./media/analysis-services-create-sample-model/aas-create-sample-cleanup-delete.png)

## <a name="next-steps"></a><span data-ttu-id="57505-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="57505-136">Next steps</span></span> 

<span data-ttu-id="57505-137">In this tutorial, you learned how to add a basic, sample model to your server.</span><span class="sxs-lookup"><span data-stu-id="57505-137">In this tutorial, you learned how to add a basic, sample model to your server.</span></span> <span data-ttu-id="57505-138">Now that you have a model database, you can connect to it from SQL Server Management Studio and add user roles.</span><span class="sxs-lookup"><span data-stu-id="57505-138">Now that you have a model database, you can connect to it from SQL Server Management Studio and add user roles.</span></span> <span data-ttu-id="57505-139">To learn more, continue with the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="57505-139">To learn more, continue with the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57505-140">Tutorial: Configure server administrator and user roles</span><span class="sxs-lookup"><span data-stu-id="57505-140">Tutorial: Configure server administrator and user roles</span></span>](analysis-services-database-users.md)


