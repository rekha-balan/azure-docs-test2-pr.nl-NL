---
title: Using Import/Export Data in Azure Machine Learning web services | Microsoft Docs
description: Learn how to use the Import Data and Export Data modules to send and receive data from a web service.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondlaghaeian
editor: ''
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: f269542b9a0dbd727ce88ed7737c0b2d458e3628
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661907"
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="35892-103">Deploying Azure ML web services that use Data Import and Data Export modules</span><span class="sxs-lookup"><span data-stu-id="35892-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="35892-104">When you create a predictive experiment, you typically add a web service input and output.</span><span class="sxs-lookup"><span data-stu-id="35892-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="35892-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="35892-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span></span> <span data-ttu-id="35892-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="35892-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="35892-107">In these cases, they do not need read and write data using web service inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="35892-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="35892-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span><span class="sxs-lookup"><span data-stu-id="35892-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span></span>

<span data-ttu-id="35892-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premise SQL database.</span><span class="sxs-lookup"><span data-stu-id="35892-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premise SQL database.</span></span>

<span data-ttu-id="35892-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span><span class="sxs-lookup"><span data-stu-id="35892-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-the-training-experiment"></a><span data-ttu-id="35892-111">Create the training experiment</span><span class="sxs-lookup"><span data-stu-id="35892-111">Create the training experiment</span></span>
<span data-ttu-id="35892-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span><span class="sxs-lookup"><span data-stu-id="35892-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="35892-113">And the experiment in the canvas will look similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="35892-113">And the experiment in the canvas will look similar to the following image:</span></span>

![Initial configuration of the experiment.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="35892-115">To read the data from the Azure SQL table:</span><span class="sxs-lookup"><span data-stu-id="35892-115">To read the data from the Azure SQL table:</span></span>

1. <span data-ttu-id="35892-116">Delete the dataset module.</span><span class="sxs-lookup"><span data-stu-id="35892-116">Delete the dataset module.</span></span>
2. <span data-ttu-id="35892-117">In the components search box, type import.</span><span class="sxs-lookup"><span data-stu-id="35892-117">In the components search box, type import.</span></span>
3. <span data-ttu-id="35892-118">From the results list, add an *Import Data* module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="35892-118">From the results list, add an *Import Data* module to the experiment canvas.</span></span>
4. <span data-ttu-id="35892-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="35892-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="35892-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span><span class="sxs-lookup"><span data-stu-id="35892-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span></span>
6. <span data-ttu-id="35892-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span><span class="sxs-lookup"><span data-stu-id="35892-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span></span>
7. <span data-ttu-id="35892-122">In the Database query field, enter the following query.</span><span class="sxs-lookup"><span data-stu-id="35892-122">In the Database query field, enter the following query.</span></span>
   
     <span data-ttu-id="35892-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="35892-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="35892-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="35892-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="35892-125">At the bottom of the experiment canvas, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="35892-125">At the bottom of the experiment canvas, click **Run**.</span></span>

## <a name="create-the-predictive-experiment"></a><span data-ttu-id="35892-126">Create the predictive experiment</span><span class="sxs-lookup"><span data-stu-id="35892-126">Create the predictive experiment</span></span>
<span data-ttu-id="35892-127">Next you set up the predictive experiment from which you deploy your web service.</span><span class="sxs-lookup"><span data-stu-id="35892-127">Next you set up the predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="35892-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span><span class="sxs-lookup"><span data-stu-id="35892-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="35892-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="35892-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span></span> 
3. <span data-ttu-id="35892-130">In the components search box, type export.</span><span class="sxs-lookup"><span data-stu-id="35892-130">In the components search box, type export.</span></span>
4. <span data-ttu-id="35892-131">From the results list, add an *Export Data* module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="35892-131">From the results list, add an *Export Data* module to the experiment canvas.</span></span>
5. <span data-ttu-id="35892-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span><span class="sxs-lookup"><span data-stu-id="35892-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span></span> 
6. <span data-ttu-id="35892-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span><span class="sxs-lookup"><span data-stu-id="35892-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span></span>
7. <span data-ttu-id="35892-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span><span class="sxs-lookup"><span data-stu-id="35892-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span></span>
8. <span data-ttu-id="35892-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="35892-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="35892-136">In the **Data table name field**, type dbo.ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="35892-136">In the **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="35892-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span><span class="sxs-lookup"><span data-stu-id="35892-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span></span>
10. <span data-ttu-id="35892-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="35892-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="35892-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span><span class="sxs-lookup"><span data-stu-id="35892-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span></span> <span data-ttu-id="35892-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span><span class="sxs-lookup"><span data-stu-id="35892-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span></span>  <span data-ttu-id="35892-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span><span class="sxs-lookup"><span data-stu-id="35892-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="35892-142">To configure the Web Service Parameters for the import query and the destination table:</span><span class="sxs-lookup"><span data-stu-id="35892-142">To configure the Web Service Parameters for the import query and the destination table:</span></span>

1. <span data-ttu-id="35892-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span><span class="sxs-lookup"><span data-stu-id="35892-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="35892-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span><span class="sxs-lookup"><span data-stu-id="35892-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="35892-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span><span class="sxs-lookup"><span data-stu-id="35892-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="35892-146">Click **Data table name** and rename it **Table**.</span><span class="sxs-lookup"><span data-stu-id="35892-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="35892-147">When you are done, your experiment should look similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="35892-147">When you are done, your experiment should look similar to the following image:</span></span>

![Final look of experiment.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="35892-149">Now you can deploy the experiment as a web service.</span><span class="sxs-lookup"><span data-stu-id="35892-149">Now you can deploy the experiment as a web service.</span></span>

## <a name="deploy-the-web-service"></a><span data-ttu-id="35892-150">Deploy the web service</span><span class="sxs-lookup"><span data-stu-id="35892-150">Deploy the web service</span></span>
<span data-ttu-id="35892-151">You can deploy to either a Classic or New web service.</span><span class="sxs-lookup"><span data-stu-id="35892-151">You can deploy to either a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="35892-152">Deploy a Classic Web Service</span><span class="sxs-lookup"><span data-stu-id="35892-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="35892-153">To deploy as a Classic Web Service and create an application to consume it:</span><span class="sxs-lookup"><span data-stu-id="35892-153">To deploy as a Classic Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="35892-154">At the bottom of the experiment canvas, click Run.</span><span class="sxs-lookup"><span data-stu-id="35892-154">At the bottom of the experiment canvas, click Run.</span></span>
2. <span data-ttu-id="35892-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span><span class="sxs-lookup"><span data-stu-id="35892-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="35892-156">On the web service dashboard, locate your API key.</span><span class="sxs-lookup"><span data-stu-id="35892-156">On the web service dashboard, locate your API key.</span></span> <span data-ttu-id="35892-157">Copy and save it to use later.</span><span class="sxs-lookup"><span data-stu-id="35892-157">Copy and save it to use later.</span></span>
4. <span data-ttu-id="35892-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span><span class="sxs-lookup"><span data-stu-id="35892-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span></span>
5. <span data-ttu-id="35892-159">In Visual Studio, create a C# console application.</span><span class="sxs-lookup"><span data-stu-id="35892-159">In Visual Studio, create a C# console application.</span></span>
6. <span data-ttu-id="35892-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="35892-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span></span>
7. <span data-ttu-id="35892-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span><span class="sxs-lookup"><span data-stu-id="35892-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span></span>
8. <span data-ttu-id="35892-162">Update the value of the *apiKey* variable with the API key saved earlier.</span><span class="sxs-lookup"><span data-stu-id="35892-162">Update the value of the *apiKey* variable with the API key saved earlier.</span></span>
9. <span data-ttu-id="35892-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span><span class="sxs-lookup"><span data-stu-id="35892-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="35892-164">In this case, you use the original query, but define a new table name.</span><span class="sxs-lookup"><span data-stu-id="35892-164">In this case, you use the original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="35892-165">Run the application.</span><span class="sxs-lookup"><span data-stu-id="35892-165">Run the application.</span></span> 

<span data-ttu-id="35892-166">On completion of the run, a new table is added to the database containing the scoring results.</span><span class="sxs-lookup"><span data-stu-id="35892-166">On completion of the run, a new table is added to the database containing the scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="35892-167">Deploy a New Web Service</span><span class="sxs-lookup"><span data-stu-id="35892-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="35892-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="35892-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="35892-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="35892-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="35892-170">To deploy as a New Web Service and create an application to consume it:</span><span class="sxs-lookup"><span data-stu-id="35892-170">To deploy as a New Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="35892-171">At the bottom of the experiment canvas, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="35892-171">At the bottom of the experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="35892-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="35892-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="35892-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="35892-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="35892-174">On the **Quickstart** page, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="35892-174">On the **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="35892-175">In the **Sample Code** section, click **Batch**.</span><span class="sxs-lookup"><span data-stu-id="35892-175">In the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="35892-176">In Visual Studio, create a C# console application.</span><span class="sxs-lookup"><span data-stu-id="35892-176">In Visual Studio, create a C# console application.</span></span>
7. <span data-ttu-id="35892-177">Copy and paste the C# sample code into your Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="35892-177">Copy and paste the C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="35892-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span><span class="sxs-lookup"><span data-stu-id="35892-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span></span>
9. <span data-ttu-id="35892-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span><span class="sxs-lookup"><span data-stu-id="35892-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="35892-180">In this case, you use the original query, but define a new table name.</span><span class="sxs-lookup"><span data-stu-id="35892-180">In this case, you use the original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="35892-181">Run the application.</span><span class="sxs-lookup"><span data-stu-id="35892-181">Run the application.</span></span> 



