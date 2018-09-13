---
title: Copy data from SQL Server to Blob storage by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from an on-premises data store to the Azure cloud by using a self-hosted integration runtime in Azure Data Factory.
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
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: ea5e393ebe204041d96d18481a5c64d2877755f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966544"
---
# <a name="tutorial-copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage"></a><span data-ttu-id="b1b47-103">Tutorial: Copy data from an on-premises SQL Server database to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="b1b47-103">Tutorial: Copy data from an on-premises SQL Server database to Azure Blob storage</span></span>
<span data-ttu-id="b1b47-104">In this tutorial, you use Azure PowerShell to create a data-factory pipeline that copies data from an on-premises SQL Server database to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1b47-104">In this tutorial, you use Azure PowerShell to create a data-factory pipeline that copies data from an on-premises SQL Server database to Azure Blob storage.</span></span> <span data-ttu-id="b1b47-105">You create and use a self-hosted integration runtime, which moves data between on-premises and cloud data stores.</span><span class="sxs-lookup"><span data-stu-id="b1b47-105">You create and use a self-hosted integration runtime, which moves data between on-premises and cloud data stores.</span></span> 

> [!NOTE]
> <span data-ttu-id="b1b47-106">This article does not provide a detailed introduction to the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="b1b47-106">This article does not provide a detailed introduction to the Data Factory service.</span></span> <span data-ttu-id="b1b47-107">For more information, see [Introduction to Azure Data Factory](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1b47-107">For more information, see [Introduction to Azure Data Factory](introduction.md).</span></span> 

<span data-ttu-id="b1b47-108">In this tutorial, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b1b47-108">In this tutorial, you perform the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1b47-109">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="b1b47-109">Create a data factory.</span></span>
> * <span data-ttu-id="b1b47-110">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="b1b47-110">Create a self-hosted integration runtime.</span></span>
> * <span data-ttu-id="b1b47-111">Create SQL Server and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="b1b47-111">Create SQL Server and Azure Storage linked services.</span></span> 
> * <span data-ttu-id="b1b47-112">Create SQL Server and Azure Blob datasets.</span><span class="sxs-lookup"><span data-stu-id="b1b47-112">Create SQL Server and Azure Blob datasets.</span></span>
> * <span data-ttu-id="b1b47-113">Create a pipeline with a copy activity to move the data.</span><span class="sxs-lookup"><span data-stu-id="b1b47-113">Create a pipeline with a copy activity to move the data.</span></span>
> * <span data-ttu-id="b1b47-114">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="b1b47-114">Start a pipeline run.</span></span>
> * <span data-ttu-id="b1b47-115">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="b1b47-115">Monitor the pipeline run.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1b47-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1b47-116">Prerequisites</span></span>
### <a name="azure-subscription"></a><span data-ttu-id="b1b47-117">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b1b47-117">Azure subscription</span></span>
<span data-ttu-id="b1b47-118">Before you begin, if you don't already have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b1b47-118">Before you begin, if you don't already have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span></span>

### <a name="azure-roles"></a><span data-ttu-id="b1b47-119">Azure roles</span><span class="sxs-lookup"><span data-stu-id="b1b47-119">Azure roles</span></span>
<span data-ttu-id="b1b47-120">To create data factory instances, the user account you use to log in to Azure must be assigned a *Contributor* or *Owner* role or must be an *administrator* of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b1b47-120">To create data factory instances, the user account you use to log in to Azure must be assigned a *Contributor* or *Owner* role or must be an *administrator* of the Azure subscription.</span></span> 

<span data-ttu-id="b1b47-121">To view the permissions you have in the subscription, go to the Azure portal, select your username at the top-right corner, and then select **Permissions**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-121">To view the permissions you have in the subscription, go to the Azure portal, select your username at the top-right corner, and then select **Permissions**.</span></span> <span data-ttu-id="b1b47-122">If you have access to multiple subscriptions, select the appropriate subscription.</span><span class="sxs-lookup"><span data-stu-id="b1b47-122">If you have access to multiple subscriptions, select the appropriate subscription.</span></span> <span data-ttu-id="b1b47-123">For sample instructions on adding a user to a role, see the [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="b1b47-123">For sample instructions on adding a user to a role, see the [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md) article.</span></span>

### <a name="sql-server-2014-2016-and-2017"></a><span data-ttu-id="b1b47-124">SQL Server 2014, 2016, and 2017</span><span class="sxs-lookup"><span data-stu-id="b1b47-124">SQL Server 2014, 2016, and 2017</span></span>
<span data-ttu-id="b1b47-125">In this tutorial, you use an on-premises SQL Server database as a *source* data store.</span><span class="sxs-lookup"><span data-stu-id="b1b47-125">In this tutorial, you use an on-premises SQL Server database as a *source* data store.</span></span> <span data-ttu-id="b1b47-126">The pipeline in the data factory you create in this tutorial copies data from this on-premises SQL Server database (source) to Azure Blob storage (sink).</span><span class="sxs-lookup"><span data-stu-id="b1b47-126">The pipeline in the data factory you create in this tutorial copies data from this on-premises SQL Server database (source) to Azure Blob storage (sink).</span></span> <span data-ttu-id="b1b47-127">You then create a table named **emp** in your SQL Server database, and insert a couple of sample entries into the table.</span><span class="sxs-lookup"><span data-stu-id="b1b47-127">You then create a table named **emp** in your SQL Server database, and insert a couple of sample entries into the table.</span></span> 

1. <span data-ttu-id="b1b47-128">Start SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b1b47-128">Start SQL Server Management Studio.</span></span> <span data-ttu-id="b1b47-129">If it is not already installed on your machine, go to [Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b1b47-129">If it is not already installed on your machine, go to [Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> 

1. <span data-ttu-id="b1b47-130">Connect to your SQL Server instance by using your credentials.</span><span class="sxs-lookup"><span data-stu-id="b1b47-130">Connect to your SQL Server instance by using your credentials.</span></span> 

1. <span data-ttu-id="b1b47-131">Create a sample database.</span><span class="sxs-lookup"><span data-stu-id="b1b47-131">Create a sample database.</span></span> <span data-ttu-id="b1b47-132">In the tree view, right-click **Databases**, and then select **New Database**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-132">In the tree view, right-click **Databases**, and then select **New Database**.</span></span> 
 
1. <span data-ttu-id="b1b47-133">In the **New Database** window, enter a name for the database, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-133">In the **New Database** window, enter a name for the database, and then select **OK**.</span></span> 

1. <span data-ttu-id="b1b47-134">To create the **emp** table and insert some sample data into it, run the following query script against the database:</span><span class="sxs-lookup"><span data-stu-id="b1b47-134">To create the **emp** table and insert some sample data into it, run the following query script against the database:</span></span>

   ```
       INSERT INTO emp VALUES ('John', 'Doe')
       INSERT INTO emp VALUES ('Jane', 'Doe')
       GO
   ```

1. <span data-ttu-id="b1b47-135">In the tree view, right-click the database that you created, and then select **New Query**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-135">In the tree view, right-click the database that you created, and then select **New Query**.</span></span>

### <a name="azure-storage-account"></a><span data-ttu-id="b1b47-136">Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="b1b47-136">Azure Storage account</span></span>
<span data-ttu-id="b1b47-137">In this tutorial, you use a general-purpose Azure storage account (specifically, Azure Blob storage) as a destination/sink data store.</span><span class="sxs-lookup"><span data-stu-id="b1b47-137">In this tutorial, you use a general-purpose Azure storage account (specifically, Azure Blob storage) as a destination/sink data store.</span></span> <span data-ttu-id="b1b47-138">If you don't have a general-purpose Azure storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b1b47-138">If you don't have a general-purpose Azure storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span> <span data-ttu-id="b1b47-139">The pipeline in the data factory you that create in this tutorial copies data from the on-premises SQL Server database (source) to this Azure Blob storage (sink).</span><span class="sxs-lookup"><span data-stu-id="b1b47-139">The pipeline in the data factory you that create in this tutorial copies data from the on-premises SQL Server database (source) to this Azure Blob storage (sink).</span></span> 

#### <a name="get-storage-account-name-and-account-key"></a><span data-ttu-id="b1b47-140">Get storage account name and account key</span><span class="sxs-lookup"><span data-stu-id="b1b47-140">Get storage account name and account key</span></span>
<span data-ttu-id="b1b47-141">You use the name and key of your Azure storage account in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-141">You use the name and key of your Azure storage account in this tutorial.</span></span> <span data-ttu-id="b1b47-142">Get the name and key of your storage account by doing the following:</span><span class="sxs-lookup"><span data-stu-id="b1b47-142">Get the name and key of your storage account by doing the following:</span></span> 

1. <span data-ttu-id="b1b47-143">Sign in to the [Azure portal](https://portal.azure.com) with your Azure username and password.</span><span class="sxs-lookup"><span data-stu-id="b1b47-143">Sign in to the [Azure portal](https://portal.azure.com) with your Azure username and password.</span></span> 

1. <span data-ttu-id="b1b47-144">In the left pane, select **More services**, filter by using the **Storage** keyword, and then select **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-144">In the left pane, select **More services**, filter by using the **Storage** keyword, and then select **Storage accounts**.</span></span>

    ![Search for storage account](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

1. <span data-ttu-id="b1b47-146">In the list of storage accounts, filter for your storage account (if needed), and then select your storage account.</span><span class="sxs-lookup"><span data-stu-id="b1b47-146">In the list of storage accounts, filter for your storage account (if needed), and then select your storage account.</span></span> 

1. <span data-ttu-id="b1b47-147">In the **Storage account** window, select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-147">In the **Storage account** window, select **Access keys**.</span></span>

    ![Get storage account name and key](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

1. <span data-ttu-id="b1b47-149">In the **Storage account name** and **key1** boxes, copy the values, and then paste them into Notepad or another editor for later use in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-149">In the **Storage account name** and **key1** boxes, copy the values, and then paste them into Notepad or another editor for later use in the tutorial.</span></span> 

#### <a name="create-the-adftutorial-container"></a><span data-ttu-id="b1b47-150">Create the adftutorial container</span><span class="sxs-lookup"><span data-stu-id="b1b47-150">Create the adftutorial container</span></span> 
<span data-ttu-id="b1b47-151">In this section, you create a blob container named **adftutorial** in your Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1b47-151">In this section, you create a blob container named **adftutorial** in your Azure Blob storage.</span></span> 

1. <span data-ttu-id="b1b47-152">In the **Storage account** window, switch to **Overview**, and then select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-152">In the **Storage account** window, switch to **Overview**, and then select **Blobs**.</span></span> 

    ![Select Blobs option](media/tutorial-hybrid-copy-powershell/select-blobs.png)

1. <span data-ttu-id="b1b47-154">In the **Blob service** window, select **Container**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-154">In the **Blob service** window, select **Container**.</span></span> 

    ![Add container button](media/tutorial-hybrid-copy-powershell/add-container-button.png)

1. <span data-ttu-id="b1b47-156">In the **New container** window, in the **Name** box, enter **adftutorial**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-156">In the **New container** window, in the **Name** box, enter **adftutorial**, and then select **OK**.</span></span> 

    ![Enter container name](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

1. <span data-ttu-id="b1b47-158">In the list of containers, select **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-158">In the list of containers, select **adftutorial**.</span></span>  

    ![Select the container](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

1. <span data-ttu-id="b1b47-160">Keep the **container** window for **adftutorial** open.</span><span class="sxs-lookup"><span data-stu-id="b1b47-160">Keep the **container** window for **adftutorial** open.</span></span> <span data-ttu-id="b1b47-161">You use it verify the output at the end of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-161">You use it verify the output at the end of the tutorial.</span></span> <span data-ttu-id="b1b47-162">Data Factory automatically creates the output folder in this container, so you don't need to create one.</span><span class="sxs-lookup"><span data-stu-id="b1b47-162">Data Factory automatically creates the output folder in this container, so you don't need to create one.</span></span>

    ![Container window](media/tutorial-hybrid-copy-powershell/container-page.png)

### <a name="windows-powershell"></a><span data-ttu-id="b1b47-164">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1b47-164">Windows PowerShell</span></span>

#### <a name="install-azure-powershell"></a><span data-ttu-id="b1b47-165">Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1b47-165">Install Azure PowerShell</span></span>
<span data-ttu-id="b1b47-166">Install the latest version of Azure PowerShell if you don't already have it on your machine.</span><span class="sxs-lookup"><span data-stu-id="b1b47-166">Install the latest version of Azure PowerShell if you don't already have it on your machine.</span></span> 

1. <span data-ttu-id="b1b47-167">Go to [Azure SDK Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b1b47-167">Go to [Azure SDK Downloads](https://azure.microsoft.com/downloads/).</span></span> 

1. <span data-ttu-id="b1b47-168">Under **Command-line tools**, in the **PowerShell** section, select **Windows install**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-168">Under **Command-line tools**, in the **PowerShell** section, select **Windows install**.</span></span> 

1. <span data-ttu-id="b1b47-169">To install Azure PowerShell, run the MSI file.</span><span class="sxs-lookup"><span data-stu-id="b1b47-169">To install Azure PowerShell, run the MSI file.</span></span> 

<span data-ttu-id="b1b47-170">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b1b47-170">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span> 

#### <a name="log-in-to-powershell"></a><span data-ttu-id="b1b47-171">Log in to PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1b47-171">Log in to PowerShell</span></span>

1. <span data-ttu-id="b1b47-172">Start PowerShell on your machine, and keep it open through completion of this quickstart tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-172">Start PowerShell on your machine, and keep it open through completion of this quickstart tutorial.</span></span> <span data-ttu-id="b1b47-173">If you close and reopen it, you'll need to run these commands again.</span><span class="sxs-lookup"><span data-stu-id="b1b47-173">If you close and reopen it, you'll need to run these commands again.</span></span>

    ![Start PowerShell](media/tutorial-hybrid-copy-powershell/search-powershell.png)

1. <span data-ttu-id="b1b47-175">Run the following command, and then enter the Azure username and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="b1b47-175">Run the following command, and then enter the Azure username and password that you use to sign in to the Azure portal:</span></span>
       
    ```powershell
    Connect-AzureRmAccount
    ```        

1. <span data-ttu-id="b1b47-176">If you have multiple Azure subscriptions, run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="b1b47-176">If you have multiple Azure subscriptions, run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="b1b47-177">Replace **SubscriptionId** with the ID of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="b1b47-177">Replace **SubscriptionId** with the ID of your Azure subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```

## <a name="create-a-data-factory"></a><span data-ttu-id="b1b47-178">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="b1b47-178">Create a data factory</span></span>

1. <span data-ttu-id="b1b47-179">Define a variable for the resource group name that you'll use later in PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="b1b47-179">Define a variable for the resource group name that you'll use later in PowerShell commands.</span></span> <span data-ttu-id="b1b47-180">Copy the following command to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) (enclosed in double quotation marks; for example, `"adfrg"`), and then run the command.</span><span class="sxs-lookup"><span data-stu-id="b1b47-180">Copy the following command to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) (enclosed in double quotation marks; for example, `"adfrg"`), and then run the command.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ```

1. <span data-ttu-id="b1b47-181">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b1b47-181">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 

    <span data-ttu-id="b1b47-182">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="b1b47-182">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="b1b47-183">Assign a different value to the `$resourceGroupName` variable and run the command again.</span><span class="sxs-lookup"><span data-stu-id="b1b47-183">Assign a different value to the `$resourceGroupName` variable and run the command again.</span></span>

1. <span data-ttu-id="b1b47-184">Define a variable for the data factory name that you can use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="b1b47-184">Define a variable for the data factory name that you can use in PowerShell commands later.</span></span> <span data-ttu-id="b1b47-185">The name must start with a letter or a number, and it can contain only letters, numbers, and the dash (-) character.</span><span class="sxs-lookup"><span data-stu-id="b1b47-185">The name must start with a letter or a number, and it can contain only letters, numbers, and the dash (-) character.</span></span>

    > [!IMPORTANT]
    >  <span data-ttu-id="b1b47-186">Update the data factory name with a globally unique name.</span><span class="sxs-lookup"><span data-stu-id="b1b47-186">Update the data factory name with a globally unique name.</span></span> <span data-ttu-id="b1b47-187">An example is ADFTutorialFactorySP1127.</span><span class="sxs-lookup"><span data-stu-id="b1b47-187">An example is ADFTutorialFactorySP1127.</span></span> 

    ```powershell
    $dataFactoryName = "ADFTutorialFactory"
    ```

1. <span data-ttu-id="b1b47-188">Define a variable for the location of the data factory:</span><span class="sxs-lookup"><span data-stu-id="b1b47-188">Define a variable for the location of the data factory:</span></span> 

    ```powershell
    $location = "East US"
    ```  

1. <span data-ttu-id="b1b47-189">To create the data factory, run the following `Set-AzureRmDataFactoryV2` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b1b47-189">To create the data factory, run the following `Set-AzureRmDataFactoryV2` cmdlet:</span></span> 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

> [!NOTE]
> 
> * <span data-ttu-id="b1b47-190">The name of the data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="b1b47-190">The name of the data factory must be globally unique.</span></span> <span data-ttu-id="b1b47-191">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="b1b47-191">If you receive the following error, change the name and try again.</span></span>
>    ```
>    The specified data factory name 'ADFv2TutorialDataFactory' is already in use. Data factory names must be globally unique.
>    ```
> * <span data-ttu-id="b1b47-192">To create data-factory instances, the user account that you use to sign in to Azure must be assigned a *contributor* or *owner* role or must be an *administrator* of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b1b47-192">To create data-factory instances, the user account that you use to sign in to Azure must be assigned a *contributor* or *owner* role or must be an *administrator* of the Azure subscription.</span></span>
> * <span data-ttu-id="b1b47-193">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="b1b47-193">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="b1b47-194">The data stores (Azure Storage, Azure SQL Database, and so on) and computes (Azure HDInsight and so on) used by the data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="b1b47-194">The data stores (Azure Storage, Azure SQL Database, and so on) and computes (Azure HDInsight and so on) used by the data factory can be in other regions.</span></span>
> 
> 

## <a name="create-a-self-hosted-integration-runtime"></a><span data-ttu-id="b1b47-195">Create a self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="b1b47-195">Create a self-hosted integration runtime</span></span>

<span data-ttu-id="b1b47-196">In this section, you create a self-hosted integration runtime and associate it with an on-premises machine with the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="b1b47-196">In this section, you create a self-hosted integration runtime and associate it with an on-premises machine with the SQL Server database.</span></span> <span data-ttu-id="b1b47-197">The self-hosted integration runtime is the component that copies data from the SQL Server database on your machine to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1b47-197">The self-hosted integration runtime is the component that copies data from the SQL Server database on your machine to Azure Blob storage.</span></span> 

1. <span data-ttu-id="b1b47-198">Create a variable for the name of integration runtime.</span><span class="sxs-lookup"><span data-stu-id="b1b47-198">Create a variable for the name of integration runtime.</span></span> <span data-ttu-id="b1b47-199">Use a unique name, and note the name.</span><span class="sxs-lookup"><span data-stu-id="b1b47-199">Use a unique name, and note the name.</span></span> <span data-ttu-id="b1b47-200">You use it later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-200">You use it later in this tutorial.</span></span> 

    ```powershell
   $integrationRuntimeName = "ADFTutorialIR"
    ```

1. <span data-ttu-id="b1b47-201">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="b1b47-201">Create a self-hosted integration runtime.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Name $integrationRuntimeName -Type SelfHosted -Description "selfhosted IR description"
    ``` 
    <span data-ttu-id="b1b47-202">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-202">Here is the sample output:</span></span>

    ```json
    Id                : /subscriptions/<subscription ID>/resourceGroups/ADFTutorialResourceGroup/providers/Microsoft.DataFactory/factories/onpremdf0914/integrationruntimes/myonpremirsp0914
    Type              : SelfHosted
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Name              : myonpremirsp0914
    Description       : selfhosted IR description
    ```

1. <span data-ttu-id="b1b47-203">To retrieve the status of the created integration runtime, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b1b47-203">To retrieve the status of the created integration runtime, run the following command:</span></span>

    ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntime -name $integrationRuntimeName -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Status
    ```

    <span data-ttu-id="b1b47-204">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-204">Here is the sample output:</span></span>
    
    ```json
    Nodes                     : {}
    CreateTime                : 9/14/2017 10:01:21 AM
    InternalChannelEncryption :
    Version                   :
    Capabilities              : {}
    ScheduledUpdateDate       :
    UpdateDelayOffset         :
    LocalTimeZoneOffset       :
    AutoUpdate                :
    ServiceUrls               : {eu.frontend.clouddatahub.net, *.servicebus.windows.net}
    ResourceGroupName         : <ResourceGroup name>
    DataFactoryName           : <DataFactory name>
    Name                      : <Integration Runtime name>
    State                     : NeedRegistration
    ```

1. <span data-ttu-id="b1b47-205">To retrieve the *authentication keys* for registering the self-hosted integration runtime with the Data Factory service in the cloud, run the following command.</span><span class="sxs-lookup"><span data-stu-id="b1b47-205">To retrieve the *authentication keys* for registering the self-hosted integration runtime with the Data Factory service in the cloud, run the following command.</span></span> <span data-ttu-id="b1b47-206">Copy one of the keys (excluding the quotation marks) for registering the self-hosted integration runtime that you install on your machine in the next step.</span><span class="sxs-lookup"><span data-stu-id="b1b47-206">Copy one of the keys (excluding the quotation marks) for registering the self-hosted integration runtime that you install on your machine in the next step.</span></span> 

    ```powershell
    Get-AzureRmDataFactoryV2IntegrationRuntimeKey -Name $integrationRuntimeName -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName | ConvertTo-Json
    ```
    
    <span data-ttu-id="b1b47-207">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-207">Here is the sample output:</span></span>
    
    ```json
    {
        "AuthKey1":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx=",
        "AuthKey2":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy="
    }
    ```

## <a name="install-the-integration-runtime"></a><span data-ttu-id="b1b47-208">Install the integration runtime</span><span class="sxs-lookup"><span data-stu-id="b1b47-208">Install the integration runtime</span></span>
1. <span data-ttu-id="b1b47-209">Download [Azure Data Factory Integration Runtime](https://www.microsoft.com/download/details.aspx?id=39717) on a local Windows machine, and then run the installation.</span><span class="sxs-lookup"><span data-stu-id="b1b47-209">Download [Azure Data Factory Integration Runtime](https://www.microsoft.com/download/details.aspx?id=39717) on a local Windows machine, and then run the installation.</span></span> 

1. <span data-ttu-id="b1b47-210">In the **Welcome to Microsoft Integration Runtime Setup** wizard, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-210">In the **Welcome to Microsoft Integration Runtime Setup** wizard, select **Next**.</span></span>  

1. <span data-ttu-id="b1b47-211">In the **End-User License Agreement** window, accept the terms and license agreement, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-211">In the **End-User License Agreement** window, accept the terms and license agreement, and select **Next**.</span></span> 

1. <span data-ttu-id="b1b47-212">In the **Destination Folder** window, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-212">In the **Destination Folder** window, select **Next**.</span></span> 

1. <span data-ttu-id="b1b47-213">In the **Ready to install Microsoft Integration Runtime** window, select **Install**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-213">In the **Ready to install Microsoft Integration Runtime** window, select **Install**.</span></span> 

1. <span data-ttu-id="b1b47-214">If you see a warning message about the computer being configured to enter sleep or hibernate mode when not in use, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-214">If you see a warning message about the computer being configured to enter sleep or hibernate mode when not in use, select **OK**.</span></span> 

1. <span data-ttu-id="b1b47-215">If a **Power Options** window is displayed, close it, and switch to the setup window.</span><span class="sxs-lookup"><span data-stu-id="b1b47-215">If a **Power Options** window is displayed, close it, and switch to the setup window.</span></span> 

1. <span data-ttu-id="b1b47-216">In the **Completed the Microsoft Integration Runtime Setup** wizard, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-216">In the **Completed the Microsoft Integration Runtime Setup** wizard, select **Finish**.</span></span>

1. <span data-ttu-id="b1b47-217">In the **Register Integration Runtime (Self-hosted)** window, paste the key you saved in the previous section, and then select **Register**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-217">In the **Register Integration Runtime (Self-hosted)** window, paste the key you saved in the previous section, and then select **Register**.</span></span> 

    ![Register integration runtime](media/tutorial-hybrid-copy-powershell/register-integration-runtime.png)

    <span data-ttu-id="b1b47-219">When the self-hosted integration runtime is registered successfully, the following message is displayed:</span><span class="sxs-lookup"><span data-stu-id="b1b47-219">When the self-hosted integration runtime is registered successfully, the following message is displayed:</span></span> 

    ![Registered successfully](media/tutorial-hybrid-copy-powershell/registered-successfully.png)

1. <span data-ttu-id="b1b47-221">In the **New Integration Runtime (Self-hosted) Node** window, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-221">In the **New Integration Runtime (Self-hosted) Node** window, select **Next**.</span></span> 

    ![New Integration Runtime Node window](media/tutorial-hybrid-copy-powershell/new-integration-runtime-node-page.png)

1. <span data-ttu-id="b1b47-223">In the **Intranet Communication Channel** window, select **Skip**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-223">In the **Intranet Communication Channel** window, select **Skip**.</span></span>  
    <span data-ttu-id="b1b47-224">You can select a TLS/SSL certification for securing intra-node communication in a multi-node integration runtime environment.</span><span class="sxs-lookup"><span data-stu-id="b1b47-224">You can select a TLS/SSL certification for securing intra-node communication in a multi-node integration runtime environment.</span></span>

    ![Intranet communication channel window](media/tutorial-hybrid-copy-powershell/intranet-communication-channel-page.png)

1. <span data-ttu-id="b1b47-226">In the **Register Integration Runtime (Self-hosted)** window, select **Launch Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-226">In the **Register Integration Runtime (Self-hosted)** window, select **Launch Configuration Manager**.</span></span> 

1. <span data-ttu-id="b1b47-227">When the node is connected to the cloud service, the following message is displayed:</span><span class="sxs-lookup"><span data-stu-id="b1b47-227">When the node is connected to the cloud service, the following message is displayed:</span></span>

    ![Node is connected](media/tutorial-hybrid-copy-powershell/node-is-connected.png)

1. <span data-ttu-id="b1b47-229">Test the connectivity to your SQL Server database by doing the following:</span><span class="sxs-lookup"><span data-stu-id="b1b47-229">Test the connectivity to your SQL Server database by doing the following:</span></span>

    ![Diagnostics tab](media/tutorial-hybrid-copy-powershell/config-manager-diagnostics-tab.png)   

    <span data-ttu-id="b1b47-231">a.</span><span class="sxs-lookup"><span data-stu-id="b1b47-231">a.</span></span> <span data-ttu-id="b1b47-232">In the **Configuration Manager** window, switch to the **Diagnostics** tab.</span><span class="sxs-lookup"><span data-stu-id="b1b47-232">In the **Configuration Manager** window, switch to the **Diagnostics** tab.</span></span>

    <span data-ttu-id="b1b47-233">b.</span><span class="sxs-lookup"><span data-stu-id="b1b47-233">b.</span></span> <span data-ttu-id="b1b47-234">In the **Data source type** box, select **SqlServer**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-234">In the **Data source type** box, select **SqlServer**.</span></span>

    <span data-ttu-id="b1b47-235">c.</span><span class="sxs-lookup"><span data-stu-id="b1b47-235">c.</span></span> <span data-ttu-id="b1b47-236">Enter the server name.</span><span class="sxs-lookup"><span data-stu-id="b1b47-236">Enter the server name.</span></span>

    <span data-ttu-id="b1b47-237">d.</span><span class="sxs-lookup"><span data-stu-id="b1b47-237">d.</span></span> <span data-ttu-id="b1b47-238">Enter the database name.</span><span class="sxs-lookup"><span data-stu-id="b1b47-238">Enter the database name.</span></span> 

    <span data-ttu-id="b1b47-239">e.</span><span class="sxs-lookup"><span data-stu-id="b1b47-239">e.</span></span> <span data-ttu-id="b1b47-240">Select the authentication mode.</span><span class="sxs-lookup"><span data-stu-id="b1b47-240">Select the authentication mode.</span></span> 

    <span data-ttu-id="b1b47-241">f.</span><span class="sxs-lookup"><span data-stu-id="b1b47-241">f.</span></span> <span data-ttu-id="b1b47-242">Enter the username.</span><span class="sxs-lookup"><span data-stu-id="b1b47-242">Enter the username.</span></span> 

    <span data-ttu-id="b1b47-243">g.</span><span class="sxs-lookup"><span data-stu-id="b1b47-243">g.</span></span> <span data-ttu-id="b1b47-244">Enter the password that's associated with the username.</span><span class="sxs-lookup"><span data-stu-id="b1b47-244">Enter the password that's associated with the username.</span></span>

    <span data-ttu-id="b1b47-245">h.</span><span class="sxs-lookup"><span data-stu-id="b1b47-245">h.</span></span> <span data-ttu-id="b1b47-246">To confirm that integration runtime can connect to the SQL Server, select **Test**.</span><span class="sxs-lookup"><span data-stu-id="b1b47-246">To confirm that integration runtime can connect to the SQL Server, select **Test**.</span></span>  
    <span data-ttu-id="b1b47-247">If the connection is successful, a green checkmark icon is displayed.</span><span class="sxs-lookup"><span data-stu-id="b1b47-247">If the connection is successful, a green checkmark icon is displayed.</span></span> <span data-ttu-id="b1b47-248">Otherwise, you'll receive an error message associated with the failure.</span><span class="sxs-lookup"><span data-stu-id="b1b47-248">Otherwise, you'll receive an error message associated with the failure.</span></span> <span data-ttu-id="b1b47-249">Fix any issues, and ensure that the integration runtime can connect to your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="b1b47-249">Fix any issues, and ensure that the integration runtime can connect to your SQL Server instance.</span></span>

    <span data-ttu-id="b1b47-250">Note all the preceding values for later use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-250">Note all the preceding values for later use in this tutorial.</span></span>
    
## <a name="create-linked-services"></a><span data-ttu-id="b1b47-251">Create linked services</span><span class="sxs-lookup"><span data-stu-id="b1b47-251">Create linked services</span></span>
<span data-ttu-id="b1b47-252">To link your data stores and compute services to the data factory, create linked services in the data factory.</span><span class="sxs-lookup"><span data-stu-id="b1b47-252">To link your data stores and compute services to the data factory, create linked services in the data factory.</span></span> <span data-ttu-id="b1b47-253">In this tutorial, you link your Azure storage account and on-premises SQL Server instance to the data store.</span><span class="sxs-lookup"><span data-stu-id="b1b47-253">In this tutorial, you link your Azure storage account and on-premises SQL Server instance to the data store.</span></span> <span data-ttu-id="b1b47-254">The linked services have the connection information that the Data Factory service uses at runtime to connect to them.</span><span class="sxs-lookup"><span data-stu-id="b1b47-254">The linked services have the connection information that the Data Factory service uses at runtime to connect to them.</span></span> 

### <a name="create-an-azure-storage-linked-service-destinationsink"></a><span data-ttu-id="b1b47-255">Create an Azure Storage linked service (destination/sink)</span><span class="sxs-lookup"><span data-stu-id="b1b47-255">Create an Azure Storage linked service (destination/sink)</span></span>
<span data-ttu-id="b1b47-256">In this step, you link your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="b1b47-256">In this step, you link your Azure storage account to the data factory.</span></span>

1. <span data-ttu-id="b1b47-257">Create a JSON file named *AzureStorageLinkedService.json* in the *C:\ADFv2Tutorial* folder with the following code.</span><span class="sxs-lookup"><span data-stu-id="b1b47-257">Create a JSON file named *AzureStorageLinkedService.json* in the *C:\ADFv2Tutorial* folder with the following code.</span></span> <span data-ttu-id="b1b47-258">If the *ADFv2Tutorial* folder does not already exist, create it.</span><span class="sxs-lookup"><span data-stu-id="b1b47-258">If the *ADFv2Tutorial* folder does not already exist, create it.</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="b1b47-259">Before you save the file, replace \<accountName> and \<accountKey> with the name and key of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="b1b47-259">Before you save the file, replace \<accountName> and \<accountKey> with the name and key of your Azure storage account.</span></span> <span data-ttu-id="b1b47-260">You noted them in the [Prerequisites](#get-storage-account-name-and-account-key) section.</span><span class="sxs-lookup"><span data-stu-id="b1b47-260">You noted them in the [Prerequisites](#get-storage-account-name-and-account-key) section.</span></span>

   ```json
    {
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>;EndpointSuffix=core.windows.net"
                }
            }
        },
        "name": "AzureStorageLinkedService"
    }
   ```

1. <span data-ttu-id="b1b47-261">In PowerShell, switch to the *C:\ADFv2Tutorial* folder.</span><span class="sxs-lookup"><span data-stu-id="b1b47-261">In PowerShell, switch to the *C:\ADFv2Tutorial* folder.</span></span>

1. <span data-ttu-id="b1b47-262">To create the linked service, AzureStorageLinkedService, run the following `Set-AzureRmDataFactoryV2LinkedService` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b1b47-262">To create the linked service, AzureStorageLinkedService, run the following `Set-AzureRmDataFactoryV2LinkedService` cmdlet:</span></span> 

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
   ```

   <span data-ttu-id="b1b47-263">Here is a sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-263">Here is a sample output:</span></span>

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

    <span data-ttu-id="b1b47-264">If you receive a "file not found" error, confirm that the file exists by running the `dir` command.</span><span class="sxs-lookup"><span data-stu-id="b1b47-264">If you receive a "file not found" error, confirm that the file exists by running the `dir` command.</span></span> <span data-ttu-id="b1b47-265">If the file name has a *.txt* extension (for example, AzureStorageLinkedService.json.txt), remove it, and then run the PowerShell command again.</span><span class="sxs-lookup"><span data-stu-id="b1b47-265">If the file name has a *.txt* extension (for example, AzureStorageLinkedService.json.txt), remove it, and then run the PowerShell command again.</span></span> 

### <a name="create-and-encrypt-a-sql-server-linked-service-source"></a><span data-ttu-id="b1b47-266">Create and encrypt a SQL Server linked service (source)</span><span class="sxs-lookup"><span data-stu-id="b1b47-266">Create and encrypt a SQL Server linked service (source)</span></span>
<span data-ttu-id="b1b47-267">In this step, you link your on-premises SQL Server instance to the data factory.</span><span class="sxs-lookup"><span data-stu-id="b1b47-267">In this step, you link your on-premises SQL Server instance to the data factory.</span></span>

1. <span data-ttu-id="b1b47-268">Create a JSON file named *SqlServerLinkedService.json* in the *C:\ADFv2Tutorial* folder by using the following code:</span><span class="sxs-lookup"><span data-stu-id="b1b47-268">Create a JSON file named *SqlServerLinkedService.json* in the *C:\ADFv2Tutorial* folder by using the following code:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b1b47-269">Select the section that's based on the authentication that you use to connect to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b1b47-269">Select the section that's based on the authentication that you use to connect to SQL Server.</span></span>

    <span data-ttu-id="b1b47-270">**Using SQL authentication (sa):**</span><span class="sxs-lookup"><span data-stu-id="b1b47-270">**Using SQL authentication (sa):**</span></span>

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    

    <span data-ttu-id="b1b47-271">**Using Windows authentication:**</span><span class="sxs-lookup"><span data-stu-id="b1b47-271">**Using Windows authentication:**</span></span>

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="b1b47-272">Select the section that's based on the authentication you use to connect to your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="b1b47-272">Select the section that's based on the authentication you use to connect to your SQL Server instance.</span></span>
    > - <span data-ttu-id="b1b47-273">Replace  **\<integration runtime name>** with the name of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="b1b47-273">Replace  **\<integration runtime name>** with the name of your integration runtime.</span></span>
    > - <span data-ttu-id="b1b47-274">Before you save the file, replace **\<servername>**, **\<databasename>**, **\<username>**, and **\<password>** with the values of your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="b1b47-274">Before you save the file, replace **\<servername>**, **\<databasename>**, **\<username>**, and **\<password>** with the values of your SQL Server instance.</span></span>
    > - <span data-ttu-id="b1b47-275">If you need to use a backslash (\\) in your user account or server name, precede it with the escape character (\\).</span><span class="sxs-lookup"><span data-stu-id="b1b47-275">If you need to use a backslash (\\) in your user account or server name, precede it with the escape character (\\).</span></span> <span data-ttu-id="b1b47-276">For example, use *mydomain\\\\myuser*.</span><span class="sxs-lookup"><span data-stu-id="b1b47-276">For example, use *mydomain\\\\myuser*.</span></span> 

1. <span data-ttu-id="b1b47-277">To encrypt the sensitive data (username, password, and so on), run the `New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1b47-277">To encrypt the sensitive data (username, password, and so on), run the `New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential` cmdlet.</span></span>  
    <span data-ttu-id="b1b47-278">This encryption ensures that the credentials are encrypted using Data Protection Application Programming Interface (DPAPI).</span><span class="sxs-lookup"><span data-stu-id="b1b47-278">This encryption ensures that the credentials are encrypted using Data Protection Application Programming Interface (DPAPI).</span></span> <span data-ttu-id="b1b47-279">The encrypted credentials are stored locally on the self-hosted integration runtime node (local machine).</span><span class="sxs-lookup"><span data-stu-id="b1b47-279">The encrypted credentials are stored locally on the self-hosted integration runtime node (local machine).</span></span> <span data-ttu-id="b1b47-280">The output payload can be redirected to another JSON file (in this case, *encryptedLinkedService.json*) that contains encrypted credentials.</span><span class="sxs-lookup"><span data-stu-id="b1b47-280">The output payload can be redirected to another JSON file (in this case, *encryptedLinkedService.json*) that contains encrypted credentials.</span></span>
    
   ```powershell
   New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -IntegrationRuntimeName $integrationRuntimeName -File ".\SQLServerLinkedService.json" > encryptedSQLServerLinkedService.json
   ```

1. <span data-ttu-id="b1b47-281">Run the following command, which creates EncryptedSqlServerLinkedService:</span><span class="sxs-lookup"><span data-stu-id="b1b47-281">Run the following command, which creates EncryptedSqlServerLinkedService:</span></span>

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "EncryptedSqlServerLinkedService" -File ".\encryptedSqlServerLinkedService.json"
   ```


## <a name="create-datasets"></a><span data-ttu-id="b1b47-282">Create datasets</span><span class="sxs-lookup"><span data-stu-id="b1b47-282">Create datasets</span></span>
<span data-ttu-id="b1b47-283">In this step, you create input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="b1b47-283">In this step, you create input and output datasets.</span></span> <span data-ttu-id="b1b47-284">They represent input and output data for the copy operation, which copies data from the on-premises SQL Server database to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1b47-284">They represent input and output data for the copy operation, which copies data from the on-premises SQL Server database to Azure Blob storage.</span></span>

### <a name="create-a-dataset-for-the-source-sql-server-database"></a><span data-ttu-id="b1b47-285">Create a dataset for the source SQL Server database</span><span class="sxs-lookup"><span data-stu-id="b1b47-285">Create a dataset for the source SQL Server database</span></span>
<span data-ttu-id="b1b47-286">In this step, you define a dataset that represents data in the SQL Server database instance.</span><span class="sxs-lookup"><span data-stu-id="b1b47-286">In this step, you define a dataset that represents data in the SQL Server database instance.</span></span> <span data-ttu-id="b1b47-287">The dataset is of type SqlServerTable.</span><span class="sxs-lookup"><span data-stu-id="b1b47-287">The dataset is of type SqlServerTable.</span></span> <span data-ttu-id="b1b47-288">It refers to the SQL Server linked service that you created in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="b1b47-288">It refers to the SQL Server linked service that you created in the preceding step.</span></span> <span data-ttu-id="b1b47-289">The linked service has the connection information that the Data Factory service uses to connect to your SQL Server instance at runtime.</span><span class="sxs-lookup"><span data-stu-id="b1b47-289">The linked service has the connection information that the Data Factory service uses to connect to your SQL Server instance at runtime.</span></span> <span data-ttu-id="b1b47-290">This dataset specifies the SQL table in the database that contains the data.</span><span class="sxs-lookup"><span data-stu-id="b1b47-290">This dataset specifies the SQL table in the database that contains the data.</span></span> <span data-ttu-id="b1b47-291">In this tutorial, the **emp** table contains the source data.</span><span class="sxs-lookup"><span data-stu-id="b1b47-291">In this tutorial, the **emp** table contains the source data.</span></span> 

1. <span data-ttu-id="b1b47-292">Create a JSON file named *SqlServerDataset.json* in the *C:\ADFv2Tutorial* folder, with the following code:</span><span class="sxs-lookup"><span data-stu-id="b1b47-292">Create a JSON file named *SqlServerDataset.json* in the *C:\ADFv2Tutorial* folder, with the following code:</span></span>  

    ```json
    {
       "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dbo.emp"
            },
            "structure": [
                 {
                    "name": "ID",
                    "type": "String"
                },
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "linkedServiceName": {
                "referenceName": "EncryptedSqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "SqlServerDataset"
    }
    ```

1. <span data-ttu-id="b1b47-293">To create the dataset SqlServerDataset, run the `Set-AzureRmDataFactoryV2Dataset` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1b47-293">To create the dataset SqlServerDataset, run the `Set-AzureRmDataFactoryV2Dataset` cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerDataset" -File ".\SqlServerDataset.json"
    ```

    <span data-ttu-id="b1b47-294">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-294">Here is the sample output:</span></span>

    ```json
    DatasetName       : SqlServerDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         : {"name": "ID" "type": "String", "name": "FirstName" "type": "String", "name": "LastName" "type": "String"}
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-dataset-for-azure-blob-storage-sink"></a><span data-ttu-id="b1b47-295">Create a dataset for Azure Blob storage (sink)</span><span class="sxs-lookup"><span data-stu-id="b1b47-295">Create a dataset for Azure Blob storage (sink)</span></span>
<span data-ttu-id="b1b47-296">In this step, you define a dataset that represents data that will be copied to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1b47-296">In this step, you define a dataset that represents data that will be copied to Azure Blob storage.</span></span> <span data-ttu-id="b1b47-297">The dataset is of the type AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="b1b47-297">The dataset is of the type AzureBlob.</span></span> <span data-ttu-id="b1b47-298">It refers to the Azure Storage linked service that you created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1b47-298">It refers to the Azure Storage linked service that you created earlier in this tutorial.</span></span> 

<span data-ttu-id="b1b47-299">The linked service has the connection information that the data factory uses at runtime to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="b1b47-299">The linked service has the connection information that the data factory uses at runtime to connect to your Azure storage account.</span></span> <span data-ttu-id="b1b47-300">This dataset specifies the folder in the Azure storage to which the data is copied from the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="b1b47-300">This dataset specifies the folder in the Azure storage to which the data is copied from the SQL Server database.</span></span> <span data-ttu-id="b1b47-301">In this tutorial, the folder is *adftutorial/fromonprem*, where `adftutorial` is the blob container and `fromonprem` is the folder.</span><span class="sxs-lookup"><span data-stu-id="b1b47-301">In this tutorial, the folder is *adftutorial/fromonprem*, where `adftutorial` is the blob container and `fromonprem` is the folder.</span></span> 

1. <span data-ttu-id="b1b47-302">Create a JSON file named *AzureBlobDataset.json* in the *C:\ADFv2Tutorial* folder, with the following code:</span><span class="sxs-lookup"><span data-stu-id="b1b47-302">Create a JSON file named *AzureBlobDataset.json* in the *C:\ADFv2Tutorial* folder, with the following code:</span></span>

    ```json
    {
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/fromonprem",
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "AzureBlobDataset"
    }
    ```

1. <span data-ttu-id="b1b47-303">To create the dataset AzureBlobDataset, run the `Set-AzureRmDataFactoryV2Dataset` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1b47-303">To create the dataset AzureBlobDataset, run the `Set-AzureRmDataFactoryV2Dataset` cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureBlobDataset" -File ".\AzureBlobDataset.json"
    ```

    <span data-ttu-id="b1b47-304">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-304">Here is the sample output:</span></span>

    ```json
    DatasetName       : AzureBlobDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="b1b47-305">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="b1b47-305">Create a pipeline</span></span>
<span data-ttu-id="b1b47-306">In this tutorial, you create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="b1b47-306">In this tutorial, you create a pipeline with a copy activity.</span></span> <span data-ttu-id="b1b47-307">The copy activity uses SqlServerDataset as the input dataset and AzureBlobDataset as the output dataset.</span><span class="sxs-lookup"><span data-stu-id="b1b47-307">The copy activity uses SqlServerDataset as the input dataset and AzureBlobDataset as the output dataset.</span></span> <span data-ttu-id="b1b47-308">The source type is set to *SqlSource* and the sink type is set to *BlobSink*.</span><span class="sxs-lookup"><span data-stu-id="b1b47-308">The source type is set to *SqlSource* and the sink type is set to *BlobSink*.</span></span>

1. <span data-ttu-id="b1b47-309">Create a JSON file named *SqlServerToBlobPipeline.json* in the *C:\ADFv2Tutorial* folder, with the following code:</span><span class="sxs-lookup"><span data-stu-id="b1b47-309">Create a JSON file named *SqlServerToBlobPipeline.json* in the *C:\ADFv2Tutorial* folder, with the following code:</span></span>

    ```json
    {
       "name": "SQLServerToBlobPipeline",
        "properties": {
            "activities": [       
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource"
                        },
                        "sink": {
                            "type":"BlobSink"
                        }
                    },
                    "name": "CopySqlServerToAzureBlobActivity",
                    "inputs": [
                        {
                            "referenceName": "SqlServerDataset",
                            "type": "DatasetReference"
                        }
                    ],
                    "outputs": [
                        {
                            "referenceName": "AzureBlobDataset",
                            "type": "DatasetReference"
                        }
                    ]
                }
            ]
        }
    }
    ```

1. <span data-ttu-id="b1b47-310">To create the pipeline SQLServerToBlobPipeline, run the `Set-AzureRmDataFactoryV2Pipeline` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1b47-310">To create the pipeline SQLServerToBlobPipeline, run the `Set-AzureRmDataFactoryV2Pipeline` cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SQLServerToBlobPipeline" -File ".\SQLServerToBlobPipeline.json"
    ```

    <span data-ttu-id="b1b47-311">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="b1b47-311">Here is the sample output:</span></span>

    ```json
    PipelineName      : SQLServerToBlobPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Activities        : {CopySqlServerToAzureBlobActivity}
    Parameters        :  
    ```

## <a name="create-a-pipeline-run"></a><span data-ttu-id="b1b47-312">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="b1b47-312">Create a pipeline run</span></span>
<span data-ttu-id="b1b47-313">Start a pipeline run for the SQLServerToBlobPipeline pipeline, and capture the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="b1b47-313">Start a pipeline run for the SQLServerToBlobPipeline pipeline, and capture the pipeline run ID for future monitoring.</span></span>

```powershell
$runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'SQLServerToBlobPipeline'
```

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="b1b47-314">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="b1b47-314">Monitor the pipeline run</span></span>

1. <span data-ttu-id="b1b47-315">To continuously check the run status of pipeline SQLServerToBlobPipeline, run the following script in PowerShell, and print the final result:</span><span class="sxs-lookup"><span data-stu-id="b1b47-315">To continuously check the run status of pipeline SQLServerToBlobPipeline, run the following script in PowerShell, and print the final result:</span></span>

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
            Start-Sleep -Seconds 30
        }
        else {
            Write-Host "Pipeline 'SQLServerToBlobPipeline' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
    }
    ```

    <span data-ttu-id="b1b47-316">Here is the output of the sample run:</span><span class="sxs-lookup"><span data-stu-id="b1b47-316">Here is the output of the sample run:</span></span>

    ```jdon
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : copy
    PipelineRunId     : 4ec8980c-62f6-466f-92fa-e69b10f33640
    PipelineName      : SQLServerToBlobPipeline
    Input             :  
    Output            :  
    LinkedServiceName :
    ActivityRunStart  : 9/13/2017 1:35:22 PM
    ActivityRunEnd    : 9/13/2017 1:35:42 PM
    DurationInMs      : 20824
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

1. <span data-ttu-id="b1b47-317">You can get the run ID of pipeline SQLServerToBlobPipeline and check the detailed activity run result by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b1b47-317">You can get the run ID of pipeline SQLServerToBlobPipeline and check the detailed activity run result by running the following command:</span></span> 

    ```powershell
    Write-Host "Pipeline 'SQLServerToBlobPipeline' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "CopySqlServerToAzureBlobActivity"}).Output.ToString()
    ```

    <span data-ttu-id="b1b47-318">Here is the output of the sample run:</span><span class="sxs-lookup"><span data-stu-id="b1b47-318">Here is the output of the sample run:</span></span>

    ```json
    {
      "dataRead": 36,
      "dataWritten": 24,
      "rowsCopied": 2,
      "copyDuration": 3,
      "throughput": 0.01171875,
      "errors": [],
      "effectiveIntegrationRuntime": "MyIntegrationRuntime",
      "billedDuration": 3
    }
    ```

## <a name="verify-the-output"></a><span data-ttu-id="b1b47-319">Verify the output</span><span class="sxs-lookup"><span data-stu-id="b1b47-319">Verify the output</span></span>
<span data-ttu-id="b1b47-320">The pipeline automatically creates the output folder named *fromonprem* in the `adftutorial` blob container.</span><span class="sxs-lookup"><span data-stu-id="b1b47-320">The pipeline automatically creates the output folder named *fromonprem* in the `adftutorial` blob container.</span></span> <span data-ttu-id="b1b47-321">Confirm that you see the *dbo.emp.txt* file in the output folder.</span><span class="sxs-lookup"><span data-stu-id="b1b47-321">Confirm that you see the *dbo.emp.txt* file in the output folder.</span></span> 

1. <span data-ttu-id="b1b47-322">In the Azure portal, in the **adftutorial** container window, select **Refresh** to see the output folder.</span><span class="sxs-lookup"><span data-stu-id="b1b47-322">In the Azure portal, in the **adftutorial** container window, select **Refresh** to see the output folder.</span></span>

    ![Output folder created](media/tutorial-hybrid-copy-powershell/fromonprem-folder.png)
1. <span data-ttu-id="b1b47-324">Select `fromonprem` in the list of folders.</span><span class="sxs-lookup"><span data-stu-id="b1b47-324">Select `fromonprem` in the list of folders.</span></span> 
1. <span data-ttu-id="b1b47-325">Confirm that you see a file named `dbo.emp.txt`.</span><span class="sxs-lookup"><span data-stu-id="b1b47-325">Confirm that you see a file named `dbo.emp.txt`.</span></span>

    ![Output file](media/tutorial-hybrid-copy-powershell/fromonprem-file.png)


## <a name="next-steps"></a><span data-ttu-id="b1b47-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1b47-327">Next steps</span></span>
<span data-ttu-id="b1b47-328">The pipeline in this sample copies data from one location to another in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b1b47-328">The pipeline in this sample copies data from one location to another in Azure Blob storage.</span></span> <span data-ttu-id="b1b47-329">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="b1b47-329">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1b47-330">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="b1b47-330">Create a data factory.</span></span>
> * <span data-ttu-id="b1b47-331">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="b1b47-331">Create a self-hosted integration runtime.</span></span>
> * <span data-ttu-id="b1b47-332">Create SQL Server and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="b1b47-332">Create SQL Server and Azure Storage linked services.</span></span> 
> * <span data-ttu-id="b1b47-333">Create SQL Server and Azure Blob datasets.</span><span class="sxs-lookup"><span data-stu-id="b1b47-333">Create SQL Server and Azure Blob datasets.</span></span>
> * <span data-ttu-id="b1b47-334">Create a pipeline with a copy activity to move the data.</span><span class="sxs-lookup"><span data-stu-id="b1b47-334">Create a pipeline with a copy activity to move the data.</span></span>
> * <span data-ttu-id="b1b47-335">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="b1b47-335">Start a pipeline run.</span></span>
> * <span data-ttu-id="b1b47-336">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="b1b47-336">Monitor the pipeline run.</span></span>

<span data-ttu-id="b1b47-337">For a list of data stores that are supported by Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b1b47-337">For a list of data stores that are supported by Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>

<span data-ttu-id="b1b47-338">To learn about copying data in bulk from a source to a destination, advance to the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="b1b47-338">To learn about copying data in bulk from a source to a destination, advance to the following tutorial:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b1b47-339">Copy data in bulk</span><span class="sxs-lookup"><span data-stu-id="b1b47-339">Copy data in bulk</span></span>](tutorial-bulk-copy.md)
