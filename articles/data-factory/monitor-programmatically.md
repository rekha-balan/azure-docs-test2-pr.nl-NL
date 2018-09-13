---
title: Programmatically monitor an Azure data factory | Microsoft Docs
description: Learn how to monitor a pipeline in a data factory by using different software development kits (SDKs).
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/16/2018
ms.author: douglasl
ms.openlocfilehash: 343af57cc8f3e63965dc1fe1827b2945009ea8bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867145"
---
# <a name="programmatically-monitor-an-azure-data-factory"></a><span data-ttu-id="dd4fe-103">Programmatically monitor an Azure data factory</span><span class="sxs-lookup"><span data-stu-id="dd4fe-103">Programmatically monitor an Azure data factory</span></span>
<span data-ttu-id="dd4fe-104">This article describes how to monitor a pipeline in a data factory by using different software development kits (SDKs).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-104">This article describes how to monitor a pipeline in a data factory by using different software development kits (SDKs).</span></span> 

## <a name="data-range"></a><span data-ttu-id="dd4fe-105">Data range</span><span class="sxs-lookup"><span data-stu-id="dd4fe-105">Data range</span></span>

<span data-ttu-id="dd4fe-106">Data Factory only stores pipeline run data for 45 days.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-106">Data Factory only stores pipeline run data for 45 days.</span></span> <span data-ttu-id="dd4fe-107">When you query programmatically for data about Data Factory pipeline runs - for example, with the PowerShell command `Get-AzureRmDataFactoryV2PipelineRun` - there are no maximum dates for the optional `LastUpdatedAfter` and `LastUpdatedBefore` parameters.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-107">When you query programmatically for data about Data Factory pipeline runs - for example, with the PowerShell command `Get-AzureRmDataFactoryV2PipelineRun` - there are no maximum dates for the optional `LastUpdatedAfter` and `LastUpdatedBefore` parameters.</span></span> <span data-ttu-id="dd4fe-108">But if you query for data for the past year, for example, the query does not return an error, but only returns pipeline run data from the last 45 days.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-108">But if you query for data for the past year, for example, the query does not return an error, but only returns pipeline run data from the last 45 days.</span></span>

<span data-ttu-id="dd4fe-109">If you want to persist pipeline run data for more than 45 days, set up your own diagnostic logging with [Azure Monitor](monitor-using-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-109">If you want to persist pipeline run data for more than 45 days, set up your own diagnostic logging with [Azure Monitor](monitor-using-azure-monitor.md).</span></span>

## <a name="net"></a><span data-ttu-id="dd4fe-110">.NET</span><span class="sxs-lookup"><span data-stu-id="dd4fe-110">.NET</span></span>
<span data-ttu-id="dd4fe-111">For a complete walkthrough of creating and monitoring a pipeline using .NET SDK, see [Create a data factory and pipeline using .NET](quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-111">For a complete walkthrough of creating and monitoring a pipeline using .NET SDK, see [Create a data factory and pipeline using .NET](quickstart-create-data-factory-dot-net.md).</span></span>

1. <span data-ttu-id="dd4fe-112">Add the following code to continuously check the status of the pipeline run until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-112">Add the following code to continuously check the status of the pipeline run until it finishes copying the data.</span></span>

    ```csharp
    // Monitor the pipeline run
    Console.WriteLine("Checking pipeline run status...");
    PipelineRun pipelineRun;
    while (true)
    {
        pipelineRun = client.PipelineRuns.Get(resourceGroup, dataFactoryName, runResponse.RunId);
        Console.WriteLine("Status: " + pipelineRun.Status);
        if (pipelineRun.Status == "InProgress")
            System.Threading.Thread.Sleep(15000);
        else
            break;
    }
    ```

2. <span data-ttu-id="dd4fe-113">Add the following code to that retrieves copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-113">Add the following code to that retrieves copy activity run details, for example, size of the data read/written.</span></span>

    ```csharp
    // Check the copy activity run details
    Console.WriteLine("Checking copy activity run details...");
   
    List<ActivityRun> activityRuns = client.ActivityRuns.ListByPipelineRun(
    resourceGroup, dataFactoryName, runResponse.RunId, DateTime.UtcNow.AddMinutes(-10), DateTime.UtcNow.AddMinutes(10)).ToList(); 
    if (pipelineRun.Status == "Succeeded")
        Console.WriteLine(activityRuns.First().Output);
    else
        Console.WriteLine(activityRuns.First().Error);
    Console.WriteLine("\nPress any key to exit...");
    Console.ReadKey();
    ```

<span data-ttu-id="dd4fe-114">For complete documentation on .NET SDK, see [Data Factory .NET SDK reference](/dotnet/api/microsoft.azure.management.datafactory?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-114">For complete documentation on .NET SDK, see [Data Factory .NET SDK reference](/dotnet/api/microsoft.azure.management.datafactory?view=azure-dotnet).</span></span>

## <a name="python"></a><span data-ttu-id="dd4fe-115">Python</span><span class="sxs-lookup"><span data-stu-id="dd4fe-115">Python</span></span>
<span data-ttu-id="dd4fe-116">For a complete walkthrough of creating and monitoring a pipeline using Python SDK, see [Create a data factory and pipeline using Python](quickstart-create-data-factory-python.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-116">For a complete walkthrough of creating and monitoring a pipeline using Python SDK, see [Create a data factory and pipeline using Python](quickstart-create-data-factory-python.md).</span></span>

<span data-ttu-id="dd4fe-117">To monitor the pipeline run, add the following code:</span><span class="sxs-lookup"><span data-stu-id="dd4fe-117">To monitor the pipeline run, add the following code:</span></span>

```python
#Monitor the pipeline run
time.sleep(30)
pipeline_run = adf_client.pipeline_runs.get(rg_name, df_name, run_response.run_id)
print("\n\tPipeline run status: {}".format(pipeline_run.status))
activity_runs_paged = list(adf_client.activity_runs.list_by_pipeline_run(rg_name, df_name, pipeline_run.run_id, datetime.now() - timedelta(1),  datetime.now() + timedelta(1)))
print_activity_run_details(activity_runs_paged[0])
```

<span data-ttu-id="dd4fe-118">For complete documentation on Python SDK, see [Data Factory Python SDK reference](/python/api/overview/azure/datafactory?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-118">For complete documentation on Python SDK, see [Data Factory Python SDK reference](/python/api/overview/azure/datafactory?view=azure-python).</span></span>

## <a name="rest-api"></a><span data-ttu-id="dd4fe-119">REST API</span><span class="sxs-lookup"><span data-stu-id="dd4fe-119">REST API</span></span>
<span data-ttu-id="dd4fe-120">For a complete walkthrough of creating and monitoring a pipeline using REST API, see [Create a data factory and pipeline using REST API](quickstart-create-data-factory-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-120">For a complete walkthrough of creating and monitoring a pipeline using REST API, see [Create a data factory and pipeline using REST API](quickstart-create-data-factory-rest-api.md).</span></span>
 
1. <span data-ttu-id="dd4fe-121">Run the following script to continuously check the pipeline run status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-121">Run the following script to continuously check the pipeline run status until it finishes copying the data.</span></span>

    ```powershell
    $request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/pipelineruns/${runId}?api-version=${apiVersion}"
    while ($True) {
        $response = Invoke-RestMethod -Method GET -Uri $request -Header $authHeader
        Write-Host  "Pipeline run status: " $response.Status -foregroundcolor "Yellow"

        if ($response.Status -eq "InProgress") {
            Start-Sleep -Seconds 15
        }
        else {
            $response | ConvertTo-Json
            break
        }
    }
    ```
2. <span data-ttu-id="dd4fe-122">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-122">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span></span>

    ```PowerShell
    $request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/pipelineruns/${runId}/activityruns?api-version=${apiVersion}&startTime="+(Get-Date).ToString('yyyy-MM-dd')+"&endTime="+(Get-Date).AddDays(1).ToString('yyyy-MM-dd')+"&pipelineName=Adfv2QuickStartPipeline"
    $response = Invoke-RestMethod -Method GET -Uri $request -Header $authHeader
    $response | ConvertTo-Json
    ```

<span data-ttu-id="dd4fe-123">For complete documentation on REST API, see [Data Factory REST API reference](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-123">For complete documentation on REST API, see [Data Factory REST API reference](/rest/api/datafactory/).</span></span>

## <a name="powershell"></a><span data-ttu-id="dd4fe-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd4fe-124">PowerShell</span></span>
<span data-ttu-id="dd4fe-125">For a complete walkthrough of creating and monitoring a pipeline using PowerShell, see [Create a data factory and pipeline using PowerShell](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-125">For a complete walkthrough of creating and monitoring a pipeline using PowerShell, see [Create a data factory and pipeline using PowerShell](quickstart-create-data-factory-powershell.md).</span></span>

1. <span data-ttu-id="dd4fe-126">Run the following script to continuously check the pipeline run status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-126">Run the following script to continuously check the pipeline run status until it finishes copying the data.</span></span>

    ```powershell
    while ($True) {
        $run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $resourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $runId

        if ($run) {
            if ($run.Status -ne 'InProgress') {
                Write-Host "Pipeline run finished. The status is: " $run.Status -foregroundcolor "Yellow"
                $run
                break
            }
            Write-Host  "Pipeline is running...status: InProgress" -foregroundcolor "Yellow"
        }

        Start-Sleep -Seconds 30
    }
    ```
2. <span data-ttu-id="dd4fe-127">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-127">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span></span>

    ```powershell
    Write-Host "Activity run details:" -foregroundcolor "Yellow"
    $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    $result
    
    Write-Host "Activity 'Output' section:" -foregroundcolor "Yellow"
    $result.Output -join "`r`n"
    
    Write-Host "\nActivity 'Error' section:" -foregroundcolor "Yellow"
    $result.Error -join "`r`n"
    ```

<span data-ttu-id="dd4fe-128">For complete documentation on PowerShell cmdlets, see [Data Factory PowerShell cmdlet reference](/powershell/module/azurerm.datafactoryv2/?view=azurermps-4.4.1).</span><span class="sxs-lookup"><span data-stu-id="dd4fe-128">For complete documentation on PowerShell cmdlets, see [Data Factory PowerShell cmdlet reference](/powershell/module/azurerm.datafactoryv2/?view=azurermps-4.4.1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd4fe-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd4fe-129">Next steps</span></span>
<span data-ttu-id="dd4fe-130">See [Monitor pipelines using Azure Monitor](monitor-using-azure-monitor.md) article to learn about using Azure Monitor to monitor Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="dd4fe-130">See [Monitor pipelines using Azure Monitor](monitor-using-azure-monitor.md) article to learn about using Azure Monitor to monitor Data Factory pipelines.</span></span> 

