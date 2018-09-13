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
# <a name="quickstart-run-a-spark-job-on-azure-databricks-using-the-azure-resource-manager-template"></a>Quickstart: Run a Spark job on Azure Databricks using the Azure Resource Manager template

This quickstart shows how to create an Azure Databricks workspace using Azure Resource Manager template. You use the workspace to create an Apache Spark cluster and run a Spark job on the Databricks cluster. For more information on Azure Databricks, see [What is Azure Databricks?](what-is-azure-databricks.md)

In this quickstart, as part of the Spark job, you analyze a radio channel subscription data to gain insights into free/paid usage based on demographics.

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.

## <a name="create-an-azure-databricks-workspace"></a>Create an Azure Databricks workspace

In this section, you create an Azure Databricks workspace using the Azure Resource Manager template. 

1. Click the following image to open the template in the Azure portal.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-databricks-workspace%2Fazuredeploy.json" target="_blank"><img src="./media/quickstart-create-databricks-workspace-resource-manager-template/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. Provide the required values to create your Azure Databricks workspace 

    ![Create Azure Databricks workspace using an Azure Resource Manager template](./media/quickstart-create-databricks-workspace-resource-manager-template/create-databricks-workspace-using-resource-manager-template.png "Create Azure Databricks workspace using an Azure Resource Manager template")

    Provide the following values: 
     
    |Property  |Description  |
    |---------|---------|
    |**Subscription**     | From the drop-down, select your Azure subscription.        |
    |**Resource group**     | Specify whether you want to create a new resource group or use an existing one. A resource group is a container that holds related resources for an Azure solution. For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md). |
    |**Location**     | Select **East US 2**. For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).        |
    |**Workspace name**     | Provide a name for your Databricks workspace        |
    |**Pricing Tier**     |  Choose between **Standard** or **Premium**. For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).       |

3. Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.

4. The workspace creation takes a few minutes. During workspace creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side. You may need to scroll right on your dashboard to see the tile. There is also a progress bar displayed near the top of the screen. You can watch either area for progress.

    ![Databricks deployment tile](./media/quickstart-create-databricks-workspace-portal/databricks-deployment-tile.png "Databricks deployment tile")

## <a name="create-a-spark-cluster-in-databricks"></a>Create a Spark cluster in Databricks

1. In the Azure portal, go to the Databricks workspace that you created, and then click **Launch Workspace**.

2. You are redirected to the Azure Databricks portal. From the portal, click **Cluster**.

    ![Databricks on Azure](./media/quickstart-create-databricks-workspace-portal/databricks-on-azure.png "Databricks on Azure")

3. In the **New cluster** page, provide the values to create a cluster.

    ![Create Databricks Spark cluster on Azure](./media/quickstart-create-databricks-workspace-portal/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")

    Accept all other default values other than the following:

    * Enter a name for the cluster.
    * For this article, create a cluster with **4.0** runtime. 
    * Make sure you select the **Terminate after ____ minutes of inactivity** checkbox. Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.
    
    Select **Create cluster**. Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs. 

For more information on creating clusters, see [Create a Spark cluster in Azure Databricks](https://docs.azuredatabricks.net/user-guide/clusters/create.html).

## <a name="run-a-spark-sql-job"></a>Run a Spark SQL job

Before you begin with this section, you must complete the following prerequisites:

* [Create an Azure Blob storage account](../storage/common/storage-quickstart-create-account.md). 
* Download a sample JSON file [from Github](https://github.com/Azure/usql/blob/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json). 
* Upload the sample JSON file to the Azure Blob storage account you created. You can use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload files.

Perform the following tasks to create a notebook in Databricks, configure the notebook to read data from an Azure Blob storage account, and then run a Spark SQL job on the data.

1. In the left pane, click **Workspace**. From the **Workspace** drop-down, click **Create**, and then click **Notebook**.

    ![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-create-notebook.png "Create notebook in Databricks")

2. In the **Create Notebook** dialog box, enter a name, select **Scala** as the language, and select the Spark cluster that you created earlier.

    ![Create notebook in Databricks](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-details.png "Create notebook in Databricks")

    Click **Create**.

3. In this step, associate the Azure Storage account with the Databricks Spark cluster. There are two ways to accomplish this association. You can mount the Azure Storage account to the Databricks Filesystem (DBFS), or directly access the Azure Storage account from the application you create.  

    > [!IMPORTANT]
    >This article uses the approach to **mount the storage with DBFS**. This approach ensures that the mounted storage gets associated with the cluster filesystem itself. Hence, any application accessing the cluster is able to use the associated storage as well. The direct-access approach is limited to the application from where you configure the access.
    >
    > To use the mounting approach, you must create a Spark cluster with Databricks runtime version **4.0**, which is what you chose in this article.

    In the following snippet, replace `{YOUR CONTAINER NAME}`, `{YOUR STORAGE ACCOUNT NAME}`, and `{YOUR STORAGE ACCOUNT ACCESS KEY}` with the appropriate values for your Azure Storage account. Paste the snippet in an empty cell in the notebook and then press SHIFT + ENTER to run the code cell.

    * **Mount the storage account with DBFS (recommended)**. In this snippet, the Azure Storage account path is mounted to `/mnt/mypath`. So, in all future occurrences where you access the Azure Storage account you don't need to give the full path. You can just use `/mnt/mypath`.

          dbutils.fs.mount(
            source = "wasbs://{YOUR CONTAINER NAME}@{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net/",
            mountPoint = "/mnt/mypath",
            extraConfigs = Map("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net" -> "{YOUR STORAGE ACCOUNT ACCESS KEY}"))

    * **Directly access the storage account**

          spark.conf.set("fs.azure.account.key.{YOUR STORAGE ACCOUNT NAME}.blob.core.windows.net", "{YOUR STORAGE ACCOUNT ACCESS KEY}")

    For instructions on how to retrieve the storage account key, see [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    > [!NOTE]
    > You can also use Azure Data Lake Store with a Spark cluster on Azure Databricks. For instructions, see [Use Data Lake Store with Azure Databricks](https://go.microsoft.com/fwlink/?linkid=864084).

4. Run a SQL statement to create a temporary table using data from the sample JSON data file, **small_radio_json.json**. In the following snippet, replace the placeholder values with your container name and storage account name. Paste the snippet in a code cell in the notebook, and then press SHIFT + ENTER. In the snippet, `path` denotes the location of the sample JSON file that you uploaded to your Azure Storage account.

    ```sql
    %sql 
    DROP TABLE IF EXISTS radio_sample_data;
    CREATE TABLE radio_sample_data
    USING json
    OPTIONS (
     path "/mnt/mypath/small_radio_json.json"
    )
    ```

    Once the command successfully completes, you have all the data from the JSON file as a table in Databricks cluster.

    The `%sql` language magic command enables you to run a SQL code from the notebook, even if the notebook is of another type. For more information, see [Mixing languages in a notebook](https://docs.azuredatabricks.net/user-guide/notebooks/index.html#mixing-languages-in-a-notebook).

5. Let's look at a snapshot of the sample JSON data to better understand the query that you run. Paste the following snippet in the code cell and press **SHIFT + ENTER**.

    ```sql
    %sql 
    SELECT * from radio_sample_data
    ```

6. You see a tabular output like shown in the following screenshot (only some columns are shown):

    ![Sample JSON data](./media/quickstart-create-databricks-workspace-portal/databricks-sample-csv-data.png "Sample JSON data")

    Among other details, the sample data captures the gender of the audience of a radio channel (column name, **gender**)  and whether their subscription is free or paid (column name, **level**).

7. You now create a visual representation of this data to show for each gender, how many users have free accounts and how many are paid subscribers. From the bottom of the tabular output, click the **Bar chart** icon, and then click **Plot Options**.

    ![Create bar chart](./media/quickstart-create-databricks-workspace-portal/create-plots-databricks-notebook.png "Create bar chart")

8. In **Customize Plot**, drag-and-drop values as shown in the screenshot.

    ![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-notebook-customize-plot.png "Customize bar chart")

    * Set **Keys** to **gender**.
    * Set **Series groupings** to **level**.
    * Set **Values** to **level**.
    * Set **Aggregation** to **COUNT**.

    Click **Apply**.

9. The output shows the visual representation as depicted in the following screenshot:

     ![Customize bar chart](./media/quickstart-create-databricks-workspace-portal/databricks-sql-query-output-bar-chart.png "Customize bar chart")

## <a name="clean-up-resources"></a>Clean up resources

After you have finished the article, you can terminate the cluster. To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**. For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.

![Stop a Databricks cluster](./media/quickstart-create-databricks-workspace-portal/terminate-databricks-cluster.png "Stop a Databricks cluster")

If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster. In such a case, the cluster automatically stops, if it has been inactive for the specified time.

## <a name="next-steps"></a>Next steps

In this article, you created a Spark cluster in Azure Databricks and ran a Spark job using data in Azure storage. You can also look at [Spark data sources](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html) to learn how to import data from other data sources into Azure Databricks. You can also look at the Resource Manager template to [Create an Azure Databricks workspace with custom VNET address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-databricks-workspace-with-custom-vnet-address).

Advance to the next article to learn how to perform an ETL operation (extract, transform, and load data) using Azure Databricks.

> [!div class="nextstepaction"]
>[Extract, transform, and load data using Azure Databricks](databricks-extract-load-sql-data-warehouse.md)