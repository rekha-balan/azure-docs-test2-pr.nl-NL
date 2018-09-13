---
title: Monitor Batch with Azure Application Insights | Microsoft Docs
description: Learn how to instrument an Azure Batch .NET application using the Azure Application Insights library.
services: batch
author: dlepow
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: .NET
ms.topic: article
ms.workload: na
ms.date: 04/05/2018
ms.author: danlep
ms.openlocfilehash: 5e0358ebf525c39c09df4268971fa71c02457821
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869161"
---
# <a name="monitor-and-debug-an-azure-batch-net-application-with-application-insights"></a><span data-ttu-id="41176-103">Monitor and debug an Azure Batch .NET application with Application Insights</span><span class="sxs-lookup"><span data-stu-id="41176-103">Monitor and debug an Azure Batch .NET application with Application Insights</span></span>

<span data-ttu-id="41176-104">[Application Insights](../application-insights/app-insights-overview.md) provides an elegant and powerful way for developers to monitor and debug applications deployed to Azure services.</span><span class="sxs-lookup"><span data-stu-id="41176-104">[Application Insights](../application-insights/app-insights-overview.md) provides an elegant and powerful way for developers to monitor and debug applications deployed to Azure services.</span></span> <span data-ttu-id="41176-105">Use Application Insights to monitor performance counters and exceptions as well as instrument your code with custom metrics and tracing.</span><span class="sxs-lookup"><span data-stu-id="41176-105">Use Application Insights to monitor performance counters and exceptions as well as instrument your code with custom metrics and tracing.</span></span> <span data-ttu-id="41176-106">Integrating Application Insights with your Azure Batch application allows you to gain deep insights into behaviors and investigate issues in near-real time.</span><span class="sxs-lookup"><span data-stu-id="41176-106">Integrating Application Insights with your Azure Batch application allows you to gain deep insights into behaviors and investigate issues in near-real time.</span></span>

<span data-ttu-id="41176-107">This article shows how to add and configure the Application Insights library into your Azure Batch .NET solution and instrument your application code.</span><span class="sxs-lookup"><span data-stu-id="41176-107">This article shows how to add and configure the Application Insights library into your Azure Batch .NET solution and instrument your application code.</span></span> <span data-ttu-id="41176-108">It also shows ways to monitor your application via the Azure portal and build custom dashboards.</span><span class="sxs-lookup"><span data-stu-id="41176-108">It also shows ways to monitor your application via the Azure portal and build custom dashboards.</span></span> <span data-ttu-id="41176-109">For Application Insights support in other languages, look at the [languages, platforms, and integrations documentation](../application-insights/app-insights-platforms.md).</span><span class="sxs-lookup"><span data-stu-id="41176-109">For Application Insights support in other languages, look at the [languages, platforms, and integrations documentation](../application-insights/app-insights-platforms.md).</span></span>

<span data-ttu-id="41176-110">A sample C# solution with code to accompany this article is available on [GitHub](https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ApplicationInsights).</span><span class="sxs-lookup"><span data-stu-id="41176-110">A sample C# solution with code to accompany this article is available on [GitHub](https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ApplicationInsights).</span></span> <span data-ttu-id="41176-111">This example adds Application Insights instrumentation code to the [TopNWords](https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords) example.</span><span class="sxs-lookup"><span data-stu-id="41176-111">This example adds Application Insights instrumentation code to the [TopNWords](https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords) example.</span></span> <span data-ttu-id="41176-112">If you're not familiar with that example, try building and running TopNWords first.</span><span class="sxs-lookup"><span data-stu-id="41176-112">If you're not familiar with that example, try building and running TopNWords first.</span></span> <span data-ttu-id="41176-113">Doing this will help you understand a basic Batch workflow of processing a set of input blobs in parallel on multiple compute nodes.</span><span class="sxs-lookup"><span data-stu-id="41176-113">Doing this will help you understand a basic Batch workflow of processing a set of input blobs in parallel on multiple compute nodes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="41176-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="41176-114">Prerequisites</span></span>
* [<span data-ttu-id="41176-115">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="41176-115">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs)

* [<span data-ttu-id="41176-116">Batch account and linked storage account</span><span class="sxs-lookup"><span data-stu-id="41176-116">Batch account and linked storage account</span></span>](batch-account-create-portal.md)

* [<span data-ttu-id="41176-117">Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="41176-117">Application Insights resource</span></span>](../application-insights/app-insights-create-new-resource.md)
  
   * <span data-ttu-id="41176-118">Use the Azure portal to create an Application Insights *resource*.</span><span class="sxs-lookup"><span data-stu-id="41176-118">Use the Azure portal to create an Application Insights *resource*.</span></span> <span data-ttu-id="41176-119">Select the *General* **Application type**.</span><span class="sxs-lookup"><span data-stu-id="41176-119">Select the *General* **Application type**.</span></span>

   * <span data-ttu-id="41176-120">Copy the [instrumentation key](../application-insights/app-insights-create-new-resource.md#copy-the-instrumentation-key) from the portal.</span><span class="sxs-lookup"><span data-stu-id="41176-120">Copy the [instrumentation key](../application-insights/app-insights-create-new-resource.md#copy-the-instrumentation-key) from the portal.</span></span> <span data-ttu-id="41176-121">It is required later in this article.</span><span class="sxs-lookup"><span data-stu-id="41176-121">It is required later in this article.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="41176-122">You may be [charged](https://azure.microsoft.com/pricing/details/application-insights/) for the data stored in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="41176-122">You may be [charged](https://azure.microsoft.com/pricing/details/application-insights/) for the data stored in Application Insights.</span></span> <span data-ttu-id="41176-123">This includes the diagnostic and monitoring data discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="41176-123">This includes the diagnostic and monitoring data discussed in this article.</span></span>
  > 

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="41176-124">Add Application Insights to your project</span><span class="sxs-lookup"><span data-stu-id="41176-124">Add Application Insights to your project</span></span>

<span data-ttu-id="41176-125">The **Microsoft.ApplicationInsights.WindowsServer** NuGet package and its dependencies are required for your project.</span><span class="sxs-lookup"><span data-stu-id="41176-125">The **Microsoft.ApplicationInsights.WindowsServer** NuGet package and its dependencies are required for your project.</span></span> <span data-ttu-id="41176-126">Add or restore them to your application's project.</span><span class="sxs-lookup"><span data-stu-id="41176-126">Add or restore them to your application's project.</span></span> <span data-ttu-id="41176-127">To install the package, use the `Install-Package` command or NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="41176-127">To install the package, use the `Install-Package` command or NuGet Package Manager.</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights.WindowsServer
```
<span data-ttu-id="41176-128">Reference Application Insights from your .NET application by using the **Microsoft.ApplicationInsights** namespace.</span><span class="sxs-lookup"><span data-stu-id="41176-128">Reference Application Insights from your .NET application by using the **Microsoft.ApplicationInsights** namespace.</span></span>

## <a name="instrument-your-code"></a><span data-ttu-id="41176-129">Instrument your code</span><span class="sxs-lookup"><span data-stu-id="41176-129">Instrument your code</span></span>

<span data-ttu-id="41176-130">To instrument your code, your solution needs to create an Application Insights [TelemetryClient](/dotnet/api/microsoft.applicationinsights.telemetryclient).</span><span class="sxs-lookup"><span data-stu-id="41176-130">To instrument your code, your solution needs to create an Application Insights [TelemetryClient](/dotnet/api/microsoft.applicationinsights.telemetryclient).</span></span> <span data-ttu-id="41176-131">In the example, the TelemetryClient loads its configuration from the [ApplicationInsights.config](../application-insights/app-insights-configuration-with-applicationinsights-config.md) file.</span><span class="sxs-lookup"><span data-stu-id="41176-131">In the example, the TelemetryClient loads its configuration from the [ApplicationInsights.config](../application-insights/app-insights-configuration-with-applicationinsights-config.md) file.</span></span> <span data-ttu-id="41176-132">Be sure to update ApplicationInsights.config in the following projects with your Application Insights instrumentation key: Microsoft.Azure.Batch.Samples.TelemetryStartTask and TopNWordsSample.</span><span class="sxs-lookup"><span data-stu-id="41176-132">Be sure to update ApplicationInsights.config in the following projects with your Application Insights instrumentation key: Microsoft.Azure.Batch.Samples.TelemetryStartTask and TopNWordsSample.</span></span>

```xml
<InstrumentationKey>YOUR-IKEY-GOES-HERE</InstrumentationKey>
```
<span data-ttu-id="41176-133">Also add the instrumentation key in the file TopNWords.cs.</span><span class="sxs-lookup"><span data-stu-id="41176-133">Also add the instrumentation key in the file TopNWords.cs.</span></span>

<span data-ttu-id="41176-134">The example in TopNWords.cs uses the following [instrumentation calls](../application-insights/app-insights-api-custom-events-metrics.md) from the Application Insights API:</span><span class="sxs-lookup"><span data-stu-id="41176-134">The example in TopNWords.cs uses the following [instrumentation calls](../application-insights/app-insights-api-custom-events-metrics.md) from the Application Insights API:</span></span>
* <span data-ttu-id="41176-135">`TrackMetric()` - Tracks how long, on average, a compute node takes to download the required text file.</span><span class="sxs-lookup"><span data-stu-id="41176-135">`TrackMetric()` - Tracks how long, on average, a compute node takes to download the required text file.</span></span>
* <span data-ttu-id="41176-136">`TrackTrace()` - Adds debugging calls to your code.</span><span class="sxs-lookup"><span data-stu-id="41176-136">`TrackTrace()` - Adds debugging calls to your code.</span></span>
* <span data-ttu-id="41176-137">`TrackEvent()` - Tracks interesting events to capture.</span><span class="sxs-lookup"><span data-stu-id="41176-137">`TrackEvent()` - Tracks interesting events to capture.</span></span>

<span data-ttu-id="41176-138">This example purposely leaves out exception handling.</span><span class="sxs-lookup"><span data-stu-id="41176-138">This example purposely leaves out exception handling.</span></span> <span data-ttu-id="41176-139">Instead, Application Insights automatically reports unhandled exceptions, which significantly improves the debugging experience.</span><span class="sxs-lookup"><span data-stu-id="41176-139">Instead, Application Insights automatically reports unhandled exceptions, which significantly improves the debugging experience.</span></span> 

<span data-ttu-id="41176-140">The following snippet illustrates how to use these methods.</span><span class="sxs-lookup"><span data-stu-id="41176-140">The following snippet illustrates how to use these methods.</span></span>

```csharp
public void CountWords(string blobName, int numTopN, string storageAccountName, string storageAccountKey)
{
    // simulate exception for some set of tasks
    Random rand = new Random();
    if (rand.Next(0, 10) % 10 == 0)
    {
        blobName += ".badUrl";
    }

    // log the url we are downloading the file from
    insightsClient.TrackTrace(new TraceTelemetry(string.Format("Task {0}: Download file from: {1}", this.taskId, blobName), SeverityLevel.Verbose));

    // open the cloud blob that contains the book
    var storageCred = new StorageCredentials(storageAccountName, storageAccountKey);
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(blobName), storageCred);
    using (Stream memoryStream = new MemoryStream())
    {
        // calculate blob download time
        DateTime start = DateTime.Now;
        blob.DownloadToStream(memoryStream);
        TimeSpan downloadTime = DateTime.Now.Subtract(start);

        // track how long the blob takes to download on this node
        // this will help debug timing issues or identify poorly performing nodes
        insightsClient.TrackMetric("Blob download in seconds", downloadTime.TotalSeconds, this.CommonProperties);

        memoryStream.Position = 0; //Reset the stream
        var sr = new StreamReader(memoryStream);
        var myStr = sr.ReadToEnd();
        string[] words = myStr.Split(' ');

        // log how many words were found in the text file
        insightsClient.TrackTrace(new TraceTelemetry(string.Format("Task {0}: Found {1} words", this.taskId, words.Length), SeverityLevel.Verbose));
        var topNWords =
            words.
                Where(word => word.Length > 0).
                GroupBy(word => word, (key, group) => new KeyValuePair<String, long>(key, group.LongCount())).
                OrderByDescending(x => x.Value).
                Take(numTopN).
                ToList();
        foreach (var pair in topNWords)
        {
            Console.WriteLine("{0} {1}", pair.Key, pair.Value);
        }

        // emit an event to track the completion of the task
        insightsClient.TrackEvent("Done counting words");
    }
}
```

### <a name="azure-batch-telemetry-initializer-helper"></a><span data-ttu-id="41176-141">Azure Batch telemetry initializer helper</span><span class="sxs-lookup"><span data-stu-id="41176-141">Azure Batch telemetry initializer helper</span></span>
<span data-ttu-id="41176-142">When reporting telemetry for a given server and instance, Application Insights uses the Azure VM Role and VM name for the default values.</span><span class="sxs-lookup"><span data-stu-id="41176-142">When reporting telemetry for a given server and instance, Application Insights uses the Azure VM Role and VM name for the default values.</span></span> <span data-ttu-id="41176-143">In the context of Azure Batch, the example shows how to use the pool name and compute node name instead.</span><span class="sxs-lookup"><span data-stu-id="41176-143">In the context of Azure Batch, the example shows how to use the pool name and compute node name instead.</span></span> <span data-ttu-id="41176-144">Use a [telemetry initializer](../application-insights/app-insights-api-filtering-sampling.md#add-properties) to override the default values.</span><span class="sxs-lookup"><span data-stu-id="41176-144">Use a [telemetry initializer](../application-insights/app-insights-api-filtering-sampling.md#add-properties) to override the default values.</span></span> 

```csharp
using Microsoft.ApplicationInsights.Channel;
using Microsoft.ApplicationInsights.Extensibility;
using System;
using System.Threading;

namespace Microsoft.Azure.Batch.Samples.TelemetryInitializer
{
    public class AzureBatchNodeTelemetryInitializer : ITelemetryInitializer
    {
        // Azure Batch environment variables
        private const string PoolIdEnvironmentVariable = "AZ_BATCH_POOL_ID";
        private const string NodeIdEnvironmentVariable = "AZ_BATCH_NODE_ID";

        private string roleInstanceName;
        private string roleName;

        public void Initialize(ITelemetry telemetry)
        {
            if (string.IsNullOrEmpty(telemetry.Context.Cloud.RoleName))
            {
                // override the role name with the Azure Batch Pool name
                string name = LazyInitializer.EnsureInitialized(ref this.roleName, this.GetPoolName);
                telemetry.Context.Cloud.RoleName = name;
            }

            if (string.IsNullOrEmpty(telemetry.Context.Cloud.RoleInstance))
            {
                // override the role instance with the Azure Batch Compute Node name
                string name = LazyInitializer.EnsureInitialized(ref this.roleInstanceName, this.GetNodeName);
                telemetry.Context.Cloud.RoleInstance = name;
            }
        }

        private string GetPoolName()
        {
            return Environment.GetEnvironmentVariable(PoolIdEnvironmentVariable) ?? string.Empty;
        }

        private string GetNodeName()
        {
            return Environment.GetEnvironmentVariable(NodeIdEnvironmentVariable) ?? string.Empty;
        }
    }
}
```

<span data-ttu-id="41176-145">To enable the telemetry initializer, the ApplicationInsights.config file in the TopNWordsSample project includes the following:</span><span class="sxs-lookup"><span data-stu-id="41176-145">To enable the telemetry initializer, the ApplicationInsights.config file in the TopNWordsSample project includes the following:</span></span>

```xml
<TelemetryInitializers>
    <Add Type="Microsoft.Azure.Batch.Samples.TelemetryInitializer.AzureBatchNodeTelemetryInitializer, Microsoft.Azure.Batch.Samples.TelemetryInitializer"/>
</TelemetryInitializers>
``` 

## <a name="update-the-job-and-tasks-to-include-application-insights-binaries"></a><span data-ttu-id="41176-146">Update the job and tasks to include Application Insights binaries</span><span class="sxs-lookup"><span data-stu-id="41176-146">Update the job and tasks to include Application Insights binaries</span></span>

<span data-ttu-id="41176-147">In order for Application Insights to run correctly on your compute nodes, make sure the binaries are correctly placed.</span><span class="sxs-lookup"><span data-stu-id="41176-147">In order for Application Insights to run correctly on your compute nodes, make sure the binaries are correctly placed.</span></span> <span data-ttu-id="41176-148">Add the required binaries to your task's resource files collection so that they get downloaded at the time your task executes.</span><span class="sxs-lookup"><span data-stu-id="41176-148">Add the required binaries to your task's resource files collection so that they get downloaded at the time your task executes.</span></span> <span data-ttu-id="41176-149">The following snippets are similar to code in Job.cs.</span><span class="sxs-lookup"><span data-stu-id="41176-149">The following snippets are similar to code in Job.cs.</span></span>

<span data-ttu-id="41176-150">First, create a static list of Application Insights files to upload.</span><span class="sxs-lookup"><span data-stu-id="41176-150">First, create a static list of Application Insights files to upload.</span></span>

```csharp
private static readonly List<string> AIFilesToUpload = new List<string>()
{
    // Application Insights config and assemblies
    "ApplicationInsights.config",
    "Microsoft.ApplicationInsights.dll",
    "Microsoft.AI.Agent.Intercept.dll",
    "Microsoft.AI.DependencyCollector.dll",
    "Microsoft.AI.PerfCounterCollector.dll",
    "Microsoft.AI.ServerTelemetryChannel.dll",
    "Microsoft.AI.WindowsServer.dll",
    
    // custom telemetry initializer assemblies
    "Microsoft.Azure.Batch.Samples.TelemetryInitializer.dll",
 };
...
```

<span data-ttu-id="41176-151">Next, create the staging files that are used by the task.</span><span class="sxs-lookup"><span data-stu-id="41176-151">Next, create the staging files that are used by the task.</span></span>
```csharp
...
// create file staging objects that represent the executable and its dependent assembly to run as the task.
// These files are copied to every node before the corresponding task is scheduled to run on that node.
FileToStage topNWordExe = new FileToStage(TopNWordsExeName, stagingStorageAccount);
FileToStage storageDll = new FileToStage(StorageClientDllName, stagingStorageAccount);

// Upload Application Insights assemblies
List<FileToStage> aiStagedFiles = new List<FileToStage>();
foreach (string aiFile in AIFilesToUpload)
{
    aiStagedFiles.Add(new FileToStage(aiFile, stagingStorageAccount));
}
...
```

<span data-ttu-id="41176-152">The `FileToStage` method is a helper function in the code sample that allows you to easily upload a file from local disk to an Azure Storage blob.</span><span class="sxs-lookup"><span data-stu-id="41176-152">The `FileToStage` method is a helper function in the code sample that allows you to easily upload a file from local disk to an Azure Storage blob.</span></span> <span data-ttu-id="41176-153">Each file is later downloaded to a compute node and referenced by a task.</span><span class="sxs-lookup"><span data-stu-id="41176-153">Each file is later downloaded to a compute node and referenced by a task.</span></span>

<span data-ttu-id="41176-154">Finally, add the tasks to the job and include the necessary Application Insights binaries.</span><span class="sxs-lookup"><span data-stu-id="41176-154">Finally, add the tasks to the job and include the necessary Application Insights binaries.</span></span>
```csharp
...
// initialize a collection to hold the tasks that will be submitted in their entirety
List<CloudTask> tasksToRun = new List<CloudTask>(topNWordsConfiguration.NumberOfTasks);
for (int i = 1; i <= topNWordsConfiguration.NumberOfTasks; i++)
{
    CloudTask task = new CloudTask("task_no_" + i, String.Format("{0} --Task {1} {2} {3} {4}",
        TopNWordsExeName,
        string.Format("https://{0}.blob.core.windows.net/{1}",
            accountSettings.StorageAccountName,
            documents[i]),
        topNWordsConfiguration.TopWordCount,
        accountSettings.StorageAccountName,
        accountSettings.StorageAccountKey));

    //This is the list of files to stage to a container -- for each job, one container is created and 
    //files all resolve to Azure Blobs by their name (so two tasks with the same named file will create just 1 blob in
    //the container).
    task.FilesToStage = new List<IFileStagingProvider>
                        {
                            // required application binaries
                            topNWordExe,
                            storageDll,
                        };
    foreach (FileToStage stagedFile in aiStagedFiles)
   {
        task.FilesToStage.Add(stagedFile);
   }    
    task.RunElevated = false;
    tasksToRun.Add(task);
}
```

## <a name="view-data-in-the-azure-portal"></a><span data-ttu-id="41176-155">View data in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="41176-155">View data in the Azure portal</span></span>

<span data-ttu-id="41176-156">Now that you've configured the job and tasks to use Application Insights, run the example job in your pool.</span><span class="sxs-lookup"><span data-stu-id="41176-156">Now that you've configured the job and tasks to use Application Insights, run the example job in your pool.</span></span> <span data-ttu-id="41176-157">Navigate to the Azure portal and open the Application Insights resource that you provisioned.</span><span class="sxs-lookup"><span data-stu-id="41176-157">Navigate to the Azure portal and open the Application Insights resource that you provisioned.</span></span> <span data-ttu-id="41176-158">After the pool is provisioned, you should start to see data flowing and getting logged.</span><span class="sxs-lookup"><span data-stu-id="41176-158">After the pool is provisioned, you should start to see data flowing and getting logged.</span></span> <span data-ttu-id="41176-159">The rest of this article touches on only a few Application Insights features, but feel free to explore the full feature set.</span><span class="sxs-lookup"><span data-stu-id="41176-159">The rest of this article touches on only a few Application Insights features, but feel free to explore the full feature set.</span></span>

### <a name="view-live-stream-data"></a><span data-ttu-id="41176-160">View live stream data</span><span class="sxs-lookup"><span data-stu-id="41176-160">View live stream data</span></span>

<span data-ttu-id="41176-161">To view trace logs in your Applications Insights resource, click **Live Stream**.</span><span class="sxs-lookup"><span data-stu-id="41176-161">To view trace logs in your Applications Insights resource, click **Live Stream**.</span></span> <span data-ttu-id="41176-162">The following screenshot shows how to view live data coming from the compute nodes in the pool, for example the CPU usage per compute node.</span><span class="sxs-lookup"><span data-stu-id="41176-162">The following screenshot shows how to view live data coming from the compute nodes in the pool, for example the CPU usage per compute node.</span></span>

![Live stream compute node data](./media/monitor-application-insights/applicationinsightslivestream.png)

### <a name="view-trace-logs"></a><span data-ttu-id="41176-164">View trace logs</span><span class="sxs-lookup"><span data-stu-id="41176-164">View trace logs</span></span>

<span data-ttu-id="41176-165">To view trace logs in your Applications Insights resource, click **Search**.</span><span class="sxs-lookup"><span data-stu-id="41176-165">To view trace logs in your Applications Insights resource, click **Search**.</span></span> <span data-ttu-id="41176-166">This view shows a list of diagnostic data captured by Application Insights including traces, events, and exceptions.</span><span class="sxs-lookup"><span data-stu-id="41176-166">This view shows a list of diagnostic data captured by Application Insights including traces, events, and exceptions.</span></span> 

<span data-ttu-id="41176-167">The following screenshot shows how a single trace for a task is logged and later queried for debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="41176-167">The following screenshot shows how a single trace for a task is logged and later queried for debugging purposes.</span></span>

![Trace logs image](./media/monitor-application-insights/tracelogsfortask.png)

### <a name="view-unhandled-exceptions"></a><span data-ttu-id="41176-169">View unhandled exceptions</span><span class="sxs-lookup"><span data-stu-id="41176-169">View unhandled exceptions</span></span>

<span data-ttu-id="41176-170">The following screenshots shows how Application Insights logs exceptions thrown from your application.</span><span class="sxs-lookup"><span data-stu-id="41176-170">The following screenshots shows how Application Insights logs exceptions thrown from your application.</span></span> <span data-ttu-id="41176-171">In this case, within seconds of the application throwing the exception, you can drill into a specific exception and diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="41176-171">In this case, within seconds of the application throwing the exception, you can drill into a specific exception and diagnose the issue.</span></span>

![Unhandled exceptions](./media/monitor-application-insights/exception.png)

### <a name="measure-blob-download-time"></a><span data-ttu-id="41176-173">Measure blob download time</span><span class="sxs-lookup"><span data-stu-id="41176-173">Measure blob download time</span></span>

<span data-ttu-id="41176-174">Custom metrics are also a valuable tool in the portal.</span><span class="sxs-lookup"><span data-stu-id="41176-174">Custom metrics are also a valuable tool in the portal.</span></span> <span data-ttu-id="41176-175">For example, you can display the average time it took each compute node to download the required text file it was processing.</span><span class="sxs-lookup"><span data-stu-id="41176-175">For example, you can display the average time it took each compute node to download the required text file it was processing.</span></span>

<span data-ttu-id="41176-176">To create a sample chart:</span><span class="sxs-lookup"><span data-stu-id="41176-176">To create a sample chart:</span></span>
1. <span data-ttu-id="41176-177">In your Application Insights resource, click **Metrics Explorer** > **Add chart**.</span><span class="sxs-lookup"><span data-stu-id="41176-177">In your Application Insights resource, click **Metrics Explorer** > **Add chart**.</span></span>
2. <span data-ttu-id="41176-178">Click **Edit** on the chart that was added.</span><span class="sxs-lookup"><span data-stu-id="41176-178">Click **Edit** on the chart that was added.</span></span>
2. <span data-ttu-id="41176-179">Update the chart details as follows:</span><span class="sxs-lookup"><span data-stu-id="41176-179">Update the chart details as follows:</span></span>
   * <span data-ttu-id="41176-180">Set **Chart type** to **Grid**.</span><span class="sxs-lookup"><span data-stu-id="41176-180">Set **Chart type** to **Grid**.</span></span>
   * <span data-ttu-id="41176-181">Set **Aggregation** to **Average**.</span><span class="sxs-lookup"><span data-stu-id="41176-181">Set **Aggregation** to **Average**.</span></span>
   * <span data-ttu-id="41176-182">Set **Group by** to **NodeId**.</span><span class="sxs-lookup"><span data-stu-id="41176-182">Set **Group by** to **NodeId**.</span></span>
   * <span data-ttu-id="41176-183">In **Metrics**, select **Custom** > **Blob download in seconds**.</span><span class="sxs-lookup"><span data-stu-id="41176-183">In **Metrics**, select **Custom** > **Blob download in seconds**.</span></span>
   * <span data-ttu-id="41176-184">Adjust display **Color palette** to your choice.</span><span class="sxs-lookup"><span data-stu-id="41176-184">Adjust display **Color palette** to your choice.</span></span> 

![Blob download time per node](./media/monitor-application-insights/blobdownloadtime.png)


## <a name="monitor-compute-nodes-continuously"></a><span data-ttu-id="41176-186">Monitor compute nodes continuously</span><span class="sxs-lookup"><span data-stu-id="41176-186">Monitor compute nodes continuously</span></span>

<span data-ttu-id="41176-187">You may have noticed that all metrics, including performance counters, are only logged when the tasks are running.</span><span class="sxs-lookup"><span data-stu-id="41176-187">You may have noticed that all metrics, including performance counters, are only logged when the tasks are running.</span></span> <span data-ttu-id="41176-188">This behavior is useful because it limits the amount of data that Application Insights logs.</span><span class="sxs-lookup"><span data-stu-id="41176-188">This behavior is useful because it limits the amount of data that Application Insights logs.</span></span> <span data-ttu-id="41176-189">However, there are cases when you would always like to monitor the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="41176-189">However, there are cases when you would always like to monitor the compute nodes.</span></span> <span data-ttu-id="41176-190">For example, they might be running background work which is not scheduled via the Batch service.</span><span class="sxs-lookup"><span data-stu-id="41176-190">For example, they might be running background work which is not scheduled via the Batch service.</span></span> <span data-ttu-id="41176-191">In this case, set up a monitoring process to run for the life of the compute node.</span><span class="sxs-lookup"><span data-stu-id="41176-191">In this case, set up a monitoring process to run for the life of the compute node.</span></span> 

<span data-ttu-id="41176-192">One way to achieve this behavior is to spawn a process that loads the Application Insights library and runs in the background.</span><span class="sxs-lookup"><span data-stu-id="41176-192">One way to achieve this behavior is to spawn a process that loads the Application Insights library and runs in the background.</span></span> <span data-ttu-id="41176-193">In the example, the start task loads the binaries on the machine and keeps a process running indefinitely.</span><span class="sxs-lookup"><span data-stu-id="41176-193">In the example, the start task loads the binaries on the machine and keeps a process running indefinitely.</span></span> <span data-ttu-id="41176-194">Configure the Application Insights configuration file for this process to emit additional data you're interested in, such as performance counters.</span><span class="sxs-lookup"><span data-stu-id="41176-194">Configure the Application Insights configuration file for this process to emit additional data you're interested in, such as performance counters.</span></span>

```csharp
...
 // Batch start task telemetry runner
private const string BatchStartTaskFolderName = "StartTask";
private const string BatchStartTaskTelemetryRunnerName = "Microsoft.Azure.Batch.Samples.TelemetryStartTask.exe";
private const string BatchStartTaskTelemetryRunnerAIConfig = "ApplicationInsights.config";
...
CloudPool pool = client.PoolOperations.CreatePool(
    topNWordsConfiguration.PoolId,
    targetDedicated: topNWordsConfiguration.PoolNodeCount,
    virtualMachineSize: "standard_d1_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));
...

// Create a start task which will run a dummy exe in background that simply emits performance
// counter data as defined in the relevant ApplicationInsights.config.
// Note that the waitForSuccess on the start task was not set so the Compute Node will be
// available immediately after this command is run.
pool.StartTask = new StartTask()
{
    CommandLine = string.Format("cmd /c {0}", BatchStartTaskTelemetryRunnerName),
    ResourceFiles = resourceFiles
};
...
```

> [!TIP]
> <span data-ttu-id="41176-195">To increase the manageability of your solution, you can bundle the assembly in an [application package](./batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="41176-195">To increase the manageability of your solution, you can bundle the assembly in an [application package](./batch-application-packages.md).</span></span> <span data-ttu-id="41176-196">Then, to deploy the application package automatically to your pools, add an application package reference to the pool configuration.</span><span class="sxs-lookup"><span data-stu-id="41176-196">Then, to deploy the application package automatically to your pools, add an application package reference to the pool configuration.</span></span>
>

## <a name="throttle-and-sample-data"></a><span data-ttu-id="41176-197">Throttle and sample data</span><span class="sxs-lookup"><span data-stu-id="41176-197">Throttle and sample data</span></span> 

<span data-ttu-id="41176-198">Due to the large-scale nature of Azure Batch applications running in production, you might want to limit the amount of data collected by Application Insights to manage costs.</span><span class="sxs-lookup"><span data-stu-id="41176-198">Due to the large-scale nature of Azure Batch applications running in production, you might want to limit the amount of data collected by Application Insights to manage costs.</span></span> <span data-ttu-id="41176-199">See [Sampling in Application Insights](../application-insights/app-insights-sampling.md) for some mechanisms to achieve this.</span><span class="sxs-lookup"><span data-stu-id="41176-199">See [Sampling in Application Insights](../application-insights/app-insights-sampling.md) for some mechanisms to achieve this.</span></span>


## <a name="next-steps"></a><span data-ttu-id="41176-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="41176-200">Next steps</span></span>
* <span data-ttu-id="41176-201">Learn more about [Application Insights](../application-insights/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41176-201">Learn more about [Application Insights](../application-insights/app-insights-overview.md).</span></span>

* <span data-ttu-id="41176-202">For Application Insights support in other languages, look at the [languages, platforms, and integrations documentation](../application-insights/app-insights-platforms.md).</span><span class="sxs-lookup"><span data-stu-id="41176-202">For Application Insights support in other languages, look at the [languages, platforms, and integrations documentation](../application-insights/app-insights-platforms.md).</span></span>


