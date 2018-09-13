---
title: Branching in Azure Data Factory pipeline | Microsoft Docs
description: Learn how to control flow of data in Azure Data Factory by branching and chaining activities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/11/2018
ms.author: shlo
ms.openlocfilehash: 4cb133cc617ecc121fb93a4da816120986e131e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966882"
---
# <a name="branching-and-chaining-activities-in-a-data-factory-pipeline"></a><span data-ttu-id="078df-103">Branching and chaining activities in a Data Factory pipeline</span><span class="sxs-lookup"><span data-stu-id="078df-103">Branching and chaining activities in a Data Factory pipeline</span></span>
<span data-ttu-id="078df-104">In this tutorial, you create a Data Factory pipeline that showcases some of the control flow features.</span><span class="sxs-lookup"><span data-stu-id="078df-104">In this tutorial, you create a Data Factory pipeline that showcases some of the control flow features.</span></span> <span data-ttu-id="078df-105">This pipeline does a simple copy from a container in Azure Blob Storage to another container in the same storage account.</span><span class="sxs-lookup"><span data-stu-id="078df-105">This pipeline does a simple copy from a container in Azure Blob Storage to another container in the same storage account.</span></span> <span data-ttu-id="078df-106">If the copy activity succeeds, the pipeline sends details of the successful copy operation (such as the amount of data written) in a success email.</span><span class="sxs-lookup"><span data-stu-id="078df-106">If the copy activity succeeds, the pipeline sends details of the successful copy operation (such as the amount of data written) in a success email.</span></span> <span data-ttu-id="078df-107">If the copy activity fails, the pipeline sends details of copy failure (such as the error message) in a failure email.</span><span class="sxs-lookup"><span data-stu-id="078df-107">If the copy activity fails, the pipeline sends details of copy failure (such as the error message) in a failure email.</span></span> <span data-ttu-id="078df-108">Throughout the tutorial, you see how to pass parameters.</span><span class="sxs-lookup"><span data-stu-id="078df-108">Throughout the tutorial, you see how to pass parameters.</span></span>

<span data-ttu-id="078df-109">A high-level overview of the scenario: ![Overview](media/tutorial-control-flow-portal/overview.png)</span><span class="sxs-lookup"><span data-stu-id="078df-109">A high-level overview of the scenario: ![Overview](media/tutorial-control-flow-portal/overview.png)</span></span>

<span data-ttu-id="078df-110">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="078df-110">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="078df-111">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="078df-111">Create a data factory.</span></span>
> * <span data-ttu-id="078df-112">Create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="078df-112">Create an Azure Storage linked service.</span></span>
> * <span data-ttu-id="078df-113">Create an Azure Blob dataset</span><span class="sxs-lookup"><span data-stu-id="078df-113">Create an Azure Blob dataset</span></span>
> * <span data-ttu-id="078df-114">Create a pipeline that contains a Copy activity and a Web activity</span><span class="sxs-lookup"><span data-stu-id="078df-114">Create a pipeline that contains a Copy activity and a Web activity</span></span>
> * <span data-ttu-id="078df-115">Send outputs of activities to subsequent activities</span><span class="sxs-lookup"><span data-stu-id="078df-115">Send outputs of activities to subsequent activities</span></span>
> * <span data-ttu-id="078df-116">Utilize parameter passing and system variables</span><span class="sxs-lookup"><span data-stu-id="078df-116">Utilize parameter passing and system variables</span></span>
> * <span data-ttu-id="078df-117">Start a pipeline run</span><span class="sxs-lookup"><span data-stu-id="078df-117">Start a pipeline run</span></span>
> * <span data-ttu-id="078df-118">Monitor the pipeline and activity runs</span><span class="sxs-lookup"><span data-stu-id="078df-118">Monitor the pipeline and activity runs</span></span>

<span data-ttu-id="078df-119">This tutorial uses Azure portal.</span><span class="sxs-lookup"><span data-stu-id="078df-119">This tutorial uses Azure portal.</span></span> <span data-ttu-id="078df-120">You can use other mechanisms to interact with Azure Data Factory, refer to "Quickstarts" in the table of contents.</span><span class="sxs-lookup"><span data-stu-id="078df-120">You can use other mechanisms to interact with Azure Data Factory, refer to "Quickstarts" in the table of contents.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="078df-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="078df-121">Prerequisites</span></span>

* <span data-ttu-id="078df-122">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="078df-122">**Azure subscription**.</span></span> <span data-ttu-id="078df-123">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="078df-123">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>
* <span data-ttu-id="078df-124">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="078df-124">**Azure Storage account**.</span></span> <span data-ttu-id="078df-125">You use the blob storage as **source** data store.</span><span class="sxs-lookup"><span data-stu-id="078df-125">You use the blob storage as **source** data store.</span></span> <span data-ttu-id="078df-126">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="078df-126">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="078df-127">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="078df-127">**Azure SQL Database**.</span></span> <span data-ttu-id="078df-128">You use the database as **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="078df-128">You use the database as **sink** data store.</span></span> <span data-ttu-id="078df-129">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="078df-129">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span></span>

### <a name="create-blob-table"></a><span data-ttu-id="078df-130">Create blob table</span><span class="sxs-lookup"><span data-stu-id="078df-130">Create blob table</span></span>

1. <span data-ttu-id="078df-131">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="078df-131">Launch Notepad.</span></span> <span data-ttu-id="078df-132">Copy the following text and save it as **input.txt** file on your disk.</span><span class="sxs-lookup"><span data-stu-id="078df-132">Copy the following text and save it as **input.txt** file on your disk.</span></span>

    ```
    John,Doe
    Jane,Doe
    ```
2. <span data-ttu-id="078df-133">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-133">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) do the following steps:</span></span> 
    1. <span data-ttu-id="078df-134">Create the **adfv2branch** container.</span><span class="sxs-lookup"><span data-stu-id="078df-134">Create the **adfv2branch** container.</span></span>
    2. <span data-ttu-id="078df-135">Create **input** folder in the **adfv2branch** container.</span><span class="sxs-lookup"><span data-stu-id="078df-135">Create **input** folder in the **adfv2branch** container.</span></span>
    3. <span data-ttu-id="078df-136">Upload **input.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="078df-136">Upload **input.txt** file to the container.</span></span>

## <a name="create-email-workflow-endpoints"></a><span data-ttu-id="078df-137">Create email workflow endpoints</span><span class="sxs-lookup"><span data-stu-id="078df-137">Create email workflow endpoints</span></span>
<span data-ttu-id="078df-138">To trigger sending an email from the pipeline, you use [Logic Apps](../logic-apps/logic-apps-overview.md) to define the workflow.</span><span class="sxs-lookup"><span data-stu-id="078df-138">To trigger sending an email from the pipeline, you use [Logic Apps](../logic-apps/logic-apps-overview.md) to define the workflow.</span></span> <span data-ttu-id="078df-139">For details on creating a Logic App workflow, see [How to create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="078df-139">For details on creating a Logic App workflow, see [How to create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> 

### <a name="success-email-workflow"></a><span data-ttu-id="078df-140">Success email workflow</span><span class="sxs-lookup"><span data-stu-id="078df-140">Success email workflow</span></span> 
<span data-ttu-id="078df-141">Create a Logic App workflow named `CopySuccessEmail`.</span><span class="sxs-lookup"><span data-stu-id="078df-141">Create a Logic App workflow named `CopySuccessEmail`.</span></span> <span data-ttu-id="078df-142">Define the workflow trigger as `When an HTTP request is received`, and add an action of `Office 365 Outlook – Send an email`.</span><span class="sxs-lookup"><span data-stu-id="078df-142">Define the workflow trigger as `When an HTTP request is received`, and add an action of `Office 365 Outlook – Send an email`.</span></span>

![Success email workflow](media/tutorial-control-flow-portal/success-email-workflow.png)

<span data-ttu-id="078df-144">For your request trigger, fill in the `Request Body JSON Schema` with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="078df-144">For your request trigger, fill in the `Request Body JSON Schema` with the following JSON:</span></span>

```json
{
    "properties": {
        "dataFactoryName": {
            "type": "string"
        },
        "message": {
            "type": "string"
        },
        "pipelineName": {
            "type": "string"
        },
        "receiver": {
            "type": "string"
        }
    },
    "type": "object"
}
```

<span data-ttu-id="078df-145">The Request in the Logic App Designer should look like the following image:</span><span class="sxs-lookup"><span data-stu-id="078df-145">The Request in the Logic App Designer should look like the following image:</span></span> 

![Logic App designer - request](media/tutorial-control-flow-portal/logic-app-designer-request.png)

<span data-ttu-id="078df-147">For the **Send Email** action, customize how you wish to format the email, utilizing the properties passed in the request Body JSON schema.</span><span class="sxs-lookup"><span data-stu-id="078df-147">For the **Send Email** action, customize how you wish to format the email, utilizing the properties passed in the request Body JSON schema.</span></span> <span data-ttu-id="078df-148">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="078df-148">Here is an example:</span></span>

![Logic App designer - send email action](media/tutorial-control-flow-portal/send-email-action-2.png)

<span data-ttu-id="078df-150">Save the workflow.</span><span class="sxs-lookup"><span data-stu-id="078df-150">Save the workflow.</span></span> <span data-ttu-id="078df-151">Make a note of your HTTP Post request URL for your success email workflow:</span><span class="sxs-lookup"><span data-stu-id="078df-151">Make a note of your HTTP Post request URL for your success email workflow:</span></span>

```
//Success Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000
```

### <a name="fail-email-workflow"></a><span data-ttu-id="078df-152">Fail email workflow</span><span class="sxs-lookup"><span data-stu-id="078df-152">Fail email workflow</span></span> 
<span data-ttu-id="078df-153">Follow the same steps to create another Logic Apps workflow of **CopyFailEmail**.</span><span class="sxs-lookup"><span data-stu-id="078df-153">Follow the same steps to create another Logic Apps workflow of **CopyFailEmail**.</span></span> <span data-ttu-id="078df-154">In the request trigger, the `Request Body JSON schema` is the same.</span><span class="sxs-lookup"><span data-stu-id="078df-154">In the request trigger, the `Request Body JSON schema` is the same.</span></span> <span data-ttu-id="078df-155">Change the format of your email like the `Subject` to tailor toward a failure email.</span><span class="sxs-lookup"><span data-stu-id="078df-155">Change the format of your email like the `Subject` to tailor toward a failure email.</span></span> <span data-ttu-id="078df-156">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="078df-156">Here is an example:</span></span>

![Logic App designer - fail email workflow](media/tutorial-control-flow-portal/fail-email-workflow-2.png)

<span data-ttu-id="078df-158">Save the workflow.</span><span class="sxs-lookup"><span data-stu-id="078df-158">Save the workflow.</span></span> <span data-ttu-id="078df-159">Make a note of your HTTP Post request URL for your failure email workflow:</span><span class="sxs-lookup"><span data-stu-id="078df-159">Make a note of your HTTP Post request URL for your failure email workflow:</span></span>

```
//Fail Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000
```

<span data-ttu-id="078df-160">You should now have two workflow URLs:</span><span class="sxs-lookup"><span data-stu-id="078df-160">You should now have two workflow URLs:</span></span>

```
//Success Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000

//Fail Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000
```

## <a name="create-a-data-factory"></a><span data-ttu-id="078df-161">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="078df-161">Create a data factory</span></span>

1. <span data-ttu-id="078df-162">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="078df-162">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="078df-163">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="078df-163">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="078df-164">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="078df-164">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-control-flow-portal/new-azure-data-factory-menu.png)
2. <span data-ttu-id="078df-166">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="078df-166">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-control-flow-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="078df-168">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="078df-168">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="078df-169">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="078df-169">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="078df-170">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="078df-170">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name “ADFTutorialDataFactory” is not available`
3. <span data-ttu-id="078df-171">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="078df-171">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="078df-172">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-172">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="078df-173">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="078df-173">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="078df-174">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="078df-174">Select **Create new**, and enter the name of a resource group.</span></span>   
         
        <span data-ttu-id="078df-175">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="078df-175">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="078df-176">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="078df-176">Select **V2** for the **version**.</span></span>
5. <span data-ttu-id="078df-177">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="078df-177">Select the **location** for the data factory.</span></span> <span data-ttu-id="078df-178">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="078df-178">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="078df-179">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="078df-179">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>
6. <span data-ttu-id="078df-180">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="078df-180">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="078df-181">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="078df-181">Click **Create**.</span></span>      
8. <span data-ttu-id="078df-182">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="078df-182">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-control-flow-portal/deploying-data-factory.png)
9. <span data-ttu-id="078df-184">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="078df-184">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
   ![Data factory home page](./media/tutorial-control-flow-portal/data-factory-home-page.png)
10. <span data-ttu-id="078df-186">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="078df-186">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) in a separate tab.</span></span>


## <a name="create-a-pipeline"></a><span data-ttu-id="078df-187">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="078df-187">Create a pipeline</span></span>
<span data-ttu-id="078df-188">In this step, you create a pipeline with one Copy activity and two Web activities.</span><span class="sxs-lookup"><span data-stu-id="078df-188">In this step, you create a pipeline with one Copy activity and two Web activities.</span></span> <span data-ttu-id="078df-189">You use the following features to create the pipeline:</span><span class="sxs-lookup"><span data-stu-id="078df-189">You use the following features to create the pipeline:</span></span>

- <span data-ttu-id="078df-190">Parameters for the pipeline that are access by datasets.</span><span class="sxs-lookup"><span data-stu-id="078df-190">Parameters for the pipeline that are access by datasets.</span></span> 
- <span data-ttu-id="078df-191">Web activity to invoke logic apps workflows to send success/failure emails.</span><span class="sxs-lookup"><span data-stu-id="078df-191">Web activity to invoke logic apps workflows to send success/failure emails.</span></span> 
- <span data-ttu-id="078df-192">Connecting one activity with another activity (on success and failure)</span><span class="sxs-lookup"><span data-stu-id="078df-192">Connecting one activity with another activity (on success and failure)</span></span>
- <span data-ttu-id="078df-193">Using output from an activity as an input to the subsequent activity</span><span class="sxs-lookup"><span data-stu-id="078df-193">Using output from an activity as an input to the subsequent activity</span></span>

1. <span data-ttu-id="078df-194">In the **get started** page of Data Factory UI, click the **Create pipeline** tile.</span><span class="sxs-lookup"><span data-stu-id="078df-194">In the **get started** page of Data Factory UI, click the **Create pipeline** tile.</span></span>  

   ![Get started page](./media/tutorial-control-flow-portal/get-started-page.png) 
3. <span data-ttu-id="078df-196">In the properties window for the pipeline, switch to the **Parameters** tab, and use the **New** button to add the following three parameters of type String: sourceBlobContainer, sinkBlobContainer, and receiver.</span><span class="sxs-lookup"><span data-stu-id="078df-196">In the properties window for the pipeline, switch to the **Parameters** tab, and use the **New** button to add the following three parameters of type String: sourceBlobContainer, sinkBlobContainer, and receiver.</span></span> 

    - <span data-ttu-id="078df-197">**sourceBlobContainer** - parameter in the pipeline consumed by the source blob dataset.</span><span class="sxs-lookup"><span data-stu-id="078df-197">**sourceBlobContainer** - parameter in the pipeline consumed by the source blob dataset.</span></span>
    - <span data-ttu-id="078df-198">**sinkBlobContainer** – parameter in the pipeline consumed by the sink blob dataset</span><span class="sxs-lookup"><span data-stu-id="078df-198">**sinkBlobContainer** – parameter in the pipeline consumed by the sink blob dataset</span></span>
    - <span data-ttu-id="078df-199">**receiver** – this parameter is used by the two Web activities in the pipeline that send success or failure emails to the receiver whose email address is specified by this parameter.</span><span class="sxs-lookup"><span data-stu-id="078df-199">**receiver** – this parameter is used by the two Web activities in the pipeline that send success or failure emails to the receiver whose email address is specified by this parameter.</span></span>

   ![New pipeline menu](./media/tutorial-control-flow-portal/pipeline-parameters.png)
4. <span data-ttu-id="078df-201">In the **Activities** toolbox, expand **Data Flow**, and drag-drop **Copy** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="078df-201">In the **Activities** toolbox, expand **Data Flow**, and drag-drop **Copy** activity to the pipeline designer surface.</span></span> 

   ![Drag-drop copy activity](./media/tutorial-control-flow-portal/drag-drop-copy-activity.png)
5. <span data-ttu-id="078df-203">In the **Properties** window for the **Copy** activity at the bottom, switch to the **Source** tab, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="078df-203">In the **Properties** window for the **Copy** activity at the bottom, switch to the **Source** tab, and click **+ New**.</span></span> <span data-ttu-id="078df-204">You create a source dataset for the copy activity in this step.</span><span class="sxs-lookup"><span data-stu-id="078df-204">You create a source dataset for the copy activity in this step.</span></span> 

   ![Source dataset](./media/tutorial-control-flow-portal/new-source-dataset-button.png)
6. <span data-ttu-id="078df-206">In the **New Dataset** window, select **Azure Blob Storage**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="078df-206">In the **New Dataset** window, select **Azure Blob Storage**, and click **Finish**.</span></span> 

   ![Select Azure Blob Storage](./media/tutorial-control-flow-portal/select-azure-blob-storage.png)
7. <span data-ttu-id="078df-208">You see a new **tab** titled **AzureBlob1**.</span><span class="sxs-lookup"><span data-stu-id="078df-208">You see a new **tab** titled **AzureBlob1**.</span></span> <span data-ttu-id="078df-209">Change the name of the dataset to **SourceBlobDataset**.</span><span class="sxs-lookup"><span data-stu-id="078df-209">Change the name of the dataset to **SourceBlobDataset**.</span></span>

   ![Dataset general settings](./media/tutorial-control-flow-portal/dataset-general-page.png)
8. <span data-ttu-id="078df-211">Switch to the **Connection** tab in the **Properties** window, and click New for the **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="078df-211">Switch to the **Connection** tab in the **Properties** window, and click New for the **Linked service**.</span></span> <span data-ttu-id="078df-212">You create a linked service to link your Azure Storage account to the data factory in this step.</span><span class="sxs-lookup"><span data-stu-id="078df-212">You create a linked service to link your Azure Storage account to the data factory in this step.</span></span> 
    
   ![Dataset connection - new linked service](./media/tutorial-control-flow-portal/dataset-connection-new-button.png)
9. <span data-ttu-id="078df-214">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-214">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="078df-215">Enter **AzureStorageLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="078df-215">Enter **AzureStorageLinkedService** for **Name**.</span></span>
    2. <span data-ttu-id="078df-216">Select your Azure storage account for the **Storage account name**.</span><span class="sxs-lookup"><span data-stu-id="078df-216">Select your Azure storage account for the **Storage account name**.</span></span>
    3. <span data-ttu-id="078df-217">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="078df-217">Click **Save**.</span></span>

   ![New Azure Storage linked service](./media/tutorial-control-flow-portal/new-azure-storage-linked-service.png)
12. <span data-ttu-id="078df-219">Enter `@pipeline().parameters.sourceBlobContainer` for the folder and `emp.txt` for the file name.</span><span class="sxs-lookup"><span data-stu-id="078df-219">Enter `@pipeline().parameters.sourceBlobContainer` for the folder and `emp.txt` for the file name.</span></span> <span data-ttu-id="078df-220">You use the sourceBlobContainer pipeline parameter to set the folder path for the dataset.</span><span class="sxs-lookup"><span data-stu-id="078df-220">You use the sourceBlobContainer pipeline parameter to set the folder path for the dataset.</span></span> 

    ![Source dataset settings](./media/tutorial-control-flow-portal/source-dataset-settings.png)
13. <span data-ttu-id="078df-222">Switch to the **pipeline** tab (or) click the pipeline in the treeview.</span><span class="sxs-lookup"><span data-stu-id="078df-222">Switch to the **pipeline** tab (or) click the pipeline in the treeview.</span></span> <span data-ttu-id="078df-223">Confirm that **SourceBlobDataset** is selected for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="078df-223">Confirm that **SourceBlobDataset** is selected for **Source Dataset**.</span></span> 

   ![Source dataset](./media/tutorial-control-flow-portal/pipeline-source-dataset-selected.png)
13. <span data-ttu-id="078df-225">In the properties window, switch to the **Sink** tab, and click **+ New** for **Sink Dataset**.</span><span class="sxs-lookup"><span data-stu-id="078df-225">In the properties window, switch to the **Sink** tab, and click **+ New** for **Sink Dataset**.</span></span> <span data-ttu-id="078df-226">You create a sink dataset for the copy activity in this step similar to the way you created the source dataset.</span><span class="sxs-lookup"><span data-stu-id="078df-226">You create a sink dataset for the copy activity in this step similar to the way you created the source dataset.</span></span> 

    ![New sink dataset button](./media/tutorial-control-flow-portal/new-sink-dataset-button.png)
14. <span data-ttu-id="078df-228">In the **New Dataset** window, select **Azure Blob Storage**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="078df-228">In the **New Dataset** window, select **Azure Blob Storage**, and click **Finish**.</span></span> 
15. <span data-ttu-id="078df-229">In the **General** settings page for the dataset, enter **SinkBlobDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="078df-229">In the **General** settings page for the dataset, enter **SinkBlobDataset** for **Name**.</span></span>
16. <span data-ttu-id="078df-230">Switch to the **Connection** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-230">Switch to the **Connection** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="078df-231">Select **AzureStorageLinkedService** for **LinkedService**.</span><span class="sxs-lookup"><span data-stu-id="078df-231">Select **AzureStorageLinkedService** for **LinkedService**.</span></span>
    2. <span data-ttu-id="078df-232">Enter `@pipeline().parameters.sinkBlobContainer` for the folder.</span><span class="sxs-lookup"><span data-stu-id="078df-232">Enter `@pipeline().parameters.sinkBlobContainer` for the folder.</span></span>
    1. <span data-ttu-id="078df-233">Enter `@CONCAT(pipeline().RunId, '.txt')` for the file name.</span><span class="sxs-lookup"><span data-stu-id="078df-233">Enter `@CONCAT(pipeline().RunId, '.txt')` for the file name.</span></span> <span data-ttu-id="078df-234">The expression uses the ID of the current pipeline run for the file name.</span><span class="sxs-lookup"><span data-stu-id="078df-234">The expression uses the ID of the current pipeline run for the file name.</span></span> <span data-ttu-id="078df-235">For the supported list of system variables and expressions, see [System variables](control-flow-system-variables.md) and [Expression language](control-flow-expression-language-functions.md).</span><span class="sxs-lookup"><span data-stu-id="078df-235">For the supported list of system variables and expressions, see [System variables](control-flow-system-variables.md) and [Expression language](control-flow-expression-language-functions.md).</span></span>

        ![Sink dataset settings](./media/tutorial-control-flow-portal/sink-dataset-settings.png)
17. <span data-ttu-id="078df-237">Switch to the **pipeline** tab at the top.</span><span class="sxs-lookup"><span data-stu-id="078df-237">Switch to the **pipeline** tab at the top.</span></span> <span data-ttu-id="078df-238">Expand **General** in the **Activities** toolbox, and drag-drop a **Web** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="078df-238">Expand **General** in the **Activities** toolbox, and drag-drop a **Web** activity to the pipeline designer surface.</span></span> <span data-ttu-id="078df-239">Set the name of the activity to **SendSuccessEmailActivity**.</span><span class="sxs-lookup"><span data-stu-id="078df-239">Set the name of the activity to **SendSuccessEmailActivity**.</span></span> <span data-ttu-id="078df-240">The Web Activity allows a call to any REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="078df-240">The Web Activity allows a call to any REST endpoint.</span></span> <span data-ttu-id="078df-241">For more information about the activity, see [Web Activity](control-flow-web-activity.md).</span><span class="sxs-lookup"><span data-stu-id="078df-241">For more information about the activity, see [Web Activity](control-flow-web-activity.md).</span></span> <span data-ttu-id="078df-242">This pipeline uses a Web Activity to call the Logic Apps email workflow.</span><span class="sxs-lookup"><span data-stu-id="078df-242">This pipeline uses a Web Activity to call the Logic Apps email workflow.</span></span> 

   ![Drag-drop first Web activity](./media/tutorial-control-flow-portal/success-web-activity-general.png)
18. <span data-ttu-id="078df-244">Switch to the **Settings** tab from the **General** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-244">Switch to the **Settings** tab from the **General** tab, and do the following steps:</span></span> 
    1. <span data-ttu-id="078df-245">For **URL**, specify URL for the logic apps workflow that sends the success email.</span><span class="sxs-lookup"><span data-stu-id="078df-245">For **URL**, specify URL for the logic apps workflow that sends the success email.</span></span>  
    2. <span data-ttu-id="078df-246">Select **POST** for **Method**.</span><span class="sxs-lookup"><span data-stu-id="078df-246">Select **POST** for **Method**.</span></span> 
    3. <span data-ttu-id="078df-247">Click **+ Add header** link in the **Headers** section.</span><span class="sxs-lookup"><span data-stu-id="078df-247">Click **+ Add header** link in the **Headers** section.</span></span> 
    4. <span data-ttu-id="078df-248">Add a header **Content-Type** and set it to **application/json**.</span><span class="sxs-lookup"><span data-stu-id="078df-248">Add a header **Content-Type** and set it to **application/json**.</span></span> 
    5. <span data-ttu-id="078df-249">Specify the following JSON for **Body**.</span><span class="sxs-lookup"><span data-stu-id="078df-249">Specify the following JSON for **Body**.</span></span> 

        ```json
        {
            "message": "@{activity('Copy1').output.dataWritten}",
            "dataFactoryName": "@{pipeline().DataFactory}",
            "pipelineName": "@{pipeline().Pipeline}",
            "receiver": "@pipeline().parameters.receiver"
        }
        ```
        <span data-ttu-id="078df-250">The message body contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="078df-250">The message body contains the following properties:</span></span>

        - <span data-ttu-id="078df-251">Message – Passing value of `@{activity('Copy1').output.dataWritten`.</span><span class="sxs-lookup"><span data-stu-id="078df-251">Message – Passing value of `@{activity('Copy1').output.dataWritten`.</span></span> <span data-ttu-id="078df-252">Accesses a property of the previous copy activity and passes the value of dataWritten.</span><span class="sxs-lookup"><span data-stu-id="078df-252">Accesses a property of the previous copy activity and passes the value of dataWritten.</span></span> <span data-ttu-id="078df-253">For the failure case, pass the error output instead of `@{activity('CopyBlobtoBlob').error.message`.</span><span class="sxs-lookup"><span data-stu-id="078df-253">For the failure case, pass the error output instead of `@{activity('CopyBlobtoBlob').error.message`.</span></span>
        - <span data-ttu-id="078df-254">Data Factory Name – Passing value of `@{pipeline().DataFactory}` This is a system variable, allowing you to access the corresponding data factory name.</span><span class="sxs-lookup"><span data-stu-id="078df-254">Data Factory Name – Passing value of `@{pipeline().DataFactory}` This is a system variable, allowing you to access the corresponding data factory name.</span></span> <span data-ttu-id="078df-255">For a list of system variables, see [System Variables](control-flow-system-variables.md) article.</span><span class="sxs-lookup"><span data-stu-id="078df-255">For a list of system variables, see [System Variables](control-flow-system-variables.md) article.</span></span>
        - <span data-ttu-id="078df-256">Pipeline Name – Passing value of `@{pipeline().Pipeline}`.</span><span class="sxs-lookup"><span data-stu-id="078df-256">Pipeline Name – Passing value of `@{pipeline().Pipeline}`.</span></span> <span data-ttu-id="078df-257">This is also a system variable, allowing you to access the corresponding pipeline name.</span><span class="sxs-lookup"><span data-stu-id="078df-257">This is also a system variable, allowing you to access the corresponding pipeline name.</span></span> 
        - <span data-ttu-id="078df-258">Receiver – Passing value of "\@pipeline().parameters.receiver").</span><span class="sxs-lookup"><span data-stu-id="078df-258">Receiver – Passing value of "\@pipeline().parameters.receiver").</span></span> <span data-ttu-id="078df-259">Accessing the pipeline parameters.</span><span class="sxs-lookup"><span data-stu-id="078df-259">Accessing the pipeline parameters.</span></span>
    
        ![Settings for the first Web activity](./media/tutorial-control-flow-portal/web-activity1-settings.png)         
19. <span data-ttu-id="078df-261">Connect the **Copy** activity to the **Web** activity by dragging the green button next to the Copy activity and dropping on the Web activity.</span><span class="sxs-lookup"><span data-stu-id="078df-261">Connect the **Copy** activity to the **Web** activity by dragging the green button next to the Copy activity and dropping on the Web activity.</span></span> 

    ![Connect Copy activity with the first Web activity](./media/tutorial-control-flow-portal/connect-copy-web-activity1.png)
20. <span data-ttu-id="078df-263">Drag-drop another **Web** activity from the Activities toolbox to the pipeline designer surface, and set the **name** to **SendFailureEmailActivity**.</span><span class="sxs-lookup"><span data-stu-id="078df-263">Drag-drop another **Web** activity from the Activities toolbox to the pipeline designer surface, and set the **name** to **SendFailureEmailActivity**.</span></span>

    ![Name of the second Web activity](./media/tutorial-control-flow-portal/web-activity2-name.png)
21. <span data-ttu-id="078df-265">Switch to the **Settings** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-265">Switch to the **Settings** tab, and do the following steps:</span></span>

    1. <span data-ttu-id="078df-266">For **URL**, specify URL for the logic apps workflow that sends the failure email.</span><span class="sxs-lookup"><span data-stu-id="078df-266">For **URL**, specify URL for the logic apps workflow that sends the failure email.</span></span>  
    2. <span data-ttu-id="078df-267">Select **POST** for **Method**.</span><span class="sxs-lookup"><span data-stu-id="078df-267">Select **POST** for **Method**.</span></span> 
    3. <span data-ttu-id="078df-268">Click **+ Add header** link in the **Headers** section.</span><span class="sxs-lookup"><span data-stu-id="078df-268">Click **+ Add header** link in the **Headers** section.</span></span> 
    4. <span data-ttu-id="078df-269">Add a header **Content-Type** and set it to **application/json**.</span><span class="sxs-lookup"><span data-stu-id="078df-269">Add a header **Content-Type** and set it to **application/json**.</span></span> 
    5. <span data-ttu-id="078df-270">Specify the following JSON for **Body**.</span><span class="sxs-lookup"><span data-stu-id="078df-270">Specify the following JSON for **Body**.</span></span> 

        ```json
        {
            "message": "@{activity('Copy1').error.message}",
            "dataFactoryName": "@{pipeline().DataFactory}",
            "pipelineName": "@{pipeline().Pipeline}",
            "receiver": "@pipeline().parameters.receiver"
        }
        ```

        ![Settings for the second Web activity](./media/tutorial-control-flow-portal/web-activity2-settings.png)         
22. <span data-ttu-id="078df-272">Select **Copy** activity in the pipeline designer, and click **+->** button, and select **Error**.</span><span class="sxs-lookup"><span data-stu-id="078df-272">Select **Copy** activity in the pipeline designer, and click **+->** button, and select **Error**.</span></span>  

    ![Settings for the second Web activity](./media/tutorial-control-flow-portal/select-copy-failure-link.png)
23. <span data-ttu-id="078df-274">Drag the **red** button next to the Copy activity to the second Web activity **SendFailureEmailActivity**.</span><span class="sxs-lookup"><span data-stu-id="078df-274">Drag the **red** button next to the Copy activity to the second Web activity **SendFailureEmailActivity**.</span></span> <span data-ttu-id="078df-275">You can move the activities around so that the pipeline looks like in the following image:</span><span class="sxs-lookup"><span data-stu-id="078df-275">You can move the activities around so that the pipeline looks like in the following image:</span></span> 

    ![Full pipeline with all activities](./media/tutorial-control-flow-portal/full-pipeline.png)
24. <span data-ttu-id="078df-277">To validate the pipeline, click **Validate** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="078df-277">To validate the pipeline, click **Validate** button on the toolbar.</span></span> <span data-ttu-id="078df-278">Close the **Pipeline Validation Output** window by clicking the **>>** button.</span><span class="sxs-lookup"><span data-stu-id="078df-278">Close the **Pipeline Validation Output** window by clicking the **>>** button.</span></span>

    ![Validate pipeline](./media/tutorial-control-flow-portal/validate-pipeline.png)
24. <span data-ttu-id="078df-280">To publish the entities (datasets, pipelines, etc.) to Data Factory service, select **Publish All**.</span><span class="sxs-lookup"><span data-stu-id="078df-280">To publish the entities (datasets, pipelines, etc.) to Data Factory service, select **Publish All**.</span></span> <span data-ttu-id="078df-281">Wait until you see the **Successfully published** message.</span><span class="sxs-lookup"><span data-stu-id="078df-281">Wait until you see the **Successfully published** message.</span></span>

    ![Publish](./media/tutorial-control-flow-portal/publish-button.png)
 
## <a name="trigger-a-pipeline-run-that-succeeds"></a><span data-ttu-id="078df-283">Trigger a pipeline run that succeeds</span><span class="sxs-lookup"><span data-stu-id="078df-283">Trigger a pipeline run that succeeds</span></span>
1. <span data-ttu-id="078df-284">To **trigger** a pipeline run, click **Trigger** on the toolbar, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="078df-284">To **trigger** a pipeline run, click **Trigger** on the toolbar, and click **Trigger Now**.</span></span> 

    ![Trigger a pipeline run](./media/tutorial-control-flow-portal/trigger-now-menu.png)
2. <span data-ttu-id="078df-286">In the **Pipeline Run** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-286">In the **Pipeline Run** window, do the following steps:</span></span> 

    1. <span data-ttu-id="078df-287">Enter **adftutorial/adfv2branch/input** for the **sourceBlobContainer** parameter.</span><span class="sxs-lookup"><span data-stu-id="078df-287">Enter **adftutorial/adfv2branch/input** for the **sourceBlobContainer** parameter.</span></span> 
    2. <span data-ttu-id="078df-288">Enter **adftutorial/adfv2branch/output** for the **sinkBlobContainer** parameter.</span><span class="sxs-lookup"><span data-stu-id="078df-288">Enter **adftutorial/adfv2branch/output** for the **sinkBlobContainer** parameter.</span></span> 
    3. <span data-ttu-id="078df-289">Enter an **email address** of the **receiver**.</span><span class="sxs-lookup"><span data-stu-id="078df-289">Enter an **email address** of the **receiver**.</span></span> 
    4. <span data-ttu-id="078df-290">Click **Finish**</span><span class="sxs-lookup"><span data-stu-id="078df-290">Click **Finish**</span></span>

        ![Pipeline run parameters](./media/tutorial-control-flow-portal/pipeline-run-parameters.png)

## <a name="monitor-the-successful-pipeline-run"></a><span data-ttu-id="078df-292">Monitor the successful pipeline run</span><span class="sxs-lookup"><span data-stu-id="078df-292">Monitor the successful pipeline run</span></span>

1. <span data-ttu-id="078df-293">To monitor the pipeline run, switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="078df-293">To monitor the pipeline run, switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="078df-294">You see the pipeline run that was triggered manually by you.</span><span class="sxs-lookup"><span data-stu-id="078df-294">You see the pipeline run that was triggered manually by you.</span></span> <span data-ttu-id="078df-295">Use the **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="078df-295">Use the **Refresh** button to refresh the list.</span></span> 
    
    ![Successful pipeline run](./media/tutorial-control-flow-portal/monitor-success-pipeline-run.png)
2. <span data-ttu-id="078df-297">To **view activity runs** associated with this pipeline run, click the first link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="078df-297">To **view activity runs** associated with this pipeline run, click the first link in the **Actions** column.</span></span> <span data-ttu-id="078df-298">You can switch back to the previous view by clicking **Pipelines** at the top.</span><span class="sxs-lookup"><span data-stu-id="078df-298">You can switch back to the previous view by clicking **Pipelines** at the top.</span></span> <span data-ttu-id="078df-299">Use the **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="078df-299">Use the **Refresh** button to refresh the list.</span></span> 

    ![Activity runs](./media/tutorial-control-flow-portal/activity-runs-success.png)

## <a name="trigger-a-pipeline-run-that-fails"></a><span data-ttu-id="078df-301">Trigger a pipeline run that fails</span><span class="sxs-lookup"><span data-stu-id="078df-301">Trigger a pipeline run that fails</span></span>
1. <span data-ttu-id="078df-302">Switch to the **Edit** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="078df-302">Switch to the **Edit** tab on the left.</span></span> 
2. <span data-ttu-id="078df-303">To **trigger** a pipeline run, click **Trigger** on the toolbar, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="078df-303">To **trigger** a pipeline run, click **Trigger** on the toolbar, and click **Trigger Now**.</span></span> 
3. <span data-ttu-id="078df-304">In the **Pipeline Run** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="078df-304">In the **Pipeline Run** window, do the following steps:</span></span> 

    1. <span data-ttu-id="078df-305">Enter **adftutorial/dummy/input** for the **sourceBlobContainer** parameter.</span><span class="sxs-lookup"><span data-stu-id="078df-305">Enter **adftutorial/dummy/input** for the **sourceBlobContainer** parameter.</span></span> <span data-ttu-id="078df-306">Ensure that the dummy folder does not exist in the adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="078df-306">Ensure that the dummy folder does not exist in the adftutorial container.</span></span> 
    2. <span data-ttu-id="078df-307">Enter **adftutorial/dummy/output** for the **sinkBlobContainer** parameter.</span><span class="sxs-lookup"><span data-stu-id="078df-307">Enter **adftutorial/dummy/output** for the **sinkBlobContainer** parameter.</span></span> 
    3. <span data-ttu-id="078df-308">Enter an **email address** of the **receiver**.</span><span class="sxs-lookup"><span data-stu-id="078df-308">Enter an **email address** of the **receiver**.</span></span> 
    4. <span data-ttu-id="078df-309">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="078df-309">Click **Finish**.</span></span>

## <a name="monitor-the-failed-pipeline-run"></a><span data-ttu-id="078df-310">Monitor the failed pipeline run</span><span class="sxs-lookup"><span data-stu-id="078df-310">Monitor the failed pipeline run</span></span>

1. <span data-ttu-id="078df-311">To monitor the pipeline run, switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="078df-311">To monitor the pipeline run, switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="078df-312">You see the pipeline run that was triggered manually by you.</span><span class="sxs-lookup"><span data-stu-id="078df-312">You see the pipeline run that was triggered manually by you.</span></span> <span data-ttu-id="078df-313">Use the **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="078df-313">Use the **Refresh** button to refresh the list.</span></span> 
    
    ![Failure pipeline run](./media/tutorial-control-flow-portal/monitor-failure-pipeline-run.png)
2. <span data-ttu-id="078df-315">Click **Error** link for the pipeline run to see details about the error.</span><span class="sxs-lookup"><span data-stu-id="078df-315">Click **Error** link for the pipeline run to see details about the error.</span></span> 

    ![Pipeline error](./media/tutorial-control-flow-portal/pipeline-error-message.png)
2. <span data-ttu-id="078df-317">To **view activity runs** associated with this pipeline run, click the first link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="078df-317">To **view activity runs** associated with this pipeline run, click the first link in the **Actions** column.</span></span> <span data-ttu-id="078df-318">Use the **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="078df-318">Use the **Refresh** button to refresh the list.</span></span> <span data-ttu-id="078df-319">Notice that the Copy activity in the pipeline failed.</span><span class="sxs-lookup"><span data-stu-id="078df-319">Notice that the Copy activity in the pipeline failed.</span></span> <span data-ttu-id="078df-320">The Web activity succeeded to send the failure email to the specified receiver.</span><span class="sxs-lookup"><span data-stu-id="078df-320">The Web activity succeeded to send the failure email to the specified receiver.</span></span> 

    ![Activity runs](./media/tutorial-control-flow-portal/activity-runs-failure.png)
4. <span data-ttu-id="078df-322">Click **Error** link in the **Actions** column to see details about the error.</span><span class="sxs-lookup"><span data-stu-id="078df-322">Click **Error** link in the **Actions** column to see details about the error.</span></span> 

    ![Activity run error](./media/tutorial-control-flow-portal/activity-run-error.png)

## <a name="next-steps"></a><span data-ttu-id="078df-324">Next steps</span><span class="sxs-lookup"><span data-stu-id="078df-324">Next steps</span></span>
<span data-ttu-id="078df-325">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="078df-325">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="078df-326">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="078df-326">Create a data factory.</span></span>
> * <span data-ttu-id="078df-327">Create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="078df-327">Create an Azure Storage linked service.</span></span>
> * <span data-ttu-id="078df-328">Create an Azure Blob dataset</span><span class="sxs-lookup"><span data-stu-id="078df-328">Create an Azure Blob dataset</span></span>
> * <span data-ttu-id="078df-329">Create a pipeline that contains a copy activity and a web activity</span><span class="sxs-lookup"><span data-stu-id="078df-329">Create a pipeline that contains a copy activity and a web activity</span></span>
> * <span data-ttu-id="078df-330">Send outputs of activities to subsequent activities</span><span class="sxs-lookup"><span data-stu-id="078df-330">Send outputs of activities to subsequent activities</span></span>
> * <span data-ttu-id="078df-331">Utilize parameter passing and system variables</span><span class="sxs-lookup"><span data-stu-id="078df-331">Utilize parameter passing and system variables</span></span>
> * <span data-ttu-id="078df-332">Start a pipeline run</span><span class="sxs-lookup"><span data-stu-id="078df-332">Start a pipeline run</span></span>
> * <span data-ttu-id="078df-333">Monitor the pipeline and activity runs</span><span class="sxs-lookup"><span data-stu-id="078df-333">Monitor the pipeline and activity runs</span></span>

<span data-ttu-id="078df-334">You can now proceed to the Concepts section for more information about Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="078df-334">You can now proceed to the Concepts section for more information about Azure Data Factory.</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="078df-335">Pipelines and activities</span><span class="sxs-lookup"><span data-stu-id="078df-335">Pipelines and activities</span></span>](concepts-pipelines-activities.md)
