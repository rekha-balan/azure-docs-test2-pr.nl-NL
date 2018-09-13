---
title: Profiling a Cloud Service Locally in the Compute Emulator | Microsoft Docs
services: cloud-services
description: Investigate performance issues in cloud services with the Visual Studio profiler
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
tags: ''
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: 31956a6d354a742c5f39ce264c37903812df7744
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553532"
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="652a0-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span><span class="sxs-lookup"><span data-stu-id="652a0-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="652a0-104">A variety of tools and techniques are available for testing the performance of cloud services.</span><span class="sxs-lookup"><span data-stu-id="652a0-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="652a0-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span><span class="sxs-lookup"><span data-stu-id="652a0-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="652a0-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span><span class="sxs-lookup"><span data-stu-id="652a0-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="652a0-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span><span class="sxs-lookup"><span data-stu-id="652a0-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="652a0-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span><span class="sxs-lookup"><span data-stu-id="652a0-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="652a0-109">CPU sampling is a method of profiling that is not very intrusive.</span><span class="sxs-lookup"><span data-stu-id="652a0-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="652a0-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span><span class="sxs-lookup"><span data-stu-id="652a0-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="652a0-111">The data is collected over a period of time, and shown in a report.</span><span class="sxs-lookup"><span data-stu-id="652a0-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="652a0-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span><span class="sxs-lookup"><span data-stu-id="652a0-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="652a0-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span><span class="sxs-lookup"><span data-stu-id="652a0-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="652a0-114">1: Configure Visual Studio for profiling</span><span class="sxs-lookup"><span data-stu-id="652a0-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="652a0-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span><span class="sxs-lookup"><span data-stu-id="652a0-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="652a0-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span><span class="sxs-lookup"><span data-stu-id="652a0-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="652a0-117">You'll want to make sure that you reference the available symbol servers.</span><span class="sxs-lookup"><span data-stu-id="652a0-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="652a0-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span><span class="sxs-lookup"><span data-stu-id="652a0-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="652a0-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span><span class="sxs-lookup"><span data-stu-id="652a0-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="652a0-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span><span class="sxs-lookup"><span data-stu-id="652a0-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Symbol options][4]

<span data-ttu-id="652a0-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span><span class="sxs-lookup"><span data-stu-id="652a0-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="652a0-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span><span class="sxs-lookup"><span data-stu-id="652a0-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="652a0-124">On the **Tools** menu, choose **Options**.</span><span class="sxs-lookup"><span data-stu-id="652a0-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="652a0-125">Then expand the **Performance Tools** node, and choose **General**.</span><span class="sxs-lookup"><span data-stu-id="652a0-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="652a0-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span><span class="sxs-lookup"><span data-stu-id="652a0-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Just My Code options][17]

<span data-ttu-id="652a0-128">You can use these instructions with an existing project or with a new project.</span><span class="sxs-lookup"><span data-stu-id="652a0-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="652a0-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span><span class="sxs-lookup"><span data-stu-id="652a0-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure Cloud Service project roles][5]

<span data-ttu-id="652a0-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span><span class="sxs-lookup"><span data-stu-id="652a0-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="652a0-132">For example, add the following code to a worker role project:</span><span class="sxs-lookup"><span data-stu-id="652a0-132">For example, add the following code to a worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="652a0-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span><span class="sxs-lookup"><span data-stu-id="652a0-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="652a0-134">(Ignore the warning about the method running synchronously.)</span><span class="sxs-lookup"><span data-stu-id="652a0-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="652a0-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span><span class="sxs-lookup"><span data-stu-id="652a0-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="652a0-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span><span class="sxs-lookup"><span data-stu-id="652a0-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="652a0-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span><span class="sxs-lookup"><span data-stu-id="652a0-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="652a0-138">2: Attach to a process</span><span class="sxs-lookup"><span data-stu-id="652a0-138">2: Attach to a process</span></span>
<span data-ttu-id="652a0-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span><span class="sxs-lookup"><span data-stu-id="652a0-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="652a0-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="652a0-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Attach profile option][6]

<span data-ttu-id="652a0-142">For a worker role, find the WaWorkerHost.exe process.</span><span class="sxs-lookup"><span data-stu-id="652a0-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![WaWorkerHost process][7]

<span data-ttu-id="652a0-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span><span class="sxs-lookup"><span data-stu-id="652a0-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="652a0-145">You can also attach to a web role by attaching to WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="652a0-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="652a0-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span><span class="sxs-lookup"><span data-stu-id="652a0-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="652a0-147">You can query the processID programmatically by accessing the Process object.</span><span class="sxs-lookup"><span data-stu-id="652a0-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="652a0-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span><span class="sxs-lookup"><span data-stu-id="652a0-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="652a0-149">To view the log, start the Compute Emulator UI.</span><span class="sxs-lookup"><span data-stu-id="652a0-149">To view the log, start the Compute Emulator UI.</span></span>

![Start the Compute Emulator UI][8]

<span data-ttu-id="652a0-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span><span class="sxs-lookup"><span data-stu-id="652a0-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="652a0-152">You can see the process ID in the log.</span><span class="sxs-lookup"><span data-stu-id="652a0-152">You can see the process ID in the log.</span></span>

![View process ID][9]

<span data-ttu-id="652a0-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span><span class="sxs-lookup"><span data-stu-id="652a0-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="652a0-155">When you want to stop profiling, choose the **Stop Profiling** link.</span><span class="sxs-lookup"><span data-stu-id="652a0-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Stop Profiling option][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="652a0-157">3: View performance reports</span><span class="sxs-lookup"><span data-stu-id="652a0-157">3: View performance reports</span></span>
<span data-ttu-id="652a0-158">The performance report for your application is displayed.</span><span class="sxs-lookup"><span data-stu-id="652a0-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="652a0-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span><span class="sxs-lookup"><span data-stu-id="652a0-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Profiler report][11]

<span data-ttu-id="652a0-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span><span class="sxs-lookup"><span data-stu-id="652a0-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="652a0-162">If you see String.Concat, try pressing the Show All Code button.</span><span class="sxs-lookup"><span data-stu-id="652a0-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="652a0-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span><span class="sxs-lookup"><span data-stu-id="652a0-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Analysis of report][12]

<span data-ttu-id="652a0-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span><span class="sxs-lookup"><span data-stu-id="652a0-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="652a0-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span><span class="sxs-lookup"><span data-stu-id="652a0-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Performance warnings][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="652a0-168">4: Make changes and compare performance</span><span class="sxs-lookup"><span data-stu-id="652a0-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="652a0-169">You can also compare the performance before and after a code change.</span><span class="sxs-lookup"><span data-stu-id="652a0-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="652a0-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="652a0-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="652a0-171">Do another performance run, and then compare the performance.</span><span class="sxs-lookup"><span data-stu-id="652a0-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="652a0-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span><span class="sxs-lookup"><span data-stu-id="652a0-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="652a0-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span><span class="sxs-lookup"><span data-stu-id="652a0-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="652a0-174">Specify both files in the dialog box that appears.</span><span class="sxs-lookup"><span data-stu-id="652a0-174">Specify both files in the dialog box that appears.</span></span>

![Compare performance reports option][15]

<span data-ttu-id="652a0-176">The reports highlight differences between the two runs.</span><span class="sxs-lookup"><span data-stu-id="652a0-176">The reports highlight differences between the two runs.</span></span>

![Comparison report][16]

<span data-ttu-id="652a0-178">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="652a0-178">Congratulations!</span></span> <span data-ttu-id="652a0-179">You've gotten started with the profiler.</span><span class="sxs-lookup"><span data-stu-id="652a0-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="652a0-180">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="652a0-180">Troubleshooting</span></span>
* <span data-ttu-id="652a0-181">Make sure you are profiling a Release build and start without debugging.</span><span class="sxs-lookup"><span data-stu-id="652a0-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="652a0-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span><span class="sxs-lookup"><span data-stu-id="652a0-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="652a0-183">Use the Compute Emulator UI to view the status of your application.</span><span class="sxs-lookup"><span data-stu-id="652a0-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="652a0-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span><span class="sxs-lookup"><span data-stu-id="652a0-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="652a0-185">If that doesn't solve the problem, try rebooting.</span><span class="sxs-lookup"><span data-stu-id="652a0-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="652a0-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span><span class="sxs-lookup"><span data-stu-id="652a0-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="652a0-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span><span class="sxs-lookup"><span data-stu-id="652a0-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="652a0-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span><span class="sxs-lookup"><span data-stu-id="652a0-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="652a0-189">Applications that are not doing any computational work might not produce any sampling data.</span><span class="sxs-lookup"><span data-stu-id="652a0-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="652a0-190">It's also possible that the process exited before any sampling was done.</span><span class="sxs-lookup"><span data-stu-id="652a0-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="652a0-191">Check to see that the Run method for a role that you are profiling does not terminate.</span><span class="sxs-lookup"><span data-stu-id="652a0-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="652a0-192">Next Steps</span><span class="sxs-lookup"><span data-stu-id="652a0-192">Next Steps</span></span>
<span data-ttu-id="652a0-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span><span class="sxs-lookup"><span data-stu-id="652a0-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="652a0-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span><span class="sxs-lookup"><span data-stu-id="652a0-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="652a0-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span><span class="sxs-lookup"><span data-stu-id="652a0-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="652a0-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="652a0-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png













