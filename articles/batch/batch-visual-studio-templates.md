---
title: Start building Batch solutions with Visual Studio project templates - Azure | Microsoft Docs
description: Learn how Visual Studio project templates can help you implement and run your compute-intensive workloads on Azure Batch.
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: ''
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a5f0201ad034f0a6e9aac27f255935737dbd160
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556590"
---
# <a name="use-visual-studio-project-templates-to-jump-start-batch-solutions"></a><span data-ttu-id="1955f-103">Use Visual Studio project templates to jump-start Batch solutions</span><span class="sxs-lookup"><span data-stu-id="1955f-103">Use Visual Studio project templates to jump-start Batch solutions</span></span>

<span data-ttu-id="1955f-104">The **Job Manager** and **Task Processor Visual Studio templates** for Batch provide code to help you to implement and run your compute-intensive workloads on Batch with the least amount of effort.</span><span class="sxs-lookup"><span data-stu-id="1955f-104">The **Job Manager** and **Task Processor Visual Studio templates** for Batch provide code to help you to implement and run your compute-intensive workloads on Batch with the least amount of effort.</span></span> <span data-ttu-id="1955f-105">This document describes these templates and provides guidance for how to use them.</span><span class="sxs-lookup"><span data-stu-id="1955f-105">This document describes these templates and provides guidance for how to use them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1955f-106">This article discusses only information applicable to these two templates, and assumes that you are familiar with the Batch service and key concepts related to it: pools, compute nodes, jobs and tasks, job manager tasks, environment variables, and other relevant information.</span><span class="sxs-lookup"><span data-stu-id="1955f-106">This article discusses only information applicable to these two templates, and assumes that you are familiar with the Batch service and key concepts related to it: pools, compute nodes, jobs and tasks, job manager tasks, environment variables, and other relevant information.</span></span> <span data-ttu-id="1955f-107">You can find more information in [Basics of Azure Batch](batch-technical-overview.md), [Batch feature overview for developers](batch-api-basics.md), and [Get started with the Azure Batch library for .NET](batch-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1955f-107">You can find more information in [Basics of Azure Batch](batch-technical-overview.md), [Batch feature overview for developers](batch-api-basics.md), and [Get started with the Azure Batch library for .NET](batch-dotnet-get-started.md).</span></span>
> 
> 

## <a name="high-level-overview"></a><span data-ttu-id="1955f-108">High-level overview</span><span class="sxs-lookup"><span data-stu-id="1955f-108">High-level overview</span></span>
<span data-ttu-id="1955f-109">The Job Manager and Task Processor templates can be used to create two useful components:</span><span class="sxs-lookup"><span data-stu-id="1955f-109">The Job Manager and Task Processor templates can be used to create two useful components:</span></span>

* <span data-ttu-id="1955f-110">A job manager task that implements a job splitter that can break a job down into multiple tasks that can run independently, in parallel.</span><span class="sxs-lookup"><span data-stu-id="1955f-110">A job manager task that implements a job splitter that can break a job down into multiple tasks that can run independently, in parallel.</span></span>
* <span data-ttu-id="1955f-111">A task processor that can be used to perform pre-processing and post-processing around an application command line.</span><span class="sxs-lookup"><span data-stu-id="1955f-111">A task processor that can be used to perform pre-processing and post-processing around an application command line.</span></span>

<span data-ttu-id="1955f-112">For example, in a movie rendering scenario, the job splitter would turn a single movie job into hundreds or thousands of separate tasks that would process individual frames separately.</span><span class="sxs-lookup"><span data-stu-id="1955f-112">For example, in a movie rendering scenario, the job splitter would turn a single movie job into hundreds or thousands of separate tasks that would process individual frames separately.</span></span> <span data-ttu-id="1955f-113">Correspondingly, the task processor would invoke the rendering application and all dependent processes that are needed to render each frame, as well as perform any additional actions (for example, copying the rendered frame to a storage location).</span><span class="sxs-lookup"><span data-stu-id="1955f-113">Correspondingly, the task processor would invoke the rendering application and all dependent processes that are needed to render each frame, as well as perform any additional actions (for example, copying the rendered frame to a storage location).</span></span>

> [!NOTE]
> <span data-ttu-id="1955f-114">The Job Manager and Task Processor templates are independent of each other, so you can choose to use both, or only one of them, depending on the requirements of your compute job and on your preferences.</span><span class="sxs-lookup"><span data-stu-id="1955f-114">The Job Manager and Task Processor templates are independent of each other, so you can choose to use both, or only one of them, depending on the requirements of your compute job and on your preferences.</span></span>
> 
> 

<span data-ttu-id="1955f-115">As shown in the diagram below, a compute job that uses these templates will go through three stages:</span><span class="sxs-lookup"><span data-stu-id="1955f-115">As shown in the diagram below, a compute job that uses these templates will go through three stages:</span></span>

1. <span data-ttu-id="1955f-116">The client code (e.g., application, web service, etc.) submits a job to the Batch service on Azure, specifying as its job manager task the job manager program.</span><span class="sxs-lookup"><span data-stu-id="1955f-116">The client code (e.g., application, web service, etc.) submits a job to the Batch service on Azure, specifying as its job manager task the job manager program.</span></span>
2. <span data-ttu-id="1955f-117">The Batch service runs the job manager task on a compute node and the job splitter launches the specified number of task processor tasks, on as many compute nodes as required, based on the parameters and specifications in the job splitter code.</span><span class="sxs-lookup"><span data-stu-id="1955f-117">The Batch service runs the job manager task on a compute node and the job splitter launches the specified number of task processor tasks, on as many compute nodes as required, based on the parameters and specifications in the job splitter code.</span></span>
3. <span data-ttu-id="1955f-118">The task processor tasks run independently, in parallel, to process the input data and generate the output data.</span><span class="sxs-lookup"><span data-stu-id="1955f-118">The task processor tasks run independently, in parallel, to process the input data and generate the output data.</span></span>

![Diagram showing how client code interacts with the Batch service][diagram01]

## <a name="prerequisites"></a><span data-ttu-id="1955f-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1955f-120">Prerequisites</span></span>
<span data-ttu-id="1955f-121">To use the Batch templates, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="1955f-121">To use the Batch templates, you will need the following:</span></span>

* <span data-ttu-id="1955f-122">A computer with Visual Studio 2015 installed.</span><span class="sxs-lookup"><span data-stu-id="1955f-122">A computer with Visual Studio 2015 installed.</span></span> <span data-ttu-id="1955f-123">Batch templates are currently only supported for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="1955f-123">Batch templates are currently only supported for Visual Studio 2015.</span></span>
* <span data-ttu-id="1955f-124">The Batch templates, which are available from the [Visual Studio Gallery][vs_gallery] as Visual Studio extensions.</span><span class="sxs-lookup"><span data-stu-id="1955f-124">The Batch templates, which are available from the [Visual Studio Gallery][vs_gallery] as Visual Studio extensions.</span></span> <span data-ttu-id="1955f-125">There are two ways to get the templates:</span><span class="sxs-lookup"><span data-stu-id="1955f-125">There are two ways to get the templates:</span></span>
  
  * <span data-ttu-id="1955f-126">Install the templates using the **Extensions and Updates** dialog box in Visual Studio (for more information, see [Finding and Using Visual Studio Extensions][vs_find_use_ext]).</span><span class="sxs-lookup"><span data-stu-id="1955f-126">Install the templates using the **Extensions and Updates** dialog box in Visual Studio (for more information, see [Finding and Using Visual Studio Extensions][vs_find_use_ext]).</span></span> <span data-ttu-id="1955f-127">In the **Extensions and Updates** dialog box, search and download the following two extensions:</span><span class="sxs-lookup"><span data-stu-id="1955f-127">In the **Extensions and Updates** dialog box, search and download the following two extensions:</span></span>
    
    * <span data-ttu-id="1955f-128">Azure Batch Job Manager with Job Splitter</span><span class="sxs-lookup"><span data-stu-id="1955f-128">Azure Batch Job Manager with Job Splitter</span></span>
    * <span data-ttu-id="1955f-129">Azure Batch Task Processor</span><span class="sxs-lookup"><span data-stu-id="1955f-129">Azure Batch Task Processor</span></span>
  * <span data-ttu-id="1955f-130">Download the templates from the online gallery for Visual Studio: [Microsoft Azure Batch Project Templates][vs_gallery_templates]</span><span class="sxs-lookup"><span data-stu-id="1955f-130">Download the templates from the online gallery for Visual Studio: [Microsoft Azure Batch Project Templates][vs_gallery_templates]</span></span>
* <span data-ttu-id="1955f-131">If you plan to use the [Application Packages](batch-application-packages.md) feature to deploy the job manager and task processor to the Batch compute nodes, you need to link a storage account to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="1955f-131">If you plan to use the [Application Packages](batch-application-packages.md) feature to deploy the job manager and task processor to the Batch compute nodes, you need to link a storage account to your Batch account.</span></span>

## <a name="preparation"></a><span data-ttu-id="1955f-132">Preparation</span><span class="sxs-lookup"><span data-stu-id="1955f-132">Preparation</span></span>
<span data-ttu-id="1955f-133">We recommend creating a solution that can contain your job manager as well as your task processor, because this can make it easier to share code between your job manager and task processor programs.</span><span class="sxs-lookup"><span data-stu-id="1955f-133">We recommend creating a solution that can contain your job manager as well as your task processor, because this can make it easier to share code between your job manager and task processor programs.</span></span> <span data-ttu-id="1955f-134">To create this solution, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1955f-134">To create this solution, follow these steps:</span></span>

1. <span data-ttu-id="1955f-135">Open Visual Studio and select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="1955f-135">Open Visual Studio and select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="1955f-136">Under **Templates**, expand **Other Project Types**, click **Visual Studio Solutions**, and then select **Blank Solution**.</span><span class="sxs-lookup"><span data-stu-id="1955f-136">Under **Templates**, expand **Other Project Types**, click **Visual Studio Solutions**, and then select **Blank Solution**.</span></span>
3. <span data-ttu-id="1955f-137">Type a name that describes your application and the purpose of this solution (e.g., "LitwareBatchTaskPrograms").</span><span class="sxs-lookup"><span data-stu-id="1955f-137">Type a name that describes your application and the purpose of this solution (e.g., "LitwareBatchTaskPrograms").</span></span>
4. <span data-ttu-id="1955f-138">To create the new solution, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1955f-138">To create the new solution, click **OK**.</span></span>

## <a name="job-manager-template"></a><span data-ttu-id="1955f-139">Job Manager template</span><span class="sxs-lookup"><span data-stu-id="1955f-139">Job Manager template</span></span>
<span data-ttu-id="1955f-140">The Job Manager template helps you to implement a job manager task that can perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="1955f-140">The Job Manager template helps you to implement a job manager task that can perform the following actions:</span></span>

* <span data-ttu-id="1955f-141">Split a job into multiple tasks.</span><span class="sxs-lookup"><span data-stu-id="1955f-141">Split a job into multiple tasks.</span></span>
* <span data-ttu-id="1955f-142">Submit those tasks to run on Batch.</span><span class="sxs-lookup"><span data-stu-id="1955f-142">Submit those tasks to run on Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="1955f-143">For more information about job manager tasks, see [Batch feature overview for developers](batch-api-basics.md#job-manager-task).</span><span class="sxs-lookup"><span data-stu-id="1955f-143">For more information about job manager tasks, see [Batch feature overview for developers](batch-api-basics.md#job-manager-task).</span></span>
> 
> 

### <a name="create-a-job-manager-using-the-template"></a><span data-ttu-id="1955f-144">Create a Job Manager using the template</span><span class="sxs-lookup"><span data-stu-id="1955f-144">Create a Job Manager using the template</span></span>
<span data-ttu-id="1955f-145">To add a job manager to the solution that you created earlier, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1955f-145">To add a job manager to the solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="1955f-146">Open your existing solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1955f-146">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="1955f-147">In Solution Explorer, right-click the solution, click **Add** > **New Project**.</span><span class="sxs-lookup"><span data-stu-id="1955f-147">In Solution Explorer, right-click the solution, click **Add** > **New Project**.</span></span>
3. <span data-ttu-id="1955f-148">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Job Manager with Job Splitter**.</span><span class="sxs-lookup"><span data-stu-id="1955f-148">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Job Manager with Job Splitter**.</span></span>
4. <span data-ttu-id="1955f-149">Type a name that describes your application and identifies this project as the job manager (e.g. "LitwareJobManager").</span><span class="sxs-lookup"><span data-stu-id="1955f-149">Type a name that describes your application and identifies this project as the job manager (e.g. "LitwareJobManager").</span></span>
5. <span data-ttu-id="1955f-150">To create the project, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1955f-150">To create the project, click **OK**.</span></span>
6. <span data-ttu-id="1955f-151">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span><span class="sxs-lookup"><span data-stu-id="1955f-151">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span></span>

### <a name="job-manager-template-files-and-their-purpose"></a><span data-ttu-id="1955f-152">Job Manager template files and their purpose</span><span class="sxs-lookup"><span data-stu-id="1955f-152">Job Manager template files and their purpose</span></span>
<span data-ttu-id="1955f-153">When you create a project using the Job Manager template, it generates three groups of code files:</span><span class="sxs-lookup"><span data-stu-id="1955f-153">When you create a project using the Job Manager template, it generates three groups of code files:</span></span>

* <span data-ttu-id="1955f-154">The main program file (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="1955f-154">The main program file (Program.cs).</span></span> <span data-ttu-id="1955f-155">This contains the program entry point and top-level exception handling.</span><span class="sxs-lookup"><span data-stu-id="1955f-155">This contains the program entry point and top-level exception handling.</span></span> <span data-ttu-id="1955f-156">You shouldn't normally need to modify this.</span><span class="sxs-lookup"><span data-stu-id="1955f-156">You shouldn't normally need to modify this.</span></span>
* <span data-ttu-id="1955f-157">The Framework directory.</span><span class="sxs-lookup"><span data-stu-id="1955f-157">The Framework directory.</span></span> <span data-ttu-id="1955f-158">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span><span class="sxs-lookup"><span data-stu-id="1955f-158">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span></span>
* <span data-ttu-id="1955f-159">The job splitter file (JobSplitter.cs).</span><span class="sxs-lookup"><span data-stu-id="1955f-159">The job splitter file (JobSplitter.cs).</span></span> <span data-ttu-id="1955f-160">This is where you will put your application-specific logic for splitting a job into tasks.</span><span class="sxs-lookup"><span data-stu-id="1955f-160">This is where you will put your application-specific logic for splitting a job into tasks.</span></span>

<span data-ttu-id="1955f-161">Of course you can add additional files as required to support your job splitter code, depending on the complexity of the job splitting logic.</span><span class="sxs-lookup"><span data-stu-id="1955f-161">Of course you can add additional files as required to support your job splitter code, depending on the complexity of the job splitting logic.</span></span>

<span data-ttu-id="1955f-162">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span><span class="sxs-lookup"><span data-stu-id="1955f-162">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="1955f-163">The rest of this section describes the different files and their code structure, and explains what each class does.</span><span class="sxs-lookup"><span data-stu-id="1955f-163">The rest of this section describes the different files and their code structure, and explains what each class does.</span></span>

![Visual Studio Solution Explorer showing the Job Manager template solution][solution_explorer01]

<span data-ttu-id="1955f-165">**Framework files**</span><span class="sxs-lookup"><span data-stu-id="1955f-165">**Framework files**</span></span>

* <span data-ttu-id="1955f-166">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span><span class="sxs-lookup"><span data-stu-id="1955f-166">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="1955f-167">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span><span class="sxs-lookup"><span data-stu-id="1955f-167">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="1955f-168">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span><span class="sxs-lookup"><span data-stu-id="1955f-168">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="1955f-169">`JobManager.cs`: Orchestrates the components of the job manager program.</span><span class="sxs-lookup"><span data-stu-id="1955f-169">`JobManager.cs`: Orchestrates the components of the job manager program.</span></span> <span data-ttu-id="1955f-170">It is responsible for the initializing the job splitter, invoking the job splitter, and dispatching the tasks returned by the job splitter to the task submitter.</span><span class="sxs-lookup"><span data-stu-id="1955f-170">It is responsible for the initializing the job splitter, invoking the job splitter, and dispatching the tasks returned by the job splitter to the task submitter.</span></span>
* <span data-ttu-id="1955f-171">`JobManagerException.cs`: Represents an error that requires the job manager to terminate.</span><span class="sxs-lookup"><span data-stu-id="1955f-171">`JobManagerException.cs`: Represents an error that requires the job manager to terminate.</span></span> <span data-ttu-id="1955f-172">JobManagerException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span><span class="sxs-lookup"><span data-stu-id="1955f-172">JobManagerException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>
* <span data-ttu-id="1955f-173">`TaskSubmitter.cs`: This class is responsible to adding tasks returned by the job splitter to the Batch job.</span><span class="sxs-lookup"><span data-stu-id="1955f-173">`TaskSubmitter.cs`: This class is responsible to adding tasks returned by the job splitter to the Batch job.</span></span> <span data-ttu-id="1955f-174">The JobManager class aggregates the sequence of tasks into batches for efficient but timely addition to the job, then calls TaskSubmitter.SubmitTasks on a background thread for each batch.</span><span class="sxs-lookup"><span data-stu-id="1955f-174">The JobManager class aggregates the sequence of tasks into batches for efficient but timely addition to the job, then calls TaskSubmitter.SubmitTasks on a background thread for each batch.</span></span>

<span data-ttu-id="1955f-175">**Job Splitter**</span><span class="sxs-lookup"><span data-stu-id="1955f-175">**Job Splitter**</span></span>

<span data-ttu-id="1955f-176">`JobSplitter.cs`: This class contains application-specific logic for splitting the job into tasks.</span><span class="sxs-lookup"><span data-stu-id="1955f-176">`JobSplitter.cs`: This class contains application-specific logic for splitting the job into tasks.</span></span> <span data-ttu-id="1955f-177">The framework invokes the JobSplitter.Split method to obtain a sequence of tasks, which it adds to the job as the method returns them.</span><span class="sxs-lookup"><span data-stu-id="1955f-177">The framework invokes the JobSplitter.Split method to obtain a sequence of tasks, which it adds to the job as the method returns them.</span></span> <span data-ttu-id="1955f-178">This is the class where you will inject the logic of your job.</span><span class="sxs-lookup"><span data-stu-id="1955f-178">This is the class where you will inject the logic of your job.</span></span> <span data-ttu-id="1955f-179">Implement the Split method to return a sequence of CloudTask instances representing the tasks into which you want to partition the job.</span><span class="sxs-lookup"><span data-stu-id="1955f-179">Implement the Split method to return a sequence of CloudTask instances representing the tasks into which you want to partition the job.</span></span>

<span data-ttu-id="1955f-180">**Standard .NET command line project files**</span><span class="sxs-lookup"><span data-stu-id="1955f-180">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="1955f-181">`App.config`: Standard .NET application configuration file.</span><span class="sxs-lookup"><span data-stu-id="1955f-181">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="1955f-182">`Packages.config`: Standard NuGet package dependency file.</span><span class="sxs-lookup"><span data-stu-id="1955f-182">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="1955f-183">`Program.cs`: Contains the program entry point and top-level exception handling.</span><span class="sxs-lookup"><span data-stu-id="1955f-183">`Program.cs`: Contains the program entry point and top-level exception handling.</span></span>

### <a name="implementing-the-job-splitter"></a><span data-ttu-id="1955f-184">Implementing the job splitter</span><span class="sxs-lookup"><span data-stu-id="1955f-184">Implementing the job splitter</span></span>
<span data-ttu-id="1955f-185">When you open the Job Manager template project, the project will have the JobSplitter.cs file open by default.</span><span class="sxs-lookup"><span data-stu-id="1955f-185">When you open the Job Manager template project, the project will have the JobSplitter.cs file open by default.</span></span> <span data-ttu-id="1955f-186">You can implement the split logic for the tasks in your workload by using the Split() method show below:</span><span class="sxs-lookup"><span data-stu-id="1955f-186">You can implement the split logic for the tasks in your workload by using the Split() method show below:</span></span>

```csharp
/// <summary>
/// Gets the tasks into which to split the job. This is where you inject
/// your application-specific logic for decomposing the job into tasks.
///
/// The job manager framework invokes the Split method for you; you need
/// only to implement it, not to call it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and the "yield return" statement; this allows tasks to be added
/// and to start running while splitting is still in progress.
/// </summary>
/// <returns>The tasks to be added to the job. Tasks are added automatically
/// by the job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for the split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> <span data-ttu-id="1955f-187">The annotated section in the `Split()` method is the only section of the Job Manager template code that is intended for you to modify by adding the logic to split your jobs into different tasks.</span><span class="sxs-lookup"><span data-stu-id="1955f-187">The annotated section in the `Split()` method is the only section of the Job Manager template code that is intended for you to modify by adding the logic to split your jobs into different tasks.</span></span> <span data-ttu-id="1955f-188">If you want to modify a different section of the template, please ensure you are familiarized with how Batch works, and try out a few of the [Batch code samples][github_samples].</span><span class="sxs-lookup"><span data-stu-id="1955f-188">If you want to modify a different section of the template, please ensure you are familiarized with how Batch works, and try out a few of the [Batch code samples][github_samples].</span></span>
> 
> 

<span data-ttu-id="1955f-189">Your Split() implementation has access to:</span><span class="sxs-lookup"><span data-stu-id="1955f-189">Your Split() implementation has access to:</span></span>

* <span data-ttu-id="1955f-190">The job parameters, via the `_parameters` field.</span><span class="sxs-lookup"><span data-stu-id="1955f-190">The job parameters, via the `_parameters` field.</span></span>
* <span data-ttu-id="1955f-191">The CloudJob object representing the job, via the `_job` field.</span><span class="sxs-lookup"><span data-stu-id="1955f-191">The CloudJob object representing the job, via the `_job` field.</span></span>
* <span data-ttu-id="1955f-192">The CloudTask object representing the job manager task, via the `_jobManagerTask` field.</span><span class="sxs-lookup"><span data-stu-id="1955f-192">The CloudTask object representing the job manager task, via the `_jobManagerTask` field.</span></span>

<span data-ttu-id="1955f-193">Your `Split()` implementation does not need to add tasks to the job directly.</span><span class="sxs-lookup"><span data-stu-id="1955f-193">Your `Split()` implementation does not need to add tasks to the job directly.</span></span> <span data-ttu-id="1955f-194">Instead, your code should return a sequence of CloudTask objects, and these will be added to the job automatically by the framework classes that invoke the job splitter.</span><span class="sxs-lookup"><span data-stu-id="1955f-194">Instead, your code should return a sequence of CloudTask objects, and these will be added to the job automatically by the framework classes that invoke the job splitter.</span></span> <span data-ttu-id="1955f-195">It's common to use C#'s iterator (`yield return`) feature to implement job splitters as this allows the tasks to start running as soon as possible rather than waiting for all tasks to be calculated.</span><span class="sxs-lookup"><span data-stu-id="1955f-195">It's common to use C#'s iterator (`yield return`) feature to implement job splitters as this allows the tasks to start running as soon as possible rather than waiting for all tasks to be calculated.</span></span>

<span data-ttu-id="1955f-196">**Job splitter failure**</span><span class="sxs-lookup"><span data-stu-id="1955f-196">**Job splitter failure**</span></span>

<span data-ttu-id="1955f-197">If your job splitter encounters an error, it should either:</span><span class="sxs-lookup"><span data-stu-id="1955f-197">If your job splitter encounters an error, it should either:</span></span>

* <span data-ttu-id="1955f-198">Terminate the sequence using the C# `yield break` statement, in which case the job manager will be treated as successful; or</span><span class="sxs-lookup"><span data-stu-id="1955f-198">Terminate the sequence using the C# `yield break` statement, in which case the job manager will be treated as successful; or</span></span>
* <span data-ttu-id="1955f-199">Throw an exception, in which case the job manager will be treated as failed and may be retried depending on how the client has configured it).</span><span class="sxs-lookup"><span data-stu-id="1955f-199">Throw an exception, in which case the job manager will be treated as failed and may be retried depending on how the client has configured it).</span></span>

<span data-ttu-id="1955f-200">In both cases, any tasks already returned by the job splitter and added to the Batch job will be eligible to run.</span><span class="sxs-lookup"><span data-stu-id="1955f-200">In both cases, any tasks already returned by the job splitter and added to the Batch job will be eligible to run.</span></span> <span data-ttu-id="1955f-201">If you don't want this to happen, then you could:</span><span class="sxs-lookup"><span data-stu-id="1955f-201">If you don't want this to happen, then you could:</span></span>

* <span data-ttu-id="1955f-202">Terminate the job before returning from the job splitter</span><span class="sxs-lookup"><span data-stu-id="1955f-202">Terminate the job before returning from the job splitter</span></span>
* <span data-ttu-id="1955f-203">Formulate the entire task collection before returning it (that is, return an `ICollection<CloudTask>` or `IList<CloudTask>` instead of implementing your job splitter using a C# iterator)</span><span class="sxs-lookup"><span data-stu-id="1955f-203">Formulate the entire task collection before returning it (that is, return an `ICollection<CloudTask>` or `IList<CloudTask>` instead of implementing your job splitter using a C# iterator)</span></span>
* <span data-ttu-id="1955f-204">Use task dependencies to make all tasks depend on the successful completion of the job manager</span><span class="sxs-lookup"><span data-stu-id="1955f-204">Use task dependencies to make all tasks depend on the successful completion of the job manager</span></span>

<span data-ttu-id="1955f-205">**Job manager retries**</span><span class="sxs-lookup"><span data-stu-id="1955f-205">**Job manager retries**</span></span>

<span data-ttu-id="1955f-206">If the job manager fails, it may be retried by the Batch service depending on the client retry settings.</span><span class="sxs-lookup"><span data-stu-id="1955f-206">If the job manager fails, it may be retried by the Batch service depending on the client retry settings.</span></span> <span data-ttu-id="1955f-207">In general, this is safe, because when the framework adds tasks to the job, it ignores any tasks that already exist.</span><span class="sxs-lookup"><span data-stu-id="1955f-207">In general, this is safe, because when the framework adds tasks to the job, it ignores any tasks that already exist.</span></span> <span data-ttu-id="1955f-208">However, if calculating tasks is expensive, you may not wish to incur the cost of recalculating tasks that have already been added to the job; conversely, if the re-run is not guaranteed to generate the same task IDs then the 'ignore duplicates' behavior will not kick in.</span><span class="sxs-lookup"><span data-stu-id="1955f-208">However, if calculating tasks is expensive, you may not wish to incur the cost of recalculating tasks that have already been added to the job; conversely, if the re-run is not guaranteed to generate the same task IDs then the 'ignore duplicates' behavior will not kick in.</span></span> <span data-ttu-id="1955f-209">In these cases you should design your job splitter to detect the work that has already been done and not repeat it, for example by performing a CloudJob.ListTasks before starting to yield tasks.</span><span class="sxs-lookup"><span data-stu-id="1955f-209">In these cases you should design your job splitter to detect the work that has already been done and not repeat it, for example by performing a CloudJob.ListTasks before starting to yield tasks.</span></span>

### <a name="exit-codes-and-exceptions-in-the-job-manager-template"></a><span data-ttu-id="1955f-210">Exit codes and exceptions in the Job Manager template</span><span class="sxs-lookup"><span data-stu-id="1955f-210">Exit codes and exceptions in the Job Manager template</span></span>
<span data-ttu-id="1955f-211">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help to identify any problems with the execution of the program.</span><span class="sxs-lookup"><span data-stu-id="1955f-211">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help to identify any problems with the execution of the program.</span></span> <span data-ttu-id="1955f-212">The Job Manager template implements the exit codes and exceptions described in this section.</span><span class="sxs-lookup"><span data-stu-id="1955f-212">The Job Manager template implements the exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="1955f-213">A job manager task that is implemented with the Job Manager template can return three possible exit codes:</span><span class="sxs-lookup"><span data-stu-id="1955f-213">A job manager task that is implemented with the Job Manager template can return three possible exit codes:</span></span>

| <span data-ttu-id="1955f-214">Code</span><span class="sxs-lookup"><span data-stu-id="1955f-214">Code</span></span> | <span data-ttu-id="1955f-215">Description</span><span class="sxs-lookup"><span data-stu-id="1955f-215">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1955f-216">0</span><span class="sxs-lookup"><span data-stu-id="1955f-216">0</span></span> |<span data-ttu-id="1955f-217">The job manager completed successfully.</span><span class="sxs-lookup"><span data-stu-id="1955f-217">The job manager completed successfully.</span></span> <span data-ttu-id="1955f-218">Your job splitter code ran to completion, and all tasks were added to the job.</span><span class="sxs-lookup"><span data-stu-id="1955f-218">Your job splitter code ran to completion, and all tasks were added to the job.</span></span> |
| <span data-ttu-id="1955f-219">1</span><span class="sxs-lookup"><span data-stu-id="1955f-219">1</span></span> |<span data-ttu-id="1955f-220">The job manager task failed with an exception in an 'expected' part of the program.</span><span class="sxs-lookup"><span data-stu-id="1955f-220">The job manager task failed with an exception in an 'expected' part of the program.</span></span> <span data-ttu-id="1955f-221">The exception was translated to a JobManagerException with diagnostic information and, where possible, suggestions for resolving the failure.</span><span class="sxs-lookup"><span data-stu-id="1955f-221">The exception was translated to a JobManagerException with diagnostic information and, where possible, suggestions for resolving the failure.</span></span> |
| <span data-ttu-id="1955f-222">2</span><span class="sxs-lookup"><span data-stu-id="1955f-222">2</span></span> |<span data-ttu-id="1955f-223">The job manager task failed with an 'unexpected' exception.</span><span class="sxs-lookup"><span data-stu-id="1955f-223">The job manager task failed with an 'unexpected' exception.</span></span> <span data-ttu-id="1955f-224">The exception was logged to standard output, but the job manager was unable to add any additional diagnostic or remediation information.</span><span class="sxs-lookup"><span data-stu-id="1955f-224">The exception was logged to standard output, but the job manager was unable to add any additional diagnostic or remediation information.</span></span> |

<span data-ttu-id="1955f-225">In the case of job manager task failure, some tasks may still have been added to the service before the error occurred.</span><span class="sxs-lookup"><span data-stu-id="1955f-225">In the case of job manager task failure, some tasks may still have been added to the service before the error occurred.</span></span> <span data-ttu-id="1955f-226">These tasks will run as normal.</span><span class="sxs-lookup"><span data-stu-id="1955f-226">These tasks will run as normal.</span></span> <span data-ttu-id="1955f-227">See "Job Splitter Failure" above for discussion of this code path.</span><span class="sxs-lookup"><span data-stu-id="1955f-227">See "Job Splitter Failure" above for discussion of this code path.</span></span>

<span data-ttu-id="1955f-228">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span><span class="sxs-lookup"><span data-stu-id="1955f-228">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="1955f-229">For more information, see [Error Handling](batch-api-basics.md#error-handling).</span><span class="sxs-lookup"><span data-stu-id="1955f-229">For more information, see [Error Handling](batch-api-basics.md#error-handling).</span></span>

### <a name="client-considerations"></a><span data-ttu-id="1955f-230">Client considerations</span><span class="sxs-lookup"><span data-stu-id="1955f-230">Client considerations</span></span>
<span data-ttu-id="1955f-231">This section describes some client implementation requirements when invoking a job manager based on this template.</span><span class="sxs-lookup"><span data-stu-id="1955f-231">This section describes some client implementation requirements when invoking a job manager based on this template.</span></span> <span data-ttu-id="1955f-232">See [How to pass parameters and environment variables from the client code](#pass-environment-settings) for details on passing parameters and environment settings.</span><span class="sxs-lookup"><span data-stu-id="1955f-232">See [How to pass parameters and environment variables from the client code](#pass-environment-settings) for details on passing parameters and environment settings.</span></span>

<span data-ttu-id="1955f-233">**Mandatory credentials**</span><span class="sxs-lookup"><span data-stu-id="1955f-233">**Mandatory credentials**</span></span>

<span data-ttu-id="1955f-234">In order to add tasks to the Azure Batch job, the job manager task requires your Azure Batch account URL and key.</span><span class="sxs-lookup"><span data-stu-id="1955f-234">In order to add tasks to the Azure Batch job, the job manager task requires your Azure Batch account URL and key.</span></span> <span data-ttu-id="1955f-235">You must pass these in environment variables named YOUR_BATCH_URL and YOUR_BATCH_KEY.</span><span class="sxs-lookup"><span data-stu-id="1955f-235">You must pass these in environment variables named YOUR_BATCH_URL and YOUR_BATCH_KEY.</span></span> <span data-ttu-id="1955f-236">You can set these in the Job Manager task environment settings.</span><span class="sxs-lookup"><span data-stu-id="1955f-236">You can set these in the Job Manager task environment settings.</span></span> <span data-ttu-id="1955f-237">For example, in a C# client:</span><span class="sxs-lookup"><span data-stu-id="1955f-237">For example, in a C# client:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
<span data-ttu-id="1955f-238">**Storage credentials**</span><span class="sxs-lookup"><span data-stu-id="1955f-238">**Storage credentials**</span></span>

<span data-ttu-id="1955f-239">Typically, the client does not need to provide the linked storage account credentials to the job manager task because (a) most job managers do not need to explicitly access the linked storage account and (b) the linked storage account is often provided to all tasks as a common environment setting for the job.</span><span class="sxs-lookup"><span data-stu-id="1955f-239">Typically, the client does not need to provide the linked storage account credentials to the job manager task because (a) most job managers do not need to explicitly access the linked storage account and (b) the linked storage account is often provided to all tasks as a common environment setting for the job.</span></span> <span data-ttu-id="1955f-240">If you are not providing the linked storage account via the common environment settings, and the job manager requires access to linked storage, then you should supply the linked storage credentials as follows:</span><span class="sxs-lookup"><span data-stu-id="1955f-240">If you are not providing the linked storage account via the common environment settings, and the job manager requires access to linked storage, then you should supply the linked storage credentials as follows:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="1955f-241">**Job manager task settings**</span><span class="sxs-lookup"><span data-stu-id="1955f-241">**Job manager task settings**</span></span>

<span data-ttu-id="1955f-242">The client should set the job manager *killJobOnCompletion* flag to **false**.</span><span class="sxs-lookup"><span data-stu-id="1955f-242">The client should set the job manager *killJobOnCompletion* flag to **false**.</span></span>

<span data-ttu-id="1955f-243">It is usually safe for the client to set *runExclusive* to **false**.</span><span class="sxs-lookup"><span data-stu-id="1955f-243">It is usually safe for the client to set *runExclusive* to **false**.</span></span>

<span data-ttu-id="1955f-244">The client should use the *resourceFiles* or *applicationPackageReferences* collection to have the job manager executable (and its required DLLs) deployed to the compute node.</span><span class="sxs-lookup"><span data-stu-id="1955f-244">The client should use the *resourceFiles* or *applicationPackageReferences* collection to have the job manager executable (and its required DLLs) deployed to the compute node.</span></span>

<span data-ttu-id="1955f-245">By default, the job manager will not be retried if it fails.</span><span class="sxs-lookup"><span data-stu-id="1955f-245">By default, the job manager will not be retried if it fails.</span></span> <span data-ttu-id="1955f-246">Depending on your job manager logic, the client may want to enable retries via *constraints*/*maxTaskRetryCount*.</span><span class="sxs-lookup"><span data-stu-id="1955f-246">Depending on your job manager logic, the client may want to enable retries via *constraints*/*maxTaskRetryCount*.</span></span>

<span data-ttu-id="1955f-247">**Job settings**</span><span class="sxs-lookup"><span data-stu-id="1955f-247">**Job settings**</span></span>

<span data-ttu-id="1955f-248">If the job splitter emits tasks with dependencies, the client must set the job's usesTaskDependencies to true.</span><span class="sxs-lookup"><span data-stu-id="1955f-248">If the job splitter emits tasks with dependencies, the client must set the job's usesTaskDependencies to true.</span></span>

<span data-ttu-id="1955f-249">In the job splitter model, it is unusual for clients to wish to add tasks to jobs over and above what the job splitter creates.</span><span class="sxs-lookup"><span data-stu-id="1955f-249">In the job splitter model, it is unusual for clients to wish to add tasks to jobs over and above what the job splitter creates.</span></span> <span data-ttu-id="1955f-250">The client should therefore normally set the job's *onAllTasksComplete* to **terminatejob**.</span><span class="sxs-lookup"><span data-stu-id="1955f-250">The client should therefore normally set the job's *onAllTasksComplete* to **terminatejob**.</span></span>

## <a name="task-processor-template"></a><span data-ttu-id="1955f-251">Task Processor template</span><span class="sxs-lookup"><span data-stu-id="1955f-251">Task Processor template</span></span>
<span data-ttu-id="1955f-252">A Task Processor template helps you to implement a task processor that can perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="1955f-252">A Task Processor template helps you to implement a task processor that can perform the following actions:</span></span>

* <span data-ttu-id="1955f-253">Set up the information required by each Batch task to run.</span><span class="sxs-lookup"><span data-stu-id="1955f-253">Set up the information required by each Batch task to run.</span></span>
* <span data-ttu-id="1955f-254">Run all actions required by each Batch task.</span><span class="sxs-lookup"><span data-stu-id="1955f-254">Run all actions required by each Batch task.</span></span>
* <span data-ttu-id="1955f-255">Save task outputs to persistent storage.</span><span class="sxs-lookup"><span data-stu-id="1955f-255">Save task outputs to persistent storage.</span></span>

<span data-ttu-id="1955f-256">Although a task processor is not required to run tasks on Batch, the key advantage of using a task processor is that it provides a wrapper to implement all task execution actions in one location.</span><span class="sxs-lookup"><span data-stu-id="1955f-256">Although a task processor is not required to run tasks on Batch, the key advantage of using a task processor is that it provides a wrapper to implement all task execution actions in one location.</span></span> <span data-ttu-id="1955f-257">For example, if you need to run several applications in the context of each task, or if you need to copy data to persistent storage after completing each task.</span><span class="sxs-lookup"><span data-stu-id="1955f-257">For example, if you need to run several applications in the context of each task, or if you need to copy data to persistent storage after completing each task.</span></span>

<span data-ttu-id="1955f-258">The actions performed by the task processor can be as simple or complex, and as many or as few, as required by your workload.</span><span class="sxs-lookup"><span data-stu-id="1955f-258">The actions performed by the task processor can be as simple or complex, and as many or as few, as required by your workload.</span></span> <span data-ttu-id="1955f-259">Additionally, by implementing all task actions into one task processor, you can readily update or add actions based on changes to applications or workload requirements.</span><span class="sxs-lookup"><span data-stu-id="1955f-259">Additionally, by implementing all task actions into one task processor, you can readily update or add actions based on changes to applications or workload requirements.</span></span> <span data-ttu-id="1955f-260">However, in some cases a task processor might not be the optimal solution for your implementation as it can add unnecessary complexity, for example when running jobs that can be quickly started from a simple command line.</span><span class="sxs-lookup"><span data-stu-id="1955f-260">However, in some cases a task processor might not be the optimal solution for your implementation as it can add unnecessary complexity, for example when running jobs that can be quickly started from a simple command line.</span></span>

### <a name="create-a-task-processor-using-the-template"></a><span data-ttu-id="1955f-261">Create a Task Processor using the template</span><span class="sxs-lookup"><span data-stu-id="1955f-261">Create a Task Processor using the template</span></span>
<span data-ttu-id="1955f-262">To add a task processor to the solution that you created earlier, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1955f-262">To add a task processor to the solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="1955f-263">Open your existing solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1955f-263">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="1955f-264">In Solution Explorer, right-click the solution, click **Add**, and then click **New Project**.</span><span class="sxs-lookup"><span data-stu-id="1955f-264">In Solution Explorer, right-click the solution, click **Add**, and then click **New Project**.</span></span>
3. <span data-ttu-id="1955f-265">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Task Processor**.</span><span class="sxs-lookup"><span data-stu-id="1955f-265">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Task Processor**.</span></span>
4. <span data-ttu-id="1955f-266">Type a name that describes your application and identifies this project as the task processor (e.g. "LitwareTaskProcessor").</span><span class="sxs-lookup"><span data-stu-id="1955f-266">Type a name that describes your application and identifies this project as the task processor (e.g. "LitwareTaskProcessor").</span></span>
5. <span data-ttu-id="1955f-267">To create the project, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1955f-267">To create the project, click **OK**.</span></span>
6. <span data-ttu-id="1955f-268">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span><span class="sxs-lookup"><span data-stu-id="1955f-268">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span></span>

### <a name="task-processor-template-files-and-their-purpose"></a><span data-ttu-id="1955f-269">Task Processor template files and their purpose</span><span class="sxs-lookup"><span data-stu-id="1955f-269">Task Processor template files and their purpose</span></span>
<span data-ttu-id="1955f-270">When you create a project using the task processor template, it generates three groups of code files:</span><span class="sxs-lookup"><span data-stu-id="1955f-270">When you create a project using the task processor template, it generates three groups of code files:</span></span>

* <span data-ttu-id="1955f-271">The main program file (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="1955f-271">The main program file (Program.cs).</span></span> <span data-ttu-id="1955f-272">This contains the program entry point and top-level exception handling.</span><span class="sxs-lookup"><span data-stu-id="1955f-272">This contains the program entry point and top-level exception handling.</span></span> <span data-ttu-id="1955f-273">You shouldn't normally need to modify this.</span><span class="sxs-lookup"><span data-stu-id="1955f-273">You shouldn't normally need to modify this.</span></span>
* <span data-ttu-id="1955f-274">The Framework directory.</span><span class="sxs-lookup"><span data-stu-id="1955f-274">The Framework directory.</span></span> <span data-ttu-id="1955f-275">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span><span class="sxs-lookup"><span data-stu-id="1955f-275">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span></span>
* <span data-ttu-id="1955f-276">The task processor file (TaskProcessor.cs).</span><span class="sxs-lookup"><span data-stu-id="1955f-276">The task processor file (TaskProcessor.cs).</span></span> <span data-ttu-id="1955f-277">This is where you will put your application-specific logic for executing a task (typically by calling out to an existing executable).</span><span class="sxs-lookup"><span data-stu-id="1955f-277">This is where you will put your application-specific logic for executing a task (typically by calling out to an existing executable).</span></span> <span data-ttu-id="1955f-278">Pre- and post-processing code, such as downloading additional data or uploading result files, also goes here.</span><span class="sxs-lookup"><span data-stu-id="1955f-278">Pre- and post-processing code, such as downloading additional data or uploading result files, also goes here.</span></span>

<span data-ttu-id="1955f-279">Of course you can add additional files as required to support your task processor code, depending on the complexity of the job splitting logic.</span><span class="sxs-lookup"><span data-stu-id="1955f-279">Of course you can add additional files as required to support your task processor code, depending on the complexity of the job splitting logic.</span></span>

<span data-ttu-id="1955f-280">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span><span class="sxs-lookup"><span data-stu-id="1955f-280">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="1955f-281">The rest of this section describes the different files and their code structure, and explains what each class does.</span><span class="sxs-lookup"><span data-stu-id="1955f-281">The rest of this section describes the different files and their code structure, and explains what each class does.</span></span>

![Visual Studio Solution Explorer showing the Task Processor template solution][solution_explorer02]

<span data-ttu-id="1955f-283">**Framework files**</span><span class="sxs-lookup"><span data-stu-id="1955f-283">**Framework files**</span></span>

* <span data-ttu-id="1955f-284">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span><span class="sxs-lookup"><span data-stu-id="1955f-284">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="1955f-285">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span><span class="sxs-lookup"><span data-stu-id="1955f-285">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="1955f-286">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span><span class="sxs-lookup"><span data-stu-id="1955f-286">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="1955f-287">`TaskProcessorException.cs`: Represents an error that requires the job manager to terminate.</span><span class="sxs-lookup"><span data-stu-id="1955f-287">`TaskProcessorException.cs`: Represents an error that requires the job manager to terminate.</span></span> <span data-ttu-id="1955f-288">TaskProcessorException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span><span class="sxs-lookup"><span data-stu-id="1955f-288">TaskProcessorException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>

<span data-ttu-id="1955f-289">**Task Processor**</span><span class="sxs-lookup"><span data-stu-id="1955f-289">**Task Processor**</span></span>

* <span data-ttu-id="1955f-290">`TaskProcessor.cs`: Runs the task.</span><span class="sxs-lookup"><span data-stu-id="1955f-290">`TaskProcessor.cs`: Runs the task.</span></span> <span data-ttu-id="1955f-291">The framework invokes the TaskProcessor.Run method.</span><span class="sxs-lookup"><span data-stu-id="1955f-291">The framework invokes the TaskProcessor.Run method.</span></span> <span data-ttu-id="1955f-292">This is the class where you will inject the application-specific logic of your task.</span><span class="sxs-lookup"><span data-stu-id="1955f-292">This is the class where you will inject the application-specific logic of your task.</span></span> <span data-ttu-id="1955f-293">Implement the Run method to:</span><span class="sxs-lookup"><span data-stu-id="1955f-293">Implement the Run method to:</span></span>
  * <span data-ttu-id="1955f-294">Parse and validate any task parameters</span><span class="sxs-lookup"><span data-stu-id="1955f-294">Parse and validate any task parameters</span></span>
  * <span data-ttu-id="1955f-295">Compose the command line for any external program you want to invoke</span><span class="sxs-lookup"><span data-stu-id="1955f-295">Compose the command line for any external program you want to invoke</span></span>
  * <span data-ttu-id="1955f-296">Log any diagnostic information you may require for debugging purposes</span><span class="sxs-lookup"><span data-stu-id="1955f-296">Log any diagnostic information you may require for debugging purposes</span></span>
  * <span data-ttu-id="1955f-297">Start a process using that command line</span><span class="sxs-lookup"><span data-stu-id="1955f-297">Start a process using that command line</span></span>
  * <span data-ttu-id="1955f-298">Wait for the process to exit</span><span class="sxs-lookup"><span data-stu-id="1955f-298">Wait for the process to exit</span></span>
  * <span data-ttu-id="1955f-299">Capture the exit code of the process to determine if it succeeded or failed</span><span class="sxs-lookup"><span data-stu-id="1955f-299">Capture the exit code of the process to determine if it succeeded or failed</span></span>
  * <span data-ttu-id="1955f-300">Save any output files you want to keep to persistent storage</span><span class="sxs-lookup"><span data-stu-id="1955f-300">Save any output files you want to keep to persistent storage</span></span>

<span data-ttu-id="1955f-301">**Standard .NET command line project files**</span><span class="sxs-lookup"><span data-stu-id="1955f-301">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="1955f-302">`App.config`: Standard .NET application configuration file.</span><span class="sxs-lookup"><span data-stu-id="1955f-302">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="1955f-303">`Packages.config`: Standard NuGet package dependency file.</span><span class="sxs-lookup"><span data-stu-id="1955f-303">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="1955f-304">`Program.cs`: Contains the program entry point and top-level exception handling.</span><span class="sxs-lookup"><span data-stu-id="1955f-304">`Program.cs`: Contains the program entry point and top-level exception handling.</span></span>

## <a name="implementing-the-task-processor"></a><span data-ttu-id="1955f-305">Implementing the task processor</span><span class="sxs-lookup"><span data-stu-id="1955f-305">Implementing the task processor</span></span>
<span data-ttu-id="1955f-306">When you open the Task Processor template project, the project will have the TaskProcessor.cs file open by default.</span><span class="sxs-lookup"><span data-stu-id="1955f-306">When you open the Task Processor template project, the project will have the TaskProcessor.cs file open by default.</span></span> <span data-ttu-id="1955f-307">You can implement the run logic for the tasks in your workload by using the Run() method shown below:</span><span class="sxs-lookup"><span data-stu-id="1955f-307">You can implement the run logic for the tasks in your workload by using the Run() method shown below:</span></span>

```csharp
/// <summary>
/// Runs the task processing logic. This is where you inject
/// your application-specific logic for decomposing the job into tasks.
///
/// The task processor framework invokes the Run method for you; you need
/// only to implement it, not to call it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check the exit code of that program and
/// save output files to persistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for the task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> <span data-ttu-id="1955f-308">The annotated section in the Run() method is the only section of the Task Processor template code that is intended for you to modify by adding the run logic for the tasks in your workload.</span><span class="sxs-lookup"><span data-stu-id="1955f-308">The annotated section in the Run() method is the only section of the Task Processor template code that is intended for you to modify by adding the run logic for the tasks in your workload.</span></span> <span data-ttu-id="1955f-309">If you want to modify a different section of the template, please first familiarize yourself with how Batch works by reviewing the Batch documentation and trying out a few of the Batch code samples.</span><span class="sxs-lookup"><span data-stu-id="1955f-309">If you want to modify a different section of the template, please first familiarize yourself with how Batch works by reviewing the Batch documentation and trying out a few of the Batch code samples.</span></span>
> 
> 

<span data-ttu-id="1955f-310">The Run() method is responsible for launching the command line, starting one or more processes, waiting for all process to complete, saving the results, and finally returning with an exit code.</span><span class="sxs-lookup"><span data-stu-id="1955f-310">The Run() method is responsible for launching the command line, starting one or more processes, waiting for all process to complete, saving the results, and finally returning with an exit code.</span></span> <span data-ttu-id="1955f-311">The Run() method is where you implement the processing logic for your tasks.</span><span class="sxs-lookup"><span data-stu-id="1955f-311">The Run() method is where you implement the processing logic for your tasks.</span></span> <span data-ttu-id="1955f-312">The task processor framework invokes the Run() method for you; you do not need to call it yourself.</span><span class="sxs-lookup"><span data-stu-id="1955f-312">The task processor framework invokes the Run() method for you; you do not need to call it yourself.</span></span>

<span data-ttu-id="1955f-313">Your Run() implementation has access to:</span><span class="sxs-lookup"><span data-stu-id="1955f-313">Your Run() implementation has access to:</span></span>

* <span data-ttu-id="1955f-314">The task parameters, via the `_parameters` field.</span><span class="sxs-lookup"><span data-stu-id="1955f-314">The task parameters, via the `_parameters` field.</span></span>
* <span data-ttu-id="1955f-315">The job and task ids, via the `_jobId` and `_taskId` fields.</span><span class="sxs-lookup"><span data-stu-id="1955f-315">The job and task ids, via the `_jobId` and `_taskId` fields.</span></span>
* <span data-ttu-id="1955f-316">The task configuration, via the `_configuration` field.</span><span class="sxs-lookup"><span data-stu-id="1955f-316">The task configuration, via the `_configuration` field.</span></span>

<span data-ttu-id="1955f-317">**Task failure**</span><span class="sxs-lookup"><span data-stu-id="1955f-317">**Task failure**</span></span>

<span data-ttu-id="1955f-318">In case of failure, you can exit the Run() method by throwing an exception, but this leaves the top level exception handler in control of the task exit code.</span><span class="sxs-lookup"><span data-stu-id="1955f-318">In case of failure, you can exit the Run() method by throwing an exception, but this leaves the top level exception handler in control of the task exit code.</span></span> <span data-ttu-id="1955f-319">If you need to control the exit code so that you can distinguish different types of failure, for example for diagnostic purposes or because some failure modes should terminate the job and others should not, then you should exit the Run() method by returning a non-zero exit code.</span><span class="sxs-lookup"><span data-stu-id="1955f-319">If you need to control the exit code so that you can distinguish different types of failure, for example for diagnostic purposes or because some failure modes should terminate the job and others should not, then you should exit the Run() method by returning a non-zero exit code.</span></span> <span data-ttu-id="1955f-320">This becomes the task exit code.</span><span class="sxs-lookup"><span data-stu-id="1955f-320">This becomes the task exit code.</span></span>

### <a name="exit-codes-and-exceptions-in-the-task-processor-template"></a><span data-ttu-id="1955f-321">Exit codes and exceptions in the Task Processor template</span><span class="sxs-lookup"><span data-stu-id="1955f-321">Exit codes and exceptions in the Task Processor template</span></span>
<span data-ttu-id="1955f-322">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help identify any problems with the execution of the program.</span><span class="sxs-lookup"><span data-stu-id="1955f-322">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help identify any problems with the execution of the program.</span></span> <span data-ttu-id="1955f-323">The Task Processor template implements the exit codes and exceptions described in this section.</span><span class="sxs-lookup"><span data-stu-id="1955f-323">The Task Processor template implements the exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="1955f-324">A task processor task that is implemented with the Task Processor template can return three possible exit codes:</span><span class="sxs-lookup"><span data-stu-id="1955f-324">A task processor task that is implemented with the Task Processor template can return three possible exit codes:</span></span>

| <span data-ttu-id="1955f-325">Code</span><span class="sxs-lookup"><span data-stu-id="1955f-325">Code</span></span> | <span data-ttu-id="1955f-326">Description</span><span class="sxs-lookup"><span data-stu-id="1955f-326">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1955f-327">[Process.ExitCode][process_exitcode]</span><span class="sxs-lookup"><span data-stu-id="1955f-327">[Process.ExitCode][process_exitcode]</span></span> |<span data-ttu-id="1955f-328">The task processor ran to completion.</span><span class="sxs-lookup"><span data-stu-id="1955f-328">The task processor ran to completion.</span></span> <span data-ttu-id="1955f-329">Note that this does not imply that the program you invoked was successful – only that the task processor invoked it successfully and performed any post-processing without exceptions.</span><span class="sxs-lookup"><span data-stu-id="1955f-329">Note that this does not imply that the program you invoked was successful – only that the task processor invoked it successfully and performed any post-processing without exceptions.</span></span> <span data-ttu-id="1955f-330">The meaning of the exit code depends on the invoked program – typically exit code 0 means the program succeeded and any other exit code means the program failed.</span><span class="sxs-lookup"><span data-stu-id="1955f-330">The meaning of the exit code depends on the invoked program – typically exit code 0 means the program succeeded and any other exit code means the program failed.</span></span> |
| <span data-ttu-id="1955f-331">1</span><span class="sxs-lookup"><span data-stu-id="1955f-331">1</span></span> |<span data-ttu-id="1955f-332">The task processor failed with an exception in an 'expected' part of the program.</span><span class="sxs-lookup"><span data-stu-id="1955f-332">The task processor failed with an exception in an 'expected' part of the program.</span></span> <span data-ttu-id="1955f-333">The exception was translated to a `TaskProcessorException` with diagnostic information and, where possible, suggestions for resolving the failure.</span><span class="sxs-lookup"><span data-stu-id="1955f-333">The exception was translated to a `TaskProcessorException` with diagnostic information and, where possible, suggestions for resolving the failure.</span></span> |
| <span data-ttu-id="1955f-334">2</span><span class="sxs-lookup"><span data-stu-id="1955f-334">2</span></span> |<span data-ttu-id="1955f-335">The task processor failed with an 'unexpected' exception.</span><span class="sxs-lookup"><span data-stu-id="1955f-335">The task processor failed with an 'unexpected' exception.</span></span> <span data-ttu-id="1955f-336">The exception was logged to standard output, but the task processor was unable to add any additional diagnostic or remediation information.</span><span class="sxs-lookup"><span data-stu-id="1955f-336">The exception was logged to standard output, but the task processor was unable to add any additional diagnostic or remediation information.</span></span> |

> [!NOTE]
> <span data-ttu-id="1955f-337">If the program you invoke uses exit codes 1 and 2 to indicate specific failure modes, then using exit codes 1 and 2 for task processor errors is ambiguous.</span><span class="sxs-lookup"><span data-stu-id="1955f-337">If the program you invoke uses exit codes 1 and 2 to indicate specific failure modes, then using exit codes 1 and 2 for task processor errors is ambiguous.</span></span> <span data-ttu-id="1955f-338">You can change these task processor error codes to distinctive exit codes by editing the exception cases in the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="1955f-338">You can change these task processor error codes to distinctive exit codes by editing the exception cases in the Program.cs file.</span></span>
> 
> 

<span data-ttu-id="1955f-339">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span><span class="sxs-lookup"><span data-stu-id="1955f-339">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="1955f-340">For more information, see Error Handling, in the Batch documentation.</span><span class="sxs-lookup"><span data-stu-id="1955f-340">For more information, see Error Handling, in the Batch documentation.</span></span>

### <a name="client-considerations"></a><span data-ttu-id="1955f-341">Client considerations</span><span class="sxs-lookup"><span data-stu-id="1955f-341">Client considerations</span></span>
<span data-ttu-id="1955f-342">**Storage credentials**</span><span class="sxs-lookup"><span data-stu-id="1955f-342">**Storage credentials**</span></span>

<span data-ttu-id="1955f-343">If your task processor uses Azure blob storage to persist outputs, for example using the file conventions helper library, then it needs access to *either* the cloud storage account credentials *or* a blob container URL that includes a shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="1955f-343">If your task processor uses Azure blob storage to persist outputs, for example using the file conventions helper library, then it needs access to *either* the cloud storage account credentials *or* a blob container URL that includes a shared access signature (SAS).</span></span> <span data-ttu-id="1955f-344">The template includes support for providing credentials via common environment variables.</span><span class="sxs-lookup"><span data-stu-id="1955f-344">The template includes support for providing credentials via common environment variables.</span></span> <span data-ttu-id="1955f-345">Your client can pass the storage credentials as follows:</span><span class="sxs-lookup"><span data-stu-id="1955f-345">Your client can pass the storage credentials as follows:</span></span>

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="1955f-346">The storage account is then available in the TaskProcessor class via the `_configuration.StorageAccount` property.</span><span class="sxs-lookup"><span data-stu-id="1955f-346">The storage account is then available in the TaskProcessor class via the `_configuration.StorageAccount` property.</span></span>

<span data-ttu-id="1955f-347">If you prefer to use a container URL with SAS, you can also pass this via an job common environment setting, but the task processor template does not currently include built-in support for this.</span><span class="sxs-lookup"><span data-stu-id="1955f-347">If you prefer to use a container URL with SAS, you can also pass this via an job common environment setting, but the task processor template does not currently include built-in support for this.</span></span>

<span data-ttu-id="1955f-348">**Storage setup**</span><span class="sxs-lookup"><span data-stu-id="1955f-348">**Storage setup**</span></span>

<span data-ttu-id="1955f-349">It is recommended that the client or job manager task create any containers required by tasks before adding the tasks to the job.</span><span class="sxs-lookup"><span data-stu-id="1955f-349">It is recommended that the client or job manager task create any containers required by tasks before adding the tasks to the job.</span></span> <span data-ttu-id="1955f-350">This is mandatory if you use a container URL with SAS, as such a URL does not include permission to create the container.</span><span class="sxs-lookup"><span data-stu-id="1955f-350">This is mandatory if you use a container URL with SAS, as such a URL does not include permission to create the container.</span></span> <span data-ttu-id="1955f-351">It is recommended even if you pass storage account credentials, as it saves every task having to call CloudBlobContainer.CreateIfNotExistsAsync on the container.</span><span class="sxs-lookup"><span data-stu-id="1955f-351">It is recommended even if you pass storage account credentials, as it saves every task having to call CloudBlobContainer.CreateIfNotExistsAsync on the container.</span></span>

## <a name="pass-parameters-and-environment-variables"></a><span data-ttu-id="1955f-352">Pass parameters and environment variables</span><span class="sxs-lookup"><span data-stu-id="1955f-352">Pass parameters and environment variables</span></span>
### <a name="pass-environment-settings"></a><span data-ttu-id="1955f-353">Pass environment settings</span><span class="sxs-lookup"><span data-stu-id="1955f-353">Pass environment settings</span></span>
<span data-ttu-id="1955f-354">A client can pass information to the job manager task in the form of environment settings.</span><span class="sxs-lookup"><span data-stu-id="1955f-354">A client can pass information to the job manager task in the form of environment settings.</span></span> <span data-ttu-id="1955f-355">This information can then be used by the job manager task when generating the task processor tasks that will run as part of the compute job.</span><span class="sxs-lookup"><span data-stu-id="1955f-355">This information can then be used by the job manager task when generating the task processor tasks that will run as part of the compute job.</span></span> <span data-ttu-id="1955f-356">Examples of the information that you can pass as environment settings are:</span><span class="sxs-lookup"><span data-stu-id="1955f-356">Examples of the information that you can pass as environment settings are:</span></span>

* <span data-ttu-id="1955f-357">Storage account name and account keys</span><span class="sxs-lookup"><span data-stu-id="1955f-357">Storage account name and account keys</span></span>
* <span data-ttu-id="1955f-358">Batch account URL</span><span class="sxs-lookup"><span data-stu-id="1955f-358">Batch account URL</span></span>
* <span data-ttu-id="1955f-359">Batch account key</span><span class="sxs-lookup"><span data-stu-id="1955f-359">Batch account key</span></span>

<span data-ttu-id="1955f-360">The Batch service has a simple mechanism to pass environment settings to a job manager task by using the `EnvironmentSettings` property in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].</span><span class="sxs-lookup"><span data-stu-id="1955f-360">The Batch service has a simple mechanism to pass environment settings to a job manager task by using the `EnvironmentSettings` property in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].</span></span>

<span data-ttu-id="1955f-361">For example, to get the `BatchClient` instance for a Batch account, you can pass as environment variables from the client code the URL and shared key credentials for the Batch account.</span><span class="sxs-lookup"><span data-stu-id="1955f-361">For example, to get the `BatchClient` instance for a Batch account, you can pass as environment variables from the client code the URL and shared key credentials for the Batch account.</span></span> <span data-ttu-id="1955f-362">Likewise, to access the storage account that is linked to the Batch account, you can pass the storage account name and the storage account key as environment variables.</span><span class="sxs-lookup"><span data-stu-id="1955f-362">Likewise, to access the storage account that is linked to the Batch account, you can pass the storage account name and the storage account key as environment variables.</span></span>

### <a name="pass-parameters-to-the-job-manager-template"></a><span data-ttu-id="1955f-363">Pass parameters to the Job Manager template</span><span class="sxs-lookup"><span data-stu-id="1955f-363">Pass parameters to the Job Manager template</span></span>
<span data-ttu-id="1955f-364">In many cases, it's useful to pass per-job parameters to the job manager task, either to control the job splitting process or to configure the tasks for the job.</span><span class="sxs-lookup"><span data-stu-id="1955f-364">In many cases, it's useful to pass per-job parameters to the job manager task, either to control the job splitting process or to configure the tasks for the job.</span></span> <span data-ttu-id="1955f-365">You can do this by uploading a JSON file named parameters.json as a resource file for the job manager task.</span><span class="sxs-lookup"><span data-stu-id="1955f-365">You can do this by uploading a JSON file named parameters.json as a resource file for the job manager task.</span></span> <span data-ttu-id="1955f-366">The parameters can then become available in the `JobSplitter._parameters` field in the Job Manager template.</span><span class="sxs-lookup"><span data-stu-id="1955f-366">The parameters can then become available in the `JobSplitter._parameters` field in the Job Manager template.</span></span>

> [!NOTE]
> <span data-ttu-id="1955f-367">The built-in parameter handler supports only string-to-string dictionaries.</span><span class="sxs-lookup"><span data-stu-id="1955f-367">The built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="1955f-368">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the job splitter, or modify the framework's `Configuration.GetJobParameters` method.</span><span class="sxs-lookup"><span data-stu-id="1955f-368">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the job splitter, or modify the framework's `Configuration.GetJobParameters` method.</span></span>
> 
> 

### <a name="pass-parameters-to-the-task-processor-template"></a><span data-ttu-id="1955f-369">Pass parameters to the Task Processor template</span><span class="sxs-lookup"><span data-stu-id="1955f-369">Pass parameters to the Task Processor template</span></span>
<span data-ttu-id="1955f-370">You can also pass parameters to individual tasks implemented using the Task Processor template.</span><span class="sxs-lookup"><span data-stu-id="1955f-370">You can also pass parameters to individual tasks implemented using the Task Processor template.</span></span> <span data-ttu-id="1955f-371">Just as with the job manager template, the task processor template looks for a resource file named</span><span class="sxs-lookup"><span data-stu-id="1955f-371">Just as with the job manager template, the task processor template looks for a resource file named</span></span>

<span data-ttu-id="1955f-372">parameters.json, and if found it loads it as the parameters dictionary.</span><span class="sxs-lookup"><span data-stu-id="1955f-372">parameters.json, and if found it loads it as the parameters dictionary.</span></span> <span data-ttu-id="1955f-373">There are a couple of options for how to pass parameters to the task processor tasks:</span><span class="sxs-lookup"><span data-stu-id="1955f-373">There are a couple of options for how to pass parameters to the task processor tasks:</span></span>

* <span data-ttu-id="1955f-374">Reuse the job parameters JSON.</span><span class="sxs-lookup"><span data-stu-id="1955f-374">Reuse the job parameters JSON.</span></span> <span data-ttu-id="1955f-375">This works well if the only parameters are job-wide ones (for example, a render height and width).</span><span class="sxs-lookup"><span data-stu-id="1955f-375">This works well if the only parameters are job-wide ones (for example, a render height and width).</span></span> <span data-ttu-id="1955f-376">To do this, when creating a CloudTask in the job splitter, add a reference to the parameters.json resource file object from the job manager task's ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) to the CloudTask's ResourceFiles collection.</span><span class="sxs-lookup"><span data-stu-id="1955f-376">To do this, when creating a CloudTask in the job splitter, add a reference to the parameters.json resource file object from the job manager task's ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) to the CloudTask's ResourceFiles collection.</span></span>
* <span data-ttu-id="1955f-377">Generate and upload a task-specific parameters.json document as part of job splitter execution, and reference that blob in the task's resource files collection.</span><span class="sxs-lookup"><span data-stu-id="1955f-377">Generate and upload a task-specific parameters.json document as part of job splitter execution, and reference that blob in the task's resource files collection.</span></span> <span data-ttu-id="1955f-378">This is necessary if different tasks have different parameters.</span><span class="sxs-lookup"><span data-stu-id="1955f-378">This is necessary if different tasks have different parameters.</span></span> <span data-ttu-id="1955f-379">An example might be a 3D rendering scenario where the frame index is passed to the task as a parameter.</span><span class="sxs-lookup"><span data-stu-id="1955f-379">An example might be a 3D rendering scenario where the frame index is passed to the task as a parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="1955f-380">The built-in parameter handler supports only string-to-string dictionaries.</span><span class="sxs-lookup"><span data-stu-id="1955f-380">The built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="1955f-381">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the task processor, or modify the framework's `Configuration.GetTaskParameters` method.</span><span class="sxs-lookup"><span data-stu-id="1955f-381">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the task processor, or modify the framework's `Configuration.GetTaskParameters` method.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1955f-382">Next steps</span><span class="sxs-lookup"><span data-stu-id="1955f-382">Next steps</span></span>
### <a name="persist-job-and-task-output-to-azure-storage"></a><span data-ttu-id="1955f-383">Persist job and task output to Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1955f-383">Persist job and task output to Azure Storage</span></span>
<span data-ttu-id="1955f-384">Another helpful tool in Batch solution development is [Azure Batch File Conventions][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="1955f-384">Another helpful tool in Batch solution development is [Azure Batch File Conventions][nuget_package].</span></span> <span data-ttu-id="1955f-385">Use this .NET class library (currently in preview) in your Batch .NET applications to easily store and retrieve task outputs to and from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1955f-385">Use this .NET class library (currently in preview) in your Batch .NET applications to easily store and retrieve task outputs to and from Azure Storage.</span></span> <span data-ttu-id="1955f-386">[Persist Azure Batch job and task output](batch-task-output.md) contains a full discussion of the library and its usage.</span><span class="sxs-lookup"><span data-stu-id="1955f-386">[Persist Azure Batch job and task output](batch-task-output.md) contains a full discussion of the library and its usage.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="1955f-387">Batch Forum</span><span class="sxs-lookup"><span data-stu-id="1955f-387">Batch Forum</span></span>
<span data-ttu-id="1955f-388">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span><span class="sxs-lookup"><span data-stu-id="1955f-388">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="1955f-389">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="1955f-389">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-visual-studio-templates/solution_explorer02.png



