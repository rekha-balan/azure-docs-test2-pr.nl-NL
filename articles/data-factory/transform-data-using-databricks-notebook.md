---
title: Run a Databricks Notebook with the Databricks Notebook activity in Azure Data Factory
description: Learn how you can use the Databricks Notebook Activity in an Azure data factory to run a Databricks notebook against the databricks jobs cluster.
services: data-factory
documentationcenter: ''
author: nabhishek
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/12/2018
ms.author: abnarain
ms.reviewer: douglasl
ms.openlocfilehash: 7fb94fa9a70faa238c54e7f5e7992ef8404d8de3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869070"
---
# <a name="run-a-databricks-notebook-with-the-databricks-notebook-activity-in-azure-data-factory"></a><span data-ttu-id="bc0eb-103">Run a Databricks notebook with the Databricks Notebook Activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bc0eb-103">Run a Databricks notebook with the Databricks Notebook Activity in Azure Data Factory</span></span>

<span data-ttu-id="bc0eb-104">In this tutorial, you use the Azure portal to create an Azure Data Factory pipeline that executes a Databricks notebook against the Databricks jobs cluster.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-104">In this tutorial, you use the Azure portal to create an Azure Data Factory pipeline that executes a Databricks notebook against the Databricks jobs cluster.</span></span> <span data-ttu-id="bc0eb-105">It also passes Azure Data Factory parameters to the Databricks notebook during execution.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-105">It also passes Azure Data Factory parameters to the Databricks notebook during execution.</span></span>

<span data-ttu-id="bc0eb-106">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-106">You perform the following steps in this tutorial:</span></span>

  - <span data-ttu-id="bc0eb-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-107">Create a data factory.</span></span>

  - <span data-ttu-id="bc0eb-108">Create a pipeline that uses Databricks Notebook Activity.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-108">Create a pipeline that uses Databricks Notebook Activity.</span></span>

  - <span data-ttu-id="bc0eb-109">Trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-109">Trigger a pipeline run.</span></span>

  - <span data-ttu-id="bc0eb-110">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-110">Monitor the pipeline run.</span></span>

<span data-ttu-id="bc0eb-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

<span data-ttu-id="bc0eb-112">For an eleven-minute introduction and demonstration of this feature, watch the following video:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-112">For an eleven-minute introduction and demonstration of this feature, watch the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/ingest-prepare-and-transform-using-azure-databricks-and-data-factory/player]

## <a name="prerequisites"></a><span data-ttu-id="bc0eb-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc0eb-113">Prerequisites</span></span>

  - <span data-ttu-id="bc0eb-114">**Azure Databricks workspace**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-114">**Azure Databricks workspace**.</span></span> <span data-ttu-id="bc0eb-115">[Create a Databricks workspace](https://docs.microsoft.com/azure/azure-databricks/quickstart-create-databricks-workspace-portal) or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-115">[Create a Databricks workspace](https://docs.microsoft.com/azure/azure-databricks/quickstart-create-databricks-workspace-portal) or use an existing one.</span></span> <span data-ttu-id="bc0eb-116">You create a Python notebook in your Azure Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-116">You create a Python notebook in your Azure Databricks workspace.</span></span> <span data-ttu-id="bc0eb-117">Then you execute the notebook and pass parameters to it using Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-117">Then you execute the notebook and pass parameters to it using Azure Data Factory.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="bc0eb-118">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="bc0eb-118">Create a data factory</span></span>

1.  <span data-ttu-id="bc0eb-119">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-119">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="bc0eb-120">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-120">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>

1.  <span data-ttu-id="bc0eb-121">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-121">Select **New** on the left menu, select **Data + Analytics**, and then select **Data Factory**.</span></span>

    ![Create a new data factory](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image1.png)

1.  <span data-ttu-id="bc0eb-123">In the **New data factory** pane, enter **ADFTutorialDataFactory** under **Name**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-123">In the **New data factory** pane, enter **ADFTutorialDataFactory** under **Name**.</span></span>

    <span data-ttu-id="bc0eb-124">The name of the Azure data factory must be *globally unique*.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-124">The name of the Azure data factory must be *globally unique*.</span></span> <span data-ttu-id="bc0eb-125">If you see the following error, change the name of the data factory.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-125">If you see the following error, change the name of the data factory.</span></span> <span data-ttu-id="bc0eb-126">(For example, use **\<yourname\>ADFTutorialDataFactory**).</span><span class="sxs-lookup"><span data-stu-id="bc0eb-126">(For example, use **\<yourname\>ADFTutorialDataFactory**).</span></span> <span data-ttu-id="bc0eb-127">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](https://docs.microsoft.com/azure/data-factory/naming-rules) article.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-127">For naming rules for Data Factory artifacts, see the [Data Factory - naming rules](https://docs.microsoft.com/azure/data-factory/naming-rules) article.</span></span>

    ![Provide a name for the new data factory](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image2.png)

1.  <span data-ttu-id="bc0eb-129">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-129">For **Subscription**, select your Azure subscription in which you want to create the data factory.</span></span>

1.  <span data-ttu-id="bc0eb-130">For **Resource Group**, take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-130">For **Resource Group**, take one of the following steps:</span></span>
    
    - <span data-ttu-id="bc0eb-131">Select **Use existing** and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-131">Select **Use existing** and select an existing resource group from the drop-down list.</span></span>
    
    - <span data-ttu-id="bc0eb-132">Select **Create new** and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-132">Select **Create new** and enter the name of a resource group.</span></span>

    <span data-ttu-id="bc0eb-133">Some of the steps in this quickstart assume that you use the name **ADFTutorialResourceGroup** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-133">Some of the steps in this quickstart assume that you use the name **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="bc0eb-134">To learn about resource groups, see [Using resource groups to manage your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="bc0eb-134">To learn about resource groups, see [Using resource groups to manage your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

1.  <span data-ttu-id="bc0eb-135">For **Version**, select **V2**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-135">For **Version**, select **V2**.</span></span>

1.  <span data-ttu-id="bc0eb-136">For **Location**, select the location for the data factory.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-136">For **Location**, select the location for the data factory.</span></span>

    <span data-ttu-id="bc0eb-137">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="bc0eb-137">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="bc0eb-138">The data stores (like Azure Storage and Azure SQL Database) and computes (like HDInsight) that Data Factory uses can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-138">The data stores (like Azure Storage and Azure SQL Database) and computes (like HDInsight) that Data Factory uses can be in other regions.</span></span>

1.  <span data-ttu-id="bc0eb-139">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-139">Select **Pin to dashboard**.</span></span>

1.  <span data-ttu-id="bc0eb-140">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-140">Select **Create**.</span></span>

1.  <span data-ttu-id="bc0eb-141">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-141">On the dashboard, you see the following tile with the status **Deploying Data Factory**:</span></span>

    ![](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image3.png)

1.  <span data-ttu-id="bc0eb-142">After the creation is complete, you see the **Data factory** page.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-142">After the creation is complete, you see the **Data factory** page.</span></span> <span data-ttu-id="bc0eb-143">Select the **Author & Monitor** tile to start the Data Factory UI application on a separate tab.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-143">Select the **Author & Monitor** tile to start the Data Factory UI application on a separate tab.</span></span>

    ![Launch the data factory UI application](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image4.png)

## <a name="create-linked-services"></a><span data-ttu-id="bc0eb-145">Create linked services</span><span class="sxs-lookup"><span data-stu-id="bc0eb-145">Create linked services</span></span>

<span data-ttu-id="bc0eb-146">In this section, you author a Databricks linked service.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-146">In this section, you author a Databricks linked service.</span></span> <span data-ttu-id="bc0eb-147">This linked service contains the connection information to the Databricks cluster:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-147">This linked service contains the connection information to the Databricks cluster:</span></span>

### <a name="create-an-azure-databricks-linked-service"></a><span data-ttu-id="bc0eb-148">Create an Azure Databricks linked service</span><span class="sxs-lookup"><span data-stu-id="bc0eb-148">Create an Azure Databricks linked service</span></span>

1.  <span data-ttu-id="bc0eb-149">On the **Let's get started** page, switch to the **Edit** tab in the left panel.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-149">On the **Let's get started** page, switch to the **Edit** tab in the left panel.</span></span>

    ![Edit the new linked service](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image5.png)

1.  <span data-ttu-id="bc0eb-151">Select **Connections** at the bottom of the window, and then select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-151">Select **Connections** at the bottom of the window, and then select **+ New**.</span></span>
    
    ![Create a new connection](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image6.png)

1.  <span data-ttu-id="bc0eb-153">In the **New Linked Service** window, select **Data Store** \> **Azure Databricks**, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-153">In the **New Linked Service** window, select **Data Store** \> **Azure Databricks**, and then select **Continue**.</span></span>
    
    ![Specify a Databricks linked service](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image7.png)

1.  <span data-ttu-id="bc0eb-155">In the **New Linked Service** window, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-155">In the **New Linked Service** window, complete the following steps:</span></span>
    
    1.  <span data-ttu-id="bc0eb-156">For **Name,** enter ***AzureDatabricks\_LinkedService***</span><span class="sxs-lookup"><span data-stu-id="bc0eb-156">For **Name,** enter ***AzureDatabricks\_LinkedService***</span></span>
    
    1.  <span data-ttu-id="bc0eb-157">For **Cluster**, select a **New Cluster**</span><span class="sxs-lookup"><span data-stu-id="bc0eb-157">For **Cluster**, select a **New Cluster**</span></span>
    
    1.  <span data-ttu-id="bc0eb-158">For **Domain/ Region**, select the region where your Azure Databricks workspace is located.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-158">For **Domain/ Region**, select the region where your Azure Databricks workspace is located.</span></span>
    
    1.  <span data-ttu-id="bc0eb-159">For **Cluster node type**, select **Standard\_D3\_v2** for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-159">For **Cluster node type**, select **Standard\_D3\_v2** for this tutorial.</span></span>
    
    1.  <span data-ttu-id="bc0eb-160">For **Access Token**, generate it from Azure Databricks workplace.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-160">For **Access Token**, generate it from Azure Databricks workplace.</span></span> <span data-ttu-id="bc0eb-161">You can find the steps [here](https://docs.databricks.com/api/latest/authentication.html#generate-token).</span><span class="sxs-lookup"><span data-stu-id="bc0eb-161">You can find the steps [here](https://docs.databricks.com/api/latest/authentication.html#generate-token).</span></span>
    
    1.  <span data-ttu-id="bc0eb-162">For **Cluster version,** select **4.0 Beta** (latest version)</span><span class="sxs-lookup"><span data-stu-id="bc0eb-162">For **Cluster version,** select **4.0 Beta** (latest version)</span></span>
    
    1.  <span data-ttu-id="bc0eb-163">For **Number of worker nodes,** enter **2**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-163">For **Number of worker nodes,** enter **2**.</span></span>
    
    1.  <span data-ttu-id="bc0eb-164">Select **Finish**</span><span class="sxs-lookup"><span data-stu-id="bc0eb-164">Select **Finish**</span></span>

        ![Finish creating the linked service](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image8.png)

## <a name="create-a-pipeline"></a><span data-ttu-id="bc0eb-166">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="bc0eb-166">Create a pipeline</span></span>

1.  <span data-ttu-id="bc0eb-167">Select the **+** (plus) button, and then select **Pipeline** on the menu.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-167">Select the **+** (plus) button, and then select **Pipeline** on the menu.</span></span>

    ![Buttons for creating a new pipeline](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image9.png)

1.  <span data-ttu-id="bc0eb-169">Create a **parameter** to be used in the **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-169">Create a **parameter** to be used in the **Pipeline**.</span></span> <span data-ttu-id="bc0eb-170">Later you pass this parameter to the Databricks Notebook Activity.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-170">Later you pass this parameter to the Databricks Notebook Activity.</span></span> <span data-ttu-id="bc0eb-171">In the empty pipeline, click on the **Parameters** tab, then **New** and name it as '**name**'.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-171">In the empty pipeline, click on the **Parameters** tab, then **New** and name it as '**name**'.</span></span>

    ![Create a new parameter](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image10.png)

    ![Create the name parameter](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image11.png)

1.  <span data-ttu-id="bc0eb-174">In the **Activities** toolbox, expand **Databricks**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-174">In the **Activities** toolbox, expand **Databricks**.</span></span> <span data-ttu-id="bc0eb-175">Drag the **Notebook** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-175">Drag the **Notebook** activity from the **Activities** toolbox to the pipeline designer surface.</span></span>

    ![Drag the notebook to the designer surface](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image12.png)

1.  <span data-ttu-id="bc0eb-177">In the properties for the **Databricks** **Notebook** activity window at the bottom, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-177">In the properties for the **Databricks** **Notebook** activity window at the bottom, complete the following steps:</span></span>

    <span data-ttu-id="bc0eb-178">a.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-178">a.</span></span> <span data-ttu-id="bc0eb-179">Switch to the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-179">Switch to the **Settings** tab.</span></span>

    <span data-ttu-id="bc0eb-180">b.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-180">b.</span></span> <span data-ttu-id="bc0eb-181">Select **myAzureDatabricks\_LinkedService** (which you created in the previous procedure).</span><span class="sxs-lookup"><span data-stu-id="bc0eb-181">Select **myAzureDatabricks\_LinkedService** (which you created in the previous procedure).</span></span>

    <span data-ttu-id="bc0eb-182">c.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-182">c.</span></span> <span data-ttu-id="bc0eb-183">Select a Databricks **Notebook path**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-183">Select a Databricks **Notebook path**.</span></span> <span data-ttu-id="bc0eb-184">Let’s create a notebook and specify the path here.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-184">Let’s create a notebook and specify the path here.</span></span> <span data-ttu-id="bc0eb-185">You get the Notebook Path by following the next few steps.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-185">You get the Notebook Path by following the next few steps.</span></span>

       1. <span data-ttu-id="bc0eb-186">Launch your Azure Databricks Workspace</span><span class="sxs-lookup"><span data-stu-id="bc0eb-186">Launch your Azure Databricks Workspace</span></span>

       1. <span data-ttu-id="bc0eb-187">Create a **New Folder** in Workplace and call it as **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-187">Create a **New Folder** in Workplace and call it as **adftutorial**.</span></span>

          ![Create a new folder](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image13.png)

       1. <span data-ttu-id="bc0eb-189">[Create a new notebook](https://docs.databricks.com/user-guide/notebooks/index.html#creating-a-notebook) (Python), let’s call it **mynotebook** under **adftutorial** Folder **,** click **Create.**</span><span class="sxs-lookup"><span data-stu-id="bc0eb-189">[Create a new notebook](https://docs.databricks.com/user-guide/notebooks/index.html#creating-a-notebook) (Python), let’s call it **mynotebook** under **adftutorial** Folder **,** click **Create.**</span></span>

          ![Create a new notebook](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image14.png)

          ![Set the properties of the new notebook](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image15.png)

       1. <span data-ttu-id="bc0eb-192">In the newly created notebook "mynotebook'" add the following code:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-192">In the newly created notebook "mynotebook'" add the following code:</span></span>

           ```
           # Creating widgets for leveraging parameters, and printing the parameters

           dbutils.widgets.text("input", "","")
           dbutils.widgets.get("input")
           y = getArgument("input")
           print "Param -\'input':"
           print y
           ```

           ![Create widgets for parameters](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image16.png)

       1. <span data-ttu-id="bc0eb-194">The **Notebook Path** in this case is **/adftutorial/mynotebook**</span><span class="sxs-lookup"><span data-stu-id="bc0eb-194">The **Notebook Path** in this case is **/adftutorial/mynotebook**</span></span>

1.  <span data-ttu-id="bc0eb-195">Switch back to the **Data Factory UI authoring tool**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-195">Switch back to the **Data Factory UI authoring tool**.</span></span> <span data-ttu-id="bc0eb-196">Navigate to **Settings** Tab under the **Notebook1 Activity**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-196">Navigate to **Settings** Tab under the **Notebook1 Activity**.</span></span> 
    
    <span data-ttu-id="bc0eb-197">a.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-197">a.</span></span>  <span data-ttu-id="bc0eb-198">**Add Parameter** to the Notebook activity.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-198">**Add Parameter** to the Notebook activity.</span></span> <span data-ttu-id="bc0eb-199">You use the same parameter that you added earlier to the **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-199">You use the same parameter that you added earlier to the **Pipeline**.</span></span>

       ![Add a parameter](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image17.png)

    <span data-ttu-id="bc0eb-201">b.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-201">b.</span></span>  <span data-ttu-id="bc0eb-202">Name the parameter as **input** and provide the value as expression **@pipeline().parameters.name**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-202">Name the parameter as **input** and provide the value as expression **@pipeline().parameters.name**.</span></span>

1.  <span data-ttu-id="bc0eb-203">To validate the pipeline, select the **Validate** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-203">To validate the pipeline, select the **Validate** button on the toolbar.</span></span> <span data-ttu-id="bc0eb-204">To close the validation window, select the **\>\>** (right arrow) button.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-204">To close the validation window, select the **\>\>** (right arrow) button.</span></span>

    ![Validate the pipeline](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image18.png)

1.  <span data-ttu-id="bc0eb-206">Select **Publish All**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-206">Select **Publish All**.</span></span> <span data-ttu-id="bc0eb-207">The Data Factory UI publishes entities (linked services and pipeline) to the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-207">The Data Factory UI publishes entities (linked services and pipeline) to the Azure Data Factory service.</span></span>

    ![Publish the new data factory entities](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image19.png)

## <a name="trigger-a-pipeline-run"></a><span data-ttu-id="bc0eb-209">Trigger a pipeline run</span><span class="sxs-lookup"><span data-stu-id="bc0eb-209">Trigger a pipeline run</span></span>

<span data-ttu-id="bc0eb-210">Select **Trigger** on the toolbar, and then select **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-210">Select **Trigger** on the toolbar, and then select **Trigger Now**.</span></span>

![Select the Trigger Now command](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image20.png)

<span data-ttu-id="bc0eb-212">The **Pipeline Run** dialog box asks for the **name** parameter.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-212">The **Pipeline Run** dialog box asks for the **name** parameter.</span></span> <span data-ttu-id="bc0eb-213">Use **/path/filename** as the parameter here.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-213">Use **/path/filename** as the parameter here.</span></span> <span data-ttu-id="bc0eb-214">Click **Finish.**</span><span class="sxs-lookup"><span data-stu-id="bc0eb-214">Click **Finish.**</span></span>

![Provide a value for the name parameters](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image21.png)

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="bc0eb-216">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="bc0eb-216">Monitor the pipeline run</span></span>

1.  <span data-ttu-id="bc0eb-217">Switch to the **Monitor** tab. Confirm that you see a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-217">Switch to the **Monitor** tab. Confirm that you see a pipeline run.</span></span> <span data-ttu-id="bc0eb-218">It takes approximately 5-8 minutes to create a Databricks job cluster, where the notebook is executed.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-218">It takes approximately 5-8 minutes to create a Databricks job cluster, where the notebook is executed.</span></span>

    ![Monitor the pipeline](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image22.png)

1.  <span data-ttu-id="bc0eb-220">Select **Refresh** periodically to check the status of the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-220">Select **Refresh** periodically to check the status of the pipeline run.</span></span>

1.  <span data-ttu-id="bc0eb-221">To see activity runs associated with the pipeline run, select **View Activity Runs** in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-221">To see activity runs associated with the pipeline run, select **View Activity Runs** in the **Actions** column.</span></span>

    ![View the activity runs](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image23.png)

<span data-ttu-id="bc0eb-223">You can switch back to the pipeline runs view by selecting the **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-223">You can switch back to the pipeline runs view by selecting the **Pipelines** link at the top.</span></span>

## <a name="verify-the-output"></a><span data-ttu-id="bc0eb-224">Verify the output</span><span class="sxs-lookup"><span data-stu-id="bc0eb-224">Verify the output</span></span>

<span data-ttu-id="bc0eb-225">You can log on to the **Azure Databricks workspace**, go to **Clusters** and you can see the **Job** status as *pending execution, running, or terminated*.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-225">You can log on to the **Azure Databricks workspace**, go to **Clusters** and you can see the **Job** status as *pending execution, running, or terminated*.</span></span>

![View the job cluster and the job](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image24.png)

<span data-ttu-id="bc0eb-227">You can click on the **Job name** and navigate to see further details.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-227">You can click on the **Job name** and navigate to see further details.</span></span> <span data-ttu-id="bc0eb-228">On successful run, you can validate the parameters passed and the output of the Python notebook.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-228">On successful run, you can validate the parameters passed and the output of the Python notebook.</span></span>

![View the run details and output](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image25.png)

## <a name="next-steps"></a><span data-ttu-id="bc0eb-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc0eb-230">Next steps</span></span>

<span data-ttu-id="bc0eb-231">The pipeline in this sample triggers a Databricks Notebook activity and passes a parameter to it.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-231">The pipeline in this sample triggers a Databricks Notebook activity and passes a parameter to it.</span></span> <span data-ttu-id="bc0eb-232">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="bc0eb-232">You learned how to:</span></span>

  - <span data-ttu-id="bc0eb-233">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-233">Create a data factory.</span></span>

  - <span data-ttu-id="bc0eb-234">Create a pipeline that uses a Databricks Notebook activity.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-234">Create a pipeline that uses a Databricks Notebook activity.</span></span>

  - <span data-ttu-id="bc0eb-235">Trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-235">Trigger a pipeline run.</span></span>

  - <span data-ttu-id="bc0eb-236">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bc0eb-236">Monitor the pipeline run.</span></span>
