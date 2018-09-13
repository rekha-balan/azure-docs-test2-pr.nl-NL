---
title: Real-time video analysis with the Emotion API | Microsoft Docs
description: Use the Emotion API in Cognitive Services to perform near-real-time analysis on frames taken from a live video stream.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 01/25/2017
ms.author: anroth
ms.openlocfilehash: 1fcf7a6c226fa285447eeabec863d662b924a546
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552480"
---
# <a name="how-to-analyze-videos-in-real-time"></a><span data-ttu-id="03914-103">How to Analyze Videos in Real-time</span><span class="sxs-lookup"><span data-stu-id="03914-103">How to Analyze Videos in Real-time</span></span>
<span data-ttu-id="03914-104">This guide will demonstrate how to perform near-real-time analysis on frames taken from a live video stream.</span><span class="sxs-lookup"><span data-stu-id="03914-104">This guide will demonstrate how to perform near-real-time analysis on frames taken from a live video stream.</span></span> <span data-ttu-id="03914-105">The basic components in such a system are:</span><span class="sxs-lookup"><span data-stu-id="03914-105">The basic components in such a system are:</span></span>
- <span data-ttu-id="03914-106">Acquire frames from a video source</span><span class="sxs-lookup"><span data-stu-id="03914-106">Acquire frames from a video source</span></span>
- <span data-ttu-id="03914-107">Select which frames to analyze</span><span class="sxs-lookup"><span data-stu-id="03914-107">Select which frames to analyze</span></span>
- <span data-ttu-id="03914-108">Submit these frames to the API</span><span class="sxs-lookup"><span data-stu-id="03914-108">Submit these frames to the API</span></span>
- <span data-ttu-id="03914-109">Consume each analysis result that is returned from the API call</span><span class="sxs-lookup"><span data-stu-id="03914-109">Consume each analysis result that is returned from the API call</span></span>

<span data-ttu-id="03914-110">These samples are written in C# and the code can be found on GitHub here: [https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/).</span><span class="sxs-lookup"><span data-stu-id="03914-110">These samples are written in C# and the code can be found on GitHub here: [https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/).</span></span>

## <a name="the-approach"></a><span data-ttu-id="03914-111">The Approach</span><span class="sxs-lookup"><span data-stu-id="03914-111">The Approach</span></span>
<span data-ttu-id="03914-112">There are multiple ways to solve the problem of running near-real-time analysis on video streams.</span><span class="sxs-lookup"><span data-stu-id="03914-112">There are multiple ways to solve the problem of running near-real-time analysis on video streams.</span></span> <span data-ttu-id="03914-113">We will start by outlining three approaches in increasing levels of sophistication.</span><span class="sxs-lookup"><span data-stu-id="03914-113">We will start by outlining three approaches in increasing levels of sophistication.</span></span>

### <a name="a-simple-approach"></a><span data-ttu-id="03914-114">A Simple Approach</span><span class="sxs-lookup"><span data-stu-id="03914-114">A Simple Approach</span></span>
<span data-ttu-id="03914-115">The simplest design for a near-real-time analysis system is an infinite loop, where in each iteration we grab a frame, analyze it, and then consume the result:</span><span class="sxs-lookup"><span data-stu-id="03914-115">The simplest design for a near-real-time analysis system is an infinite loop, where in each iteration we grab a frame, analyze it, and then consume the result:</span></span>
```CSharp
while (true)
{
    Frame f = GrabFrame();
    if (ShouldAnalyze(f))
    {
        AnalysisResult r = await Analyze(f);
        ConsumeResult(r);
    }
}
```
<span data-ttu-id="03914-116">If our analysis consisted of a lightweight client-side algorithm, this approach would be suitable.</span><span class="sxs-lookup"><span data-stu-id="03914-116">If our analysis consisted of a lightweight client-side algorithm, this approach would be suitable.</span></span> <span data-ttu-id="03914-117">However, when our analysis is happening in the cloud, the latency involved means that an API call might take several seconds, during which time we are not capturing images, and our thread is essentially doing nothing.</span><span class="sxs-lookup"><span data-stu-id="03914-117">However, when our analysis is happening in the cloud, the latency involved means that an API call might take several seconds, during which time we are not capturing images, and our thread is essentially doing nothing.</span></span> <span data-ttu-id="03914-118">Our maximum frame-rate is limited by the latency of the API calls.</span><span class="sxs-lookup"><span data-stu-id="03914-118">Our maximum frame-rate is limited by the latency of the API calls.</span></span>

### <a name="parallelizing-api-calls"></a><span data-ttu-id="03914-119">Parallelizing API Calls</span><span class="sxs-lookup"><span data-stu-id="03914-119">Parallelizing API Calls</span></span>
<span data-ttu-id="03914-120">While a simple single-threaded loop makes sense for a lightweight client-side algorithm, it doesn't fit well with the latency involved in cloud API calls.</span><span class="sxs-lookup"><span data-stu-id="03914-120">While a simple single-threaded loop makes sense for a lightweight client-side algorithm, it doesn't fit well with the latency involved in cloud API calls.</span></span> <span data-ttu-id="03914-121">The solution to this problem is to allow the long-running API calls to execute in parallel with the frame-grabbing.</span><span class="sxs-lookup"><span data-stu-id="03914-121">The solution to this problem is to allow the long-running API calls to execute in parallel with the frame-grabbing.</span></span> <span data-ttu-id="03914-122">In C#, we could achieve this using Task-based parallelism, for example:</span><span class="sxs-lookup"><span data-stu-id="03914-122">In C#, we could achieve this using Task-based parallelism, for example:</span></span>
```CSharp
while (true)
{
    Frame f = GrabFrame();
    if (ShouldAnalyze(f))
    {
        var t = Task.Run(async () => 
        {
            AnalysisResult r = await Analyze(f);
            ConsumeResult(r);
        }
    }
}
```
<span data-ttu-id="03914-123">This launches each analysis in a separate Task, which can run in the background while we continue grabbing new frames.</span><span class="sxs-lookup"><span data-stu-id="03914-123">This launches each analysis in a separate Task, which can run in the background while we continue grabbing new frames.</span></span> <span data-ttu-id="03914-124">This avoids blocking the main thread while waiting for an API call to return, however we have lost some of the guarantees that the simple version provided -- multiple API calls might occur in parallel, and the results might get returned in the wrong order.</span><span class="sxs-lookup"><span data-stu-id="03914-124">This avoids blocking the main thread while waiting for an API call to return, however we have lost some of the guarantees that the simple version provided -- multiple API calls might occur in parallel, and the results might get returned in the wrong order.</span></span> <span data-ttu-id="03914-125">This could also cause multiple threads to enter the ConsumeResult() function simultaneously, which could be dangerous, if the function is not thread-safe.</span><span class="sxs-lookup"><span data-stu-id="03914-125">This could also cause multiple threads to enter the ConsumeResult() function simultaneously, which could be dangerous, if the function is not thread-safe.</span></span> <span data-ttu-id="03914-126">Finally, this simple code does not keep track of the Tasks that get created, so exceptions will silently disappear.</span><span class="sxs-lookup"><span data-stu-id="03914-126">Finally, this simple code does not keep track of the Tasks that get created, so exceptions will silently disappear.</span></span> <span data-ttu-id="03914-127">Thus, the final ingredient for us to add is a "consumer" thread that will track the analysis tasks, raise exceptions, kill long-running tasks, and ensure the results get consumed in the correct order, one at a time.</span><span class="sxs-lookup"><span data-stu-id="03914-127">Thus, the final ingredient for us to add is a "consumer" thread that will track the analysis tasks, raise exceptions, kill long-running tasks, and ensure the results get consumed in the correct order, one at a time.</span></span>

### <a name="a-producer-consumer-design"></a><span data-ttu-id="03914-128">A Producer-Consumer Design</span><span class="sxs-lookup"><span data-stu-id="03914-128">A Producer-Consumer Design</span></span>
<span data-ttu-id="03914-129">In our final "producer-consumer" system, we have a producer thread that looks very similar to our previous infinite loop.</span><span class="sxs-lookup"><span data-stu-id="03914-129">In our final "producer-consumer" system, we have a producer thread that looks very similar to our previous infinite loop.</span></span> <span data-ttu-id="03914-130">However, instead of consuming analysis results as soon as they are available, the producer simply puts the tasks into a queue to keep track of them.</span><span class="sxs-lookup"><span data-stu-id="03914-130">However, instead of consuming analysis results as soon as they are available, the producer simply puts the tasks into a queue to keep track of them.</span></span>
```CSharp
// Queue that will contain the API call tasks. 
var taskQueue = new BlockingCollection<Task<ResultWrapper>>();
     
// Producer thread. 
while (true)
{
    // Grab a frame. 
    Frame f = GrabFrame();
 
    // Decide whether to analyze the frame. 
    if (ShouldAnalyze(f))
    {
        // Start a task that will run in parallel with this thread. 
        var analysisTask = Task.Run(async () => 
        {
            // Put the frame, and the result/exception into a wrapper object.
            var output = new ResultWrapper(f);
            try
            {
                output.Analysis = await Analyze(f);
            }
            catch (Exception e)
            {
                output.Exception = e;
            }
            return output;
        }
        
        // Push the task onto the queue. 
        taskQueue.Add(analysisTask);
    }
}
```
<span data-ttu-id="03914-131">We also have a consumer thread, that is taking tasks off the queue, waiting for them to finish, and either displaying the result or raising the exception that was thrown.</span><span class="sxs-lookup"><span data-stu-id="03914-131">We also have a consumer thread, that is taking tasks off the queue, waiting for them to finish, and either displaying the result or raising the exception that was thrown.</span></span> <span data-ttu-id="03914-132">By using the queue, we can guarantee that results get consumed one at a time, in the correct order, without limiting the maximum frame-rate of the system.</span><span class="sxs-lookup"><span data-stu-id="03914-132">By using the queue, we can guarantee that results get consumed one at a time, in the correct order, without limiting the maximum frame-rate of the system.</span></span>
```CSharp
// Consumer thread. 
while (true)
{
    // Get the oldest task. 
    Task<ResultWrapper> analysisTask = taskQueue.Take();
 
    // Await until the task is completed. 
    var output = await analysisTask;
     
    // Consume the exception or result. 
    if (output.Exception != null)
    {
        throw output.Exception;
    }
    else
    {
        ConsumeResult(output.Analysis);
    }
}
```

## <a name="implementing-the-solution"></a><span data-ttu-id="03914-133">Implementing the Solution</span><span class="sxs-lookup"><span data-stu-id="03914-133">Implementing the Solution</span></span>
### <a name="getting-started"></a><span data-ttu-id="03914-134">Getting Started</span><span class="sxs-lookup"><span data-stu-id="03914-134">Getting Started</span></span>
<span data-ttu-id="03914-135">To get your app up and running as quickly as possible, we have implemented the system described above, intending it to be flexible enough to implement many scenarios, while being easy to use.</span><span class="sxs-lookup"><span data-stu-id="03914-135">To get your app up and running as quickly as possible, we have implemented the system described above, intending it to be flexible enough to implement many scenarios, while being easy to use.</span></span> <span data-ttu-id="03914-136">To access the code, go to [https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis).</span><span class="sxs-lookup"><span data-stu-id="03914-136">To access the code, go to [https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis).</span></span>

<span data-ttu-id="03914-137">The library contains the class FrameGrabber, which implements the producer-consumer system discussed above to process video frames from a webcam.</span><span class="sxs-lookup"><span data-stu-id="03914-137">The library contains the class FrameGrabber, which implements the producer-consumer system discussed above to process video frames from a webcam.</span></span> <span data-ttu-id="03914-138">The user can specify the exact form of the API call, and the class uses events to let the calling code know when a new frame is acquired, or a new analysis result is available.</span><span class="sxs-lookup"><span data-stu-id="03914-138">The user can specify the exact form of the API call, and the class uses events to let the calling code know when a new frame is acquired, or a new analysis result is available.</span></span>

<span data-ttu-id="03914-139">To illustrate some of the possibilities, there are two sample apps that uses the library.</span><span class="sxs-lookup"><span data-stu-id="03914-139">To illustrate some of the possibilities, there are two sample apps that uses the library.</span></span> <span data-ttu-id="03914-140">The first is a simple console app, and a simplified version of this is reproduced below.</span><span class="sxs-lookup"><span data-stu-id="03914-140">The first is a simple console app, and a simplified version of this is reproduced below.</span></span> <span data-ttu-id="03914-141">It grabs frames from the default webcam, and submits them to the Face API for face detection.</span><span class="sxs-lookup"><span data-stu-id="03914-141">It grabs frames from the default webcam, and submits them to the Face API for face detection.</span></span>
```CSharp
using System;
using VideoFrameAnalyzer;
using Microsoft.ProjectOxford.Face;
using Microsoft.ProjectOxford.Face.Contract;
     
namespace VideoFrameConsoleApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create grabber, with analysis type Face[]. 
            FrameGrabber<Face[]> grabber = new FrameGrabber<Face[]>();
            
            // Create Face API Client. Insert your Face API key here.
            FaceServiceClient faceClient = new FaceServiceClient("<subscription key>");

            // Set up our Face API call.
            grabber.AnalysisFunction = async frame => return await faceClient.DetectAsync(frame.Image.ToMemoryStream(".jpg"));

            // Set up a listener for when we receive a new result from an API call. 
            grabber.NewResultAvailable += (s, e) =>
            {
                if (e.Analysis != null)
                    Console.WriteLine("New result received for frame acquired at {0}. {1} faces detected", e.Frame.Metadata.Timestamp, e.Analysis.Length);
            };
            
            // Tell grabber to call the Face API every 3 seconds.
            grabber.TriggerAnalysisOnInterval(TimeSpan.FromMilliseconds(3000));

            // Start running.
            grabber.StartProcessingCameraAsync().Wait();

            // Wait for keypress to stop
            Console.WriteLine("Press any key to stop...");
            Console.ReadKey();
            
            // Stop, blocking until done.
            grabber.StopProcessingAsync().Wait();
        }
    }
}
```
<span data-ttu-id="03914-142">The second sample app is a bit more interesting, and allows you to choose which API to call on the video frames.</span><span class="sxs-lookup"><span data-stu-id="03914-142">The second sample app is a bit more interesting, and allows you to choose which API to call on the video frames.</span></span> <span data-ttu-id="03914-143">On the left hand side, the app shows a preview of the live video, on the right hand side it shows the most recent API result overlaid on the corresponding frame.</span><span class="sxs-lookup"><span data-stu-id="03914-143">On the left hand side, the app shows a preview of the live video, on the right hand side it shows the most recent API result overlaid on the corresponding frame.</span></span>

<span data-ttu-id="03914-144">In most modes, there will be a visible delay between the live video on the left, and the visualized analysis on the right.</span><span class="sxs-lookup"><span data-stu-id="03914-144">In most modes, there will be a visible delay between the live video on the left, and the visualized analysis on the right.</span></span> <span data-ttu-id="03914-145">This delay is the time taken to make the API call.</span><span class="sxs-lookup"><span data-stu-id="03914-145">This delay is the time taken to make the API call.</span></span> <span data-ttu-id="03914-146">The exception to this is in the "EmotionsWithClientFaceDetect" mode, which performs face detection locally on the client computer using OpenCV, before submitting any images to Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="03914-146">The exception to this is in the "EmotionsWithClientFaceDetect" mode, which performs face detection locally on the client computer using OpenCV, before submitting any images to Cognitive Services.</span></span> <span data-ttu-id="03914-147">By doing this, we can visualize the detected face immediately, and then update the emotions later once the API call returns.</span><span class="sxs-lookup"><span data-stu-id="03914-147">By doing this, we can visualize the detected face immediately, and then update the emotions later once the API call returns.</span></span> <span data-ttu-id="03914-148">This demonstrates the possibility of a "hybrid" approach, where some simple processing can be performed on the client, and then Cognitive Services APIs can be used to augment this with more advanced analysis when necessary.</span><span class="sxs-lookup"><span data-stu-id="03914-148">This demonstrates the possibility of a "hybrid" approach, where some simple processing can be performed on the client, and then Cognitive Services APIs can be used to augment this with more advanced analysis when necessary.</span></span>

![HowToAnalyzeVideo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Video/Images/FramebyFrame.jpg)

### <a name="integrating-into-your-codebase"></a><span data-ttu-id="03914-150">Integrating into your codebase</span><span class="sxs-lookup"><span data-stu-id="03914-150">Integrating into your codebase</span></span>
<span data-ttu-id="03914-151">To get started with this sample, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="03914-151">To get started with this sample, follow these steps:</span></span>

1. <span data-ttu-id="03914-152">Get API keys for the Vision APIs from [microsoft.com/cognitive](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="03914-152">Get API keys for the Vision APIs from [microsoft.com/cognitive](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> <span data-ttu-id="03914-153">For video frame analysis, the applicable APIs are:</span><span class="sxs-lookup"><span data-stu-id="03914-153">For video frame analysis, the applicable APIs are:</span></span>
    - [<span data-ttu-id="03914-154">Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="03914-154">Computer Vision API</span></span>](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api)
    - [<span data-ttu-id="03914-155">Emotion API</span><span class="sxs-lookup"><span data-stu-id="03914-155">Emotion API</span></span>](https://www.microsoft.com/cognitive-services/en-us/emotion-api)
    - [<span data-ttu-id="03914-156">Face API</span><span class="sxs-lookup"><span data-stu-id="03914-156">Face API</span></span>](https://www.microsoft.com/cognitive-services/en-us/face-api)
2. <span data-ttu-id="03914-157">Clone the [Cognitive-Samples-VideoFrameAnalysis](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/) GitHub repo</span><span class="sxs-lookup"><span data-stu-id="03914-157">Clone the [Cognitive-Samples-VideoFrameAnalysis](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/) GitHub repo</span></span>

3. <span data-ttu-id="03914-158">Open the sample in Visual Studio 2015, build and run the sample applications:</span><span class="sxs-lookup"><span data-stu-id="03914-158">Open the sample in Visual Studio 2015, build and run the sample applications:</span></span>
    - <span data-ttu-id="03914-159">For BasicConsoleSample, the Face API key is hard-coded directly in [BasicConsoleSample/Program.cs](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/blob/master/Windows/BasicConsoleSample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="03914-159">For BasicConsoleSample, the Face API key is hard-coded directly in [BasicConsoleSample/Program.cs](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/blob/master/Windows/BasicConsoleSample/Program.cs).</span></span>
    - <span data-ttu-id="03914-160">For LiveCameraSample, the keys should be entered into the Settings pane of the app.</span><span class="sxs-lookup"><span data-stu-id="03914-160">For LiveCameraSample, the keys should be entered into the Settings pane of the app.</span></span> <span data-ttu-id="03914-161">They will be persisted across sessions as user data.</span><span class="sxs-lookup"><span data-stu-id="03914-161">They will be persisted across sessions as user data.</span></span>
        

<span data-ttu-id="03914-162">When you're ready to integrate, **simply reference the VideoFrameAnalyzer library from your own projects.**</span><span class="sxs-lookup"><span data-stu-id="03914-162">When you're ready to integrate, **simply reference the VideoFrameAnalyzer library from your own projects.**</span></span> 



## <a name="developer-code-of-conduct"></a><span data-ttu-id="03914-163">Developer Code of Conduct</span><span class="sxs-lookup"><span data-stu-id="03914-163">Developer Code of Conduct</span></span>
<span data-ttu-id="03914-164">As with all the Cognitive Services, Developers developing with our APIs and samples are required to follow the "[Developer Code of Conduct for Microsoft Cognitive Services](http://go.microsoft.com/fwlink/?LinkId=698895)."</span><span class="sxs-lookup"><span data-stu-id="03914-164">As with all the Cognitive Services, Developers developing with our APIs and samples are required to follow the "[Developer Code of Conduct for Microsoft Cognitive Services](http://go.microsoft.com/fwlink/?LinkId=698895)."</span></span> 


<span data-ttu-id="03914-165">The image, voice, video or text understanding capabilities of VideoFrameAnalyzer uses Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="03914-165">The image, voice, video or text understanding capabilities of VideoFrameAnalyzer uses Microsoft Cognitive Services.</span></span> <span data-ttu-id="03914-166">Microsoft will receive the images, audio, video, and other data that you upload (via this app) and may use them for service improvement purposes.</span><span class="sxs-lookup"><span data-stu-id="03914-166">Microsoft will receive the images, audio, video, and other data that you upload (via this app) and may use them for service improvement purposes.</span></span> <span data-ttu-id="03914-167">We ask for your help in protecting the people whose data your app sends to Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="03914-167">We ask for your help in protecting the people whose data your app sends to Microsoft Cognitive Services.</span></span> 
 

<span data-ttu-id="03914-168">To report abuse of the Microsoft Cognitive Services to Microsoft, please visit the [Microsoft Cognitive Services website](https://www.microsoft.com/cognitive-services), and use the "Report Abuse" link at the bottom of the page to contact Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03914-168">To report abuse of the Microsoft Cognitive Services to Microsoft, please visit the [Microsoft Cognitive Services website](https://www.microsoft.com/cognitive-services), and use the "Report Abuse" link at the bottom of the page to contact Microsoft.</span></span> <span data-ttu-id="03914-169">For more information about Microsoft privacy policies please see their privacy statement here: [https://go.microsoft.com/fwlink/?LinkId=521839](https://go.microsoft.com/fwlink/?LinkId=521839).</span><span class="sxs-lookup"><span data-stu-id="03914-169">For more information about Microsoft privacy policies please see their privacy statement here: [https://go.microsoft.com/fwlink/?LinkId=521839](https://go.microsoft.com/fwlink/?LinkId=521839).</span></span> 



## <a name="summary"></a><span data-ttu-id="03914-170">Summary</span><span class="sxs-lookup"><span data-stu-id="03914-170">Summary</span></span>
<span data-ttu-id="03914-171">In this guide, you learned how to run near-real-time analysis on live video streams using the Face, Computer Vision, and Emotion APIs, and how you can use our sample code to get started.</span><span class="sxs-lookup"><span data-stu-id="03914-171">In this guide, you learned how to run near-real-time analysis on live video streams using the Face, Computer Vision, and Emotion APIs, and how you can use our sample code to get started.</span></span>  <span data-ttu-id="03914-172">You can get started building your app with free API keys at the [Microsoft Cognitive Services sign-up page](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="03914-172">You can get started building your app with free API keys at the [Microsoft Cognitive Services sign-up page](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> 

<span data-ttu-id="03914-173">Please feel free to provide feedback and suggestions in the [GitHub repository](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/), or for more broad API feedback, on our [UserVoice site](https://cognitive.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="03914-173">Please feel free to provide feedback and suggestions in the [GitHub repository](https://github.com/Microsoft/Cognitive-Samples-VideoFrameAnalysis/), or for more broad API feedback, on our [UserVoice site](https://cognitive.uservoice.com/).</span></span>


