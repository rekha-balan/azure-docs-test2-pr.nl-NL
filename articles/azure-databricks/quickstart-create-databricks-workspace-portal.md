---
title: 'Quickstart: Run a Spark job on Azure Databricks using Azure portal'
description: The quickstart shows how to use the Azure portal to create an Azure Databricks workspace, an Apache Spark cluster, and run a Spark job.
services: azure-databricks
ms.service: azure-databricks
author: jasonwhowell
ms.author: jasonh
manager: cgronlun
editor: cgronlun
ms.workload: big-data
ms.topic: quickstart
ms.date: 07/23/2018
ms.custom: mvc
ms.openlocfilehash: cd6a3b768077880d47462d1db559a4884cceb84a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869275"
---
# <a name="quickstart-run-a-spark-job-on-azure-databricks-using-the-azure-portal"></a><span data-ttu-id="64714-103">Quickstart: Run a Spark job on Azure Databricks using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="64714-103">Quickstart: Run a Spark job on Azure Databricks using the Azure portal</span></span>

<span data-ttu-id="64714-104">This quickstart shows how to create an Azure Databricks workspace and an Apache Spark cluster within that workspace.</span><span class="sxs-lookup"><span data-stu-id="64714-104">This quickstart shows how to create an Azure Databricks workspace and an Apache Spark cluster within that workspace.</span></span> <span data-ttu-id="64714-105">Finally, you learn how to run a Spark job on the Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-105">Finally, you learn how to run a Spark job on the Databricks cluster.</span></span> <span data-ttu-id="64714-106">For more information on Azure Databricks, see [What is Azure Databricks?](what-is-azure-databricks.md)</span><span class="sxs-lookup"><span data-stu-id="64714-106">For more information on Azure Databricks, see [What is Azure Databricks?](what-is-azure-databricks.md)</span></span>

<span data-ttu-id="64714-107">In this quickstart, as part of the Spark job, you analyze a radio channel subscription data to gain insights into free/paid usage based on demographics.</span><span class="sxs-lookup"><span data-stu-id="64714-107">In this quickstart, as part of the Spark job, you analyze a radio channel subscription data to gain insights into free/paid usage based on demographics.</span></span> 

<span data-ttu-id="64714-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="64714-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="64714-109">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="64714-109">Log in to the Azure portal</span></span>

<span data-ttu-id="64714-110">Log in to the [Azure  portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64714-110">Log in to the [Azure  portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-databricks-workspace"></a><span data-ttu-id="64714-111">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="64714-111">Create an Azure Databricks workspace</span></span>

<span data-ttu-id="64714-112">In this section, you create an Azure Databricks workspace using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="64714-112">In this section, you create an Azure Databricks workspace using the Azure portal.</span></span> 

1. <span data-ttu-id="64714-113">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span><span class="sxs-lookup"><span data-stu-id="64714-113">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span></span> 

    <span data-ttu-id="64714-114">![Databricks on Azure portal](./media/quickstart-create-databricks-workspace-portal/azure-databricks-on-portal.png "Databricks on Azure portal")</span><span class="sxs-lookup"><span data-stu-id="64714-114">![Databricks on Azure portal](./media/quickstart-create-databricks-workspace-portal/azure-databricks-on-portal.png "Databricks on Azure portal")</span></span>

2. <span data-ttu-id="64714-115">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="64714-115">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span></span>

    <span data-ttu-id="64714-116">![Create an Azure Databricks workspace](./media/quickstart-create-databricks-workspace-portal/create-databricks-workspace.png "Create an Azure Databricks workspace")</span><span class="sxs-lookup"><span data-stu-id="64714-116">![Create an Azure Databricks workspace](./media/quickstart-create-databricks-workspace-portal/create-databricks-workspace.png "Create an Azure Databricks workspace")</span></span>

    <span data-ttu-id="64714-117">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="64714-117">Provide the following values:</span></span> 
     
    |<span data-ttu-id="64714-118">Property</span><span class="sxs-lookup"><span data-stu-id="64714-118">Property</span></span>  |<span data-ttu-id="64714-119">Description</span><span class="sxs-lookup"><span data-stu-id="64714-119">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="64714-120">**Workspace name**</span><span class="sxs-lookup"><span data-stu-id="64714-120">**Workspace name**</span></span>     | <span data-ttu-id="64714-121">Provide a name for your Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="64714-121">Provide a name for your Databricks workspace</span></span>        |
    |<span data-ttu-id="64714-122">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="64714-122">**Subscription**</span></span>     | <span data-ttu-id="64714-123">From the drop-down, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="64714-123">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="64714-124">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="64714-124">**Resource group**</span></span>     | <span data-ttu-id="64714-125">Specify whether you want to create a new resource group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="64714-125">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="64714-126">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="64714-126">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="64714-127">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64714-127">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span></span> |
    |<span data-ttu-id="64714-128">**Location**</span><span class="sxs-lookup"><span data-stu-id="64714-128">**Location**</span></span>     | <span data-ttu-id="64714-129">Select **East US 2**.</span><span class="sxs-lookup"><span data-stu-id="64714-129">Select **East US 2**.</span></span> <span data-ttu-id="64714-130">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="64714-130">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span></span>        |
    |<span data-ttu-id="64714-131">**Pricing Tier**</span><span class="sxs-lookup"><span data-stu-id="64714-131">**Pricing Tier**</span></span>     |  <span data-ttu-id="64714-132">Choose between **Standard** or **Premium**.</span><span class="sxs-lookup"><span data-stu-id="64714-132">Choose between **Standard** or **Premium**.</span></span> <span data-ttu-id="64714-133">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span><span class="sxs-lookup"><span data-stu-id="64714-133">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span></span>       |

    <span data-ttu-id="64714-134">Select **Pin to dashboard** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="64714-134">Select **Pin to dashboard** and then click **Create**.</span></span>

4. <span data-ttu-id="64714-135">The workspace creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="64714-135">The workspace creation takes a few minutes.</span></span> <span data-ttu-id="64714-136">During workspace creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span><span class="sxs-lookup"><span data-stu-id="64714-136">During workspace creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span></span> <span data-ttu-id="64714-137">You may need to scroll right on your dashboard to see the tile.</span><span class="sxs-lookup"><span data-stu-id="64714-137">You may need to scroll right on your dashboard to see the tile.</span></span> <span data-ttu-id="64714-138">There is also a progress bar displayed near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="64714-138">There is also a progress bar displayed near the top of the screen.</span></span> <span data-ttu-id="64714-139">You can watch either area for progress.</span><span class="sxs-lookup"><span data-stu-id="64714-139">You can watch either area for progress.</span></span>

    <span data-ttu-id="64714-140">![Databricks deployment tile](./media/quickstart-create-databricks-workspace-portal/databricks-deployment-tile.png "Databricks deployment tile")</span><span class="sxs-lookup"><span data-stu-id="64714-140">![Databricks deployment tile](./media/quickstart-create-databricks-workspace-portal/databricks-deployment-tile.png "Databricks deployment tile")</span></span>

## <a name="create-a-spark-cluster-in-databricks"></a><span data-ttu-id="64714-141">Create a Spark cluster in Databricks</span><span class="sxs-lookup"><span data-stu-id="64714-141">Create a Spark cluster in Databricks</span></span>

> [!NOTE] 
> <span data-ttu-id="64714-142">To use a free account to create the Azure Databricks cluster, before creating the cluster, go to your profile and change your subscription to **pay-as-you-go**.</span><span class="sxs-lookup"><span data-stu-id="64714-142">To use a free account to create the Azure Databricks cluster, before creating the cluster, go to your profile and change your subscription to **pay-as-you-go**.</span></span> <span data-ttu-id="64714-143">For more information, see [Azure free account](https://azure.microsoft.com/en-us/free/).</span><span class="sxs-lookup"><span data-stu-id="64714-143">For more information, see [Azure free account](https://azure.microsoft.com/en-us/free/).</span></span>  

1. <span data-ttu-id="64714-144">In the Azure portal, go to the Databricks workspace that you created, and then click **Launch Workspace**.</span><span class="sxs-lookup"><span data-stu-id="64714-144">In the Azure portal, go to the Databricks workspace that you created, and then click **Launch Workspace**.</span></span>

2. <span data-ttu-id="64714-145">You are redirected to the Azure Databricks portal.</span><span class="sxs-lookup"><span data-stu-id="64714-145">You are redirected to the Azure Databricks portal.</span></span> <span data-ttu-id="64714-146">From the portal, click **Cluster**.</span><span class="sxs-lookup"><span data-stu-id="64714-146">From the portal, click **Cluster**.</span></span>

    <span data-ttu-id="64714-147">![Databricks on Azure](./media/quickstart-create-databricks-workspace-portal/databricks-on-azure.png "Databricks on Azure")</span><span class="sxs-lookup"><span data-stu-id="64714-147">![Databricks on Azure](./media/quickstart-create-databricks-workspace-portal/databricks-on-azure.png "Databricks on Azure")</span></span>

3. <span data-ttu-id="64714-148">In the **New cluster** page, provide the values to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-148">In the **New cluster** page, provide the values to create a cluster.</span></span>

    <span data-ttu-id="64714-149">![Create Databricks Spark cluster on Azure](./media/quickstart-create-databricks-workspace-portal/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span><span class="sxs-lookup"><span data-stu-id="64714-149">![Create Databricks Spark cluster on Azure](./media/quickstart-create-databricks-workspace-portal/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span></span>

    <span data-ttu-id="64714-150">Accept all other default values other than the following:</span><span class="sxs-lookup"><span data-stu-id="64714-150">Accept all other default values other than the following:</span></span>

    * <span data-ttu-id="64714-151">Enter a name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-151">Enter a name for the cluster.</span></span>
    * <span data-ttu-id="64714-152">For this article, create a cluster with **4.0** runtime.</span><span class="sxs-lookup"><span data-stu-id="64714-152">For this article, create a cluster with **4.0** runtime.</span></span> 
    * <span data-ttu-id="64714-153">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span><span class="sxs-lookup"><span data-stu-id="64714-153">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span></span> <span data-ttu-id="64714-154">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span><span class="sxs-lookup"><span data-stu-id="64714-154">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span></span>
    
    <span data-ttu-id="64714-155">Select **Create cluster**.</span><span class="sxs-lookup"><span data-stu-id="64714-155">Select **Create cluster**.</span></span> <span data-ttu-id="64714-156">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="64714-156">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span></span> 

<span data-ttu-id="64714-157">For more information on creating clusters, see [Create a Spark cluster in Azure Databricks](https://docs.azuredatabricks.net/user-guide/clusters/create.html).</span><span class="sxs-lookup"><span data-stu-id="64714-157">For more information on creating clusters, see [Create a Spark cluster in Azure Databricks](https://docs.azuredatabricks.net/user-guide/clusters/create.html).</span></span>


## <a name="download-a-sample-data-file"></a><span data-ttu-id="64714-158">Download a sample data file</span><span class="sxs-lookup"><span data-stu-id="64714-158">Download a sample data file</span></span>
<span data-ttu-id="64714-159">Download a sample JSON data file and save it into Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="64714-159">Download a sample JSON data file and save it into Azure blob storage.</span></span>

1. <span data-ttu-id="64714-160">Download this sample JSON data file [from Github](https://raw.githubusercontent.com/Azure/usql/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json) onto your local computer.</span><span class="sxs-lookup"><span data-stu-id="64714-160">Download this sample JSON data file [from Github](https://raw.githubusercontent.com/Azure/usql/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json) onto your local computer.</span></span> <span data-ttu-id="64714-161">Right-click and save as to save the raw file locally.</span><span class="sxs-lookup"><span data-stu-id="64714-161">Right-click and save as to save the raw file locally.</span></span> 

2. <span data-ttu-id="64714-162">If you don't already have a storage account, create one.</span><span class="sxs-lookup"><span data-stu-id="64714-162">If you don't already have a storage account, create one.</span></span> 
   - <span data-ttu-id="64714-163">In the Azure portal, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="64714-163">In the Azure portal, select **Create a resource**.</span></span>  <span data-ttu-id="64714-164">Select the **Storage** category, and select **Storage Accounts**</span><span class="sxs-lookup"><span data-stu-id="64714-164">Select the **Storage** category, and select **Storage Accounts**</span></span>  
   - <span data-ttu-id="64714-165">Provide a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="64714-165">Provide a unique name for the storage account.</span></span>
   - <span data-ttu-id="64714-166">Select **Account Kind**: **Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="64714-166">Select **Account Kind**: **Blob Storage**</span></span>
   - <span data-ttu-id="64714-167">Select a **Resource Group** name.</span><span class="sxs-lookup"><span data-stu-id="64714-167">Select a **Resource Group** name.</span></span> <span data-ttu-id="64714-168">Use the same resource group you created the Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="64714-168">Use the same resource group you created the Databricks workspace.</span></span>
   
   <span data-ttu-id="64714-169">For more information, see [Create an Azure Blob storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="64714-169">For more information, see [Create an Azure Blob storage account](../storage/common/storage-quickstart-create-account.md).</span></span> 

3. <span data-ttu-id="64714-170">Create a storage Container in the Blob Storage account and upload the sample json file into the container.</span><span class="sxs-lookup"><span data-stu-id="64714-170">Create a storage Container in the Blob Storage account and upload the sample json file into the container.</span></span> <span data-ttu-id="64714-171">You can use the Azure portal or the  [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload the file.</span><span class="sxs-lookup"><span data-stu-id="64714-171">You can use the Azure portal or the  [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload the file.</span></span>

   - <span data-ttu-id="64714-172">Open the storage account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="64714-172">Open the storage account in the Azure portal.</span></span>
   - <span data-ttu-id="64714-173">Select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="64714-173">Select **Blobs**.</span></span>
   - <span data-ttu-id="64714-174">Select **+ Container** to create a new empty container.</span><span class="sxs-lookup"><span data-stu-id="64714-174">Select **+ Container** to create a new empty container.</span></span>
   - <span data-ttu-id="64714-175">Provide a **Name** for the container, such as `databricks`.</span><span class="sxs-lookup"><span data-stu-id="64714-175">Provide a **Name** for the container, such as `databricks`.</span></span> 
   - <span data-ttu-id="64714-176">Select  **Private (non anonymous access)** access level.</span><span class="sxs-lookup"><span data-stu-id="64714-176">Select  **Private (non anonymous access)** access level.</span></span>
   - <span data-ttu-id="64714-177">Once the container is created, select the container name.</span><span class="sxs-lookup"><span data-stu-id="64714-177">Once the container is created, select the container name.</span></span>
   - <span data-ttu-id="64714-178">Select the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="64714-178">Select the **Upload** button.</span></span>
   - <span data-ttu-id="64714-179">On the **Files** page, select the **Folder icon** to browse and select the sample file `small_radio_json.json` for upload.</span><span class="sxs-lookup"><span data-stu-id="64714-179">On the **Files** page, select the **Folder icon** to browse and select the sample file `small_radio_json.json` for upload.</span></span> 
   - <span data-ttu-id="64714-180">Select **Upload** to upload the file.</span><span class="sxs-lookup"><span data-stu-id="64714-180">Select **Upload** to upload the file.</span></span>
   
   
## <a name="run-a-spark-sql-job"></a><span data-ttu-id="64714-181">Run a Spark SQL job</span><span class="sxs-lookup"><span data-stu-id="64714-181">Run a Spark SQL job</span></span>
<span data-ttu-id="64714-182">Perform the following tasks to create a notebook in Databricks, configure the notebook to read data from an Azure Blob storage account, and then run a Spark SQL job on the data.</span><span class="sxs-lookup"><span data-stu-id="64714-182">Perform the following tasks to create a notebook in Databricks, configure the notebook to read data from an Azure Blob storage account, and then run a Spark SQL job on the data.</span></span>

1. <span data-ttu-id="64714-183">In the left pane, click **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="64714-183">In the left pane, click **Workspace**.</span></span> <span data-ttu-id="64714-184">From the **Workspace** drop-down, click **Create**, and then click **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="64714-184">From the **Workspace** drop-down, click **Create**, and then click **Notebook**.</span></span>

    <span data-ttu-id="64714-185">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-create-notebook.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="64714-185">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-create-notebook.png "Create notebook in Databricks")</span></span>

2. <span data-ttu-id="64714-186">In the **Create Notebook** dialog box, enter a name, select **Scala** as the language, and select the Spark cluster that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="64714-186">In the **Create Notebook** dialog box, enter a name, select **Scala** as the language, and select the Spark cluster that you created earlier.</span></span>

    <span data-ttu-id="64714-187">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-details.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="64714-187">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-details.png "Create notebook in Databricks")</span></span>

    <span data-ttu-id="64714-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="64714-188">Click **Create**.</span></span>

3. <span data-ttu-id="64714-189">In this step, associate the Azure Storage account with the Databricks Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-189">In this step, associate the Azure Storage account with the Databricks Spark cluster.</span></span> <span data-ttu-id="64714-190">There are two ways to accomplish this association.</span><span class="sxs-lookup"><span data-stu-id="64714-190">There are two ways to accomplish this association.</span></span> <span data-ttu-id="64714-191">You can mount the Azure Storage account to the Databricks Filesystem (DBFS), or directly access the Azure Storage account from the application you create.</span><span class="sxs-lookup"><span data-stu-id="64714-191">You can mount the Azure Storage account to the Databricks Filesystem (DBFS), or directly access the Azure Storage account from the application you create.</span></span>  

    > [!IMPORTANT]
    ><span data-ttu-id="64714-192">This article uses the approach to **mount the storage with DBFS**.</span><span class="sxs-lookup"><span data-stu-id="64714-192">This article uses the approach to **mount the storage with DBFS**.</span></span> <span data-ttu-id="64714-193">This approach ensures that the mounted storage gets associated with the cluster filesystem itself.</span><span class="sxs-lookup"><span data-stu-id="64714-193">This approach ensures that the mounted storage gets associated with the cluster filesystem itself.</span></span> <span data-ttu-id="64714-194">Hence, any application accessing the cluster is able to use the associated storage as well.</span><span class="sxs-lookup"><span data-stu-id="64714-194">Hence, any application accessing the cluster is able to use the associated storage as well.</span></span> <span data-ttu-id="64714-195">The direct-access approach is limited to the application from where you configure the access.</span><span class="sxs-lookup"><span data-stu-id="64714-195">The direct-access approach is limited to the application from where you configure the access.</span></span>
    >
    > <span data-ttu-id="64714-196">To use the mounting approach, you must create a Spark cluster with Databricks runtime version **4.0**, which is what you chose in this article.</span><span class="sxs-lookup"><span data-stu-id="64714-196">To use the mounting approach, you must create a Spark cluster with Databricks runtime version **4.0**, which is what you chose in this article.</span></span>

    <span data-ttu-id="64714-197">In the following snippet, replace `{YOUR CONTAINER NAME}`, `{YOUR STORAGE ACCOUNT NAME}`, and `{YOUR STORAGE ACCOUNT ACCESS KEY}` with the appropriate values for your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="64714-197">In the following snippet, replace `{YOUR CONTAINER NAME}`, `{YOUR STORAGE ACCOUNT NAME}`, and `{YOUR STORAGE ACCOUNT ACCESS KEY}` with the appropriate values for your Azure Storage account.</span></span> <span data-ttu-id="64714-198">Paste the snippet in an empty cell in the notebook and then press SHIFT + ENTER to run the code cell.</span><span class="sxs-lookup"><span data-stu-id="64714-198">Paste the snippet in an empty cell in the notebook and then press SHIFT + ENTER to run the code cell.</span></span>

    * <span data-ttu-id="64714-199">**Mount the storage account with DBFS (recommended)**.</span><span class="sxs-lookup"><span data-stu-id="64714-199">**Mount the storage account with DBFS (recommended)**.</span></span> <span data-ttu-id="64714-200">In this snippet, the Azure Storage account path is mounted to `/mnt/mypath`.</span><span class="sxs-lookup"><span data-stu-id="64714-200">In this snippet, the Azure Storage account path is mounted to `/mnt/mypath`.</span></span> <span data-ttu-id="64714-201">So, in all future occurrences where you access the Azure Storage account you don't need to give the full path.</span><span class="sxs-lookup"><span data-stu-id="64714-201">So, in all future occurrences where you access the Azure Storage account you don't need to give the full path.</span></span> <span data-ttu-id="64714-202">You can just use `/mnt/mypath`.</span><span class="sxs-lookup"><span data-stu-id="64714-202">You can just use `/mnt/mypath`.</span></span>

          dbutils.fs.mount(
            source = "wasbs://{YOUR CONTAINER NAME}@{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net/",
            mountPoint = "/mnt/mypath",
            extraConfigs = Map("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net" -> "{YOUR STORAGE ACCOUNT ACCESS KEY}"))

    * <span data-ttu-id="64714-203">**Directly access the storage account**</span><span class="sxs-lookup"><span data-stu-id="64714-203">**Directly access the storage account**</span></span>

          spark.conf.set("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net", "{YOUR STORAGE ACCOUNT ACCESS KEY}")

    <span data-ttu-id="64714-204">For instructions on how to retrieve the storage account key, see [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="64714-204">For instructions on how to retrieve the storage account key, see [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    > [!NOTE]
    > <span data-ttu-id="64714-205">You can also use Azure Data Lake Store with a Spark cluster on Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="64714-205">You can also use Azure Data Lake Store with a Spark cluster on Azure Databricks.</span></span> <span data-ttu-id="64714-206">For instructions, see [Use Data Lake Store with Azure Databricks](https://go.microsoft.com/fwlink/?linkid=864084).</span><span class="sxs-lookup"><span data-stu-id="64714-206">For instructions, see [Use Data Lake Store with Azure Databricks](https://go.microsoft.com/fwlink/?linkid=864084).</span></span>

4. <span data-ttu-id="64714-207">Run a SQL statement to create a temporary table using data from the sample JSON data file, **small_radio_json.json**.</span><span class="sxs-lookup"><span data-stu-id="64714-207">Run a SQL statement to create a temporary table using data from the sample JSON data file, **small_radio_json.json**.</span></span> <span data-ttu-id="64714-208">In the following snippet, replace the placeholder values with your container name and storage account name.</span><span class="sxs-lookup"><span data-stu-id="64714-208">In the following snippet, replace the placeholder values with your container name and storage account name.</span></span> <span data-ttu-id="64714-209">Paste the snippet in a code cell in the notebook, and then press SHIFT + ENTER.</span><span class="sxs-lookup"><span data-stu-id="64714-209">Paste the snippet in a code cell in the notebook, and then press SHIFT + ENTER.</span></span> <span data-ttu-id="64714-210">In the snippet, `path` denotes the location of the sample JSON file that you uploaded to your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="64714-210">In the snippet, `path` denotes the location of the sample JSON file that you uploaded to your Azure Storage account.</span></span>

    ```sql
    %sql 
    DROP TABLE IF EXISTS radio_sample_data;
    CREATE TABLE radio_sample_data
    USING json
    OPTIONS (
     path "/mnt/mypath/small_radio_json.json"
    )
    ```

    <span data-ttu-id="64714-211">Once the command successfully completes, you have all the data from the JSON file as a table in Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-211">Once the command successfully completes, you have all the data from the JSON file as a table in Databricks cluster.</span></span>

    <span data-ttu-id="64714-212">The `%sql` language magic command enables you to run a SQL code from the notebook, even if the notebook is of another type.</span><span class="sxs-lookup"><span data-stu-id="64714-212">The `%sql` language magic command enables you to run a SQL code from the notebook, even if the notebook is of another type.</span></span> <span data-ttu-id="64714-213">For more information, see [Mixing languages in a notebook](https://docs.azuredatabricks.net/user-guide/notebooks/index.html#mixing-languages-in-a-notebook).</span><span class="sxs-lookup"><span data-stu-id="64714-213">For more information, see [Mixing languages in a notebook](https://docs.azuredatabricks.net/user-guide/notebooks/index.html#mixing-languages-in-a-notebook).</span></span>

5. <span data-ttu-id="64714-214">Let's look at a snapshot of the sample JSON data to better understand the query that you run.</span><span class="sxs-lookup"><span data-stu-id="64714-214">Let's look at a snapshot of the sample JSON data to better understand the query that you run.</span></span> <span data-ttu-id="64714-215">Paste the following snippet in the code cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="64714-215">Paste the following snippet in the code cell and press **SHIFT + ENTER**.</span></span>

    ```sql
    %sql 
    SELECT * from radio_sample_data
    ```

6. <span data-ttu-id="64714-216">You see a tabular output like shown in the following screenshot (only some columns are shown):</span><span class="sxs-lookup"><span data-stu-id="64714-216">You see a tabular output like shown in the following screenshot (only some columns are shown):</span></span>

    <span data-ttu-id="64714-217">![Sample JSON data](./media/quickstart-create-databricks-workspace-portal/databricks-sample-csv-data.png "Sample JSON data")</span><span class="sxs-lookup"><span data-stu-id="64714-217">![Sample JSON data](./media/quickstart-create-databricks-workspace-portal/databricks-sample-csv-data.png "Sample JSON data")</span></span>

    <span data-ttu-id="64714-218">Among other details, the sample data captures the gender of the audience of a radio channel (column name, **gender**)  and whether their subscription is free or paid (column name, **level**).</span><span class="sxs-lookup"><span data-stu-id="64714-218">Among other details, the sample data captures the gender of the audience of a radio channel (column name, **gender**)  and whether their subscription is free or paid (column name, **level**).</span></span>

7. <span data-ttu-id="64714-219">You now create a visual representation of this data to show for each gender, how many users have free accounts and how many are paid subscribers.</span><span class="sxs-lookup"><span data-stu-id="64714-219">You now create a visual representation of this data to show for each gender, how many users have free accounts and how many are paid subscribers.</span></span> <span data-ttu-id="64714-220">From the bottom of the tabular output, click the **Bar chart** icon, and then click **Plot Options**.</span><span class="sxs-lookup"><span data-stu-id="64714-220">From the bottom of the tabular output, click the **Bar chart** icon, and then click **Plot Options**.</span></span>

    <span data-ttu-id="64714-221">![Create bar chart](./media/quickstart-create-databricks-workspace-portal/create-plots-databricks-notebook.png "Create bar chart")</span><span class="sxs-lookup"><span data-stu-id="64714-221">![Create bar chart](./media/quickstart-create-databricks-workspace-portal/create-plots-databricks-notebook.png "Create bar chart")</span></span>

8. <span data-ttu-id="64714-222">In **Customize Plot**, drag-and-drop values as shown in the screenshot.</span><span class="sxs-lookup"><span data-stu-id="64714-222">In **Customize Plot**, drag-and-drop values as shown in the screenshot.</span></span>

    <span data-ttu-id="64714-223">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-customize-plot.png "Customize bar chart")</span><span class="sxs-lookup"><span data-stu-id="64714-223">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-customize-plot.png "Customize bar chart")</span></span>

    * <span data-ttu-id="64714-224">Set **Keys** to **gender**.</span><span class="sxs-lookup"><span data-stu-id="64714-224">Set **Keys** to **gender**.</span></span>
    * <span data-ttu-id="64714-225">Set **Series groupings** to **level**.</span><span class="sxs-lookup"><span data-stu-id="64714-225">Set **Series groupings** to **level**.</span></span>
    * <span data-ttu-id="64714-226">Set **Values** to **level**.</span><span class="sxs-lookup"><span data-stu-id="64714-226">Set **Values** to **level**.</span></span>
    * <span data-ttu-id="64714-227">Set **Aggregation** to **COUNT**.</span><span class="sxs-lookup"><span data-stu-id="64714-227">Set **Aggregation** to **COUNT**.</span></span>

    <span data-ttu-id="64714-228">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="64714-228">Click **Apply**.</span></span>

9. <span data-ttu-id="64714-229">The output shows the visual representation as depicted in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="64714-229">The output shows the visual representation as depicted in the following screenshot:</span></span>

     <span data-ttu-id="64714-230">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-sql-query-output-bar-chart.png "Customize bar chart")</span><span class="sxs-lookup"><span data-stu-id="64714-230">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-sql-query-output-bar-chart.png "Customize bar chart")</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="64714-231">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="64714-231">Clean up resources</span></span>

<span data-ttu-id="64714-232">After you have finished the article, you can terminate the cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-232">After you have finished the article, you can terminate the cluster.</span></span> <span data-ttu-id="64714-233">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span><span class="sxs-lookup"><span data-stu-id="64714-233">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span></span> <span data-ttu-id="64714-234">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span><span class="sxs-lookup"><span data-stu-id="64714-234">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span></span>

<span data-ttu-id="64714-235">![Stop a Databricks cluster](./media/quickstart-create-databricks-workspace-portal/terminate-databricks-cluster.png "Stop a Databricks cluster")</span><span class="sxs-lookup"><span data-stu-id="64714-235">![Stop a Databricks cluster](./media/quickstart-create-databricks-workspace-portal/terminate-databricks-cluster.png "Stop a Databricks cluster")</span></span>

<span data-ttu-id="64714-236">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="64714-236">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span></span> <span data-ttu-id="64714-237">In such a case, the cluster automatically stops, if it has been inactive for the specified time.</span><span class="sxs-lookup"><span data-stu-id="64714-237">In such a case, the cluster automatically stops, if it has been inactive for the specified time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64714-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="64714-238">Next steps</span></span>

<span data-ttu-id="64714-239">In this article, you created a Spark cluster in Azure Databricks and ran a Spark job using data in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="64714-239">In this article, you created a Spark cluster in Azure Databricks and ran a Spark job using data in Azure storage.</span></span> <span data-ttu-id="64714-240">You can also look at [Spark data sources](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html) to learn how to import data from other data sources into Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="64714-240">You can also look at [Spark data sources](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html) to learn how to import data from other data sources into Azure Databricks.</span></span> <span data-ttu-id="64714-241">Advance to the next article to learn how to perform an ETL operation (extract, transform, and load data) using Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="64714-241">Advance to the next article to learn how to perform an ETL operation (extract, transform, and load data) using Azure Databricks.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="64714-242">Extract, transform, and load data using Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="64714-242">Extract, transform, and load data using Azure Databricks</span></span>](databricks-extract-load-sql-data-warehouse.md)
