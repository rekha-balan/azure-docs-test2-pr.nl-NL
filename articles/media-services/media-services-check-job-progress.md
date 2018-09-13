---
title: Monitor Job Progress using .NET
description: Learn how to use event handler code to track job progress and send status updates. The code sample is written in C# and uses the Media Services SDK for .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: ee720ed6-8ce5-4434-b6d6-4df71fca224e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: juliako
ms.openlocfilehash: 1420c9dbaba1767526fa86a27aacb4fa3b2e2fe0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549555"
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="730ae-104">Monitor Job Progress using .NET</span><span class="sxs-lookup"><span data-stu-id="730ae-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-check-job-progress.md)
> * [.NET](media-services-check-job-progress.md)
> * [REST](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="730ae-108">When you run jobs, you often require a way to track job progress.</span><span class="sxs-lookup"><span data-stu-id="730ae-108">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="730ae-109">You can check the progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage to monitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span><span class="sxs-lookup"><span data-stu-id="730ae-109">You can check the progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage to monitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-to-monitor-job-progress"></a><span data-ttu-id="730ae-110">Define StateChanged event handler to monitor job progress</span><span class="sxs-lookup"><span data-stu-id="730ae-110">Define StateChanged event handler to monitor job progress</span></span>
<span data-ttu-id="730ae-111">The following code example defines the StateChanged event handler.</span><span class="sxs-lookup"><span data-stu-id="730ae-111">The following code example defines the StateChanged event handler.</span></span> <span data-ttu-id="730ae-112">This event handler tracks job progress and provides updated status, depending on the state.</span><span class="sxs-lookup"><span data-stu-id="730ae-112">This event handler tracks job progress and provides updated status, depending on the state.</span></span> <span data-ttu-id="730ae-113">The code also defines the LogJobStop method.</span><span class="sxs-lookup"><span data-stu-id="730ae-113">The code also defines the LogJobStop method.</span></span> <span data-ttu-id="730ae-114">This helper method logs error details.</span><span class="sxs-lookup"><span data-stu-id="730ae-114">This helper method logs error details.</span></span>

    private static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);

        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("********************");
                Console.WriteLine("Job is finished.");
                Console.WriteLine("Please wait while local tasks or downloads complete...");
                Console.WriteLine("********************");
                Console.WriteLine();
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                LogJobStop(job.Id);
                break;
            default:
                break;
        }
    }

    private static void LogJobStop(string jobId)
    {
        StringBuilder builder = new StringBuilder();
        IJob job = GetJob(jobId);

        builder.AppendLine("\nThe job stopped due to cancellation or an error.");
        builder.AppendLine("***************************");
        builder.AppendLine("Job ID: " + job.Id);
        builder.AppendLine("Job Name: " + job.Name);
        builder.AppendLine("Job State: " + job.State.ToString());
        builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
        builder.AppendLine("Media Services account name: " + _accountName);
        builder.AppendLine("Media Services account location: " + _accountLocation);
        // Log job errors if they exist.  
        if (job.State == JobState.Error)
        {
            builder.Append("Error Details: \n");
            foreach (ITask task in job.Tasks)
            {
                foreach (ErrorDetail detail in task.ErrorDetails)
                {
                    builder.AppendLine("  Task Id: " + task.Id);
                    builder.AppendLine("    Error Code: " + detail.Code);
                    builder.AppendLine("    Error Message: " + detail.Message + "\n");
                }
            }
        }
        builder.AppendLine("***************************\n");
        // Write the output to a local file and to the console. The template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="730ae-115">Next step</span><span class="sxs-lookup"><span data-stu-id="730ae-115">Next step</span></span>
<span data-ttu-id="730ae-116">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="730ae-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="730ae-117">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="730ae-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

