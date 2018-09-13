---
title: Create schedule triggers in Azure Data Factory | Microsoft Docs
description: Learn how to create a trigger in Azure Data Factory that runs a pipeline on a schedule.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/23/2018
ms.author: shlo
ms.openlocfilehash: eee68481f4396f8a09241b664d4c3d7d4a4f6567
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868173"
---
# <a name="create-a-trigger-that-runs-a-pipeline-on-a-schedule"></a><span data-ttu-id="c7ffa-103">Create a trigger that runs a pipeline on a schedule</span><span class="sxs-lookup"><span data-stu-id="c7ffa-103">Create a trigger that runs a pipeline on a schedule</span></span>
<span data-ttu-id="c7ffa-104">This article provides information about the schedule trigger and the steps to create, start, and monitor a schedule trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-104">This article provides information about the schedule trigger and the steps to create, start, and monitor a schedule trigger.</span></span> <span data-ttu-id="c7ffa-105">For other types of triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-105">For other types of triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md).</span></span>

<span data-ttu-id="c7ffa-106">When creating a schedule trigger, you specify a schedule (start date, recurrence, end date etc.) for the trigger, and associate with a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-106">When creating a schedule trigger, you specify a schedule (start date, recurrence, end date etc.) for the trigger, and associate with a pipeline.</span></span> <span data-ttu-id="c7ffa-107">Pipelines and triggers have a many-to-many relationship.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-107">Pipelines and triggers have a many-to-many relationship.</span></span> <span data-ttu-id="c7ffa-108">Multiple triggers can kick off a single pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-108">Multiple triggers can kick off a single pipeline.</span></span> <span data-ttu-id="c7ffa-109">A single trigger can kick off multiple pipelines.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-109">A single trigger can kick off multiple pipelines.</span></span>

<span data-ttu-id="c7ffa-110">The following sections provide steps to create a schedule trigger in different ways.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-110">The following sections provide steps to create a schedule trigger in different ways.</span></span> 

## <a name="data-factory-ui"></a><span data-ttu-id="c7ffa-111">Data Factory UI</span><span class="sxs-lookup"><span data-stu-id="c7ffa-111">Data Factory UI</span></span>
<span data-ttu-id="c7ffa-112">You can create a **schedule trigger** to schedule a pipeline to run periodically (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-112">You can create a **schedule trigger** to schedule a pipeline to run periodically (hourly, daily, etc.).</span></span> 

> [!NOTE]
> <span data-ttu-id="c7ffa-113">For a complete walkthrough of creating a pipeline and a schedule trigger, associating the trigger with the pipeline, and running and monitoring the pipeline, see [Quickstart: create a data factory using Data Factory UI](quickstart-create-data-factory-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-113">For a complete walkthrough of creating a pipeline and a schedule trigger, associating the trigger with the pipeline, and running and monitoring the pipeline, see [Quickstart: create a data factory using Data Factory UI](quickstart-create-data-factory-portal.md).</span></span>

1. <span data-ttu-id="c7ffa-114">Switch to the **Edit** tab.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-114">Switch to the **Edit** tab.</span></span> 

    ![Switch to Edit tab](./media/how-to-create-schedule-trigger/switch-edit-tab.png)
1. <span data-ttu-id="c7ffa-116">Click **Trigger** on the menu, and click **New/Edit**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-116">Click **Trigger** on the menu, and click **New/Edit**.</span></span> 

    ![New trigger menu](./media/how-to-create-schedule-trigger/new-trigger-menu.png)
2. <span data-ttu-id="c7ffa-118">In the **Add Triggers** page, click **Choose trigger...**, and click **New**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-118">In the **Add Triggers** page, click **Choose trigger...**, and click **New**.</span></span> 

    ![Add triggers - new trigger](./media/how-to-create-schedule-trigger/add-trigger-new-button.png)
3. <span data-ttu-id="c7ffa-120">In the **New Trigger** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-120">In the **New Trigger** page, do the following steps:</span></span> 

    1. <span data-ttu-id="c7ffa-121">Confirm that **Schedule** is selected for **Type**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-121">Confirm that **Schedule** is selected for **Type**.</span></span> 
    2. <span data-ttu-id="c7ffa-122">Specify the start datetime of the trigger for **Start Date (UTC)**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-122">Specify the start datetime of the trigger for **Start Date (UTC)**.</span></span> <span data-ttu-id="c7ffa-123">It's set to the current datetime by default.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-123">It's set to the current datetime by default.</span></span> 
    3. <span data-ttu-id="c7ffa-124">Specify **Recurrence** for the trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-124">Specify **Recurrence** for the trigger.</span></span> <span data-ttu-id="c7ffa-125">Select one of the values from the drop-down list (Every minute, Hourly, Daily, Weekly, and Monthly).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-125">Select one of the values from the drop-down list (Every minute, Hourly, Daily, Weekly, and Monthly).</span></span> <span data-ttu-id="c7ffa-126">Enter the multiplier in the text box.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-126">Enter the multiplier in the text box.</span></span> <span data-ttu-id="c7ffa-127">For example, if you want the trigger to run once for every 15 minutes, you select **Every Minute**, and enter **15** in the text box.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-127">For example, if you want the trigger to run once for every 15 minutes, you select **Every Minute**, and enter **15** in the text box.</span></span> 
    4. <span data-ttu-id="c7ffa-128">For the **End** field, if you do not want to specify an end datetime for the trigger, select **No End**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-128">For the **End** field, if you do not want to specify an end datetime for the trigger, select **No End**.</span></span> <span data-ttu-id="c7ffa-129">To specify an end date time, select **On Date**, and specify end datetime, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-129">To specify an end date time, select **On Date**, and specify end datetime, and click **Apply**.</span></span> <span data-ttu-id="c7ffa-130">There is a cost associated with each pipeline run.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-130">There is a cost associated with each pipeline run.</span></span> <span data-ttu-id="c7ffa-131">If you are testing, you may want to ensure that the pipeline is triggered only a couple of times.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-131">If you are testing, you may want to ensure that the pipeline is triggered only a couple of times.</span></span> <span data-ttu-id="c7ffa-132">However, ensure that there is enough time for the pipeline to run between the publish time and the end time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-132">However, ensure that there is enough time for the pipeline to run between the publish time and the end time.</span></span> <span data-ttu-id="c7ffa-133">The trigger comes into effect only after you publish the solution to Data Factory, not when you save the trigger in the UI.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-133">The trigger comes into effect only after you publish the solution to Data Factory, not when you save the trigger in the UI.</span></span>

        ![Trigger settings](./media/how-to-create-schedule-trigger/trigger-settings.png)
4. <span data-ttu-id="c7ffa-135">In the **New Trigger** window, check the **Activated** option, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-135">In the **New Trigger** window, check the **Activated** option, and click **Next**.</span></span> <span data-ttu-id="c7ffa-136">You can use this checkbox to deactivate the trigger later.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-136">You can use this checkbox to deactivate the trigger later.</span></span> 

    ![Trigger settings - Next button](./media/how-to-create-schedule-trigger/trigger-settings-next.png)
5. <span data-ttu-id="c7ffa-138">In the **New Trigger** page, review the warning message, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-138">In the **New Trigger** page, review the warning message, and click **Finish**.</span></span>

    ![Trigger settings - Finish button](./media/how-to-create-schedule-trigger/new-trigger-finish.png)
6. <span data-ttu-id="c7ffa-140">Click **Publish** to publish changes to Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-140">Click **Publish** to publish changes to Data Factory.</span></span> <span data-ttu-id="c7ffa-141">Until you publish changes to Data Factory, the trigger does not start triggering the pipeline runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-141">Until you publish changes to Data Factory, the trigger does not start triggering the pipeline runs.</span></span> 

    ![Publish button](./media/how-to-create-schedule-trigger/publish-2.png)
8. <span data-ttu-id="c7ffa-143">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-143">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="c7ffa-144">Click **Refresh** to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-144">Click **Refresh** to refresh the list.</span></span> <span data-ttu-id="c7ffa-145">You see the pipeline runs triggered by the scheduled trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-145">You see the pipeline runs triggered by the scheduled trigger.</span></span> <span data-ttu-id="c7ffa-146">Notice the values in the **Triggered By** column.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-146">Notice the values in the **Triggered By** column.</span></span> <span data-ttu-id="c7ffa-147">If you use **Trigger Now** option, you see the manual trigger run in the list.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-147">If you use **Trigger Now** option, you see the manual trigger run in the list.</span></span> 

    ![Monitor triggered runs](./media/how-to-create-schedule-trigger/monitor-triggered-runs.png)
9. <span data-ttu-id="c7ffa-149">Click the down-arrow next to **Pipeline Runs** to switch to the **Trigger Runs** view.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-149">Click the down-arrow next to **Pipeline Runs** to switch to the **Trigger Runs** view.</span></span> 

    ![Monitor trigger runs](./media/how-to-create-schedule-trigger/monitor-trigger-runs.png)

## <a name="azure-powershell"></a><span data-ttu-id="c7ffa-151">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7ffa-151">Azure PowerShell</span></span>
<span data-ttu-id="c7ffa-152">This section shows you how to use Azure PowerShell to create, start, and monitor a schedule trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-152">This section shows you how to use Azure PowerShell to create, start, and monitor a schedule trigger.</span></span> <span data-ttu-id="c7ffa-153">To see this sample working, first go through the [Quickstart: Create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-153">To see this sample working, first go through the [Quickstart: Create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span></span> <span data-ttu-id="c7ffa-154">Then, add the following code to the main method, which creates and starts a schedule trigger that runs every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-154">Then, add the following code to the main method, which creates and starts a schedule trigger that runs every 15 minutes.</span></span> <span data-ttu-id="c7ffa-155">The trigger is associated with a pipeline named **Adfv2QuickStartPipeline** that you create as part of the Quickstart.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-155">The trigger is associated with a pipeline named **Adfv2QuickStartPipeline** that you create as part of the Quickstart.</span></span>

1. <span data-ttu-id="c7ffa-156">Create a JSON file named **MyTrigger.json** in the C:\ADFv2QuickStartPSH\ folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-156">Create a JSON file named **MyTrigger.json** in the C:\ADFv2QuickStartPSH\ folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7ffa-157">Before you save the JSON file, set the value of the **startTime** element to the current UTC time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-157">Before you save the JSON file, set the value of the **startTime** element to the current UTC time.</span></span> <span data-ttu-id="c7ffa-158">Set the value of the **endTime** element to one hour past the current UTC time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-158">Set the value of the **endTime** element to one hour past the current UTC time.</span></span>

    ```json   
    {
        "properties": {
            "name": "MyTrigger",
            "type": "ScheduleTrigger",
            "typeProperties": {
                "recurrence": {
                    "frequency": "Minute",
                    "interval": 15,
                    "startTime": "2017-12-08T00:00:00",
                    "endTime": "2017-12-08T01:00:00"
                }
            },
            "pipelines": [{
                    "pipelineReference": {
                        "type": "PipelineReference",
                        "referenceName": "Adfv2QuickStartPipeline"
                    },
                    "parameters": {
                        "inputPath": "adftutorial/input",
                        "outputPath": "adftutorial/output"
                    }
                }
            ]
        }
    }
    ```

    <span data-ttu-id="c7ffa-159">In the JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-159">In the JSON snippet:</span></span>
    - <span data-ttu-id="c7ffa-160">The **type** element of the trigger is set to "ScheduleTrigger."</span><span class="sxs-lookup"><span data-stu-id="c7ffa-160">The **type** element of the trigger is set to "ScheduleTrigger."</span></span>
    - <span data-ttu-id="c7ffa-161">The **frequency** element is set to "Minute" and the **interval** element is set to 15.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-161">The **frequency** element is set to "Minute" and the **interval** element is set to 15.</span></span> <span data-ttu-id="c7ffa-162">Therefore, the trigger runs the pipeline every 15 minutes between the start and end times.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-162">Therefore, the trigger runs the pipeline every 15 minutes between the start and end times.</span></span>
    - <span data-ttu-id="c7ffa-163">The **endTime** element is one hour after the value of the **startTime** element.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-163">The **endTime** element is one hour after the value of the **startTime** element.</span></span> <span data-ttu-id="c7ffa-164">Therefore, the trigger runs the pipeline 15 minutes, 30 minutes, and 45 minutes after the start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-164">Therefore, the trigger runs the pipeline 15 minutes, 30 minutes, and 45 minutes after the start time.</span></span> <span data-ttu-id="c7ffa-165">Don't forget to update the start time to the current UTC time, and the end time to one hour past the start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-165">Don't forget to update the start time to the current UTC time, and the end time to one hour past the start time.</span></span> 
    - <span data-ttu-id="c7ffa-166">The trigger is associated with the **Adfv2QuickStartPipeline** pipeline.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-166">The trigger is associated with the **Adfv2QuickStartPipeline** pipeline.</span></span> <span data-ttu-id="c7ffa-167">To associate multiple pipelines with a trigger, add more **pipelineReference** sections.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-167">To associate multiple pipelines with a trigger, add more **pipelineReference** sections.</span></span>
    - <span data-ttu-id="c7ffa-168">The pipeline in the Quickstart takes two **parameters** values: **inputPath** and **outputPath**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-168">The pipeline in the Quickstart takes two **parameters** values: **inputPath** and **outputPath**.</span></span> <span data-ttu-id="c7ffa-169">Therefore, you pass values for these parameters from the trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-169">Therefore, you pass values for these parameters from the trigger.</span></span>

2. <span data-ttu-id="c7ffa-170">Create a trigger by using the **Set-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-170">Create a trigger by using the **Set-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger" -DefinitionFile "C:\ADFv2QuickStartPSH\MyTrigger.json"
    ```

3. <span data-ttu-id="c7ffa-171">Confirm that the status of the trigger is **Stopped** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-171">Confirm that the status of the trigger is **Stopped** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"
    ```

4. <span data-ttu-id="c7ffa-172">Start the trigger by using the **Start-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-172">Start the trigger by using the **Start-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"
    ```

5. <span data-ttu-id="c7ffa-173">Confirm that the status of the trigger is **Started** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-173">Confirm that the status of the trigger is **Started** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"
    ```

6.  <span data-ttu-id="c7ffa-174">Get the trigger runs in Azure PowerShell by using the **Get-AzureRmDataFactoryV2TriggerRun** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-174">Get the trigger runs in Azure PowerShell by using the **Get-AzureRmDataFactoryV2TriggerRun** cmdlet.</span></span> <span data-ttu-id="c7ffa-175">To get the information about the trigger runs, execute the following command periodically.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-175">To get the information about the trigger runs, execute the following command periodically.</span></span> <span data-ttu-id="c7ffa-176">Update the **TriggerRunStartedAfter** and **TriggerRunStartedBefore** values to match the values in your trigger definition:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-176">Update the **TriggerRunStartedAfter** and **TriggerRunStartedBefore** values to match the values in your trigger definition:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2TriggerRun -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -TriggerName "MyTrigger" -TriggerRunStartedAfter "2017-12-08T00:00:00" -TriggerRunStartedBefore "2017-12-08T01:00:00"
    ```
    
    <span data-ttu-id="c7ffa-177">To monitor the trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-177">To monitor the trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span></span>


## <a name="net-sdk"></a><span data-ttu-id="c7ffa-178">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="c7ffa-178">.NET SDK</span></span>
<span data-ttu-id="c7ffa-179">This section shows you how to use the .NET SDK to create, start, and monitor a trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-179">This section shows you how to use the .NET SDK to create, start, and monitor a trigger.</span></span> <span data-ttu-id="c7ffa-180">To see this sample working, first go through the [Quickstart: Create a data factory by using the .NET SDK](quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-180">To see this sample working, first go through the [Quickstart: Create a data factory by using the .NET SDK](quickstart-create-data-factory-dot-net.md).</span></span> <span data-ttu-id="c7ffa-181">Then, add the following code to the main method, which creates and starts a schedule trigger that runs every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-181">Then, add the following code to the main method, which creates and starts a schedule trigger that runs every 15 minutes.</span></span> <span data-ttu-id="c7ffa-182">The trigger is associated with a pipeline named **Adfv2QuickStartPipeline** that you create as part of the Quickstart.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-182">The trigger is associated with a pipeline named **Adfv2QuickStartPipeline** that you create as part of the Quickstart.</span></span>

<span data-ttu-id="c7ffa-183">To create and start a schedule trigger that runs every 15 minutes, add the following code to the main method:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-183">To create and start a schedule trigger that runs every 15 minutes, add the following code to the main method:</span></span>

```csharp
            // Create the trigger
            Console.WriteLine("Creating the trigger");

            // Set the start time to the current UTC time
            DateTime startTime = DateTime.UtcNow;

            // Specify values for the inputPath and outputPath parameters
            Dictionary<string, object> pipelineParameters = new Dictionary<string, object>();
            pipelineParameters.Add("inputPath", "adftutorial/input");
            pipelineParameters.Add("outputPath", "adftutorial/output");

            // Create a schedule trigger
            string triggerName = "MyTrigger";
            ScheduleTrigger myTrigger = new ScheduleTrigger()
            {
                Pipelines = new List<TriggerPipelineReference>()
                {
                    // Associate the Adfv2QuickStartPipeline pipeline with the trigger
                    new TriggerPipelineReference()
                    {
                        PipelineReference = new PipelineReference(pipelineName),
                        Parameters = pipelineParameters,
                    }
                },
                Recurrence = new ScheduleTriggerRecurrence()
                {
                    // Set the start time to the current UTC time and the end time to one hour after the start time
                    StartTime = startTime,
                    TimeZone = "UTC",
                    EndTime = startTime.AddHours(1),
                    Frequency = RecurrenceFrequency.Minute,
                    Interval = 15,
                }
            };

            // Now, create the trigger by invoking the CreateOrUpdate method
            TriggerResource triggerResource = new TriggerResource()
            {
                Properties = myTrigger
            };
            client.Triggers.CreateOrUpdate(resourceGroup, dataFactoryName, triggerName, triggerResource);

            // Start the trigger
            Console.WriteLine("Starting the trigger");
            client.Triggers.Start(resourceGroup, dataFactoryName, triggerName);
```

<span data-ttu-id="c7ffa-184">To monitor a trigger run, add the following code before the last `Console.WriteLine` statement in the sample:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-184">To monitor a trigger run, add the following code before the last `Console.WriteLine` statement in the sample:</span></span>

```csharp
            // Check that the trigger runs every 15 minutes
            Console.WriteLine("Trigger runs. You see the output every 15 minutes");

            for (int i = 0; i < 3; i++)
            {
                System.Threading.Thread.Sleep(TimeSpan.FromMinutes(15));
                List<TriggerRun> triggerRuns = client.Triggers.ListRuns(resourceGroup, dataFactoryName, triggerName, DateTime.UtcNow.AddMinutes(-15 * (i + 1)), DateTime.UtcNow.AddMinutes(2)).ToList();
                Console.WriteLine("{0} trigger runs found", triggerRuns.Count);

                foreach (TriggerRun run in triggerRuns)
                {
                    foreach (KeyValuePair<string, string> triggeredPipeline in run.TriggeredPipelines)
                    {
                        PipelineRun triggeredPipelineRun = client.PipelineRuns.Get(resourceGroup, dataFactoryName, triggeredPipeline.Value);
                        Console.WriteLine("Pipeline run ID: {0}, Status: {1}", triggeredPipelineRun.RunId, triggeredPipelineRun.Status);
                        List<ActivityRun> runs = client.ActivityRuns.ListByPipelineRun(resourceGroup, dataFactoryName, triggeredPipelineRun.RunId, run.TriggerRunTimestamp.Value, run.TriggerRunTimestamp.Value.AddMinutes(20)).ToList();
                    }
                }
            }
```

<span data-ttu-id="c7ffa-185">To monitor the trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-185">To monitor the trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span></span>


## <a name="python-sdk"></a><span data-ttu-id="c7ffa-186">Python SDK</span><span class="sxs-lookup"><span data-stu-id="c7ffa-186">Python SDK</span></span>
<span data-ttu-id="c7ffa-187">This section shows you how to use the Python SDK to create, start, and monitor a trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-187">This section shows you how to use the Python SDK to create, start, and monitor a trigger.</span></span> <span data-ttu-id="c7ffa-188">To see this sample working, first go through the [Quickstart: Create a data factory by using the Python SDK](quickstart-create-data-factory-python.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-188">To see this sample working, first go through the [Quickstart: Create a data factory by using the Python SDK](quickstart-create-data-factory-python.md).</span></span> <span data-ttu-id="c7ffa-189">Then, add the following code block after the "monitor the pipeline run" code block in the Python script.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-189">Then, add the following code block after the "monitor the pipeline run" code block in the Python script.</span></span> <span data-ttu-id="c7ffa-190">This code creates a schedule trigger that runs every 15 minutes between the specified start and end times.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-190">This code creates a schedule trigger that runs every 15 minutes between the specified start and end times.</span></span> <span data-ttu-id="c7ffa-191">Update the **start_time** variable to the current UTC time, and the **end_time** variable to one hour past the current UTC time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-191">Update the **start_time** variable to the current UTC time, and the **end_time** variable to one hour past the current UTC time.</span></span>

```python
    # Create a trigger
    tr_name = 'mytrigger'
    scheduler_recurrence = ScheduleTriggerRecurrence(frequency='Minute', interval='15',start_time='2017-12-12T04:00:00', end_time='2017-12-12T05:00:00', time_zone='UTC')
    pipeline_parameters = {'inputPath':'adftutorial/input', 'outputPath':'adftutorial/output'}
    pipelines_to_run = []
    pipeline_reference = PipelineReference('copyPipeline')
    pipelines_to_run.append(TriggerPipelineReference(pipeline_reference, pipeline_parameters))
    tr_properties = ScheduleTrigger(description='My scheduler trigger', pipelines = pipelines_to_run, recurrence=scheduler_recurrence)    
    adf_client.triggers.create_or_update(rg_name, df_name, tr_name, tr_properties)

    # Start the trigger
    adf_client.triggers.start(rg_name, df_name, tr_name)
```

<span data-ttu-id="c7ffa-192">To monitor the trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-192">To monitor the trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span></span>

## <a name="azure-resource-manager-template"></a><span data-ttu-id="c7ffa-193">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="c7ffa-193">Azure Resource Manager template</span></span>
<span data-ttu-id="c7ffa-194">You can use an Azure Resource Manager template to create a trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-194">You can use an Azure Resource Manager template to create a trigger.</span></span> <span data-ttu-id="c7ffa-195">For step-by-step instructions, see [Create an Azure data factory by using a Resource Manager template](quickstart-create-data-factory-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-195">For step-by-step instructions, see [Create an Azure data factory by using a Resource Manager template](quickstart-create-data-factory-resource-manager-template.md).</span></span>  

## <a name="pass-the-trigger-start-time-to-a-pipeline"></a><span data-ttu-id="c7ffa-196">Pass the trigger start time to a pipeline</span><span class="sxs-lookup"><span data-stu-id="c7ffa-196">Pass the trigger start time to a pipeline</span></span>
<span data-ttu-id="c7ffa-197">Azure Data Factory version 1 supports reading or writing partitioned data by using the system variables: **SliceStart**, **SliceEnd**, **WindowStart**, and **WindowEnd**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-197">Azure Data Factory version 1 supports reading or writing partitioned data by using the system variables: **SliceStart**, **SliceEnd**, **WindowStart**, and **WindowEnd**.</span></span> <span data-ttu-id="c7ffa-198">In the current version of Azure Data Factory, you can achieve this behavior by using a pipeline parameter.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-198">In the current version of Azure Data Factory, you can achieve this behavior by using a pipeline parameter.</span></span> <span data-ttu-id="c7ffa-199">The start time and scheduled time for the trigger are set as the value for the pipeline parameter.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-199">The start time and scheduled time for the trigger are set as the value for the pipeline parameter.</span></span> <span data-ttu-id="c7ffa-200">In the following example, the scheduled time for the trigger is passed as a value to the pipeline **scheduledRunTime** parameter:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-200">In the following example, the scheduled time for the trigger is passed as a value to the pipeline **scheduledRunTime** parameter:</span></span>

```json
"parameters": {
    "scheduledRunTime": "@trigger().scheduledTime"
}
```    

<span data-ttu-id="c7ffa-201">For more information, see the instructions in [How to read or write partitioned data](how-to-read-write-partitioned-data.md).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-201">For more information, see the instructions in [How to read or write partitioned data](how-to-read-write-partitioned-data.md).</span></span>

## <a name="json-schema"></a><span data-ttu-id="c7ffa-202">JSON schema</span><span class="sxs-lookup"><span data-stu-id="c7ffa-202">JSON schema</span></span>
<span data-ttu-id="c7ffa-203">The following JSON definition shows you how to create a schedule trigger with scheduling and recurrence:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-203">The following JSON definition shows you how to create a schedule trigger with scheduling and recurrence:</span></span>

```json
{
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      "recurrence": {
        "frequency": <<Minute, Hour, Day, Week, Month>>,
        "interval": <<int>>,             // Optional, specifies how often to fire (default to 1)
        "startTime": <<datetime>>,
        "endTime": <<datetime - optional>>,
        "timeZone": "UTC"
        "schedule": {                    // Optional (advanced scheduling specifics)
          "hours": [<<0-23>>],
          "weekDays": : [<<Monday-Sunday>>],
          "minutes": [<<0-59>>],
          "monthDays": [<<1-31>>],
          "monthlyOccurences": [
               {
                    "day": <<Monday-Sunday>>,
                    "occurrence": <<1-5>>
               }
           ]
        }
      }
    },
   "pipelines": [
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "<Name of your pipeline>"
                },
                "parameters": {
                    "<parameter 1 Name>": {
                        "type": "Expression",
                        "value": "<parameter 1 Value>"
                    },
                    "<parameter 2 Name>" : "<parameter 2 Value>"
                }
           }
      ]
  }
}
```

> [!IMPORTANT]
>  <span data-ttu-id="c7ffa-204">The **parameters** property is a mandatory property of the **pipelines** element.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-204">The **parameters** property is a mandatory property of the **pipelines** element.</span></span> <span data-ttu-id="c7ffa-205">If your pipeline doesn't take any parameters, you must include an empty JSON definition for the **parameters** property.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-205">If your pipeline doesn't take any parameters, you must include an empty JSON definition for the **parameters** property.</span></span>


### <a name="schema-overview"></a><span data-ttu-id="c7ffa-206">Schema overview</span><span class="sxs-lookup"><span data-stu-id="c7ffa-206">Schema overview</span></span>
<span data-ttu-id="c7ffa-207">The following table provides a high-level overview of the major schema elements that are related to recurrence and scheduling of a trigger:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-207">The following table provides a high-level overview of the major schema elements that are related to recurrence and scheduling of a trigger:</span></span>

| <span data-ttu-id="c7ffa-208">JSON property</span><span class="sxs-lookup"><span data-stu-id="c7ffa-208">JSON property</span></span> | <span data-ttu-id="c7ffa-209">Description</span><span class="sxs-lookup"><span data-stu-id="c7ffa-209">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c7ffa-210">**startTime**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-210">**startTime**</span></span> | <span data-ttu-id="c7ffa-211">A Date-Time value.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-211">A Date-Time value.</span></span> <span data-ttu-id="c7ffa-212">For simple schedules, the value of the **startTime** property applies to the first occurrence.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-212">For simple schedules, the value of the **startTime** property applies to the first occurrence.</span></span> <span data-ttu-id="c7ffa-213">For complex schedules, the trigger starts no sooner than the specified **startTime** value.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-213">For complex schedules, the trigger starts no sooner than the specified **startTime** value.</span></span> |
| <span data-ttu-id="c7ffa-214">**endTime**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-214">**endTime**</span></span> | <span data-ttu-id="c7ffa-215">The end date and time for the trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-215">The end date and time for the trigger.</span></span> <span data-ttu-id="c7ffa-216">The trigger doesn't execute after the specified end date and time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-216">The trigger doesn't execute after the specified end date and time.</span></span> <span data-ttu-id="c7ffa-217">The value for the property can't be in the past.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-217">The value for the property can't be in the past.</span></span> <span data-ttu-id="c7ffa-218">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-218">This property is optional.</span></span> |
| <span data-ttu-id="c7ffa-219">**timeZone**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-219">**timeZone**</span></span> | <span data-ttu-id="c7ffa-220">The time zone.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-220">The time zone.</span></span> <span data-ttu-id="c7ffa-221">Currently, only the UTC time zone is supported.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-221">Currently, only the UTC time zone is supported.</span></span> |
| <span data-ttu-id="c7ffa-222">**recurrence**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-222">**recurrence**</span></span> | <span data-ttu-id="c7ffa-223">A recurrence object that specifies the recurrence rules for the trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-223">A recurrence object that specifies the recurrence rules for the trigger.</span></span> <span data-ttu-id="c7ffa-224">The recurrence object supports the **frequency**, **interva**l, **endTime**, **count**, and **schedule** elements.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-224">The recurrence object supports the **frequency**, **interva**l, **endTime**, **count**, and **schedule** elements.</span></span> <span data-ttu-id="c7ffa-225">When a recurrence object is defined, the **frequency** element is required.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-225">When a recurrence object is defined, the **frequency** element is required.</span></span> <span data-ttu-id="c7ffa-226">The other elements of the recurrence object are optional.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-226">The other elements of the recurrence object are optional.</span></span> |
| <span data-ttu-id="c7ffa-227">**frequency**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-227">**frequency**</span></span> | <span data-ttu-id="c7ffa-228">The unit of frequency at which the trigger recurs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-228">The unit of frequency at which the trigger recurs.</span></span> <span data-ttu-id="c7ffa-229">The supported values include "minute," "hour," "day," "week," and "month."</span><span class="sxs-lookup"><span data-stu-id="c7ffa-229">The supported values include "minute," "hour," "day," "week," and "month."</span></span> |
| <span data-ttu-id="c7ffa-230">**interval**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-230">**interval**</span></span> | <span data-ttu-id="c7ffa-231">A positive integer that denotes the interval for the **frequency** value, which determines how often the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-231">A positive integer that denotes the interval for the **frequency** value, which determines how often the trigger runs.</span></span> <span data-ttu-id="c7ffa-232">For example, if the **interval** is 3 and the **frequency** is "week," the trigger recurs every 3 weeks.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-232">For example, if the **interval** is 3 and the **frequency** is "week," the trigger recurs every 3 weeks.</span></span> |
| <span data-ttu-id="c7ffa-233">**schedule**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-233">**schedule**</span></span> | <span data-ttu-id="c7ffa-234">The recurrence schedule for the trigger.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-234">The recurrence schedule for the trigger.</span></span> <span data-ttu-id="c7ffa-235">A trigger with a specified **frequency** value alters its recurrence based on a recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-235">A trigger with a specified **frequency** value alters its recurrence based on a recurrence schedule.</span></span> <span data-ttu-id="c7ffa-236">The **schedule** property contains modifications for the recurrence that are based on minutes, hours, weekdays, month days, and week number.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-236">The **schedule** property contains modifications for the recurrence that are based on minutes, hours, weekdays, month days, and week number.</span></span>


### <a name="schema-defaults-limits-and-examples"></a><span data-ttu-id="c7ffa-237">Schema defaults, limits, and examples</span><span class="sxs-lookup"><span data-stu-id="c7ffa-237">Schema defaults, limits, and examples</span></span>

| <span data-ttu-id="c7ffa-238">JSON property</span><span class="sxs-lookup"><span data-stu-id="c7ffa-238">JSON property</span></span> | <span data-ttu-id="c7ffa-239">Type</span><span class="sxs-lookup"><span data-stu-id="c7ffa-239">Type</span></span> | <span data-ttu-id="c7ffa-240">Required</span><span class="sxs-lookup"><span data-stu-id="c7ffa-240">Required</span></span> | <span data-ttu-id="c7ffa-241">Default value</span><span class="sxs-lookup"><span data-stu-id="c7ffa-241">Default value</span></span> | <span data-ttu-id="c7ffa-242">Valid values</span><span class="sxs-lookup"><span data-stu-id="c7ffa-242">Valid values</span></span> | <span data-ttu-id="c7ffa-243">Example</span><span class="sxs-lookup"><span data-stu-id="c7ffa-243">Example</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="c7ffa-244">**startTime**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-244">**startTime**</span></span> | <span data-ttu-id="c7ffa-245">String</span><span class="sxs-lookup"><span data-stu-id="c7ffa-245">String</span></span> | <span data-ttu-id="c7ffa-246">Yes</span><span class="sxs-lookup"><span data-stu-id="c7ffa-246">Yes</span></span> | <span data-ttu-id="c7ffa-247">None</span><span class="sxs-lookup"><span data-stu-id="c7ffa-247">None</span></span> | <span data-ttu-id="c7ffa-248">ISO-8601 Date-Times</span><span class="sxs-lookup"><span data-stu-id="c7ffa-248">ISO-8601 Date-Times</span></span> | `"startTime" : "2013-01-09T09:30:00-08:00"` |
| <span data-ttu-id="c7ffa-249">**recurrence**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-249">**recurrence**</span></span> | <span data-ttu-id="c7ffa-250">Object</span><span class="sxs-lookup"><span data-stu-id="c7ffa-250">Object</span></span> | <span data-ttu-id="c7ffa-251">Yes</span><span class="sxs-lookup"><span data-stu-id="c7ffa-251">Yes</span></span> | <span data-ttu-id="c7ffa-252">None</span><span class="sxs-lookup"><span data-stu-id="c7ffa-252">None</span></span> | <span data-ttu-id="c7ffa-253">Recurrence object</span><span class="sxs-lookup"><span data-stu-id="c7ffa-253">Recurrence object</span></span> | `"recurrence" : { "frequency" : "monthly", "interval" : 1 }` |
| <span data-ttu-id="c7ffa-254">**interval**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-254">**interval**</span></span> | <span data-ttu-id="c7ffa-255">Number</span><span class="sxs-lookup"><span data-stu-id="c7ffa-255">Number</span></span> | <span data-ttu-id="c7ffa-256">No</span><span class="sxs-lookup"><span data-stu-id="c7ffa-256">No</span></span> | <span data-ttu-id="c7ffa-257">1</span><span class="sxs-lookup"><span data-stu-id="c7ffa-257">1</span></span> | <span data-ttu-id="c7ffa-258">1 to 1,000</span><span class="sxs-lookup"><span data-stu-id="c7ffa-258">1 to 1,000</span></span> | `"interval":10` |
| <span data-ttu-id="c7ffa-259">**endTime**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-259">**endTime**</span></span> | <span data-ttu-id="c7ffa-260">String</span><span class="sxs-lookup"><span data-stu-id="c7ffa-260">String</span></span> | <span data-ttu-id="c7ffa-261">Yes</span><span class="sxs-lookup"><span data-stu-id="c7ffa-261">Yes</span></span> | <span data-ttu-id="c7ffa-262">None</span><span class="sxs-lookup"><span data-stu-id="c7ffa-262">None</span></span> | <span data-ttu-id="c7ffa-263">A Date-Time value that represents a time in the future.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-263">A Date-Time value that represents a time in the future.</span></span> | `"endTime" : "2013-02-09T09:30:00-08:00"` |
| <span data-ttu-id="c7ffa-264">**schedule**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-264">**schedule**</span></span> | <span data-ttu-id="c7ffa-265">Object</span><span class="sxs-lookup"><span data-stu-id="c7ffa-265">Object</span></span> | <span data-ttu-id="c7ffa-266">No</span><span class="sxs-lookup"><span data-stu-id="c7ffa-266">No</span></span> | <span data-ttu-id="c7ffa-267">None</span><span class="sxs-lookup"><span data-stu-id="c7ffa-267">None</span></span> | <span data-ttu-id="c7ffa-268">Schedule object</span><span class="sxs-lookup"><span data-stu-id="c7ffa-268">Schedule object</span></span> | `"schedule" : { "minute" : [30], "hour" : [8,17] }` |

### <a name="starttime-property"></a><span data-ttu-id="c7ffa-269">startTime property</span><span class="sxs-lookup"><span data-stu-id="c7ffa-269">startTime property</span></span>
<span data-ttu-id="c7ffa-270">The following table shows you how the **startTime** property controls a trigger run:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-270">The following table shows you how the **startTime** property controls a trigger run:</span></span>

| <span data-ttu-id="c7ffa-271">startTime value</span><span class="sxs-lookup"><span data-stu-id="c7ffa-271">startTime value</span></span> | <span data-ttu-id="c7ffa-272">Recurrence without schedule</span><span class="sxs-lookup"><span data-stu-id="c7ffa-272">Recurrence without schedule</span></span> | <span data-ttu-id="c7ffa-273">Recurrence with schedule</span><span class="sxs-lookup"><span data-stu-id="c7ffa-273">Recurrence with schedule</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c7ffa-274">Start time in past</span><span class="sxs-lookup"><span data-stu-id="c7ffa-274">Start time in past</span></span> | <span data-ttu-id="c7ffa-275">Calculates the first future execution time after the start time and runs at that time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-275">Calculates the first future execution time after the start time and runs at that time.</span></span><br/><br/><span data-ttu-id="c7ffa-276">Runs subsequent executions based on calculating from the last execution time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-276">Runs subsequent executions based on calculating from the last execution time.</span></span><br/><br/><span data-ttu-id="c7ffa-277">See the example that follows this table.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-277">See the example that follows this table.</span></span> | <span data-ttu-id="c7ffa-278">The trigger starts _no sooner than_ the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-278">The trigger starts _no sooner than_ the specified start time.</span></span> <span data-ttu-id="c7ffa-279">The first occurrence is based on the schedule that's calculated from the start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-279">The first occurrence is based on the schedule that's calculated from the start time.</span></span><br/><br/><span data-ttu-id="c7ffa-280">Runs subsequent executions based on the recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-280">Runs subsequent executions based on the recurrence schedule.</span></span> |
| <span data-ttu-id="c7ffa-281">Start time in future or at present</span><span class="sxs-lookup"><span data-stu-id="c7ffa-281">Start time in future or at present</span></span> | <span data-ttu-id="c7ffa-282">Runs once at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-282">Runs once at the specified start time.</span></span><br/><br/><span data-ttu-id="c7ffa-283">Runs subsequent executions based on calculating from the last execution time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-283">Runs subsequent executions based on calculating from the last execution time.</span></span> | <span data-ttu-id="c7ffa-284">The trigger starts _no sooner_ than the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-284">The trigger starts _no sooner_ than the specified start time.</span></span> <span data-ttu-id="c7ffa-285">The first occurrence is based on the schedule that's calculated from the start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-285">The first occurrence is based on the schedule that's calculated from the start time.</span></span><br/><br/><span data-ttu-id="c7ffa-286">Runs subsequent executions based on the recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-286">Runs subsequent executions based on the recurrence schedule.</span></span> |

<span data-ttu-id="c7ffa-287">Let's see an example of what happens when the start time is in the past, with a recurrence, but no schedule.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-287">Let's see an example of what happens when the start time is in the past, with a recurrence, but no schedule.</span></span> <span data-ttu-id="c7ffa-288">Assume that the current time is `2017-04-08 13:00`, the start time is `2017-04-07 14:00`, and the recurrence is every two days.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-288">Assume that the current time is `2017-04-08 13:00`, the start time is `2017-04-07 14:00`, and the recurrence is every two days.</span></span> <span data-ttu-id="c7ffa-289">(The **recurrence** value is defined by setting the **frequency** property to "day" and the **interval** property to 2.) Notice that the **startTime** value is in the past and occurs before the current time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-289">(The **recurrence** value is defined by setting the **frequency** property to "day" and the **interval** property to 2.) Notice that the **startTime** value is in the past and occurs before the current time.</span></span>

<span data-ttu-id="c7ffa-290">Under these conditions, the first execution is at `2017-04-09 at 14:00`.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-290">Under these conditions, the first execution is at `2017-04-09 at 14:00`.</span></span> <span data-ttu-id="c7ffa-291">The Scheduler engine calculates execution occurrences from the start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-291">The Scheduler engine calculates execution occurrences from the start time.</span></span> <span data-ttu-id="c7ffa-292">Any instances in the past are discarded.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-292">Any instances in the past are discarded.</span></span> <span data-ttu-id="c7ffa-293">The engine uses the next instance that occurs in the future.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-293">The engine uses the next instance that occurs in the future.</span></span> <span data-ttu-id="c7ffa-294">In this scenario, the start time is `2017-04-07 at 2:00pm`, so the next instance is two days from that time, which is `2017-04-09 at 2:00pm`.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-294">In this scenario, the start time is `2017-04-07 at 2:00pm`, so the next instance is two days from that time, which is `2017-04-09 at 2:00pm`.</span></span>

<span data-ttu-id="c7ffa-295">The first execution time is the same even if the **startTime** value is `2017-04-05 14:00` or `2017-04-01 14:00`.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-295">The first execution time is the same even if the **startTime** value is `2017-04-05 14:00` or `2017-04-01 14:00`.</span></span> <span data-ttu-id="c7ffa-296">After the first execution, subsequent executions are calculated by using the schedule.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-296">After the first execution, subsequent executions are calculated by using the schedule.</span></span> <span data-ttu-id="c7ffa-297">Therefore, the subsequent executions are at `2017-04-11 at 2:00pm`, then `2017-04-13 at 2:00pm`, then `2017-04-15 at 2:00pm`, and so on.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-297">Therefore, the subsequent executions are at `2017-04-11 at 2:00pm`, then `2017-04-13 at 2:00pm`, then `2017-04-15 at 2:00pm`, and so on.</span></span>

<span data-ttu-id="c7ffa-298">Finally, when the hours or minutes aren’t set in the schedule for a trigger, the hours or minutes of the first execution are used as the defaults.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-298">Finally, when the hours or minutes aren’t set in the schedule for a trigger, the hours or minutes of the first execution are used as the defaults.</span></span>

### <a name="schedule-property"></a><span data-ttu-id="c7ffa-299">schedule property</span><span class="sxs-lookup"><span data-stu-id="c7ffa-299">schedule property</span></span>
<span data-ttu-id="c7ffa-300">On one hand, the use of a schedule can limit the number of trigger executions.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-300">On one hand, the use of a schedule can limit the number of trigger executions.</span></span> <span data-ttu-id="c7ffa-301">For example, if a trigger with a monthly frequency is scheduled to run only on day 31, the trigger runs only in those months that have a 31st day.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-301">For example, if a trigger with a monthly frequency is scheduled to run only on day 31, the trigger runs only in those months that have a 31st day.</span></span>

<span data-ttu-id="c7ffa-302">Whereas, a schedule can also expand the number of trigger executions.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-302">Whereas, a schedule can also expand the number of trigger executions.</span></span> <span data-ttu-id="c7ffa-303">For example, a trigger with a monthly frequency that's scheduled to run on month days 1 and 2, runs on the 1st and 2nd days of the month, rather than once a month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-303">For example, a trigger with a monthly frequency that's scheduled to run on month days 1 and 2, runs on the 1st and 2nd days of the month, rather than once a month.</span></span>

<span data-ttu-id="c7ffa-304">If multiple **schedule** elements are specified, the order of evaluation is from the largest to the smallest schedule setting.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-304">If multiple **schedule** elements are specified, the order of evaluation is from the largest to the smallest schedule setting.</span></span> <span data-ttu-id="c7ffa-305">The evaluation starts with week number, and then month day, weekday, hour, and finally, minute.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-305">The evaluation starts with week number, and then month day, weekday, hour, and finally, minute.</span></span>

<span data-ttu-id="c7ffa-306">The following table describes the **schedule** elements in detail:</span><span class="sxs-lookup"><span data-stu-id="c7ffa-306">The following table describes the **schedule** elements in detail:</span></span>


| <span data-ttu-id="c7ffa-307">JSON element</span><span class="sxs-lookup"><span data-stu-id="c7ffa-307">JSON element</span></span> | <span data-ttu-id="c7ffa-308">Description</span><span class="sxs-lookup"><span data-stu-id="c7ffa-308">Description</span></span> | <span data-ttu-id="c7ffa-309">Valid values</span><span class="sxs-lookup"><span data-stu-id="c7ffa-309">Valid values</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c7ffa-310">**minutes**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-310">**minutes**</span></span> | <span data-ttu-id="c7ffa-311">Minutes of the hour at which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-311">Minutes of the hour at which the trigger runs.</span></span> | <ul><li><span data-ttu-id="c7ffa-312">Integer</span><span class="sxs-lookup"><span data-stu-id="c7ffa-312">Integer</span></span></li><li><span data-ttu-id="c7ffa-313">Array of integers</span><span class="sxs-lookup"><span data-stu-id="c7ffa-313">Array of integers</span></span></li></ul>
| <span data-ttu-id="c7ffa-314">**hours**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-314">**hours**</span></span> | <span data-ttu-id="c7ffa-315">Hours of the day at which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-315">Hours of the day at which the trigger runs.</span></span> | <ul><li><span data-ttu-id="c7ffa-316">Integer</span><span class="sxs-lookup"><span data-stu-id="c7ffa-316">Integer</span></span></li><li><span data-ttu-id="c7ffa-317">Array of integers</span><span class="sxs-lookup"><span data-stu-id="c7ffa-317">Array of integers</span></span></li></ul> |
| <span data-ttu-id="c7ffa-318">**weekDays**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-318">**weekDays**</span></span> | <span data-ttu-id="c7ffa-319">Days of the week on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-319">Days of the week on which the trigger runs.</span></span> <span data-ttu-id="c7ffa-320">The value can be specified with a weekly frequency only.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-320">The value can be specified with a weekly frequency only.</span></span> | <ul><li><span data-ttu-id="c7ffa-321">Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="c7ffa-321">Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span></li><li><span data-ttu-id="c7ffa-322">Array of day values (maximum array size is 7)</span><span class="sxs-lookup"><span data-stu-id="c7ffa-322">Array of day values (maximum array size is 7)</span></span></li><li><span data-ttu-id="c7ffa-323">Day values are not case-sensitive</span><span class="sxs-lookup"><span data-stu-id="c7ffa-323">Day values are not case-sensitive</span></span></li></ul> |
| <span data-ttu-id="c7ffa-324">**monthlyOccurrences**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-324">**monthlyOccurrences**</span></span> | <span data-ttu-id="c7ffa-325">Days of the month on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-325">Days of the month on which the trigger runs.</span></span> <span data-ttu-id="c7ffa-326">The value can be specified with a monthly frequency only.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-326">The value can be specified with a monthly frequency only.</span></span> | <ul><li><span data-ttu-id="c7ffa-327">Array of **monthlyOccurence** objects: `{ "day": day,  "occurrence": occurence }`.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-327">Array of **monthlyOccurence** objects: `{ "day": day,  "occurrence": occurence }`.</span></span></li><li><span data-ttu-id="c7ffa-328">The **day** attribute is the day of the week on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-328">The **day** attribute is the day of the week on which the trigger runs.</span></span> <span data-ttu-id="c7ffa-329">For example, a **monthlyOccurrences** property with a **day** value of `{Sunday}` means every Sunday of the month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-329">For example, a **monthlyOccurrences** property with a **day** value of `{Sunday}` means every Sunday of the month.</span></span> <span data-ttu-id="c7ffa-330">The **day** attribute is required.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-330">The **day** attribute is required.</span></span></li><li><span data-ttu-id="c7ffa-331">The **occurrence** attribute is the occurrence of the specified **day** during the month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-331">The **occurrence** attribute is the occurrence of the specified **day** during the month.</span></span> <span data-ttu-id="c7ffa-332">For example, a **monthlyOccurrences** property with **day** and **occurrence** values of `{Sunday, -1}` means the last Sunday of the month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-332">For example, a **monthlyOccurrences** property with **day** and **occurrence** values of `{Sunday, -1}` means the last Sunday of the month.</span></span> <span data-ttu-id="c7ffa-333">The **occurrence** attribute is optional.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-333">The **occurrence** attribute is optional.</span></span></li></ul> |
| <span data-ttu-id="c7ffa-334">**monthDays**</span><span class="sxs-lookup"><span data-stu-id="c7ffa-334">**monthDays**</span></span> | <span data-ttu-id="c7ffa-335">Day of the month on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-335">Day of the month on which the trigger runs.</span></span> <span data-ttu-id="c7ffa-336">The value can be specified with a monthly frequency only.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-336">The value can be specified with a monthly frequency only.</span></span> | <ul><li><span data-ttu-id="c7ffa-337">Any value <= -1 and >= -31</span><span class="sxs-lookup"><span data-stu-id="c7ffa-337">Any value <= -1 and >= -31</span></span></li><li><span data-ttu-id="c7ffa-338">Any value >= 1 and <= 31</span><span class="sxs-lookup"><span data-stu-id="c7ffa-338">Any value >= 1 and <= 31</span></span></li><li><span data-ttu-id="c7ffa-339">Array of values</span><span class="sxs-lookup"><span data-stu-id="c7ffa-339">Array of values</span></span></li></ul> |


## <a name="examples-of-trigger-recurrence-schedules"></a><span data-ttu-id="c7ffa-340">Examples of trigger recurrence schedules</span><span class="sxs-lookup"><span data-stu-id="c7ffa-340">Examples of trigger recurrence schedules</span></span>
<span data-ttu-id="c7ffa-341">This section provides examples of recurrence schedules and focuses on the **schedule** object and its elements.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-341">This section provides examples of recurrence schedules and focuses on the **schedule** object and its elements.</span></span>

<span data-ttu-id="c7ffa-342">The examples assume that the **interval** value is 1, and that the **frequency** value is correct according to the schedule definition.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-342">The examples assume that the **interval** value is 1, and that the **frequency** value is correct according to the schedule definition.</span></span> <span data-ttu-id="c7ffa-343">For example, you can't have a **frequency** value of "day" and also have a "monthDays" modification in the **schedule** object.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-343">For example, you can't have a **frequency** value of "day" and also have a "monthDays" modification in the **schedule** object.</span></span> <span data-ttu-id="c7ffa-344">Restrictions such as these are mentioned in the table in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-344">Restrictions such as these are mentioned in the table in the previous section.</span></span>

| <span data-ttu-id="c7ffa-345">Example</span><span class="sxs-lookup"><span data-stu-id="c7ffa-345">Example</span></span> | <span data-ttu-id="c7ffa-346">Description</span><span class="sxs-lookup"><span data-stu-id="c7ffa-346">Description</span></span> |
|:--- |:--- |
| `{"hours":[5]}` | <span data-ttu-id="c7ffa-347">Run at 5:00 AM every day.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-347">Run at 5:00 AM every day.</span></span> |
| `{"minutes":[15], "hours":[5]}` | <span data-ttu-id="c7ffa-348">Run at 5:15 AM every day.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-348">Run at 5:15 AM every day.</span></span> |
| `{"minutes":[15], "hours":[5,17]}` | <span data-ttu-id="c7ffa-349">Run at 5:15 AM and 5:15 PM every day.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-349">Run at 5:15 AM and 5:15 PM every day.</span></span> |
| `{"minutes":[15,45], "hours":[5,17]}` | <span data-ttu-id="c7ffa-350">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM every day.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-350">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM every day.</span></span> |
| `{"minutes":[0,15,30,45]}` | <span data-ttu-id="c7ffa-351">Run every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-351">Run every 15 minutes.</span></span> |
| `{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}` | <span data-ttu-id="c7ffa-352">Run every hour.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-352">Run every hour.</span></span> <span data-ttu-id="c7ffa-353">This trigger runs every hour.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-353">This trigger runs every hour.</span></span> <span data-ttu-id="c7ffa-354">The minutes are controlled by the **startTime** value, when a value is specified.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-354">The minutes are controlled by the **startTime** value, when a value is specified.</span></span> <span data-ttu-id="c7ffa-355">If a value not specified, the minutes are controlled by the creation time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-355">If a value not specified, the minutes are controlled by the creation time.</span></span> <span data-ttu-id="c7ffa-356">For example, if the start time or creation time (whichever applies) is 12:25 PM, the trigger runs at 00:25, 01:25, 02:25, ..., and 23:25.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-356">For example, if the start time or creation time (whichever applies) is 12:25 PM, the trigger runs at 00:25, 01:25, 02:25, ..., and 23:25.</span></span><br/><br/><span data-ttu-id="c7ffa-357">This schedule is equivalent to having a trigger with a **frequency** value of "hour," an **interval** value of 1, and no **schedule**.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-357">This schedule is equivalent to having a trigger with a **frequency** value of "hour," an **interval** value of 1, and no **schedule**.</span></span>  <span data-ttu-id="c7ffa-358">This schedule can be used with different **frequency** and **interval** values to create other triggers.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-358">This schedule can be used with different **frequency** and **interval** values to create other triggers.</span></span> <span data-ttu-id="c7ffa-359">For example, when the **frequency** value is "month," the schedule runs only once a month, rather than every day, when the **frequency** value is "day."</span><span class="sxs-lookup"><span data-stu-id="c7ffa-359">For example, when the **frequency** value is "month," the schedule runs only once a month, rather than every day, when the **frequency** value is "day."</span></span> |
| `{"minutes":[0]}` | <span data-ttu-id="c7ffa-360">Run every hour on the hour.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-360">Run every hour on the hour.</span></span> <span data-ttu-id="c7ffa-361">This trigger runs every hour on the hour starting at 12:00 AM, 1:00 AM, 2:00 AM, and so on.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-361">This trigger runs every hour on the hour starting at 12:00 AM, 1:00 AM, 2:00 AM, and so on.</span></span><br/><br/><span data-ttu-id="c7ffa-362">This schedule is equivalent to a trigger with a **frequency** value of "hour" and a **startTime** value of zero minutes, or no **schedule** but a **frequency** value of "day."</span><span class="sxs-lookup"><span data-stu-id="c7ffa-362">This schedule is equivalent to a trigger with a **frequency** value of "hour" and a **startTime** value of zero minutes, or no **schedule** but a **frequency** value of "day."</span></span> <span data-ttu-id="c7ffa-363">If the **frequency** value is "week" or "month," the schedule executes one day a week or one day a month only, respectively.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-363">If the **frequency** value is "week" or "month," the schedule executes one day a week or one day a month only, respectively.</span></span> |
| `{"minutes":[15]}` | <span data-ttu-id="c7ffa-364">Run at 15 minutes past every hour.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-364">Run at 15 minutes past every hour.</span></span> <span data-ttu-id="c7ffa-365">This trigger runs every hour at 15 minutes past the hour starting at 00:15 AM, 1:15 AM, 2:15 AM, and so on, and ending at 11:15 PM.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-365">This trigger runs every hour at 15 minutes past the hour starting at 00:15 AM, 1:15 AM, 2:15 AM, and so on, and ending at 11:15 PM.</span></span> |
| `{"hours":[17], "weekDays":["saturday"]}` | <span data-ttu-id="c7ffa-366">Run at 5:00 PM on Saturdays every week.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-366">Run at 5:00 PM on Saturdays every week.</span></span> |
| `{"hours":[17], "weekDays":["monday", "wednesday", "friday"]}` | <span data-ttu-id="c7ffa-367">Run at 5:00 PM on Monday, Wednesday, and Friday every week.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-367">Run at 5:00 PM on Monday, Wednesday, and Friday every week.</span></span> |
| `{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}` | <span data-ttu-id="c7ffa-368">Run at 5:15 PM and 5:45 PM on Monday, Wednesday, and Friday every week.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-368">Run at 5:15 PM and 5:45 PM on Monday, Wednesday, and Friday every week.</span></span> |
| `{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}` | <span data-ttu-id="c7ffa-369">Run every 15 minutes on weekdays.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-369">Run every 15 minutes on weekdays.</span></span> |
| `{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}` | <span data-ttu-id="c7ffa-370">Run every 15 minutes on weekdays between 9:00 AM and 4:45 PM.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-370">Run every 15 minutes on weekdays between 9:00 AM and 4:45 PM.</span></span> |
| `{"weekDays":["tuesday", "thursday"]}` | <span data-ttu-id="c7ffa-371">Run on Tuesdays and Thursdays at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-371">Run on Tuesdays and Thursdays at the specified start time.</span></span> |
| `{"minutes":[0], "hours":[6], "monthDays":[28]}` | <span data-ttu-id="c7ffa-372">Run at 6:00 AM on the 28th day of every month (assuming a **frequency** value of "month").</span><span class="sxs-lookup"><span data-stu-id="c7ffa-372">Run at 6:00 AM on the 28th day of every month (assuming a **frequency** value of "month").</span></span> |
| `{"minutes":[0], "hours":[6], "monthDays":[-1]}` | <span data-ttu-id="c7ffa-373">Run at 6:00 AM on the last day of the month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-373">Run at 6:00 AM on the last day of the month.</span></span> <span data-ttu-id="c7ffa-374">To run a trigger on the last day of a month, use -1 instead of day 28, 29, 30, or 31.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-374">To run a trigger on the last day of a month, use -1 instead of day 28, 29, 30, or 31.</span></span> |
| `{"minutes":[0], "hours":[6], "monthDays":[1,-1]}` | <span data-ttu-id="c7ffa-375">Run at 6:00 AM on the first and last day of every month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-375">Run at 6:00 AM on the first and last day of every month.</span></span> |
| `{monthDays":[1,14]}` | <span data-ttu-id="c7ffa-376">Run on the first and 14th day of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-376">Run on the first and 14th day of every month at the specified start time.</span></span> |
| `{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}` | <span data-ttu-id="c7ffa-377">Run on the first Friday of every month at 5:00 AM.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-377">Run on the first Friday of every month at 5:00 AM.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}` | <span data-ttu-id="c7ffa-378">Run on the first Friday of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-378">Run on the first Friday of every month at the specified start time.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}` | <span data-ttu-id="c7ffa-379">Run on the third Friday from the end of the month, every month, at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-379">Run on the third Friday from the end of the month, every month, at the specified start time.</span></span> |
| `{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}` | <span data-ttu-id="c7ffa-380">Run on the first and last Friday of every month at 5:15 AM.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-380">Run on the first and last Friday of every month at 5:15 AM.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}` | <span data-ttu-id="c7ffa-381">Run on the first and last Friday of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-381">Run on the first and last Friday of every month at the specified start time.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}` | <span data-ttu-id="c7ffa-382">Run on the fifth Friday of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-382">Run on the fifth Friday of every month at the specified start time.</span></span> <span data-ttu-id="c7ffa-383">When there's no fifth Friday in a month, the pipeline doesn't run, since it's scheduled to run only on fifth Fridays.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-383">When there's no fifth Friday in a month, the pipeline doesn't run, since it's scheduled to run only on fifth Fridays.</span></span> <span data-ttu-id="c7ffa-384">To run the trigger on the last occurring Friday of the month, consider using -1 instead of 5 for the **occurrence** value.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-384">To run the trigger on the last occurring Friday of the month, consider using -1 instead of 5 for the **occurrence** value.</span></span> |
| `{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}` | <span data-ttu-id="c7ffa-385">Run every 15 minutes on the last Friday of the month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-385">Run every 15 minutes on the last Friday of the month.</span></span> |
| `{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}` | <span data-ttu-id="c7ffa-386">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM on the third Wednesday of every month.</span><span class="sxs-lookup"><span data-stu-id="c7ffa-386">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM on the third Wednesday of every month.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c7ffa-387">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7ffa-387">Next steps</span></span>
<span data-ttu-id="c7ffa-388">For detailed information about triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md#triggers).</span><span class="sxs-lookup"><span data-stu-id="c7ffa-388">For detailed information about triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md#triggers).</span></span>
