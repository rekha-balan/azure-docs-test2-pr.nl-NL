---
title: Create a data pipeline with the Azure Log Analytics Data Collector API | Microsoft Docs
description: You can use the Log Analytics HTTP Data Collector API to add POST JSON data to the Log Analytics repository from any client that can call the REST API. This article describes how to upload data stored in files in an automated way.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/09/2018
ms.author: magoedte
ms.component: ''
ms.openlocfilehash: 180f1a39b92dd699fa114cb98a5842b0ab0dc89a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868378"
---
# <a name="create-a-data-pipeline-with-the-data-collector-api"></a><span data-ttu-id="7a197-104">Create a data pipeline with the Data Collector API</span><span class="sxs-lookup"><span data-stu-id="7a197-104">Create a data pipeline with the Data Collector API</span></span>

<span data-ttu-id="7a197-105">The [Log Analytics Data Collector API](log-analytics-data-collector-api.md) allows you to import any custom data into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7a197-105">The [Log Analytics Data Collector API](log-analytics-data-collector-api.md) allows you to import any custom data into Log Analytics.</span></span> <span data-ttu-id="7a197-106">The only requirements are that the data be JSON-formatted and split into 30 MB or less segments.</span><span class="sxs-lookup"><span data-stu-id="7a197-106">The only requirements are that the data be JSON-formatted and split into 30 MB or less segments.</span></span> <span data-ttu-id="7a197-107">This is a completely flexible mechanism that can be plugged into in many ways: from data being sent directly from your application, to one-off adhoc uploads.</span><span class="sxs-lookup"><span data-stu-id="7a197-107">This is a completely flexible mechanism that can be plugged into in many ways: from data being sent directly from your application, to one-off adhoc uploads.</span></span> <span data-ttu-id="7a197-108">This article will outline some starting points for a common scenario: the need to upload data stored in files on a regular, automated basis.</span><span class="sxs-lookup"><span data-stu-id="7a197-108">This article will outline some starting points for a common scenario: the need to upload data stored in files on a regular, automated basis.</span></span> <span data-ttu-id="7a197-109">While the pipeline presented here will not be the most performant or otherwise optimized, it is intended to serve as a starting point towards building a production pipeline of your own.</span><span class="sxs-lookup"><span data-stu-id="7a197-109">While the pipeline presented here will not be the most performant or otherwise optimized, it is intended to serve as a starting point towards building a production pipeline of your own.</span></span>

## <a name="example-problem"></a><span data-ttu-id="7a197-110">Example problem</span><span class="sxs-lookup"><span data-stu-id="7a197-110">Example problem</span></span>
<span data-ttu-id="7a197-111">For the remainder of this article, we will examine page view data in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7a197-111">For the remainder of this article, we will examine page view data in Application Insights.</span></span> <span data-ttu-id="7a197-112">In our hypothetical scenario, we want to correlate geographical information collected by default by the Application Insights SDK to custom data containing the population of every country in the world, with the goal of identifying where we should be spending the most marketing dollars.</span><span class="sxs-lookup"><span data-stu-id="7a197-112">In our hypothetical scenario, we want to correlate geographical information collected by default by the Application Insights SDK to custom data containing the population of every country in the world, with the goal of identifying where we should be spending the most marketing dollars.</span></span> 

<span data-ttu-id="7a197-113">We use a public data source such as the [UN World Population Prospects](https://esa.un.org/unpd/wpp/) for this purpose.</span><span class="sxs-lookup"><span data-stu-id="7a197-113">We use a public data source such as the [UN World Population Prospects](https://esa.un.org/unpd/wpp/) for this purpose.</span></span> <span data-ttu-id="7a197-114">The data will have the following simple schema:</span><span class="sxs-lookup"><span data-stu-id="7a197-114">The data will have the following simple schema:</span></span>

![Example simple schema](./media/log-analytics-create-pipeline-datacollector-api/example-simple-schema-01.png)

<span data-ttu-id="7a197-116">In our example, we assume that we will upload a new file with the latest year’s data as soon as it becomes available.</span><span class="sxs-lookup"><span data-stu-id="7a197-116">In our example, we assume that we will upload a new file with the latest year’s data as soon as it becomes available.</span></span>

## <a name="general-design"></a><span data-ttu-id="7a197-117">General design</span><span class="sxs-lookup"><span data-stu-id="7a197-117">General design</span></span>
<span data-ttu-id="7a197-118">We are using a classic ETL-type logic to design our pipeline.</span><span class="sxs-lookup"><span data-stu-id="7a197-118">We are using a classic ETL-type logic to design our pipeline.</span></span> <span data-ttu-id="7a197-119">The architecture will look as follows:</span><span class="sxs-lookup"><span data-stu-id="7a197-119">The architecture will look as follows:</span></span>

![Data collection pipeline architecture](./media/log-analytics-create-pipeline-datacollector-api/data-pipeline-dataflow-architecture.png)

<span data-ttu-id="7a197-121">This article will not cover how to create data or [upload it to an Azure Blob Storage account](../storage/blobs/storage-upload-process-images.md).</span><span class="sxs-lookup"><span data-stu-id="7a197-121">This article will not cover how to create data or [upload it to an Azure Blob Storage account](../storage/blobs/storage-upload-process-images.md).</span></span> <span data-ttu-id="7a197-122">Rather, we pick the flow up as soon as a new file is uploaded to the blob.</span><span class="sxs-lookup"><span data-stu-id="7a197-122">Rather, we pick the flow up as soon as a new file is uploaded to the blob.</span></span> <span data-ttu-id="7a197-123">From here:</span><span class="sxs-lookup"><span data-stu-id="7a197-123">From here:</span></span>

1. <span data-ttu-id="7a197-124">A process will detect that new data has been uploaded.</span><span class="sxs-lookup"><span data-stu-id="7a197-124">A process will detect that new data has been uploaded.</span></span>  <span data-ttu-id="7a197-125">Our example uses an [Azure Logic App](../logic-apps/logic-apps-overview.md), which has available a trigger to detect new data being uploaded to a blob.</span><span class="sxs-lookup"><span data-stu-id="7a197-125">Our example uses an [Azure Logic App](../logic-apps/logic-apps-overview.md), which has available a trigger to detect new data being uploaded to a blob.</span></span>

2. <span data-ttu-id="7a197-126">A processor reads this new data and converts it to JSON, the format required by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7a197-126">A processor reads this new data and converts it to JSON, the format required by Log Analytics.</span></span>  <span data-ttu-id="7a197-127">In this example, we use an [Azure Function](../azure-functions/functions-overview.md) as a lightweight, cost-efficient way of executing our processing code.</span><span class="sxs-lookup"><span data-stu-id="7a197-127">In this example, we use an [Azure Function](../azure-functions/functions-overview.md) as a lightweight, cost-efficient way of executing our processing code.</span></span> <span data-ttu-id="7a197-128">The function is kicked off by the same Logic App that we used to detect a the new data.</span><span class="sxs-lookup"><span data-stu-id="7a197-128">The function is kicked off by the same Logic App that we used to detect a the new data.</span></span>

3. <span data-ttu-id="7a197-129">Finally, once the JSON object is available, it is sent to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7a197-129">Finally, once the JSON object is available, it is sent to Log Analytics.</span></span> <span data-ttu-id="7a197-130">The same Logic App sends the data to Log Analytics using the built in Log Analytics Data Collector activity.</span><span class="sxs-lookup"><span data-stu-id="7a197-130">The same Logic App sends the data to Log Analytics using the built in Log Analytics Data Collector activity.</span></span>

<span data-ttu-id="7a197-131">While the detailed setup of the blob storage, Logic App, or Azure Function is not outlined in this article, detailed instructions are available on the specific products’ pages.</span><span class="sxs-lookup"><span data-stu-id="7a197-131">While the detailed setup of the blob storage, Logic App, or Azure Function is not outlined in this article, detailed instructions are available on the specific products’ pages.</span></span>

<span data-ttu-id="7a197-132">To monitor this pipeline, we use Application Insights to monitor our Azure Function [details here](../azure-functions/functions-monitoring.md), and Log Analytics to monitor our Logic App [details here](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md).</span><span class="sxs-lookup"><span data-stu-id="7a197-132">To monitor this pipeline, we use Application Insights to monitor our Azure Function [details here](../azure-functions/functions-monitoring.md), and Log Analytics to monitor our Logic App [details here](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md).</span></span> 

## <a name="setting-up-the-pipeline"></a><span data-ttu-id="7a197-133">Setting up the pipeline</span><span class="sxs-lookup"><span data-stu-id="7a197-133">Setting up the pipeline</span></span>
<span data-ttu-id="7a197-134">To set the pipeline, first make sure you have your blob container created and configured.</span><span class="sxs-lookup"><span data-stu-id="7a197-134">To set the pipeline, first make sure you have your blob container created and configured.</span></span> <span data-ttu-id="7a197-135">Likewise, make sure that the Log Analytics workspace where you’d like to send the data to is created.</span><span class="sxs-lookup"><span data-stu-id="7a197-135">Likewise, make sure that the Log Analytics workspace where you’d like to send the data to is created.</span></span>

## <a name="ingesting-json-data"></a><span data-ttu-id="7a197-136">Ingesting JSON data</span><span class="sxs-lookup"><span data-stu-id="7a197-136">Ingesting JSON data</span></span>
<span data-ttu-id="7a197-137">Ingesting JSON data is trivial with Logic Apps, and since no transformation needs to take place, we can encase the entire pipeline in a single Logic App.</span><span class="sxs-lookup"><span data-stu-id="7a197-137">Ingesting JSON data is trivial with Logic Apps, and since no transformation needs to take place, we can encase the entire pipeline in a single Logic App.</span></span> <span data-ttu-id="7a197-138">Once both the blob container and the Log Analytics workspace have been configured, create a new Logic App and configure it as follows:</span><span class="sxs-lookup"><span data-stu-id="7a197-138">Once both the blob container and the Log Analytics workspace have been configured, create a new Logic App and configure it as follows:</span></span>

![Logic apps workflow example](./media/log-analytics-create-pipeline-datacollector-api/logic-apps-workflow-example-01.png)

<span data-ttu-id="7a197-140">Save your Logic App and proceed to test it.</span><span class="sxs-lookup"><span data-stu-id="7a197-140">Save your Logic App and proceed to test it.</span></span>

## <a name="ingesting-xml-csv-or-other-formats-of-data"></a><span data-ttu-id="7a197-141">Ingesting XML, CSV, or other formats of data</span><span class="sxs-lookup"><span data-stu-id="7a197-141">Ingesting XML, CSV, or other formats of data</span></span>
<span data-ttu-id="7a197-142">Logic Apps today does not have built-in capabilities to easily transform XML, CSV, or other types into JSON format.</span><span class="sxs-lookup"><span data-stu-id="7a197-142">Logic Apps today does not have built-in capabilities to easily transform XML, CSV, or other types into JSON format.</span></span> <span data-ttu-id="7a197-143">Therefore, we need to use another means to complete this transformation.</span><span class="sxs-lookup"><span data-stu-id="7a197-143">Therefore, we need to use another means to complete this transformation.</span></span> <span data-ttu-id="7a197-144">For this article, we use the serverless compute capabilities of Azure Functions as a very lightweight and cost-friendly way of doing so.</span><span class="sxs-lookup"><span data-stu-id="7a197-144">For this article, we use the serverless compute capabilities of Azure Functions as a very lightweight and cost-friendly way of doing so.</span></span> 

<span data-ttu-id="7a197-145">In this example, we parse a CSV file, but any other file type can be similarly processed.</span><span class="sxs-lookup"><span data-stu-id="7a197-145">In this example, we parse a CSV file, but any other file type can be similarly processed.</span></span> <span data-ttu-id="7a197-146">Simply modify the deserializing portion of the Azure Function to reflect the correct logic for your specific data type.</span><span class="sxs-lookup"><span data-stu-id="7a197-146">Simply modify the deserializing portion of the Azure Function to reflect the correct logic for your specific data type.</span></span>

1.  <span data-ttu-id="7a197-147">Create a new Azure Function, using the Function runtime v1 and consumption-based when prompted.</span><span class="sxs-lookup"><span data-stu-id="7a197-147">Create a new Azure Function, using the Function runtime v1 and consumption-based when prompted.</span></span>  <span data-ttu-id="7a197-148">Select the **HTTP trigger** template targeted at C# as a starting point that configures your bindings as we require.</span><span class="sxs-lookup"><span data-stu-id="7a197-148">Select the **HTTP trigger** template targeted at C# as a starting point that configures your bindings as we require.</span></span> 
2.  <span data-ttu-id="7a197-149">From the **View Files** tab on the right pane, create a new file called **project.json** and paste the following code from NuGet packages that we are using:</span><span class="sxs-lookup"><span data-stu-id="7a197-149">From the **View Files** tab on the right pane, create a new file called **project.json** and paste the following code from NuGet packages that we are using:</span></span>

    ![Azure Functions example project](./media/log-analytics-create-pipeline-datacollector-api/functions-example-project-01.png)
    
    ``` JSON
    {
      "frameworks": {
        "net46":{
          "dependencies": {
            "CsvHelper": "7.1.1",
            "Newtonsoft.Json": "11.0.2"
          }  
        }  
       }  
     }  
    ```

3. <span data-ttu-id="7a197-151">Switch to **run.csx** from the right pane, and replace the default code with the following.</span><span class="sxs-lookup"><span data-stu-id="7a197-151">Switch to **run.csx** from the right pane, and replace the default code with the following.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="7a197-152">For your project, you have to replace the record model (the “PopulationRecord” class) with your own data schema.</span><span class="sxs-lookup"><span data-stu-id="7a197-152">For your project, you have to replace the record model (the “PopulationRecord” class) with your own data schema.</span></span>
    >

    ```   
    using System.Net;
    using Newtonsoft.Json;
    using CsvHelper;
    
    class PopulationRecord
    {
        public String Location { get; set; }
        public int Time { get; set; }
        public long Population { get; set; }
    }

    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        string filePath = await req.Content.ReadAsStringAsync(); //get the CSV URI being passed from Logic App
        string response = "";

        //get a stream from blob
        WebClient wc = new WebClient();
        Stream s = wc.OpenRead(filePath);         

        //read the stream
        using (var sr = new StreamReader(s))
        {
            var csvReader = new CsvReader(sr);
    
            var records = csvReader.GetRecords<PopulationRecord>(); //deserialize the CSV stream as an IEnumerable
    
            response = JsonConvert.SerializeObject(records); //serialize the IEnumerable back into JSON
        }    

        return response == null
            ? req.CreateResponse(HttpStatusCode.BadRequest, "There was an issue getting data")
            : req.CreateResponse(HttpStatusCode.OK, response);
     }  
    ```

4. <span data-ttu-id="7a197-153">Save your function.</span><span class="sxs-lookup"><span data-stu-id="7a197-153">Save your function.</span></span>
5. <span data-ttu-id="7a197-154">Test the function to make sure the code is working correctly.</span><span class="sxs-lookup"><span data-stu-id="7a197-154">Test the function to make sure the code is working correctly.</span></span> <span data-ttu-id="7a197-155">Switch to the **Test** tab in the right pane, configuring the test as follows.</span><span class="sxs-lookup"><span data-stu-id="7a197-155">Switch to the **Test** tab in the right pane, configuring the test as follows.</span></span> <span data-ttu-id="7a197-156">Place a link to a blob with sample data into the **Request body** textbox.</span><span class="sxs-lookup"><span data-stu-id="7a197-156">Place a link to a blob with sample data into the **Request body** textbox.</span></span> <span data-ttu-id="7a197-157">After clicking **Run**, you should see JSON output in the **Output** box:</span><span class="sxs-lookup"><span data-stu-id="7a197-157">After clicking **Run**, you should see JSON output in the **Output** box:</span></span>

    ![Function Apps test code](./media/log-analytics-create-pipeline-datacollector-api/functions-test-01.png)

<span data-ttu-id="7a197-159">Now we need to go back and modify the Logic App we started building earlier to include the data ingested and converted to JSON format.</span><span class="sxs-lookup"><span data-stu-id="7a197-159">Now we need to go back and modify the Logic App we started building earlier to include the data ingested and converted to JSON format.</span></span>  <span data-ttu-id="7a197-160">Using View Designer, configure as follows and then save your Logic App:</span><span class="sxs-lookup"><span data-stu-id="7a197-160">Using View Designer, configure as follows and then save your Logic App:</span></span>

![Logic Apps workflow complete example](./media/log-analytics-create-pipeline-datacollector-api/logic-apps-workflow-example-02.png)

## <a name="testing-the-pipeline"></a><span data-ttu-id="7a197-162">Testing the pipeline</span><span class="sxs-lookup"><span data-stu-id="7a197-162">Testing the pipeline</span></span>
<span data-ttu-id="7a197-163">Now you can upload a new file to the blob configured earlier and have it monitored by your  Logic App.</span><span class="sxs-lookup"><span data-stu-id="7a197-163">Now you can upload a new file to the blob configured earlier and have it monitored by your  Logic App.</span></span> <span data-ttu-id="7a197-164">Soon, you should see a new instance of the Logic App kick off, call out to your Azure Function, and then successfully send the data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7a197-164">Soon, you should see a new instance of the Logic App kick off, call out to your Azure Function, and then successfully send the data to Log Analytics.</span></span> 

>[!NOTE]
><span data-ttu-id="7a197-165">It can take up to 30 minutes for the data to appear in Log Analytics the first time you send a new data type.</span><span class="sxs-lookup"><span data-stu-id="7a197-165">It can take up to 30 minutes for the data to appear in Log Analytics the first time you send a new data type.</span></span>


## <a name="correlating-with-other-data-in-log-analytics-and-application-insights"></a><span data-ttu-id="7a197-166">Correlating with other data in Log Analytics and Application Insights</span><span class="sxs-lookup"><span data-stu-id="7a197-166">Correlating with other data in Log Analytics and Application Insights</span></span>
<span data-ttu-id="7a197-167">To complete our goal of correlating Application Insights page view data with the population data we ingested from our custom data source, run the following query from either your Application Insights Analytics window or Log Analytics workspace:</span><span class="sxs-lookup"><span data-stu-id="7a197-167">To complete our goal of correlating Application Insights page view data with the population data we ingested from our custom data source, run the following query from either your Application Insights Analytics window or Log Analytics workspace:</span></span>

``` KQL
app("fabrikamprod").pageViews
| summarize numUsers = count() by client_CountryOrRegion
| join kind=leftouter (
   workspace("customdatademo").Population_CL
) on $left.client_CountryOrRegion == $right.Location_s
| project client_CountryOrRegion, numUsers, Population_d
```

<span data-ttu-id="7a197-168">The output should show the two data sources now joined.</span><span class="sxs-lookup"><span data-stu-id="7a197-168">The output should show the two data sources now joined.</span></span>  

![Correlating disjoined data in a search result example](./media/log-analytics-create-pipeline-datacollector-api/correlating-disjoined-data-example-01.png)

## <a name="suggested-improvements-for-a-production-pipeline"></a><span data-ttu-id="7a197-170">Suggested improvements for a production pipeline</span><span class="sxs-lookup"><span data-stu-id="7a197-170">Suggested improvements for a production pipeline</span></span>
<span data-ttu-id="7a197-171">This article presented a working prototype, the logic behind which can be applied towards a true production-quality solution.</span><span class="sxs-lookup"><span data-stu-id="7a197-171">This article presented a working prototype, the logic behind which can be applied towards a true production-quality solution.</span></span> <span data-ttu-id="7a197-172">For such a production-quality solution, the following improvements are recommended:</span><span class="sxs-lookup"><span data-stu-id="7a197-172">For such a production-quality solution, the following improvements are recommended:</span></span>

* <span data-ttu-id="7a197-173">Add error handling and retry logic in your Logic App and Function.</span><span class="sxs-lookup"><span data-stu-id="7a197-173">Add error handling and retry logic in your Logic App and Function.</span></span>
* <span data-ttu-id="7a197-174">Add logic to ensure that the 30MB/single Log Analytics Ingestion API call limit is not exceeded.</span><span class="sxs-lookup"><span data-stu-id="7a197-174">Add logic to ensure that the 30MB/single Log Analytics Ingestion API call limit is not exceeded.</span></span> <span data-ttu-id="7a197-175">Split the data into smaller segments if needed.</span><span class="sxs-lookup"><span data-stu-id="7a197-175">Split the data into smaller segments if needed.</span></span>
* <span data-ttu-id="7a197-176">Set up a clean-up policy on your blob storage.</span><span class="sxs-lookup"><span data-stu-id="7a197-176">Set up a clean-up policy on your blob storage.</span></span> <span data-ttu-id="7a197-177">Once successfully sent to Log Analytics, unless you’d like to keep the raw data available for archival purposes, there is no reason to continue storing it.</span><span class="sxs-lookup"><span data-stu-id="7a197-177">Once successfully sent to Log Analytics, unless you’d like to keep the raw data available for archival purposes, there is no reason to continue storing it.</span></span> 
* <span data-ttu-id="7a197-178">Verify monitoring is enabled across the full pipeline, adding trace points and alerts as appropriate.</span><span class="sxs-lookup"><span data-stu-id="7a197-178">Verify monitoring is enabled across the full pipeline, adding trace points and alerts as appropriate.</span></span>
* <span data-ttu-id="7a197-179">Leverage source control to manage the code for your function and Logic App.</span><span class="sxs-lookup"><span data-stu-id="7a197-179">Leverage source control to manage the code for your function and Logic App.</span></span>
* <span data-ttu-id="7a197-180">Ensure that a proper change management policy is followed, such that if the schema changes, the function and Logic Apps are modified accordingly.</span><span class="sxs-lookup"><span data-stu-id="7a197-180">Ensure that a proper change management policy is followed, such that if the schema changes, the function and Logic Apps are modified accordingly.</span></span>
* <span data-ttu-id="7a197-181">If you are uploading multiple different data types, segregate them into individual folders within your blob container, and create logic to fan the logic out based on the data type.</span><span class="sxs-lookup"><span data-stu-id="7a197-181">If you are uploading multiple different data types, segregate them into individual folders within your blob container, and create logic to fan the logic out based on the data type.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="7a197-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a197-182">Next steps</span></span>
<span data-ttu-id="7a197-183">Learn more about the  [Data Collector API](log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span><span class="sxs-lookup"><span data-stu-id="7a197-183">Learn more about the  [Data Collector API](log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>
