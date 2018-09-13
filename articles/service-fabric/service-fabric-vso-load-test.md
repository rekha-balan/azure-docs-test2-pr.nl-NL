---
title: Load test your application by using Visual Studio Team Services | Microsoft Docs
description: Learn how to stress test your Azure Service Fabric applications by using Visual Studio Team Services.
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: ''
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 1180c2e4384fa342f1acfd0f45abb214f4e5f3c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551120"
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a><span data-ttu-id="d0e70-103">Load test your application by using Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="d0e70-103">Load test your application by using Visual Studio Team Services</span></span>
<span data-ttu-id="d0e70-104">This article shows how to use Microsoft Visual Studio load test features to stress test an application.</span><span class="sxs-lookup"><span data-stu-id="d0e70-104">This article shows how to use Microsoft Visual Studio load test features to stress test an application.</span></span> <span data-ttu-id="d0e70-105">It uses an Azure Service Fabric stateful service back end and a stateless service web front end.</span><span class="sxs-lookup"><span data-stu-id="d0e70-105">It uses an Azure Service Fabric stateful service back end and a stateless service web front end.</span></span> <span data-ttu-id="d0e70-106">The example application used here is an airplane location simulator.</span><span class="sxs-lookup"><span data-stu-id="d0e70-106">The example application used here is an airplane location simulator.</span></span> <span data-ttu-id="d0e70-107">You provide an airplane ID, departure time, and destination.</span><span class="sxs-lookup"><span data-stu-id="d0e70-107">You provide an airplane ID, departure time, and destination.</span></span> <span data-ttu-id="d0e70-108">The application’s back end processes the requests, and the front end displays on a map the airplane that matches the criteria.</span><span class="sxs-lookup"><span data-stu-id="d0e70-108">The application’s back end processes the requests, and the front end displays on a map the airplane that matches the criteria.</span></span>

<span data-ttu-id="d0e70-109">The following diagram illustrates the Service Fabric application that you'll be testing.</span><span class="sxs-lookup"><span data-stu-id="d0e70-109">The following diagram illustrates the Service Fabric application that you'll be testing.</span></span>

![Diagram of the example airplane location application][0]

## <a name="prerequisites"></a><span data-ttu-id="d0e70-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0e70-111">Prerequisites</span></span>
<span data-ttu-id="d0e70-112">Before getting started, you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="d0e70-112">Before getting started, you need to do the following:</span></span>

* <span data-ttu-id="d0e70-113">Get a Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="d0e70-113">Get a Visual Studio Team Services account.</span></span> <span data-ttu-id="d0e70-114">You can get one for free at [Visual Studio Team Services](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d0e70-114">You can get one for free at [Visual Studio Team Services](https://www.visualstudio.com).</span></span>
* <span data-ttu-id="d0e70-115">Get and install Visual Studio 2013 or Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d0e70-115">Get and install Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="d0e70-116">This article uses Visual Studio 2015 Enterprise edition, but Visual Studio 2013 and other editions should work similarly.</span><span class="sxs-lookup"><span data-stu-id="d0e70-116">This article uses Visual Studio 2015 Enterprise edition, but Visual Studio 2013 and other editions should work similarly.</span></span>
* <span data-ttu-id="d0e70-117">Deploy your application to a staging environment.</span><span class="sxs-lookup"><span data-stu-id="d0e70-117">Deploy your application to a staging environment.</span></span> <span data-ttu-id="d0e70-118">See [How to deploy applications to a remote cluster using Visual Studio](service-fabric-publish-app-remote-cluster.md) for information about this.</span><span class="sxs-lookup"><span data-stu-id="d0e70-118">See [How to deploy applications to a remote cluster using Visual Studio](service-fabric-publish-app-remote-cluster.md) for information about this.</span></span>
* <span data-ttu-id="d0e70-119">Understand your application’s usage pattern.</span><span class="sxs-lookup"><span data-stu-id="d0e70-119">Understand your application’s usage pattern.</span></span> <span data-ttu-id="d0e70-120">This information is used to simulate the load pattern.</span><span class="sxs-lookup"><span data-stu-id="d0e70-120">This information is used to simulate the load pattern.</span></span>
* <span data-ttu-id="d0e70-121">Understand the goal for your load testing.</span><span class="sxs-lookup"><span data-stu-id="d0e70-121">Understand the goal for your load testing.</span></span> <span data-ttu-id="d0e70-122">This helps you interpret and analyze the load test results.</span><span class="sxs-lookup"><span data-stu-id="d0e70-122">This helps you interpret and analyze the load test results.</span></span>

## <a name="create-and-run-the-web-performance-and-load-test-project"></a><span data-ttu-id="d0e70-123">Create and run the Web Performance and Load Test project</span><span class="sxs-lookup"><span data-stu-id="d0e70-123">Create and run the Web Performance and Load Test project</span></span>
### <a name="create-a-web-performance-and-load-test-project"></a><span data-ttu-id="d0e70-124">Create a Web Performance and Load Test project</span><span class="sxs-lookup"><span data-stu-id="d0e70-124">Create a Web Performance and Load Test project</span></span>
1. <span data-ttu-id="d0e70-125">Open Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d0e70-125">Open Visual Studio 2015.</span></span> <span data-ttu-id="d0e70-126">Choose **File** > **New** > **Project** on the menu bar to open the **New Project** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d0e70-126">Choose **File** > **New** > **Project** on the menu bar to open the **New Project** dialog box.</span></span>
2. <span data-ttu-id="d0e70-127">Expand the **Visual C#** node and choose **Test** > **Web Performance and Load Test project**.</span><span class="sxs-lookup"><span data-stu-id="d0e70-127">Expand the **Visual C#** node and choose **Test** > **Web Performance and Load Test project**.</span></span> <span data-ttu-id="d0e70-128">Give the project a name and then choose the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="d0e70-128">Give the project a name and then choose the **OK** button.</span></span>

    ![Screen shot of the New Project dialog box][1]

    <span data-ttu-id="d0e70-130">You should see a new Web Performance and Load Test project in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="d0e70-130">You should see a new Web Performance and Load Test project in Solution Explorer.</span></span>

    ![Screen shot of Solution Explorer showing the new project][2]

### <a name="record-a-web-performance-test"></a><span data-ttu-id="d0e70-132">Record a web performance test</span><span class="sxs-lookup"><span data-stu-id="d0e70-132">Record a web performance test</span></span>
1. <span data-ttu-id="d0e70-133">Open the .webtest project.</span><span class="sxs-lookup"><span data-stu-id="d0e70-133">Open the .webtest project.</span></span>
2. <span data-ttu-id="d0e70-134">Choose the **Add Recording** icon to start a recording session in your browser.</span><span class="sxs-lookup"><span data-stu-id="d0e70-134">Choose the **Add Recording** icon to start a recording session in your browser.</span></span>

    ![Screen shot of the Add Recording icon in a browser][3]

    ![Screen shot of the Record button in a browser][4]
3. <span data-ttu-id="d0e70-137">Browse to the Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="d0e70-137">Browse to the Service Fabric application.</span></span> <span data-ttu-id="d0e70-138">The recording panel should show the web requests.</span><span class="sxs-lookup"><span data-stu-id="d0e70-138">The recording panel should show the web requests.</span></span>

    ![Screen shot of web requests in the recording panel][5]
4. <span data-ttu-id="d0e70-140">Perform a sequence of actions that you expect the users to perform.</span><span class="sxs-lookup"><span data-stu-id="d0e70-140">Perform a sequence of actions that you expect the users to perform.</span></span> <span data-ttu-id="d0e70-141">These actions are used as a pattern to generate the load.</span><span class="sxs-lookup"><span data-stu-id="d0e70-141">These actions are used as a pattern to generate the load.</span></span>
5. <span data-ttu-id="d0e70-142">When you're done, choose the **Stop** button to stop recording.</span><span class="sxs-lookup"><span data-stu-id="d0e70-142">When you're done, choose the **Stop** button to stop recording.</span></span>

    ![Screen shot of the Stop button][6]

    <span data-ttu-id="d0e70-144">The .webtest project in Visual Studio should have captured a series of requests.</span><span class="sxs-lookup"><span data-stu-id="d0e70-144">The .webtest project in Visual Studio should have captured a series of requests.</span></span> <span data-ttu-id="d0e70-145">Dynamic parameters are replaced automatically.</span><span class="sxs-lookup"><span data-stu-id="d0e70-145">Dynamic parameters are replaced automatically.</span></span> <span data-ttu-id="d0e70-146">At this point, you can delete any extra, repeated dependency requests that are not part of your test scenario.</span><span class="sxs-lookup"><span data-stu-id="d0e70-146">At this point, you can delete any extra, repeated dependency requests that are not part of your test scenario.</span></span>
6. <span data-ttu-id="d0e70-147">Save the project and then choose the **Run Test** command to run the web performance test locally and make sure everything works correctly.</span><span class="sxs-lookup"><span data-stu-id="d0e70-147">Save the project and then choose the **Run Test** command to run the web performance test locally and make sure everything works correctly.</span></span>

    ![Screen shot of the Run Test command][7]

### <a name="parameterize-the-web-performance-test"></a><span data-ttu-id="d0e70-149">Parameterize the web performance test</span><span class="sxs-lookup"><span data-stu-id="d0e70-149">Parameterize the web performance test</span></span>
<span data-ttu-id="d0e70-150">You can parameterize the web performance test by converting it to a coded web performance test and then editing the code.</span><span class="sxs-lookup"><span data-stu-id="d0e70-150">You can parameterize the web performance test by converting it to a coded web performance test and then editing the code.</span></span> <span data-ttu-id="d0e70-151">As an alternative, you can bind the web performance test to a data list so that the test iterates through the data.</span><span class="sxs-lookup"><span data-stu-id="d0e70-151">As an alternative, you can bind the web performance test to a data list so that the test iterates through the data.</span></span> <span data-ttu-id="d0e70-152">See [Generate and run a coded web performance test](https://msdn.microsoft.com/library/ms182552.aspx) for details about how to convert the web performance test to a coded test.</span><span class="sxs-lookup"><span data-stu-id="d0e70-152">See [Generate and run a coded web performance test](https://msdn.microsoft.com/library/ms182552.aspx) for details about how to convert the web performance test to a coded test.</span></span> <span data-ttu-id="d0e70-153">See [Add a data source to a web performance test](https://msdn.microsoft.com/library/ms243142.aspx) for information about how to bind data to a web performance test.</span><span class="sxs-lookup"><span data-stu-id="d0e70-153">See [Add a data source to a web performance test](https://msdn.microsoft.com/library/ms243142.aspx) for information about how to bind data to a web performance test.</span></span>

<span data-ttu-id="d0e70-154">For this example, we'll convert the web performance test to a coded test so you can replace the airplane ID with a generated GUID and add more requests to send flights to different locations.</span><span class="sxs-lookup"><span data-stu-id="d0e70-154">For this example, we'll convert the web performance test to a coded test so you can replace the airplane ID with a generated GUID and add more requests to send flights to different locations.</span></span>

### <a name="create-a-load-test-project"></a><span data-ttu-id="d0e70-155">Create a load test project</span><span class="sxs-lookup"><span data-stu-id="d0e70-155">Create a load test project</span></span>
<span data-ttu-id="d0e70-156">A load test project is composed of one or more scenarios described by the web performance test and unit test, along with additional specified load test settings.</span><span class="sxs-lookup"><span data-stu-id="d0e70-156">A load test project is composed of one or more scenarios described by the web performance test and unit test, along with additional specified load test settings.</span></span> <span data-ttu-id="d0e70-157">The following steps show how to create a load test project:</span><span class="sxs-lookup"><span data-stu-id="d0e70-157">The following steps show how to create a load test project:</span></span>

1. <span data-ttu-id="d0e70-158">On the shortcut menu of your Web Performance and Load Test project, choose **Add** > **Load Test**.</span><span class="sxs-lookup"><span data-stu-id="d0e70-158">On the shortcut menu of your Web Performance and Load Test project, choose **Add** > **Load Test**.</span></span> <span data-ttu-id="d0e70-159">In the **Load Test** wizard, choose the **Next** button to configure the test settings.</span><span class="sxs-lookup"><span data-stu-id="d0e70-159">In the **Load Test** wizard, choose the **Next** button to configure the test settings.</span></span>
2. <span data-ttu-id="d0e70-160">In the **Load Pattern** section, choose whether you want a constant user load or a step load, which starts with a few users and increases the users over time.</span><span class="sxs-lookup"><span data-stu-id="d0e70-160">In the **Load Pattern** section, choose whether you want a constant user load or a step load, which starts with a few users and increases the users over time.</span></span>

    <span data-ttu-id="d0e70-161">If you have a good estimate of the amount of user load and want to see how the current system performs, choose **Constant Load**.</span><span class="sxs-lookup"><span data-stu-id="d0e70-161">If you have a good estimate of the amount of user load and want to see how the current system performs, choose **Constant Load**.</span></span> <span data-ttu-id="d0e70-162">If your goal is to learn whether the system performs consistently under various loads, choose **Step Load**.</span><span class="sxs-lookup"><span data-stu-id="d0e70-162">If your goal is to learn whether the system performs consistently under various loads, choose **Step Load**.</span></span>
3. <span data-ttu-id="d0e70-163">In the **Test Mix** section, choose the **Add** button and then select the test that you want to include in the load test.</span><span class="sxs-lookup"><span data-stu-id="d0e70-163">In the **Test Mix** section, choose the **Add** button and then select the test that you want to include in the load test.</span></span> <span data-ttu-id="d0e70-164">You can use the **Distribution** column to specify the percentage of total tests run for each test.</span><span class="sxs-lookup"><span data-stu-id="d0e70-164">You can use the **Distribution** column to specify the percentage of total tests run for each test.</span></span>
4. <span data-ttu-id="d0e70-165">In the **Run Settings** section, specify the load test duration.</span><span class="sxs-lookup"><span data-stu-id="d0e70-165">In the **Run Settings** section, specify the load test duration.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d0e70-166">The **Test Iterations** option is available only when you run a load test locally using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0e70-166">The **Test Iterations** option is available only when you run a load test locally using Visual Studio.</span></span>
   >
   >
5. <span data-ttu-id="d0e70-167">In the **Location** section of **Run Settings**, specify the location where load test requests are generated.</span><span class="sxs-lookup"><span data-stu-id="d0e70-167">In the **Location** section of **Run Settings**, specify the location where load test requests are generated.</span></span> <span data-ttu-id="d0e70-168">The wizard may prompt you to log in to your Team Services account.</span><span class="sxs-lookup"><span data-stu-id="d0e70-168">The wizard may prompt you to log in to your Team Services account.</span></span> <span data-ttu-id="d0e70-169">Log in and then choose a geographic location.</span><span class="sxs-lookup"><span data-stu-id="d0e70-169">Log in and then choose a geographic location.</span></span> <span data-ttu-id="d0e70-170">When you're done, choose the **Finish** button.</span><span class="sxs-lookup"><span data-stu-id="d0e70-170">When you're done, choose the **Finish** button.</span></span>
6. <span data-ttu-id="d0e70-171">After the load test is created, open the .loadtest project and choose the current run setting, such as **Run Settings** > **Run Settings1 [Active]**.</span><span class="sxs-lookup"><span data-stu-id="d0e70-171">After the load test is created, open the .loadtest project and choose the current run setting, such as **Run Settings** > **Run Settings1 [Active]**.</span></span> <span data-ttu-id="d0e70-172">This opens the run settings in the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="d0e70-172">This opens the run settings in the **Properties** window.</span></span>
7. <span data-ttu-id="d0e70-173">In the **Results** section of the **Run Settings** properties window, the **Timing Details Storage** setting should have **None** as its default value.</span><span class="sxs-lookup"><span data-stu-id="d0e70-173">In the **Results** section of the **Run Settings** properties window, the **Timing Details Storage** setting should have **None** as its default value.</span></span> <span data-ttu-id="d0e70-174">Change this value to **All Individual Details** to get more information on the load test results.</span><span class="sxs-lookup"><span data-stu-id="d0e70-174">Change this value to **All Individual Details** to get more information on the load test results.</span></span> <span data-ttu-id="d0e70-175">See [Load Testing](https://www.visualstudio.com/load-testing.aspx) for more information on how to connect to Visual Studio Team Services and run a load test.</span><span class="sxs-lookup"><span data-stu-id="d0e70-175">See [Load Testing](https://www.visualstudio.com/load-testing.aspx) for more information on how to connect to Visual Studio Team Services and run a load test.</span></span>

### <a name="run-the-load-test-by-using-visual-studio-team-services"></a><span data-ttu-id="d0e70-176">Run the load test by using Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="d0e70-176">Run the load test by using Visual Studio Team Services</span></span>
<span data-ttu-id="d0e70-177">Choose the **Run Load Test** command to start the test run.</span><span class="sxs-lookup"><span data-stu-id="d0e70-177">Choose the **Run Load Test** command to start the test run.</span></span>

![Screen shot of the Run Load Test command][8]

## <a name="view-and-analyze-the-load-test-results"></a><span data-ttu-id="d0e70-179">View and analyze the load test results</span><span class="sxs-lookup"><span data-stu-id="d0e70-179">View and analyze the load test results</span></span>
<span data-ttu-id="d0e70-180">As the load test progresses, the performance information is graphed.</span><span class="sxs-lookup"><span data-stu-id="d0e70-180">As the load test progresses, the performance information is graphed.</span></span> <span data-ttu-id="d0e70-181">You should see something similar to the following graph.</span><span class="sxs-lookup"><span data-stu-id="d0e70-181">You should see something similar to the following graph.</span></span>

![Screen shot of performance graph for load test results][9]

1. <span data-ttu-id="d0e70-183">Choose the **Download report** link near the top of the page.</span><span class="sxs-lookup"><span data-stu-id="d0e70-183">Choose the **Download report** link near the top of the page.</span></span> <span data-ttu-id="d0e70-184">After the report is downloaded, choose the **View report** button.</span><span class="sxs-lookup"><span data-stu-id="d0e70-184">After the report is downloaded, choose the **View report** button.</span></span>

    <span data-ttu-id="d0e70-185">On the **Graph** tab you can see graphs for various performance counters.</span><span class="sxs-lookup"><span data-stu-id="d0e70-185">On the **Graph** tab you can see graphs for various performance counters.</span></span> <span data-ttu-id="d0e70-186">On the **Summary** tab, the overall test results appear.</span><span class="sxs-lookup"><span data-stu-id="d0e70-186">On the **Summary** tab, the overall test results appear.</span></span> <span data-ttu-id="d0e70-187">The **Tables** tab shows the total number of passed and failed load tests.</span><span class="sxs-lookup"><span data-stu-id="d0e70-187">The **Tables** tab shows the total number of passed and failed load tests.</span></span>
2. <span data-ttu-id="d0e70-188">Choose the number links on the **Test** > **Failed** and the **Errors** > **Count** columns to see error details.</span><span class="sxs-lookup"><span data-stu-id="d0e70-188">Choose the number links on the **Test** > **Failed** and the **Errors** > **Count** columns to see error details.</span></span>

    <span data-ttu-id="d0e70-189">The **Detail** tab shows virtual user and test scenario information for failed requests.</span><span class="sxs-lookup"><span data-stu-id="d0e70-189">The **Detail** tab shows virtual user and test scenario information for failed requests.</span></span> <span data-ttu-id="d0e70-190">This data can be useful if the load test includes multiple scenarios.</span><span class="sxs-lookup"><span data-stu-id="d0e70-190">This data can be useful if the load test includes multiple scenarios.</span></span>

<span data-ttu-id="d0e70-191">See [Analyzing Load Test Results in the Graphs View of the Load Test Analyzer](https://www.visualstudio.com/load-testing.aspx) for more information on viewing load test results.</span><span class="sxs-lookup"><span data-stu-id="d0e70-191">See [Analyzing Load Test Results in the Graphs View of the Load Test Analyzer](https://www.visualstudio.com/load-testing.aspx) for more information on viewing load test results.</span></span>

## <a name="automate-your-load-test"></a><span data-ttu-id="d0e70-192">Automate your load test</span><span class="sxs-lookup"><span data-stu-id="d0e70-192">Automate your load test</span></span>
<span data-ttu-id="d0e70-193">Visual Studio Team Services Load Test provides APIs to help you manage load tests and analyze results in a Team Services account.</span><span class="sxs-lookup"><span data-stu-id="d0e70-193">Visual Studio Team Services Load Test provides APIs to help you manage load tests and analyze results in a Team Services account.</span></span> <span data-ttu-id="d0e70-194">See [Cloud Load Testing Rest APIs](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="d0e70-194">See [Cloud Load Testing Rest APIs](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e70-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0e70-195">Next steps</span></span>
* [<span data-ttu-id="d0e70-196">Monitoring and diagnosing services in a local machine development setup</span><span class="sxs-lookup"><span data-stu-id="d0e70-196">Monitoring and diagnosing services in a local machine development setup</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/Project.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/AddRecording.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/AddRecording2.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/ActionSequence.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/StopRecording.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/RunTest.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/RunTest2.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-vso-load-test/Graph.png










