---
title: Copy data from SQL Server to Blob storage by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from an on-premises data store to the cloud by using a self-hosted integration runtime in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/11/2018
ms.author: jingwang
ms.openlocfilehash: f408d24a5957061bf03d340a555b87bdc6b2aacc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869418"
---
# <a name="copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage"></a><span data-ttu-id="603bc-103">Copy data from an on-premises SQL Server database to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="603bc-103">Copy data from an on-premises SQL Server database to Azure Blob storage</span></span>
<span data-ttu-id="603bc-104">In this tutorial, you use the Azure Data Factory user interface (UI) to create a data factory pipeline that copies data from an on-premises SQL Server database to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="603bc-104">In this tutorial, you use the Azure Data Factory user interface (UI) to create a data factory pipeline that copies data from an on-premises SQL Server database to Azure Blob storage.</span></span> <span data-ttu-id="603bc-105">You create and use a self-hosted integration runtime, which moves data between on-premises and cloud data stores.</span><span class="sxs-lookup"><span data-stu-id="603bc-105">You create and use a self-hosted integration runtime, which moves data between on-premises and cloud data stores.</span></span>

> [!NOTE]
> <span data-ttu-id="603bc-106">This article doesn't provide a detailed introduction to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="603bc-106">This article doesn't provide a detailed introduction to Data Factory.</span></span> <span data-ttu-id="603bc-107">For more information, see [Introduction to Data Factory](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="603bc-107">For more information, see [Introduction to Data Factory](introduction.md).</span></span> 

<span data-ttu-id="603bc-108">In this tutorial, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-108">In this tutorial, you perform the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="603bc-109">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="603bc-109">Create a data factory.</span></span>
> * <span data-ttu-id="603bc-110">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="603bc-110">Create a self-hosted integration runtime.</span></span>
> * <span data-ttu-id="603bc-111">Create SQL Server and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="603bc-111">Create SQL Server and Azure Storage linked services.</span></span> 
> * <span data-ttu-id="603bc-112">Create SQL Server and Azure Blob datasets.</span><span class="sxs-lookup"><span data-stu-id="603bc-112">Create SQL Server and Azure Blob datasets.</span></span>
> * <span data-ttu-id="603bc-113">Create a pipeline with a copy activity to move the data.</span><span class="sxs-lookup"><span data-stu-id="603bc-113">Create a pipeline with a copy activity to move the data.</span></span>
> * <span data-ttu-id="603bc-114">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="603bc-114">Start a pipeline run.</span></span>
> * <span data-ttu-id="603bc-115">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="603bc-115">Monitor the pipeline run.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="603bc-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="603bc-116">Prerequisites</span></span>
### <a name="azure-subscription"></a><span data-ttu-id="603bc-117">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="603bc-117">Azure subscription</span></span>
<span data-ttu-id="603bc-118">Before you begin, if you don't already have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="603bc-118">Before you begin, if you don't already have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span></span>

### <a name="azure-roles"></a><span data-ttu-id="603bc-119">Azure roles</span><span class="sxs-lookup"><span data-stu-id="603bc-119">Azure roles</span></span>
<span data-ttu-id="603bc-120">To create data factory instances, the user account you use to sign in to Azure must be assigned a *Contributor* or *Owner* role or must be an *administrator* of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="603bc-120">To create data factory instances, the user account you use to sign in to Azure must be assigned a *Contributor* or *Owner* role or must be an *administrator* of the Azure subscription.</span></span> 

<span data-ttu-id="603bc-121">To view the permissions you have in the subscription, go to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="603bc-121">To view the permissions you have in the subscription, go to the Azure portal.</span></span> <span data-ttu-id="603bc-122">In the upper-right corner, select your user name, and then select **Permissions**.</span><span class="sxs-lookup"><span data-stu-id="603bc-122">In the upper-right corner, select your user name, and then select **Permissions**.</span></span> <span data-ttu-id="603bc-123">If you have access to multiple subscriptions, select the appropriate subscription.</span><span class="sxs-lookup"><span data-stu-id="603bc-123">If you have access to multiple subscriptions, select the appropriate subscription.</span></span> <span data-ttu-id="603bc-124">For sample instructions on how to add a user to a role, see [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="603bc-124">For sample instructions on how to add a user to a role, see [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md).</span></span>

### <a name="sql-server-2014-2016-and-2017"></a><span data-ttu-id="603bc-125">SQL Server 2014, 2016, and 2017</span><span class="sxs-lookup"><span data-stu-id="603bc-125">SQL Server 2014, 2016, and 2017</span></span>
<span data-ttu-id="603bc-126">In this tutorial, you use an on-premises SQL Server database as a *source* data store.</span><span class="sxs-lookup"><span data-stu-id="603bc-126">In this tutorial, you use an on-premises SQL Server database as a *source* data store.</span></span> <span data-ttu-id="603bc-127">The pipeline in the data factory you create in this tutorial copies data from this on-premises SQL Server database (source) to Blob storage (sink).</span><span class="sxs-lookup"><span data-stu-id="603bc-127">The pipeline in the data factory you create in this tutorial copies data from this on-premises SQL Server database (source) to Blob storage (sink).</span></span> <span data-ttu-id="603bc-128">You then create a table named **emp** in your SQL Server database and insert a couple of sample entries into the table.</span><span class="sxs-lookup"><span data-stu-id="603bc-128">You then create a table named **emp** in your SQL Server database and insert a couple of sample entries into the table.</span></span> 

1. <span data-ttu-id="603bc-129">Start SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="603bc-129">Start SQL Server Management Studio.</span></span> <span data-ttu-id="603bc-130">If it's not already installed on your machine, go to [Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="603bc-130">If it's not already installed on your machine, go to [Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> 

1. <span data-ttu-id="603bc-131">Connect to your SQL Server instance by using your credentials.</span><span class="sxs-lookup"><span data-stu-id="603bc-131">Connect to your SQL Server instance by using your credentials.</span></span> 

1. <span data-ttu-id="603bc-132">Create a sample database.</span><span class="sxs-lookup"><span data-stu-id="603bc-132">Create a sample database.</span></span> <span data-ttu-id="603bc-133">In the tree view, right-click **Databases**, and then select **New Database**.</span><span class="sxs-lookup"><span data-stu-id="603bc-133">In the tree view, right-click **Databases**, and then select **New Database**.</span></span> 
1. <span data-ttu-id="603bc-134">In the **New Database** window, enter a name for the database, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="603bc-134">In the **New Database** window, enter a name for the database, and then select **OK**.</span></span> 

1. <span data-ttu-id="603bc-135">To create the **emp** table and insert some sample data into it, run the following query script against the database:</span><span class="sxs-lookup"><span data-stu-id="603bc-135">To create the **emp** table and insert some sample data into it, run the following query script against the database:</span></span>

   ```
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO
    
    INSERT INTO emp (FirstName, LastName) VALUES ('John', 'Doe')
    INSERT INTO emp (FirstName, LastName) VALUES ('Jane', 'Doe')
    GO
   ```

1. <span data-ttu-id="603bc-136">In the tree view, right-click the database that you created, and then select **New Query**.</span><span class="sxs-lookup"><span data-stu-id="603bc-136">In the tree view, right-click the database that you created, and then select **New Query**.</span></span>

### <a name="azure-storage-account"></a><span data-ttu-id="603bc-137">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="603bc-137">Azure storage account</span></span>
<span data-ttu-id="603bc-138">In this tutorial, you use a general-purpose Azure storage account (specifically, Blob storage) as a destination/sink data store.</span><span class="sxs-lookup"><span data-stu-id="603bc-138">In this tutorial, you use a general-purpose Azure storage account (specifically, Blob storage) as a destination/sink data store.</span></span> <span data-ttu-id="603bc-139">If you don't have a general-purpose Azure storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="603bc-139">If you don't have a general-purpose Azure storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span> <span data-ttu-id="603bc-140">The pipeline in the data factory that you create in this tutorial copies data from the on-premises SQL Server database (source) to Blob storage (sink).</span><span class="sxs-lookup"><span data-stu-id="603bc-140">The pipeline in the data factory that you create in this tutorial copies data from the on-premises SQL Server database (source) to Blob storage (sink).</span></span> 

#### <a name="get-the-storage-account-name-and-account-key"></a><span data-ttu-id="603bc-141">Get the storage account name and account key</span><span class="sxs-lookup"><span data-stu-id="603bc-141">Get the storage account name and account key</span></span>
<span data-ttu-id="603bc-142">You use the name and key of your storage account in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="603bc-142">You use the name and key of your storage account in this tutorial.</span></span> <span data-ttu-id="603bc-143">To get the name and key of your storage account, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-143">To get the name and key of your storage account, take the following steps:</span></span> 

1. <span data-ttu-id="603bc-144">Sign in to the [Azure portal](https://portal.azure.com) with your Azure user name and password.</span><span class="sxs-lookup"><span data-stu-id="603bc-144">Sign in to the [Azure portal](https://portal.azure.com) with your Azure user name and password.</span></span> 

1. <span data-ttu-id="603bc-145">In the left pane, select **More services**.</span><span class="sxs-lookup"><span data-stu-id="603bc-145">In the left pane, select **More services**.</span></span> <span data-ttu-id="603bc-146">Filter by using the **Storage** keyword, and then select **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="603bc-146">Filter by using the **Storage** keyword, and then select **Storage accounts**.</span></span>

    ![Storage account search](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

1. <span data-ttu-id="603bc-148">In the list of storage accounts, filter for your storage account, if needed.</span><span class="sxs-lookup"><span data-stu-id="603bc-148">In the list of storage accounts, filter for your storage account, if needed.</span></span> <span data-ttu-id="603bc-149">Then select your storage account.</span><span class="sxs-lookup"><span data-stu-id="603bc-149">Then select your storage account.</span></span> 

1. <span data-ttu-id="603bc-150">In the **Storage account** window, select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="603bc-150">In the **Storage account** window, select **Access keys**.</span></span>

    ![Access keys](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

1. <span data-ttu-id="603bc-152">In the **Storage account name** and **key1** boxes, copy the values, and then paste them into Notepad or another editor for later use in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="603bc-152">In the **Storage account name** and **key1** boxes, copy the values, and then paste them into Notepad or another editor for later use in the tutorial.</span></span> 

#### <a name="create-the-adftutorial-container"></a><span data-ttu-id="603bc-153">Create the adftutorial container</span><span class="sxs-lookup"><span data-stu-id="603bc-153">Create the adftutorial container</span></span> 
<span data-ttu-id="603bc-154">In this section, you create a blob container named **adftutorial** in your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="603bc-154">In this section, you create a blob container named **adftutorial** in your Blob storage.</span></span> 

1. <span data-ttu-id="603bc-155">In the **Storage account** window, go to **Overview**, and then select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="603bc-155">In the **Storage account** window, go to **Overview**, and then select **Blobs**.</span></span> 

    ![Select Blobs option](media/tutorial-hybrid-copy-powershell/select-blobs.png)

1. <span data-ttu-id="603bc-157">In the **Blob service** window, select **Container**.</span><span class="sxs-lookup"><span data-stu-id="603bc-157">In the **Blob service** window, select **Container**.</span></span> 

    ![Container button](media/tutorial-hybrid-copy-powershell/add-container-button.png)

1. <span data-ttu-id="603bc-159">In the **New container** window, under **Name**, enter **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="603bc-159">In the **New container** window, under **Name**, enter **adftutorial**.</span></span> <span data-ttu-id="603bc-160">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="603bc-160">Then select **OK**.</span></span> 

    ![New container window](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

1. <span data-ttu-id="603bc-162">In the list of containers, select **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="603bc-162">In the list of containers, select **adftutorial**.</span></span>

    ![Container selection](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

1. <span data-ttu-id="603bc-164">Keep the **container** window for **adftutorial** open.</span><span class="sxs-lookup"><span data-stu-id="603bc-164">Keep the **container** window for **adftutorial** open.</span></span> <span data-ttu-id="603bc-165">You use it verify the output at the end of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="603bc-165">You use it verify the output at the end of the tutorial.</span></span> <span data-ttu-id="603bc-166">Data Factory automatically creates the output folder in this container, so you don't need to create one.</span><span class="sxs-lookup"><span data-stu-id="603bc-166">Data Factory automatically creates the output folder in this container, so you don't need to create one.</span></span>

    ![Container window](media/tutorial-hybrid-copy-powershell/container-page.png)


## <a name="create-a-data-factory"></a><span data-ttu-id="603bc-168">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="603bc-168">Create a data factory</span></span>
<span data-ttu-id="603bc-169">In this step, you create a data factory and start the Data Factory UI to create a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="603bc-169">In this step, you create a data factory and start the Data Factory UI to create a pipeline in the data factory.</span></span> 

1. <span data-ttu-id="603bc-170">Open the **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="603bc-170">Open the **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="603bc-171">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="603bc-171">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="603bc-172">On the left menu, select **New** > **Data + Analytics** > **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="603bc-172">On the left menu, select **New** > **Data + Analytics** > **Data Factory**.</span></span>
   
   ![New data factory creation](./media/tutorial-hybrid-copy-portal/new-azure-data-factory-menu.png)
1. <span data-ttu-id="603bc-174">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="603bc-174">On the **New data factory** page, under **Name**, enter **ADFTutorialDataFactory**.</span></span> 
   
     ![New data factory page](./media/tutorial-hybrid-copy-portal/new-azure-data-factory.png)

<span data-ttu-id="603bc-176">The name of the data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="603bc-176">The name of the data factory must be *globally unique*.</span></span> <span data-ttu-id="603bc-177">If you see the following error message for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span><span class="sxs-lookup"><span data-stu-id="603bc-177">If you see the following error message for the name field, change the name of the data factory (for example, yournameADFTutorialDataFactory).</span></span> <span data-ttu-id="603bc-178">For naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="603bc-178">For naming rules for Data Factory artifacts, see [Data Factory naming rules](naming-rules.md).</span></span>

   ![New data factory name](./media/tutorial-hybrid-copy-portal/name-not-available-error.png)
1. <span data-ttu-id="603bc-180">Select the Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="603bc-180">Select the Azure **subscription** in which you want to create the data factory.</span></span>
1. <span data-ttu-id="603bc-181">For **Resource Group**, take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-181">For **Resource Group**, take one of the following steps:</span></span>
   
      - <span data-ttu-id="603bc-182">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="603bc-182">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span>

      - <span data-ttu-id="603bc-183">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="603bc-183">Select **Create new**, and enter the name of a resource group.</span></span>
        
    <span data-ttu-id="603bc-184">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="603bc-184">To learn about resource groups, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
1. <span data-ttu-id="603bc-185">Under **Version**, select **V2**.</span><span class="sxs-lookup"><span data-stu-id="603bc-185">Under **Version**, select **V2**.</span></span>
1. <span data-ttu-id="603bc-186">Under **Location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="603bc-186">Under **Location**, select the location for the data factory.</span></span> <span data-ttu-id="603bc-187">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="603bc-187">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="603bc-188">The data stores (for example, Storage and SQL Database) and computes (for example, Azure HDInsight) used by Data Factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="603bc-188">The data stores (for example, Storage and SQL Database) and computes (for example, Azure HDInsight) used by Data Factory can be in other regions.</span></span>
1. <span data-ttu-id="603bc-189">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="603bc-189">Select **Pin to dashboard**.</span></span> 
1. <span data-ttu-id="603bc-190">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="603bc-190">Select **Create**.</span></span>
1. <span data-ttu-id="603bc-191">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="603bc-191">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span>

    ![Deploying data factory tile](media/tutorial-hybrid-copy-portal/deploying-data-factory.png)
1. <span data-ttu-id="603bc-193">After the creation is finished, you see the **Data Factory** page as shown in the image:</span><span class="sxs-lookup"><span data-stu-id="603bc-193">After the creation is finished, you see the **Data Factory** page as shown in the image:</span></span>
   
    ![Data factory home page](./media/tutorial-hybrid-copy-portal/data-factory-home-page.png)
1. <span data-ttu-id="603bc-195">Select the **Author & Monitor** tile to launch the Data Factory UI in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="603bc-195">Select the **Author & Monitor** tile to launch the Data Factory UI in a separate tab.</span></span> 


## <a name="create-a-pipeline"></a><span data-ttu-id="603bc-196">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="603bc-196">Create a pipeline</span></span>

1. <span data-ttu-id="603bc-197">On the **Let's get started** page, select **Create pipeline**.</span><span class="sxs-lookup"><span data-stu-id="603bc-197">On the **Let's get started** page, select **Create pipeline**.</span></span> <span data-ttu-id="603bc-198">A pipeline is automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="603bc-198">A pipeline is automatically created for you.</span></span> <span data-ttu-id="603bc-199">You see the pipeline in the tree view, and its editor opens.</span><span class="sxs-lookup"><span data-stu-id="603bc-199">You see the pipeline in the tree view, and its editor opens.</span></span> 

   ![Let's get started page](./media/tutorial-hybrid-copy-portal/get-started-page.png)

1. <span data-ttu-id="603bc-201">On the **General** tab at the bottom of the **Properties** window, in **Name**, enter **SQLServerToBlobPipeline**.</span><span class="sxs-lookup"><span data-stu-id="603bc-201">On the **General** tab at the bottom of the **Properties** window, in **Name**, enter **SQLServerToBlobPipeline**.</span></span>

   ![Pipeline name](./media/tutorial-hybrid-copy-portal/pipeline-name.png)

1. <span data-ttu-id="603bc-203">In the **Activities** tool box, expand **DataFlow**.</span><span class="sxs-lookup"><span data-stu-id="603bc-203">In the **Activities** tool box, expand **DataFlow**.</span></span> <span data-ttu-id="603bc-204">Drag and drop the **Copy** activity to the pipeline design surface.</span><span class="sxs-lookup"><span data-stu-id="603bc-204">Drag and drop the **Copy** activity to the pipeline design surface.</span></span> <span data-ttu-id="603bc-205">Set the name of the activity to **CopySqlServerToAzureBlobActivity**.</span><span class="sxs-lookup"><span data-stu-id="603bc-205">Set the name of the activity to **CopySqlServerToAzureBlobActivity**.</span></span>

   ![Activity name](./media/tutorial-hybrid-copy-portal/copy-activity-name.png)

1. <span data-ttu-id="603bc-207">In the **Properties** window, go to the **Source** tab, and select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="603bc-207">In the **Properties** window, go to the **Source** tab, and select **+ New**.</span></span>

   ![Source tab](./media/tutorial-hybrid-copy-portal/source-dataset-new-button.png)

1. <span data-ttu-id="603bc-209">In the **New Dataset** window, search for **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="603bc-209">In the **New Dataset** window, search for **SQL Server**.</span></span> <span data-ttu-id="603bc-210">Select **SQL Server**, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="603bc-210">Select **SQL Server**, and then select **Finish**.</span></span> <span data-ttu-id="603bc-211">You see a new tab titled **SqlServerTable1**.</span><span class="sxs-lookup"><span data-stu-id="603bc-211">You see a new tab titled **SqlServerTable1**.</span></span> <span data-ttu-id="603bc-212">You also see the **SqlServerTable1** dataset in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="603bc-212">You also see the **SqlServerTable1** dataset in the tree view on the left.</span></span> 

   ![SQL Server selection](./media/tutorial-hybrid-copy-portal/select-sql-server.png)

1. <span data-ttu-id="603bc-214">On the **General** tab at the bottom of the **Properties** window, in **Name**, enter **SqlServerDataset**.</span><span class="sxs-lookup"><span data-stu-id="603bc-214">On the **General** tab at the bottom of the **Properties** window, in **Name**, enter **SqlServerDataset**.</span></span>

   ![Source dataset name](./media/tutorial-hybrid-copy-portal/source-dataset-name.png)

1. <span data-ttu-id="603bc-216">Go to the **Connection** tab, and select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="603bc-216">Go to the **Connection** tab, and select **+ New**.</span></span> <span data-ttu-id="603bc-217">You create a connection to the source data store (SQL Server database) in this step.</span><span class="sxs-lookup"><span data-stu-id="603bc-217">You create a connection to the source data store (SQL Server database) in this step.</span></span> 

   ![Connection to source dataset](./media/tutorial-hybrid-copy-portal/source-connection-new-button.png)

1. <span data-ttu-id="603bc-219">In the **New Linked Service** window, add **Name** as **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="603bc-219">In the **New Linked Service** window, add **Name** as **SqlServerLinkedService**.</span></span> <span data-ttu-id="603bc-220">Select **New** under **Connect via integration runtime**.</span><span class="sxs-lookup"><span data-stu-id="603bc-220">Select **New** under **Connect via integration runtime**.</span></span> <span data-ttu-id="603bc-221">In this section, you create a self-hosted integration runtime and associate it with an on-premises machine with the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="603bc-221">In this section, you create a self-hosted integration runtime and associate it with an on-premises machine with the SQL Server database.</span></span> <span data-ttu-id="603bc-222">The self-hosted integration runtime is the component that copies data from the SQL Server database on your machine to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="603bc-222">The self-hosted integration runtime is the component that copies data from the SQL Server database on your machine to Blob storage.</span></span> 

   ![New integration runtime](./media/tutorial-hybrid-copy-portal/new-integration-runtime-button.png)

1. <span data-ttu-id="603bc-224">In the **Integration Runtime Setup** window, select **Private Network**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="603bc-224">In the **Integration Runtime Setup** window, select **Private Network**, and then select **Next**.</span></span> 

   ![Private network selection](./media/tutorial-hybrid-copy-portal/select-private-network.png)

1. <span data-ttu-id="603bc-226">Enter a name for the integration runtime, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="603bc-226">Enter a name for the integration runtime, and select **Next**.</span></span>

    ![Integration runtime name](./media/tutorial-hybrid-copy-portal/integration-runtime-name.png)

1. <span data-ttu-id="603bc-228">Under **Option 1: Express setup**, select **Click here to launch the express setup for this computer**.</span><span class="sxs-lookup"><span data-stu-id="603bc-228">Under **Option 1: Express setup**, select **Click here to launch the express setup for this computer**.</span></span> 

    ![Express setup link](./media/tutorial-hybrid-copy-portal/click-exress-setup.png)

1. <span data-ttu-id="603bc-230">In the **Integration Runtime (Self-hosted) Express Setup** window, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="603bc-230">In the **Integration Runtime (Self-hosted) Express Setup** window, select **Close**.</span></span> 

    ![Integration runtime (self-hosted) express setup](./media/tutorial-hybrid-copy-portal/integration-runtime-setup-successful.png)

1. <span data-ttu-id="603bc-232">In the **New Linked Service** window, ensure the **Integration Runtime** created above is selected under **Connect via integration runtime**.</span><span class="sxs-lookup"><span data-stu-id="603bc-232">In the **New Linked Service** window, ensure the **Integration Runtime** created above is selected under **Connect via integration runtime**.</span></span> 

    ![](./media/tutorial-hybrid-copy-portal/select-integration-runtime.png)

1. <span data-ttu-id="603bc-233">In the **New Linked Service** window, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-233">In the **New Linked Service** window, take the following steps:</span></span>

    <span data-ttu-id="603bc-234">a.</span><span class="sxs-lookup"><span data-stu-id="603bc-234">a.</span></span> <span data-ttu-id="603bc-235">Under **Name**, enter **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="603bc-235">Under **Name**, enter **SqlServerLinkedService**.</span></span>

    <span data-ttu-id="603bc-236">b.</span><span class="sxs-lookup"><span data-stu-id="603bc-236">b.</span></span> <span data-ttu-id="603bc-237">Under **Connect via integration runtime**, confirm that the self-hosted integration runtime you created earlier shows up.</span><span class="sxs-lookup"><span data-stu-id="603bc-237">Under **Connect via integration runtime**, confirm that the self-hosted integration runtime you created earlier shows up.</span></span>

    <span data-ttu-id="603bc-238">c.</span><span class="sxs-lookup"><span data-stu-id="603bc-238">c.</span></span> <span data-ttu-id="603bc-239">Under **Server name**, enter the name of your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="603bc-239">Under **Server name**, enter the name of your SQL Server instance.</span></span> 

    <span data-ttu-id="603bc-240">d.</span><span class="sxs-lookup"><span data-stu-id="603bc-240">d.</span></span> <span data-ttu-id="603bc-241">Under **Database name**, enter the name of the database with the **emp** table.</span><span class="sxs-lookup"><span data-stu-id="603bc-241">Under **Database name**, enter the name of the database with the **emp** table.</span></span>

    <span data-ttu-id="603bc-242">e.</span><span class="sxs-lookup"><span data-stu-id="603bc-242">e.</span></span> <span data-ttu-id="603bc-243">Under **Authentication type**, select the appropriate authentication type that Data Factory should use to connect to your SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="603bc-243">Under **Authentication type**, select the appropriate authentication type that Data Factory should use to connect to your SQL Server database.</span></span>

    <span data-ttu-id="603bc-244">f.</span><span class="sxs-lookup"><span data-stu-id="603bc-244">f.</span></span> <span data-ttu-id="603bc-245">Under **User name** and **Password**, enter the user name and password.</span><span class="sxs-lookup"><span data-stu-id="603bc-245">Under **User name** and **Password**, enter the user name and password.</span></span> <span data-ttu-id="603bc-246">If you need to use a backslash (\\) in your user account or server name, precede it with the escape character (\\).</span><span class="sxs-lookup"><span data-stu-id="603bc-246">If you need to use a backslash (\\) in your user account or server name, precede it with the escape character (\\).</span></span> <span data-ttu-id="603bc-247">For example, use *mydomain\\\\myuser*.</span><span class="sxs-lookup"><span data-stu-id="603bc-247">For example, use *mydomain\\\\myuser*.</span></span>

    <span data-ttu-id="603bc-248">g.</span><span class="sxs-lookup"><span data-stu-id="603bc-248">g.</span></span> <span data-ttu-id="603bc-249">Select **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="603bc-249">Select **Test connection**.</span></span> <span data-ttu-id="603bc-250">Do this step to confirm that Data Factory can connect to your SQL Server database by using the self-hosted integration runtime you created.</span><span class="sxs-lookup"><span data-stu-id="603bc-250">Do this step to confirm that Data Factory can connect to your SQL Server database by using the self-hosted integration runtime you created.</span></span>

    <span data-ttu-id="603bc-251">h.</span><span class="sxs-lookup"><span data-stu-id="603bc-251">h.</span></span> <span data-ttu-id="603bc-252">To save the linked service, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="603bc-252">To save the linked service, select **Finish**.</span></span>

       

1. <span data-ttu-id="603bc-253">You should be back in the window with the source dataset opened.</span><span class="sxs-lookup"><span data-stu-id="603bc-253">You should be back in the window with the source dataset opened.</span></span> <span data-ttu-id="603bc-254">On the **Connection** tab of the **Properties** window, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-254">On the **Connection** tab of the **Properties** window, take the following steps:</span></span> 

    <span data-ttu-id="603bc-255">a.</span><span class="sxs-lookup"><span data-stu-id="603bc-255">a.</span></span> <span data-ttu-id="603bc-256">In **Linked service**, confirm that you see **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="603bc-256">In **Linked service**, confirm that you see **SqlServerLinkedService**.</span></span>

    <span data-ttu-id="603bc-257">b.</span><span class="sxs-lookup"><span data-stu-id="603bc-257">b.</span></span> <span data-ttu-id="603bc-258">In **Table**, select **[dbo].[emp]**.</span><span class="sxs-lookup"><span data-stu-id="603bc-258">In **Table**, select **[dbo].[emp]**.</span></span>

    ![Source dataset connection information](./media/tutorial-hybrid-copy-portal/source-dataset-connection.png)

1. <span data-ttu-id="603bc-260">Go to the tab with **SQLServerToBlobPipeline**, or select **SQLServerToBlobPipeline** in the tree view.</span><span class="sxs-lookup"><span data-stu-id="603bc-260">Go to the tab with **SQLServerToBlobPipeline**, or select **SQLServerToBlobPipeline** in the tree view.</span></span> 

    ![Pipeline tab](./media/tutorial-hybrid-copy-portal/pipeliene-tab.png)

1. <span data-ttu-id="603bc-262">Go to the **Sink** tab at the bottom of the **Properties** window, and select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="603bc-262">Go to the **Sink** tab at the bottom of the **Properties** window, and select **+ New**.</span></span> 

    ![Sink tab](./media/tutorial-hybrid-copy-portal/sink-dataset-new-button.png)

1. <span data-ttu-id="603bc-264">In the **New Dataset** window, select **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="603bc-264">In the **New Dataset** window, select **Azure Blob Storage**.</span></span> <span data-ttu-id="603bc-265">Then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="603bc-265">Then select **Finish**.</span></span> <span data-ttu-id="603bc-266">You see a new tab opened for the dataset.</span><span class="sxs-lookup"><span data-stu-id="603bc-266">You see a new tab opened for the dataset.</span></span> <span data-ttu-id="603bc-267">You also see the dataset in the tree view.</span><span class="sxs-lookup"><span data-stu-id="603bc-267">You also see the dataset in the tree view.</span></span> 

    ![Blob storage selection](./media/tutorial-hybrid-copy-portal/select-azure-blob-storage.png)

1. <span data-ttu-id="603bc-269">In **Name**, enter **AzureBlobDataset**.</span><span class="sxs-lookup"><span data-stu-id="603bc-269">In **Name**, enter **AzureBlobDataset**.</span></span>

    ![Sink dataset name](./media/tutorial-hybrid-copy-portal/sink-dataset-name.png)

1. <span data-ttu-id="603bc-271">Go to the **Connection** tab at the bottom of the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="603bc-271">Go to the **Connection** tab at the bottom of the **Properties** window.</span></span> <span data-ttu-id="603bc-272">Next to **Linked service**, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="603bc-272">Next to **Linked service**, select **+ New**.</span></span> 

    ![New linked service button](./media/tutorial-hybrid-copy-portal/new-storage-linked-service-button.png)

1. <span data-ttu-id="603bc-274">In the **New Linked Service** window, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-274">In the **New Linked Service** window, take the following steps:</span></span>

    <span data-ttu-id="603bc-275">a.</span><span class="sxs-lookup"><span data-stu-id="603bc-275">a.</span></span> <span data-ttu-id="603bc-276">Under **Name**, enter **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="603bc-276">Under **Name**, enter **AzureStorageLinkedService**.</span></span>

    <span data-ttu-id="603bc-277">b.</span><span class="sxs-lookup"><span data-stu-id="603bc-277">b.</span></span> <span data-ttu-id="603bc-278">Under **Storage account name**, select your storage account.</span><span class="sxs-lookup"><span data-stu-id="603bc-278">Under **Storage account name**, select your storage account.</span></span>

    <span data-ttu-id="603bc-279">c.</span><span class="sxs-lookup"><span data-stu-id="603bc-279">c.</span></span> <span data-ttu-id="603bc-280">To test the connection to your storage account, select **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="603bc-280">To test the connection to your storage account, select **Test connection**.</span></span>

    <span data-ttu-id="603bc-281">d.</span><span class="sxs-lookup"><span data-stu-id="603bc-281">d.</span></span> <span data-ttu-id="603bc-282">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="603bc-282">Select **Save**.</span></span>

    ![Storage linked service settings](./media/tutorial-hybrid-copy-portal/azure-storage-linked-service-settings.png) 

1. <span data-ttu-id="603bc-284">You should be back in the window with the sink dataset open.</span><span class="sxs-lookup"><span data-stu-id="603bc-284">You should be back in the window with the sink dataset open.</span></span> <span data-ttu-id="603bc-285">On the **Connection** tab, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="603bc-285">On the **Connection** tab, take the following steps:</span></span> 

    <span data-ttu-id="603bc-286">a.</span><span class="sxs-lookup"><span data-stu-id="603bc-286">a.</span></span> <span data-ttu-id="603bc-287">In **Linked service**, confirm that **AzureStorageLinkedService** is selected.</span><span class="sxs-lookup"><span data-stu-id="603bc-287">In **Linked service**, confirm that **AzureStorageLinkedService** is selected.</span></span>

    <span data-ttu-id="603bc-288">b.</span><span class="sxs-lookup"><span data-stu-id="603bc-288">b.</span></span> <span data-ttu-id="603bc-289">For the **folder**/ **Directory** part of **File path**, enter **adftutorial/fromonprem**.</span><span class="sxs-lookup"><span data-stu-id="603bc-289">For the **folder**/ **Directory** part of **File path**, enter **adftutorial/fromonprem**.</span></span> <span data-ttu-id="603bc-290">If the output folder doesn't exist in the adftutorial container, Data Factory automatically creates the output folder.</span><span class="sxs-lookup"><span data-stu-id="603bc-290">If the output folder doesn't exist in the adftutorial container, Data Factory automatically creates the output folder.</span></span>

    <span data-ttu-id="603bc-291">c.</span><span class="sxs-lookup"><span data-stu-id="603bc-291">c.</span></span> <span data-ttu-id="603bc-292">For the **file name** part of **File path**, select **Add dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="603bc-292">For the **file name** part of **File path**, select **Add dynamic content**.</span></span>   

    ![dynamic file name value](./media/tutorial-hybrid-copy-portal/file-name.png)

    <span data-ttu-id="603bc-294">d.</span><span class="sxs-lookup"><span data-stu-id="603bc-294">d.</span></span> <span data-ttu-id="603bc-295">Add `@CONCAT(pipeline().RunId, '.txt')`, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="603bc-295">Add `@CONCAT(pipeline().RunId, '.txt')`, select **Finish**.</span></span> <span data-ttu-id="603bc-296">This will rename the file with PipelineRunID.txt.</span><span class="sxs-lookup"><span data-stu-id="603bc-296">This will rename the file with PipelineRunID.txt.</span></span> 

    ![dynamic expression for resolving file name](./media/tutorial-hybrid-copy-portal/add-dynamic-file-name.png)

    ![Connection to sink dataset](./media/tutorial-hybrid-copy-portal/sink-dataset-connection.png)

1. <span data-ttu-id="603bc-299">Go to the tab with the pipeline opened, or select the pipeline in the tree view.</span><span class="sxs-lookup"><span data-stu-id="603bc-299">Go to the tab with the pipeline opened, or select the pipeline in the tree view.</span></span> <span data-ttu-id="603bc-300">In **Sink Dataset**, confirm that **AzureBlobDataset** is selected.</span><span class="sxs-lookup"><span data-stu-id="603bc-300">In **Sink Dataset**, confirm that **AzureBlobDataset** is selected.</span></span> 

    ![Sink dataset selected](./media/tutorial-hybrid-copy-portal/sink-dataset-selected.png)

1. <span data-ttu-id="603bc-302">To validate the pipeline settings, select **Validate** on the toolbar for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="603bc-302">To validate the pipeline settings, select **Validate** on the toolbar for the pipeline.</span></span> <span data-ttu-id="603bc-303">To close the **Pipe Validation Report**, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="603bc-303">To close the **Pipe Validation Report**, select **Close**.</span></span> 

    ![Validate pipeline](./media/tutorial-hybrid-copy-portal/validate-pipeline.png)

1. <span data-ttu-id="603bc-305">To publish entities you created to Data Factory, select **Publish All**.</span><span class="sxs-lookup"><span data-stu-id="603bc-305">To publish entities you created to Data Factory, select **Publish All**.</span></span>

    ![Publish button](./media/tutorial-hybrid-copy-portal/publish-button.png)

1. <span data-ttu-id="603bc-307">Wait until you see the **Publishing succeeded** pop-up.</span><span class="sxs-lookup"><span data-stu-id="603bc-307">Wait until you see the **Publishing succeeded** pop-up.</span></span> <span data-ttu-id="603bc-308">To check the status of publishing, select the **Show Notifications** link on the left.</span><span class="sxs-lookup"><span data-stu-id="603bc-308">To check the status of publishing, select the **Show Notifications** link on the left.</span></span> <span data-ttu-id="603bc-309">To close the notification window, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="603bc-309">To close the notification window, select **Close**.</span></span> 

    ![Publishing succeeded](./media/tutorial-hybrid-copy-portal/publishing-succeeded.png)


## <a name="trigger-a-pipeline-run"></a><span data-ttu-id="603bc-311">Trigger a pipeline run</span><span class="sxs-lookup"><span data-stu-id="603bc-311">Trigger a pipeline run</span></span>
<span data-ttu-id="603bc-312">Select **Trigger** on the toolbar for the pipeline, and then select **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="603bc-312">Select **Trigger** on the toolbar for the pipeline, and then select **Trigger Now**.</span></span>

![Trigger pipeline run](./media/tutorial-hybrid-copy-portal/trigger-now.png)

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="603bc-314">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="603bc-314">Monitor the pipeline run</span></span>

1. <span data-ttu-id="603bc-315">Go to the **Monitor** tab. You see the pipeline that you manually triggered in the previous step.</span><span class="sxs-lookup"><span data-stu-id="603bc-315">Go to the **Monitor** tab. You see the pipeline that you manually triggered in the previous step.</span></span> 

    ![Monitor pipeline runs](./media/tutorial-hybrid-copy-portal/pipeline-runs.png)
1. <span data-ttu-id="603bc-317">To view activity runs associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="603bc-317">To view activity runs associated with the pipeline run, select the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="603bc-318">You see only activity runs because there is only one activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="603bc-318">You see only activity runs because there is only one activity in the pipeline.</span></span> <span data-ttu-id="603bc-319">To see details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="603bc-319">To see details about the copy operation, select the **Details** link (eyeglasses icon) in the **Actions** column.</span></span> <span data-ttu-id="603bc-320">To go back to the **Pipeline Runs** view, select **Pipelines** at the top.</span><span class="sxs-lookup"><span data-stu-id="603bc-320">To go back to the **Pipeline Runs** view, select **Pipelines** at the top.</span></span>

    ![Monitor activity runs](./media/tutorial-hybrid-copy-portal/activity-runs.png)

## <a name="verify-the-output"></a><span data-ttu-id="603bc-322">Verify the output</span><span class="sxs-lookup"><span data-stu-id="603bc-322">Verify the output</span></span>
<span data-ttu-id="603bc-323">The pipeline automatically creates the output folder named *fromonprem* in the `adftutorial` blob container.</span><span class="sxs-lookup"><span data-stu-id="603bc-323">The pipeline automatically creates the output folder named *fromonprem* in the `adftutorial` blob container.</span></span> <span data-ttu-id="603bc-324">Confirm that you see the *[pipeline().RunId].txt* file in the output folder.</span><span class="sxs-lookup"><span data-stu-id="603bc-324">Confirm that you see the *[pipeline().RunId].txt* file in the output folder.</span></span> 

![confirm output file name](./media/tutorial-hybrid-copy-portal/sink-output.png)


## <a name="next-steps"></a><span data-ttu-id="603bc-326">Next steps</span><span class="sxs-lookup"><span data-stu-id="603bc-326">Next steps</span></span>
<span data-ttu-id="603bc-327">The pipeline in this sample copies data from one location to another in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="603bc-327">The pipeline in this sample copies data from one location to another in Blob storage.</span></span> <span data-ttu-id="603bc-328">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="603bc-328">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="603bc-329">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="603bc-329">Create a data factory.</span></span>
> * <span data-ttu-id="603bc-330">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="603bc-330">Create a self-hosted integration runtime.</span></span>
> * <span data-ttu-id="603bc-331">Create SQL Server and Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="603bc-331">Create SQL Server and Storage linked services.</span></span> 
> * <span data-ttu-id="603bc-332">Create SQL Server and Blob storage datasets.</span><span class="sxs-lookup"><span data-stu-id="603bc-332">Create SQL Server and Blob storage datasets.</span></span>
> * <span data-ttu-id="603bc-333">Create a pipeline with a copy activity to move the data.</span><span class="sxs-lookup"><span data-stu-id="603bc-333">Create a pipeline with a copy activity to move the data.</span></span>
> * <span data-ttu-id="603bc-334">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="603bc-334">Start a pipeline run.</span></span>
> * <span data-ttu-id="603bc-335">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="603bc-335">Monitor the pipeline run.</span></span>

<span data-ttu-id="603bc-336">For a list of data stores that are supported by Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="603bc-336">For a list of data stores that are supported by Data Factory, see [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>

<span data-ttu-id="603bc-337">To learn how to copy data in bulk from a source to a destination, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="603bc-337">To learn how to copy data in bulk from a source to a destination, advance to the following tutorial:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="603bc-338">Copy data in bulk</span><span class="sxs-lookup"><span data-stu-id="603bc-338">Copy data in bulk</span></span>](tutorial-bulk-copy-portal.md)
