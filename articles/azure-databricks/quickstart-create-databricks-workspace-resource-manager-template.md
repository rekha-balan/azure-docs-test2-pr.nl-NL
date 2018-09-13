---
title: 'Quickstart: Run a Spark job on Azure Databricks using Resource Manager template | Microsoft Docs'
description: The quickstart shows how to use the Azure Resource Manager template to create an Azure Databricks workspace, then create an Apache Spark cluster, and run a Spark job.
services: azure-databricks
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/23/2018
ms.author: nitinme
ms.custom: mvc
ms.openlocfilehash: 573d8f6927cbd17c0f095bccf5132674faf94928
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870448"
---
# <a name="quickstart-run-a-spark-job-on-azure-databricks-using-the-azure-resource-manager-template"></a><span data-ttu-id="fea2c-103">Quickstart: Run a Spark job on Azure Databricks using the Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="fea2c-103">Quickstart: Run a Spark job on Azure Databricks using the Azure Resource Manager template</span></span>

<span data-ttu-id="fea2c-104">This quickstart shows how to create an Azure Databricks workspace using Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="fea2c-104">This quickstart shows how to create an Azure Databricks workspace using Azure Resource Manager template.</span></span> <span data-ttu-id="fea2c-105">You use the workspace to create an Apache Spark cluster and run a Spark job on the Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-105">You use the workspace to create an Apache Spark cluster and run a Spark job on the Databricks cluster.</span></span> <span data-ttu-id="fea2c-106">For more information on Azure Databricks, see [What is Azure Databricks?](what-is-azure-databricks.md)</span><span class="sxs-lookup"><span data-stu-id="fea2c-106">For more information on Azure Databricks, see [What is Azure Databricks?](what-is-azure-databricks.md)</span></span>

<span data-ttu-id="fea2c-107">In this quickstart, as part of the Spark job, you analyze a radio channel subscription data to gain insights into free/paid usage based on demographics.</span><span class="sxs-lookup"><span data-stu-id="fea2c-107">In this quickstart, as part of the Spark job, you analyze a radio channel subscription data to gain insights into free/paid usage based on demographics.</span></span>

<span data-ttu-id="fea2c-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="fea2c-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="create-an-azure-databricks-workspace"></a><span data-ttu-id="fea2c-109">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="fea2c-109">Create an Azure Databricks workspace</span></span>

<span data-ttu-id="fea2c-110">In this section, you create an Azure Databricks workspace using the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="fea2c-110">In this section, you create an Azure Databricks workspace using the Azure Resource Manager template.</span></span> 

1. <span data-ttu-id="fea2c-111">Click the following image to open the template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fea2c-111">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-databricks-workspace%2Fazuredeploy.json" target="_blank"><img src="./media/quickstart-create-databricks-workspace-resource-manager-template/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="fea2c-112">Provide the required values to create your Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="fea2c-112">Provide the required values to create your Azure Databricks workspace</span></span> 

    <span data-ttu-id="fea2c-113">![Create Azure Databricks workspace using an Azure Resource Manager template](./media/quickstart-create-databricks-workspace-resource-manager-template/create-databricks-workspace-using-resource-manager-template.png "Create Azure Databricks workspace using an Azure Resource Manager template")</span><span class="sxs-lookup"><span data-stu-id="fea2c-113">![Create Azure Databricks workspace using an Azure Resource Manager template](./media/quickstart-create-databricks-workspace-resource-manager-template/create-databricks-workspace-using-resource-manager-template.png "Create Azure Databricks workspace using an Azure Resource Manager template")</span></span>

    <span data-ttu-id="fea2c-114">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="fea2c-114">Provide the following values:</span></span> 
     
    |<span data-ttu-id="fea2c-115">Property</span><span class="sxs-lookup"><span data-stu-id="fea2c-115">Property</span></span>  |<span data-ttu-id="fea2c-116">Description</span><span class="sxs-lookup"><span data-stu-id="fea2c-116">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="fea2c-117">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="fea2c-117">**Subscription**</span></span>     | <span data-ttu-id="fea2c-118">From the drop-down, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fea2c-118">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="fea2c-119">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="fea2c-119">**Resource group**</span></span>     | <span data-ttu-id="fea2c-120">Specify whether you want to create a new resource group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="fea2c-120">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="fea2c-121">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="fea2c-121">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="fea2c-122">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fea2c-122">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span></span> |
    |<span data-ttu-id="fea2c-123">**Location**</span><span class="sxs-lookup"><span data-stu-id="fea2c-123">**Location**</span></span>     | <span data-ttu-id="fea2c-124">Select **East US 2**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-124">Select **East US 2**.</span></span> <span data-ttu-id="fea2c-125">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="fea2c-125">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span></span>        |
    |<span data-ttu-id="fea2c-126">**Workspace name**</span><span class="sxs-lookup"><span data-stu-id="fea2c-126">**Workspace name**</span></span>     | <span data-ttu-id="fea2c-127">Provide a name for your Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="fea2c-127">Provide a name for your Databricks workspace</span></span>        |
    |<span data-ttu-id="fea2c-128">**Pricing Tier**</span><span class="sxs-lookup"><span data-stu-id="fea2c-128">**Pricing Tier**</span></span>     |  <span data-ttu-id="fea2c-129">Choose between **Standard** or **Premium**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-129">Choose between **Standard** or **Premium**.</span></span> <span data-ttu-id="fea2c-130">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span><span class="sxs-lookup"><span data-stu-id="fea2c-130">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span></span>       |

3. <span data-ttu-id="fea2c-131">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-131">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span>

4. <span data-ttu-id="fea2c-132">The workspace creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="fea2c-132">The workspace creation takes a few minutes.</span></span> <span data-ttu-id="fea2c-133">During workspace creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span><span class="sxs-lookup"><span data-stu-id="fea2c-133">During workspace creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span></span> <span data-ttu-id="fea2c-134">You may need to scroll right on your dashboard to see the tile.</span><span class="sxs-lookup"><span data-stu-id="fea2c-134">You may need to scroll right on your dashboard to see the tile.</span></span> <span data-ttu-id="fea2c-135">There is also a progress bar displayed near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="fea2c-135">There is also a progress bar displayed near the top of the screen.</span></span> <span data-ttu-id="fea2c-136">You can watch either area for progress.</span><span class="sxs-lookup"><span data-stu-id="fea2c-136">You can watch either area for progress.</span></span>

    <span data-ttu-id="fea2c-137">![Databricks deployment tile](./media/quickstart-create-databricks-workspace-portal/databricks-deployment-tile.png "Databricks deployment tile")</span><span class="sxs-lookup"><span data-stu-id="fea2c-137">![Databricks deployment tile](./media/quickstart-create-databricks-workspace-portal/databricks-deployment-tile.png "Databricks deployment tile")</span></span>

## <a name="create-a-spark-cluster-in-databricks"></a><span data-ttu-id="fea2c-138">Create a Spark cluster in Databricks</span><span class="sxs-lookup"><span data-stu-id="fea2c-138">Create a Spark cluster in Databricks</span></span>

1. <span data-ttu-id="fea2c-139">In the Azure portal, go to the Databricks workspace that you created, and then click **Launch Workspace**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-139">In the Azure portal, go to the Databricks workspace that you created, and then click **Launch Workspace**.</span></span>

2. <span data-ttu-id="fea2c-140">You are redirected to the Azure Databricks portal.</span><span class="sxs-lookup"><span data-stu-id="fea2c-140">You are redirected to the Azure Databricks portal.</span></span> <span data-ttu-id="fea2c-141">From the portal, click **Cluster**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-141">From the portal, click **Cluster**.</span></span>

    <span data-ttu-id="fea2c-142">![Databricks on Azure](./media/quickstart-create-databricks-workspace-portal/databricks-on-azure.png "Databricks on Azure")</span><span class="sxs-lookup"><span data-stu-id="fea2c-142">![Databricks on Azure](./media/quickstart-create-databricks-workspace-portal/databricks-on-azure.png "Databricks on Azure")</span></span>

3. <span data-ttu-id="fea2c-143">In the **New cluster** page, provide the values to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-143">In the **New cluster** page, provide the values to create a cluster.</span></span>

    <span data-ttu-id="fea2c-144">![Create Databricks Spark cluster on Azure](./media/quickstart-create-databricks-workspace-portal/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span><span class="sxs-lookup"><span data-stu-id="fea2c-144">![Create Databricks Spark cluster on Azure](./media/quickstart-create-databricks-workspace-portal/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span></span>

    <span data-ttu-id="fea2c-145">Accept all other default values other than the following:</span><span class="sxs-lookup"><span data-stu-id="fea2c-145">Accept all other default values other than the following:</span></span>

    * <span data-ttu-id="fea2c-146">Enter a name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-146">Enter a name for the cluster.</span></span>
    * <span data-ttu-id="fea2c-147">For this article, create a cluster with **4.0** runtime.</span><span class="sxs-lookup"><span data-stu-id="fea2c-147">For this article, create a cluster with **4.0** runtime.</span></span> 
    * <span data-ttu-id="fea2c-148">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span><span class="sxs-lookup"><span data-stu-id="fea2c-148">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span></span> <span data-ttu-id="fea2c-149">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span><span class="sxs-lookup"><span data-stu-id="fea2c-149">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span></span>
    
    <span data-ttu-id="fea2c-150">Select **Create cluster**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-150">Select **Create cluster**.</span></span> <span data-ttu-id="fea2c-151">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="fea2c-151">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span></span> 

<span data-ttu-id="fea2c-152">For more information on creating clusters, see [Create a Spark cluster in Azure Databricks](https://docs.azuredatabricks.net/user-guide/clusters/create.html).</span><span class="sxs-lookup"><span data-stu-id="fea2c-152">For more information on creating clusters, see [Create a Spark cluster in Azure Databricks](https://docs.azuredatabricks.net/user-guide/clusters/create.html).</span></span>

## <a name="run-a-spark-sql-job"></a><span data-ttu-id="fea2c-153">Run a Spark SQL job</span><span class="sxs-lookup"><span data-stu-id="fea2c-153">Run a Spark SQL job</span></span>

<span data-ttu-id="fea2c-154">Before you begin with this section, you must complete the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="fea2c-154">Before you begin with this section, you must complete the following prerequisites:</span></span>

* <span data-ttu-id="fea2c-155">[Create an Azure Blob storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="fea2c-155">[Create an Azure Blob storage account](../storage/common/storage-quickstart-create-account.md).</span></span> 
* <span data-ttu-id="fea2c-156">Download a sample JSON file [from Github](https://github.com/Azure/usql/blob/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json).</span><span class="sxs-lookup"><span data-stu-id="fea2c-156">Download a sample JSON file [from Github](https://github.com/Azure/usql/blob/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json).</span></span> 
* <span data-ttu-id="fea2c-157">Upload the sample JSON file to the Azure Blob storage account you created.</span><span class="sxs-lookup"><span data-stu-id="fea2c-157">Upload the sample JSON file to the Azure Blob storage account you created.</span></span> <span data-ttu-id="fea2c-158">You can use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload files.</span><span class="sxs-lookup"><span data-stu-id="fea2c-158">You can use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload files.</span></span>

<span data-ttu-id="fea2c-159">Perform the following tasks to create a notebook in Databricks, configure the notebook to read data from an Azure Blob storage account, and then run a Spark SQL job on the data.</span><span class="sxs-lookup"><span data-stu-id="fea2c-159">Perform the following tasks to create a notebook in Databricks, configure the notebook to read data from an Azure Blob storage account, and then run a Spark SQL job on the data.</span></span>

1. <span data-ttu-id="fea2c-160">In the left pane, click **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-160">In the left pane, click **Workspace**.</span></span> <span data-ttu-id="fea2c-161">From the **Workspace** drop-down, click **Create**, and then click **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-161">From the **Workspace** drop-down, click **Create**, and then click **Notebook**.</span></span>

    <span data-ttu-id="fea2c-162">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-create-notebook.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="fea2c-162">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-create-notebook.png "Create notebook in Databricks")</span></span>

2. <span data-ttu-id="fea2c-163">In the **Create Notebook** dialog box, enter a name, select **Scala** as the language, and select the Spark cluster that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="fea2c-163">In the **Create Notebook** dialog box, enter a name, select **Scala** as the language, and select the Spark cluster that you created earlier.</span></span>

    <span data-ttu-id="fea2c-164">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-details.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="fea2c-164">![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-details.png "Create notebook in Databricks")</span></span>

    <span data-ttu-id="fea2c-165">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-165">Click **Create**.</span></span>

3. <span data-ttu-id="fea2c-166">In this step, associate the Azure Storage account with the Databricks Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-166">In this step, associate the Azure Storage account with the Databricks Spark cluster.</span></span> <span data-ttu-id="fea2c-167">There are two ways to accomplish this association.</span><span class="sxs-lookup"><span data-stu-id="fea2c-167">There are two ways to accomplish this association.</span></span> <span data-ttu-id="fea2c-168">You can mount the Azure Storage account to the Databricks Filesystem (DBFS), or directly access the Azure Storage account from the application you create.</span><span class="sxs-lookup"><span data-stu-id="fea2c-168">You can mount the Azure Storage account to the Databricks Filesystem (DBFS), or directly access the Azure Storage account from the application you create.</span></span>  

    > [!IMPORTANT]
    ><span data-ttu-id="fea2c-169">This article uses the approach to **mount the storage with DBFS**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-169">This article uses the approach to **mount the storage with DBFS**.</span></span> <span data-ttu-id="fea2c-170">This approach ensures that the mounted storage gets associated with the cluster filesystem itself.</span><span class="sxs-lookup"><span data-stu-id="fea2c-170">This approach ensures that the mounted storage gets associated with the cluster filesystem itself.</span></span> <span data-ttu-id="fea2c-171">Hence, any application accessing the cluster is able to use the associated storage as well.</span><span class="sxs-lookup"><span data-stu-id="fea2c-171">Hence, any application accessing the cluster is able to use the associated storage as well.</span></span> <span data-ttu-id="fea2c-172">The direct-access approach is limited to the application from where you configure the access.</span><span class="sxs-lookup"><span data-stu-id="fea2c-172">The direct-access approach is limited to the application from where you configure the access.</span></span>
    >
    > <span data-ttu-id="fea2c-173">To use the mounting approach, you must create a Spark cluster with Databricks runtime version **4.0**, which is what you chose in this article.</span><span class="sxs-lookup"><span data-stu-id="fea2c-173">To use the mounting approach, you must create a Spark cluster with Databricks runtime version **4.0**, which is what you chose in this article.</span></span>

    <span data-ttu-id="fea2c-174">In the following snippet, replace `{YOUR CONTAINER NAME}`, `{YOUR STORAGE ACCOUNT NAME}`, and `{YOUR STORAGE ACCOUNT ACCESS KEY}` with the appropriate values for your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="fea2c-174">In the following snippet, replace `{YOUR CONTAINER NAME}`, `{YOUR STORAGE ACCOUNT NAME}`, and `{YOUR STORAGE ACCOUNT ACCESS KEY}` with the appropriate values for your Azure Storage account.</span></span> <span data-ttu-id="fea2c-175">Paste the snippet in an empty cell in the notebook and then press SHIFT + ENTER to run the code cell.</span><span class="sxs-lookup"><span data-stu-id="fea2c-175">Paste the snippet in an empty cell in the notebook and then press SHIFT + ENTER to run the code cell.</span></span>

    * <span data-ttu-id="fea2c-176">**Mount the storage account with DBFS (recommended)**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-176">**Mount the storage account with DBFS (recommended)**.</span></span> <span data-ttu-id="fea2c-177">In this snippet, the Azure Storage account path is mounted to `/mnt/mypath`.</span><span class="sxs-lookup"><span data-stu-id="fea2c-177">In this snippet, the Azure Storage account path is mounted to `/mnt/mypath`.</span></span> <span data-ttu-id="fea2c-178">So, in all future occurrences where you access the Azure Storage account you don't need to give the full path.</span><span class="sxs-lookup"><span data-stu-id="fea2c-178">So, in all future occurrences where you access the Azure Storage account you don't need to give the full path.</span></span> <span data-ttu-id="fea2c-179">You can just use `/mnt/mypath`.</span><span class="sxs-lookup"><span data-stu-id="fea2c-179">You can just use `/mnt/mypath`.</span></span>

          dbutils.fs.mount(
            source = "wasbs://{YOUR CONTAINER NAME}@{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net/",
            mountPoint = "/mnt/mypath",
            extraConfigs = Map("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net" -> "{YOUR STORAGE ACCOUNT ACCESS KEY}"))

    * <span data-ttu-id="fea2c-180">**Directly access the storage account**</span><span class="sxs-lookup"><span data-stu-id="fea2c-180">**Directly access the storage account**</span></span>

          spark.conf.set("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net", "{YOUR STORAGE ACCOUNT ACCESS KEY}")

    <span data-ttu-id="fea2c-181">For instructions on how to retrieve the storage account key, see [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fea2c-181">For instructions on how to retrieve the storage account key, see [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    > [!NOTE]
    > <span data-ttu-id="fea2c-182">You can also use Azure Data Lake Store with a Spark cluster on Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="fea2c-182">You can also use Azure Data Lake Store with a Spark cluster on Azure Databricks.</span></span> <span data-ttu-id="fea2c-183">For instructions, see [Use Data Lake Store with Azure Databricks](https://go.microsoft.com/fwlink/?linkid=864084).</span><span class="sxs-lookup"><span data-stu-id="fea2c-183">For instructions, see [Use Data Lake Store with Azure Databricks](https://go.microsoft.com/fwlink/?linkid=864084).</span></span>

4. <span data-ttu-id="fea2c-184">Run a SQL statement to create a temporary table using data from the sample JSON data file, **small_radio_json.json**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-184">Run a SQL statement to create a temporary table using data from the sample JSON data file, **small_radio_json.json**.</span></span> <span data-ttu-id="fea2c-185">In the following snippet, replace the placeholder values with your container name and storage account name.</span><span class="sxs-lookup"><span data-stu-id="fea2c-185">In the following snippet, replace the placeholder values with your container name and storage account name.</span></span> <span data-ttu-id="fea2c-186">Paste the snippet in a code cell in the notebook, and then press SHIFT + ENTER.</span><span class="sxs-lookup"><span data-stu-id="fea2c-186">Paste the snippet in a code cell in the notebook, and then press SHIFT + ENTER.</span></span> <span data-ttu-id="fea2c-187">In the snippet, `path` denotes the location of the sample JSON file that you uploaded to your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="fea2c-187">In the snippet, `path` denotes the location of the sample JSON file that you uploaded to your Azure Storage account.</span></span>

    ```sql
    %sql 
    DROP TABLE IF EXISTS radio_sample_data;
    CREATE TABLE radio_sample_data
    USING json
    OPTIONS (
     path "/mnt/mypath/small_radio_json.json"
    )
    ```

    <span data-ttu-id="fea2c-188">Once the command successfully completes, you have all the data from the JSON file as a table in Databricks cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-188">Once the command successfully completes, you have all the data from the JSON file as a table in Databricks cluster.</span></span>

    <span data-ttu-id="fea2c-189">The `%sql` language magic command enables you to run a SQL code from the notebook, even if the notebook is of another type.</span><span class="sxs-lookup"><span data-stu-id="fea2c-189">The `%sql` language magic command enables you to run a SQL code from the notebook, even if the notebook is of another type.</span></span> <span data-ttu-id="fea2c-190">For more information, see [Mixing languages in a notebook](https://docs.azuredatabricks.net/user-guide/notebooks/index.html#mixing-languages-in-a-notebook).</span><span class="sxs-lookup"><span data-stu-id="fea2c-190">For more information, see [Mixing languages in a notebook](https://docs.azuredatabricks.net/user-guide/notebooks/index.html#mixing-languages-in-a-notebook).</span></span>

5. <span data-ttu-id="fea2c-191">Let's look at a snapshot of the sample JSON data to better understand the query that you run.</span><span class="sxs-lookup"><span data-stu-id="fea2c-191">Let's look at a snapshot of the sample JSON data to better understand the query that you run.</span></span> <span data-ttu-id="fea2c-192">Paste the following snippet in the code cell and press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-192">Paste the following snippet in the code cell and press **SHIFT + ENTER**.</span></span>

    ```sql
    %sql 
    SELECT * from radio_sample_data
    ```

6. <span data-ttu-id="fea2c-193">You see a tabular output like shown in the following screenshot (only some columns are shown):</span><span class="sxs-lookup"><span data-stu-id="fea2c-193">You see a tabular output like shown in the following screenshot (only some columns are shown):</span></span>

    <span data-ttu-id="fea2c-194">![Sample JSON data](./media/quickstart-create-databricks-workspace-portal/databricks-sample-csv-data.png "Sample JSON data")</span><span class="sxs-lookup"><span data-stu-id="fea2c-194">![Sample JSON data](./media/quickstart-create-databricks-workspace-portal/databricks-sample-csv-data.png "Sample JSON data")</span></span>

    <span data-ttu-id="fea2c-195">Among other details, the sample data captures the gender of the audience of a radio channel (column name, **gender**)  and whether their subscription is free or paid (column name, **level**).</span><span class="sxs-lookup"><span data-stu-id="fea2c-195">Among other details, the sample data captures the gender of the audience of a radio channel (column name, **gender**)  and whether their subscription is free or paid (column name, **level**).</span></span>

7. <span data-ttu-id="fea2c-196">You now create a visual representation of this data to show for each gender, how many users have free accounts and how many are paid subscribers.</span><span class="sxs-lookup"><span data-stu-id="fea2c-196">You now create a visual representation of this data to show for each gender, how many users have free accounts and how many are paid subscribers.</span></span> <span data-ttu-id="fea2c-197">From the bottom of the tabular output, click the **Bar chart** icon, and then click **Plot Options**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-197">From the bottom of the tabular output, click the **Bar chart** icon, and then click **Plot Options**.</span></span>

    <span data-ttu-id="fea2c-198">![Create bar chart](./media/quickstart-create-databricks-workspace-portal/create-plots-databricks-notebook.png "Create bar chart")</span><span class="sxs-lookup"><span data-stu-id="fea2c-198">![Create bar chart](./media/quickstart-create-databricks-workspace-portal/create-plots-databricks-notebook.png "Create bar chart")</span></span>

8. <span data-ttu-id="fea2c-199">In **Customize Plot**, drag-and-drop values as shown in the screenshot.</span><span class="sxs-lookup"><span data-stu-id="fea2c-199">In **Customize Plot**, drag-and-drop values as shown in the screenshot.</span></span>

    <span data-ttu-id="fea2c-200">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-customize-plot.png "Customize bar chart")</span><span class="sxs-lookup"><span data-stu-id="fea2c-200">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-customize-plot.png "Customize bar chart")</span></span>

    * <span data-ttu-id="fea2c-201">Set **Keys** to **gender**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-201">Set **Keys** to **gender**.</span></span>
    * <span data-ttu-id="fea2c-202">Set **Series groupings** to **level**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-202">Set **Series groupings** to **level**.</span></span>
    * <span data-ttu-id="fea2c-203">Set **Values** to **level**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-203">Set **Values** to **level**.</span></span>
    * <span data-ttu-id="fea2c-204">Set **Aggregation** to **COUNT**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-204">Set **Aggregation** to **COUNT**.</span></span>

    <span data-ttu-id="fea2c-205">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-205">Click **Apply**.</span></span>

9. <span data-ttu-id="fea2c-206">The output shows the visual representation as depicted in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="fea2c-206">The output shows the visual representation as depicted in the following screenshot:</span></span>

     <span data-ttu-id="fea2c-207">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-sql-query-output-bar-chart.png "Customize bar chart")</span><span class="sxs-lookup"><span data-stu-id="fea2c-207">![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-sql-query-output-bar-chart.png "Customize bar chart")</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fea2c-208">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="fea2c-208">Clean up resources</span></span>

<span data-ttu-id="fea2c-209">After you have finished the article, you can terminate the cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-209">After you have finished the article, you can terminate the cluster.</span></span> <span data-ttu-id="fea2c-210">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span><span class="sxs-lookup"><span data-stu-id="fea2c-210">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span></span> <span data-ttu-id="fea2c-211">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span><span class="sxs-lookup"><span data-stu-id="fea2c-211">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span></span>

<span data-ttu-id="fea2c-212">![Stop a Databricks cluster](./media/quickstart-create-databricks-workspace-portal/terminate-databricks-cluster.png "Stop a Databricks cluster")</span><span class="sxs-lookup"><span data-stu-id="fea2c-212">![Stop a Databricks cluster](./media/quickstart-create-databricks-workspace-portal/terminate-databricks-cluster.png "Stop a Databricks cluster")</span></span>

<span data-ttu-id="fea2c-213">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="fea2c-213">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span></span> <span data-ttu-id="fea2c-214">In such a case, the cluster automatically stops, if it has been inactive for the specified time.</span><span class="sxs-lookup"><span data-stu-id="fea2c-214">In such a case, the cluster automatically stops, if it has been inactive for the specified time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fea2c-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="fea2c-215">Next steps</span></span>

<span data-ttu-id="fea2c-216">In this article, you created a Spark cluster in Azure Databricks and ran a Spark job using data in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="fea2c-216">In this article, you created a Spark cluster in Azure Databricks and ran a Spark job using data in Azure storage.</span></span> <span data-ttu-id="fea2c-217">You can also look at [Spark data sources](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html) to learn how to import data from other data sources into Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="fea2c-217">You can also look at [Spark data sources](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html) to learn how to import data from other data sources into Azure Databricks.</span></span> <span data-ttu-id="fea2c-218">You can also look at the Resource Manager template to [Create an Azure Databricks workspace with custom VNET address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-databricks-workspace-with-custom-vnet-address).</span><span class="sxs-lookup"><span data-stu-id="fea2c-218">You can also look at the Resource Manager template to [Create an Azure Databricks workspace with custom VNET address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-databricks-workspace-with-custom-vnet-address).</span></span>

<span data-ttu-id="fea2c-219">Advance to the next article to learn how to perform an ETL operation (extract, transform, and load data) using Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="fea2c-219">Advance to the next article to learn how to perform an ETL operation (extract, transform, and load data) using Azure Databricks.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="fea2c-220">Extract, transform, and load data using Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="fea2c-220">Extract, transform, and load data using Azure Databricks</span></span>](databricks-extract-load-sql-data-warehouse.md)
