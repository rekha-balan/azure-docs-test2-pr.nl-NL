---
title: Use Azure Queue storage to monitor Media Services job notifications with .NET | Microsoft Docs
description: Learn how to use Azure Queue storage to monitor Media Services job notifications. The code sample is written in C# and uses the Media Services SDK for .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: juliako
ms.openlocfilehash: 0ddac6ef30439e6bea04d63c41662bc49309de2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555380"
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="6cc63-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span><span class="sxs-lookup"><span data-stu-id="6cc63-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="6cc63-105">When you run jobs, you often require a way to track job progress.</span><span class="sxs-lookup"><span data-stu-id="6cc63-105">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="6cc63-106">You can check the progress by using Azure Queue storage to monitor Azure Media Services job notifications (as described in this article).</span><span class="sxs-lookup"><span data-stu-id="6cc63-106">You can check the progress by using Azure Queue storage to monitor Azure Media Services job notifications (as described in this article).</span></span> <span data-ttu-id="6cc63-107">You can also define a **StateChanged** event handler, as described in [Monitor job progress using .NET](media-services-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="6cc63-107">You can also define a **StateChanged** event handler, as described in [Monitor job progress using .NET](media-services-check-job-progress.md).</span></span>  

## <a name="use-queue-storage-to-monitor-media-services-job-notifications"></a><span data-ttu-id="6cc63-108">Use Queue storage to monitor Media Services job notifications</span><span class="sxs-lookup"><span data-stu-id="6cc63-108">Use Queue storage to monitor Media Services job notifications</span></span>
<span data-ttu-id="6cc63-109">When processing media jobs, Media Services can deliver notifications to [Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="6cc63-109">When processing media jobs, Media Services can deliver notifications to [Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="6cc63-110">This topic shows how to get these notification messages from Queue storage.</span><span class="sxs-lookup"><span data-stu-id="6cc63-110">This topic shows how to get these notification messages from Queue storage.</span></span>

<span data-ttu-id="6cc63-111">Messages delivered to Queue storage can be accessed from anywhere in the world.</span><span class="sxs-lookup"><span data-stu-id="6cc63-111">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="6cc63-112">The Queue storage messaging architecture is reliable and highly scalable.</span><span class="sxs-lookup"><span data-stu-id="6cc63-112">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="6cc63-113">Polling Queue storage for messages is recommended over using other methods.</span><span class="sxs-lookup"><span data-stu-id="6cc63-113">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="6cc63-114">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span><span class="sxs-lookup"><span data-stu-id="6cc63-114">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

### <a name="considerations"></a><span data-ttu-id="6cc63-115">Considerations</span><span class="sxs-lookup"><span data-stu-id="6cc63-115">Considerations</span></span>
<span data-ttu-id="6cc63-116">Consider the following when developing Media Services applications that use Queue storage:</span><span class="sxs-lookup"><span data-stu-id="6cc63-116">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="6cc63-117">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span><span class="sxs-lookup"><span data-stu-id="6cc63-117">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="6cc63-118">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cc63-118">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="6cc63-119">Queue storage is not a push service.</span><span class="sxs-lookup"><span data-stu-id="6cc63-119">Queue storage is not a push service.</span></span> <span data-ttu-id="6cc63-120">You have to poll the queue.</span><span class="sxs-lookup"><span data-stu-id="6cc63-120">You have to poll the queue.</span></span>
* <span data-ttu-id="6cc63-121">You can have any number of queues.</span><span class="sxs-lookup"><span data-stu-id="6cc63-121">You can have any number of queues.</span></span> <span data-ttu-id="6cc63-122">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="6cc63-122">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="6cc63-123">Queue storage has some limitations and specifics to be aware of.</span><span class="sxs-lookup"><span data-stu-id="6cc63-123">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="6cc63-124">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="6cc63-124">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

### <a name="code-example"></a><span data-ttu-id="6cc63-125">Code example</span><span class="sxs-lookup"><span data-stu-id="6cc63-125">Code example</span></span>
<span data-ttu-id="6cc63-126">The code example in this section does the following:</span><span class="sxs-lookup"><span data-stu-id="6cc63-126">The code example in this section does the following:</span></span>

1. <span data-ttu-id="6cc63-127">Defines the **EncodingJobMessage** class that maps to the notification message format.</span><span class="sxs-lookup"><span data-stu-id="6cc63-127">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="6cc63-128">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span><span class="sxs-lookup"><span data-stu-id="6cc63-128">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="6cc63-129">Loads the Media Services and Storage account information from the app.config file.</span><span class="sxs-lookup"><span data-stu-id="6cc63-129">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="6cc63-130">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span><span class="sxs-lookup"><span data-stu-id="6cc63-130">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="6cc63-131">Creates the queue that receives notification messages about the encoding job.</span><span class="sxs-lookup"><span data-stu-id="6cc63-131">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="6cc63-132">Creates the notification end point that is mapped to the queue.</span><span class="sxs-lookup"><span data-stu-id="6cc63-132">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="6cc63-133">Attaches the notification end point to the job and submits the encoding job.</span><span class="sxs-lookup"><span data-stu-id="6cc63-133">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="6cc63-134">You can have multiple notification end points attached to a job.</span><span class="sxs-lookup"><span data-stu-id="6cc63-134">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="6cc63-135">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span><span class="sxs-lookup"><span data-stu-id="6cc63-135">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="6cc63-136">(In this example, we are only interested in final states of the job processing.)</span><span class="sxs-lookup"><span data-stu-id="6cc63-136">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="6cc63-137">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span><span class="sxs-lookup"><span data-stu-id="6cc63-137">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="6cc63-138">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span><span class="sxs-lookup"><span data-stu-id="6cc63-138">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="6cc63-139">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span><span class="sxs-lookup"><span data-stu-id="6cc63-139">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="6cc63-140">Duplicate messages are possible.</span><span class="sxs-lookup"><span data-stu-id="6cc63-140">Duplicate messages are possible.</span></span> <span data-ttu-id="6cc63-141">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span><span class="sxs-lookup"><span data-stu-id="6cc63-141">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="6cc63-142">It is also possible that some state change notifications get skipped.</span><span class="sxs-lookup"><span data-stu-id="6cc63-142">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="6cc63-143">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="6cc63-143">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="6cc63-144">Deletes messages after they have been processed.</span><span class="sxs-lookup"><span data-stu-id="6cc63-144">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="6cc63-145">Deletes the queue and the notification end point.</span><span class="sxs-lookup"><span data-stu-id="6cc63-145">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="6cc63-146">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="6cc63-146">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="6cc63-147">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span><span class="sxs-lookup"><span data-stu-id="6cc63-147">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="6cc63-148">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span><span class="sxs-lookup"><span data-stu-id="6cc63-148">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="6cc63-149">The **IJob.State**  property reflects the accurate state with a slight delay.</span><span class="sxs-lookup"><span data-stu-id="6cc63-149">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

    using System;
    using System.Linq;
    using System.Configuration;
    using System.IO;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Collections.Generic;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Web;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    using System.Runtime.Serialization.Json;

    namespace JobNotification
    {
        public class EncodingJobMessage
        {
            // MessageVersion is used for version control.
            public String MessageVersion { get; set; }

            // Type of the event. Valid values are
            // JobStateChange and NotificationEndpointRegistration.
            public String EventType { get; set; }

            // ETag is used to help the customer detect if
            // the message is a duplicate of another message previously sent.
            public String ETag { get; set; }

            // Time of occurrence of the event.
            public String TimeStamp { get; set; }

            // Collection of values specific to the event.

            // For the JobStateChange event the values are:
            //     JobId - Id of the Job that triggered the notification.
            //     NewState- The new state of the Job. Valid values are:
            //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
            //     OldState- The old state of the Job. Valid values are:
            //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

            // For the NotificationEndpointRegistration event the values are:
            //     NotificationEndpointId- Id of the NotificationEndpoint
            //          that triggered the notification.
            //     State- The state of the Endpoint.
            //          Valid values are: Registered and Unregistered.

            public IDictionary<string, object> Properties { get; set; }
        }

        class Program
        {
            private static CloudMediaContext _context = null;
            private static CloudQueue _queue = null;
            private static INotificationEndPoint _notificationEndPoint = null;

            private static readonly string _singleInputMp4Path =
                Path.GetFullPath(@"C:\supportFiles\multifile\BigBuckBunny.mp4");

            static void Main(string[] args)
            {
                // Get the values from app.config file.
                string mediaServicesAccountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
                string mediaServicesAccountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];
                string storageConnectionString = ConfigurationManager.AppSettings["StorageConnectionString"];


                string endPointAddress = Guid.NewGuid().ToString();

                // Create the context.
                _context = new CloudMediaContext(mediaServicesAccountName, mediaServicesAccountKey);

                // Create the queue that will be receiving the notification messages.
                _queue = CreateQueue(storageConnectionString, endPointAddress);

                // Create the notification point that is mapped to the queue.
                _notificationEndPoint =
                        _context.NotificationEndPoints.Create(
                        Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


                if (_notificationEndPoint != null)
                {
                    IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                    WaitForJobToReachedFinishedState(job.Id);
                }

                // Clean up.
                _queue.Delete();      
                _notificationEndPoint.Delete();
           }


            static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
            {
                CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

                // Create the queue client
                CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

                // Retrieve a reference to a queue
                CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

                // Create the queue if it doesn't already exist
                queue.CreateIfNotExists();

                return queue;
            }


            public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
            {
                // Declare a new job.
                IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

                //Create an encrypted asset and upload the mp4.
                IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                    inputMediaFilePath);

                // Get a media processor reference, and pass to it the name of the
                // processor to use for the specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                // Create a task with the conversion details, using a configuration file.
                ITask task = job.Tasks.AddNew("My encoding Task",
                    processor,
                    "Adaptive Streaming",
                    Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

                // Specify the input asset to be encoded.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("Output asset",
                    AssetCreationOptions.None);

                // Add a notification point to the job. You can add multiple notification points.  
                job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                    _notificationEndPoint);

                job.Submit();

                return job;
            }

            public static void WaitForJobToReachedFinishedState(string jobId)
            {
                int expectedState = (int)JobState.Finished;
                int timeOutInSeconds = 600;

                bool jobReachedExpectedState = false;
                DateTime startTime = DateTime.Now;
                int jobState = -1;

                while (!jobReachedExpectedState)
                {
                    // Specify how often you want to get messages from the queue.
                    Thread.Sleep(TimeSpan.FromSeconds(10));

                    foreach (var message in _queue.GetMessages(10))
                    {
                        using (Stream stream = new MemoryStream(message.AsBytes))
                        {
                            DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                            settings.UseSimpleDictionaryFormat = true;
                            DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                            EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                            Console.WriteLine();

                            // Display the message information.
                            Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                            Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                            Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                            Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                            foreach (var property in encodingJobMsg.Properties)
                            {
                                Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                            }

                            // We are only interested in messages
                            // where EventType is "JobStateChange".
                            if (encodingJobMsg.EventType == "JobStateChange")
                            {
                                string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                                if (JobId == jobId)
                                {
                                    string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                                Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                    string newJobStateStr = (String)encodingJobMsg.Properties.
                                                                Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                    JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                    JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                    if (newJobState == (JobState)expectedState)
                                    {
                                        Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                            jobId, newJobState);
                                        jobReachedExpectedState = true;
                                        break;
                                    }
                                }
                            }
                        }
                        // Delete the message after we've read it.
                        _queue.DeleteMessage(message);
                    }

                    // Wait until timeout
                    TimeSpan timeDiff = DateTime.Now - startTime;
                    bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                    if (timedOut)
                    {
                        Console.WriteLine(@"Timeout for checking job notification messages,
                                            latest found state ='{0}', wait time = {1} secs",
                            jobState,
                            timeDiff.TotalSeconds);

                        throw new TimeoutException();
                    }
                }
            }

            static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
            {
                var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                    assetCreationOptions);

                var fileName = Path.GetFileName(singleFilePath);

                var assetFile = asset.AssetFiles.Create(fileName);

                Console.WriteLine("Created assetFile {0}", assetFile.Name);
                Console.WriteLine("Upload {0}", assetFile.Name);

                assetFile.Upload(singleFilePath);
                Console.WriteLine("Done uploading of {0}", assetFile.Name);

                return asset;
            }

            static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                return processor;
            }
        }
    }

<span data-ttu-id="6cc63-150">The preceding example produced the following output.</span><span class="sxs-lookup"><span data-stu-id="6cc63-150">The preceding example produced the following output.</span></span> <span data-ttu-id="6cc63-151">Your values will vary.</span><span class="sxs-lookup"><span data-stu-id="6cc63-151">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="6cc63-152">Next step</span><span class="sxs-lookup"><span data-stu-id="6cc63-152">Next step</span></span>
<span data-ttu-id="6cc63-153">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="6cc63-153">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6cc63-154">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="6cc63-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
