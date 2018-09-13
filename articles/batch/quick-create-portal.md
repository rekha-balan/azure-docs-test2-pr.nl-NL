---
title: Azure Quickstart - Run Batch job - Portal
description: Quickly learn to run a Batch job with the Azure portal.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.devlang: na
ms.topic: quickstart
ms.date: 07/03/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7daaf042d22ba4ac0369b732b586a3760d8cd51c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864962"
---
# <a name="quickstart-run-your-first-batch-job-in-the-azure-portal"></a><span data-ttu-id="20396-103">Quickstart: Run your first Batch job in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="20396-103">Quickstart: Run your first Batch job in the Azure portal</span></span>

<span data-ttu-id="20396-104">This quickstart shows how to use the Azure portal to create a Batch account, a *pool* of compute nodes (virtual machines), and a *job* that runs basic *tasks* on the pool.</span><span class="sxs-lookup"><span data-stu-id="20396-104">This quickstart shows how to use the Azure portal to create a Batch account, a *pool* of compute nodes (virtual machines), and a *job* that runs basic *tasks* on the pool.</span></span> <span data-ttu-id="20396-105">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="20396-105">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="sign-in-to-azure"></a><span data-ttu-id="20396-106">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="20396-106">Sign in to Azure</span></span> 

<span data-ttu-id="20396-107">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="20396-107">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-a-batch-account"></a><span data-ttu-id="20396-108">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="20396-108">Create a Batch account</span></span>

<span data-ttu-id="20396-109">Follow these steps to create a sample Batch account for test purposes.</span><span class="sxs-lookup"><span data-stu-id="20396-109">Follow these steps to create a sample Batch account for test purposes.</span></span> <span data-ttu-id="20396-110">You need a Batch account to create pools and jobs.</span><span class="sxs-lookup"><span data-stu-id="20396-110">You need a Batch account to create pools and jobs.</span></span> <span data-ttu-id="20396-111">As shown here, you can link an Azure storage account with the Batch account.</span><span class="sxs-lookup"><span data-stu-id="20396-111">As shown here, you can link an Azure storage account with the Batch account.</span></span> <span data-ttu-id="20396-112">Although not required for this quickstart, the storage account is useful to deploy applications and store input and output data for most real-world workloads.</span><span class="sxs-lookup"><span data-stu-id="20396-112">Although not required for this quickstart, the storage account is useful to deploy applications and store input and output data for most real-world workloads.</span></span>


1. <span data-ttu-id="20396-113">Select **Create a resource** > **Compute** > **Batch Service**.</span><span class="sxs-lookup"><span data-stu-id="20396-113">Select **Create a resource** > **Compute** > **Batch Service**.</span></span> 

  ![Batch in the Marketplace][marketplace_portal]

2. <span data-ttu-id="20396-115">Enter values for **Account name** and **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="20396-115">Enter values for **Account name** and **Resource group**.</span></span> <span data-ttu-id="20396-116">The account name must be unique within the Azure **Location** selected, use only lowercase characters or numbers, and contain 3-24 characters.</span><span class="sxs-lookup"><span data-stu-id="20396-116">The account name must be unique within the Azure **Location** selected, use only lowercase characters or numbers, and contain 3-24 characters.</span></span> 

3. <span data-ttu-id="20396-117">In **Storage account**, select an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="20396-117">In **Storage account**, select an existing storage account or create a new one.</span></span>

4. <span data-ttu-id="20396-118">Keep the defaults for remaining settings, and select **Create** to create the account.</span><span class="sxs-lookup"><span data-stu-id="20396-118">Keep the defaults for remaining settings, and select **Create** to create the account.</span></span>

  ![Create a Batch account][account_portal]  

<span data-ttu-id="20396-120">When the **Deployment succeeded** message appears, go to the Batch account in the portal.</span><span class="sxs-lookup"><span data-stu-id="20396-120">When the **Deployment succeeded** message appears, go to the Batch account in the portal.</span></span>

## <a name="create-a-pool-of-compute-nodes"></a><span data-ttu-id="20396-121">Create a pool of compute nodes</span><span class="sxs-lookup"><span data-stu-id="20396-121">Create a pool of compute nodes</span></span>

<span data-ttu-id="20396-122">Now that you have a Batch account, create a sample pool of Windows compute nodes for test purposes.</span><span class="sxs-lookup"><span data-stu-id="20396-122">Now that you have a Batch account, create a sample pool of Windows compute nodes for test purposes.</span></span> <span data-ttu-id="20396-123">The pool for this quick example consists of 2 nodes running a Windows Server 2012 R2 image from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="20396-123">The pool for this quick example consists of 2 nodes running a Windows Server 2012 R2 image from the Azure Marketplace.</span></span>


1. <span data-ttu-id="20396-124">In the Batch account, select **Pools** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="20396-124">In the Batch account, select **Pools** > **Add**.</span></span>

2. <span data-ttu-id="20396-125">Enter a **Pool ID** called *mypool*.</span><span class="sxs-lookup"><span data-stu-id="20396-125">Enter a **Pool ID** called *mypool*.</span></span> 

3. <span data-ttu-id="20396-126">In **Operating System**, select the following settings (you can explore other options).</span><span class="sxs-lookup"><span data-stu-id="20396-126">In **Operating System**, select the following settings (you can explore other options).</span></span>
  
  |<span data-ttu-id="20396-127">Setting</span><span class="sxs-lookup"><span data-stu-id="20396-127">Setting</span></span>  |<span data-ttu-id="20396-128">Value</span><span class="sxs-lookup"><span data-stu-id="20396-128">Value</span></span>  |
  |---------|---------|
  |<span data-ttu-id="20396-129">**Image Type**</span><span class="sxs-lookup"><span data-stu-id="20396-129">**Image Type**</span></span>|<span data-ttu-id="20396-130">Marketplace (Linux/Windows)</span><span class="sxs-lookup"><span data-stu-id="20396-130">Marketplace (Linux/Windows)</span></span>|
  |<span data-ttu-id="20396-131">**Publisher**</span><span class="sxs-lookup"><span data-stu-id="20396-131">**Publisher**</span></span>     |<span data-ttu-id="20396-132">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="20396-132">MicrosoftWindowsServer</span></span>|
  |<span data-ttu-id="20396-133">**Offer**</span><span class="sxs-lookup"><span data-stu-id="20396-133">**Offer**</span></span>     |<span data-ttu-id="20396-134">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="20396-134">WindowsServer</span></span>|
  |<span data-ttu-id="20396-135">**Sku**</span><span class="sxs-lookup"><span data-stu-id="20396-135">**Sku**</span></span>     |<span data-ttu-id="20396-136">2012-R2-Datacenter-smalldisk</span><span class="sxs-lookup"><span data-stu-id="20396-136">2012-R2-Datacenter-smalldisk</span></span>|

  ![Select a pool operating system][pool_os] 

4. <span data-ttu-id="20396-138">Scroll down to enter **Node Size** and **Scale** settings.</span><span class="sxs-lookup"><span data-stu-id="20396-138">Scroll down to enter **Node Size** and **Scale** settings.</span></span> <span data-ttu-id="20396-139">The suggested node size offers a good balance of performance versus cost for this quick example.</span><span class="sxs-lookup"><span data-stu-id="20396-139">The suggested node size offers a good balance of performance versus cost for this quick example.</span></span>
  
  |<span data-ttu-id="20396-140">Setting</span><span class="sxs-lookup"><span data-stu-id="20396-140">Setting</span></span>  |<span data-ttu-id="20396-141">Value</span><span class="sxs-lookup"><span data-stu-id="20396-141">Value</span></span>  |
  |---------|---------|
  |<span data-ttu-id="20396-142">**Node pricing tier**</span><span class="sxs-lookup"><span data-stu-id="20396-142">**Node pricing tier**</span></span>     |<span data-ttu-id="20396-143">Standard_A1</span><span class="sxs-lookup"><span data-stu-id="20396-143">Standard_A1</span></span>|
  |<span data-ttu-id="20396-144">**Target dedicated nodes**</span><span class="sxs-lookup"><span data-stu-id="20396-144">**Target dedicated nodes**</span></span>     |<span data-ttu-id="20396-145">2</span><span class="sxs-lookup"><span data-stu-id="20396-145">2</span></span>|

  ![Select a pool size][pool_size] 

5. <span data-ttu-id="20396-147">Keep the defaults for remaining settings, and select **OK** to create the pool.</span><span class="sxs-lookup"><span data-stu-id="20396-147">Keep the defaults for remaining settings, and select **OK** to create the pool.</span></span>

<span data-ttu-id="20396-148">Batch creates the pool immediately, but it takes a few minutes to allocate and start the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="20396-148">Batch creates the pool immediately, but it takes a few minutes to allocate and start the compute nodes.</span></span> <span data-ttu-id="20396-149">During this time, the pool's **Allocation state** is **Resizing**.</span><span class="sxs-lookup"><span data-stu-id="20396-149">During this time, the pool's **Allocation state** is **Resizing**.</span></span> <span data-ttu-id="20396-150">You can go ahead and create a job and tasks while the pool is resizing.</span><span class="sxs-lookup"><span data-stu-id="20396-150">You can go ahead and create a job and tasks while the pool is resizing.</span></span> 

![Pool in Resizing state][pool_resizing]

<span data-ttu-id="20396-152">After a few minutes, the state of the pool is **Steady**, and the nodes start.</span><span class="sxs-lookup"><span data-stu-id="20396-152">After a few minutes, the state of the pool is **Steady**, and the nodes start.</span></span> <span data-ttu-id="20396-153">Select **Nodes** to check the state of the nodes.</span><span class="sxs-lookup"><span data-stu-id="20396-153">Select **Nodes** to check the state of the nodes.</span></span> <span data-ttu-id="20396-154">When a node's state is **Idle**, it is ready to run tasks.</span><span class="sxs-lookup"><span data-stu-id="20396-154">When a node's state is **Idle**, it is ready to run tasks.</span></span> 

## <a name="create-a-job"></a><span data-ttu-id="20396-155">Create a job</span><span class="sxs-lookup"><span data-stu-id="20396-155">Create a job</span></span>

<span data-ttu-id="20396-156">Now that you have a pool, create a job to run on it.</span><span class="sxs-lookup"><span data-stu-id="20396-156">Now that you have a pool, create a job to run on it.</span></span> <span data-ttu-id="20396-157">A Batch job is a logical group for one or more tasks.</span><span class="sxs-lookup"><span data-stu-id="20396-157">A Batch job is a logical group for one or more tasks.</span></span> <span data-ttu-id="20396-158">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span><span class="sxs-lookup"><span data-stu-id="20396-158">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span></span> <span data-ttu-id="20396-159">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="20396-159">Initially the job has no tasks.</span></span> 

1. <span data-ttu-id="20396-160">In the Batch account view, select **Jobs** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="20396-160">In the Batch account view, select **Jobs** > **Add**.</span></span> 

2. <span data-ttu-id="20396-161">Enter a **Job ID** called *myjob*.</span><span class="sxs-lookup"><span data-stu-id="20396-161">Enter a **Job ID** called *myjob*.</span></span> <span data-ttu-id="20396-162">In **Pool**, select *mypool*.</span><span class="sxs-lookup"><span data-stu-id="20396-162">In **Pool**, select *mypool*.</span></span> <span data-ttu-id="20396-163">Keep the defaults for the remaining settings, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="20396-163">Keep the defaults for the remaining settings, and select **OK**.</span></span>

  ![Create a job][job_create]

<span data-ttu-id="20396-165">After the job is created, the **Tasks** page opens.</span><span class="sxs-lookup"><span data-stu-id="20396-165">After the job is created, the **Tasks** page opens.</span></span>

## <a name="create-tasks"></a><span data-ttu-id="20396-166">Create tasks</span><span class="sxs-lookup"><span data-stu-id="20396-166">Create tasks</span></span>

<span data-ttu-id="20396-167">Now create sample tasks to run in the job.</span><span class="sxs-lookup"><span data-stu-id="20396-167">Now create sample tasks to run in the job.</span></span> <span data-ttu-id="20396-168">Typically you create multiple tasks that Batch queues and distributes to run on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="20396-168">Typically you create multiple tasks that Batch queues and distributes to run on the compute nodes.</span></span> <span data-ttu-id="20396-169">In this example, you create two identical tasks.</span><span class="sxs-lookup"><span data-stu-id="20396-169">In this example, you create two identical tasks.</span></span> <span data-ttu-id="20396-170">Each task runs a command line to display the Batch environment variables on a compute node, and then waits 90 seconds.</span><span class="sxs-lookup"><span data-stu-id="20396-170">Each task runs a command line to display the Batch environment variables on a compute node, and then waits 90 seconds.</span></span> 

<span data-ttu-id="20396-171">When you use Batch, the command line is where you specify your app or script.</span><span class="sxs-lookup"><span data-stu-id="20396-171">When you use Batch, the command line is where you specify your app or script.</span></span> <span data-ttu-id="20396-172">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="20396-172">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span></span> 

<span data-ttu-id="20396-173">To create the first task:</span><span class="sxs-lookup"><span data-stu-id="20396-173">To create the first task:</span></span>

1. <span data-ttu-id="20396-174">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="20396-174">Select **Add**.</span></span>

2. <span data-ttu-id="20396-175">Enter a **Task ID** called *mytask*.</span><span class="sxs-lookup"><span data-stu-id="20396-175">Enter a **Task ID** called *mytask*.</span></span> 

3. <span data-ttu-id="20396-176">In **Command line**, enter `cmd /c "set AZ_BATCH & timeout /t 90 > NUL"`.</span><span class="sxs-lookup"><span data-stu-id="20396-176">In **Command line**, enter `cmd /c "set AZ_BATCH & timeout /t 90 > NUL"`.</span></span> <span data-ttu-id="20396-177">Keep the defaults for the remaining settings, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="20396-177">Keep the defaults for the remaining settings, and select **OK**.</span></span>

  ![Create a task][task_create]

<span data-ttu-id="20396-179">After you create a task, Batch queues it to run on the pool.</span><span class="sxs-lookup"><span data-stu-id="20396-179">After you create a task, Batch queues it to run on the pool.</span></span> <span data-ttu-id="20396-180">When a node is available to run it, the task runs.</span><span class="sxs-lookup"><span data-stu-id="20396-180">When a node is available to run it, the task runs.</span></span>

<span data-ttu-id="20396-181">To create a second task, go back to step 1.</span><span class="sxs-lookup"><span data-stu-id="20396-181">To create a second task, go back to step 1.</span></span> <span data-ttu-id="20396-182">Enter a different **Task ID**, but specify an identical command line.</span><span class="sxs-lookup"><span data-stu-id="20396-182">Enter a different **Task ID**, but specify an identical command line.</span></span> <span data-ttu-id="20396-183">If the first task is still running, Batch starts the second task on the other node in the pool.</span><span class="sxs-lookup"><span data-stu-id="20396-183">If the first task is still running, Batch starts the second task on the other node in the pool.</span></span>

## <a name="view-task-output"></a><span data-ttu-id="20396-184">View task output</span><span class="sxs-lookup"><span data-stu-id="20396-184">View task output</span></span>

<span data-ttu-id="20396-185">The preceding task examples complete in a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="20396-185">The preceding task examples complete in a couple of minutes.</span></span> <span data-ttu-id="20396-186">To view the output of a completed task, select **Files on node**, and then select the file `stdout.txt`.</span><span class="sxs-lookup"><span data-stu-id="20396-186">To view the output of a completed task, select **Files on node**, and then select the file `stdout.txt`.</span></span> <span data-ttu-id="20396-187">This file shows the standard output of the task.</span><span class="sxs-lookup"><span data-stu-id="20396-187">This file shows the standard output of the task.</span></span> <span data-ttu-id="20396-188">The contents are similar to the following:</span><span class="sxs-lookup"><span data-stu-id="20396-188">The contents are similar to the following:</span></span>

![View task output][task_output]

<span data-ttu-id="20396-190">The contents show the Azure Batch environment variables that are set on the node.</span><span class="sxs-lookup"><span data-stu-id="20396-190">The contents show the Azure Batch environment variables that are set on the node.</span></span> <span data-ttu-id="20396-191">When you create your own Batch jobs and tasks, you can reference these environment variables in task command lines, and in the apps and scripts run by the command lines.</span><span class="sxs-lookup"><span data-stu-id="20396-191">When you create your own Batch jobs and tasks, you can reference these environment variables in task command lines, and in the apps and scripts run by the command lines.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="20396-192">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="20396-192">Clean up resources</span></span>

<span data-ttu-id="20396-193">If you want to continue with Batch tutorials and samples, use the Batch account and linked storage account created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="20396-193">If you want to continue with Batch tutorials and samples, use the Batch account and linked storage account created in this quickstart.</span></span> <span data-ttu-id="20396-194">There is no charge for the Batch account itself.</span><span class="sxs-lookup"><span data-stu-id="20396-194">There is no charge for the Batch account itself.</span></span>

<span data-ttu-id="20396-195">You are charged for the pool while the nodes are running, even if no jobs are scheduled.</span><span class="sxs-lookup"><span data-stu-id="20396-195">You are charged for the pool while the nodes are running, even if no jobs are scheduled.</span></span> <span data-ttu-id="20396-196">When you no longer need the pool, delete it.</span><span class="sxs-lookup"><span data-stu-id="20396-196">When you no longer need the pool, delete it.</span></span> <span data-ttu-id="20396-197">In the account view, select **Pools** and the name of the pool.</span><span class="sxs-lookup"><span data-stu-id="20396-197">In the account view, select **Pools** and the name of the pool.</span></span> <span data-ttu-id="20396-198">Then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="20396-198">Then select **Delete**.</span></span>  <span data-ttu-id="20396-199">When you delete the pool, all task output on the nodes is deleted.</span><span class="sxs-lookup"><span data-stu-id="20396-199">When you delete the pool, all task output on the nodes is deleted.</span></span> 

<span data-ttu-id="20396-200">When no longer needed, delete the resource group, Batch account, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="20396-200">When no longer needed, delete the resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="20396-201">To do so, select the resource group for the Batch account and select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="20396-201">To do so, select the resource group for the Batch account and select **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20396-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="20396-202">Next steps</span></span>

<span data-ttu-id="20396-203">In this quickstart, you created a Batch account, a Batch pool, and a Batch job.</span><span class="sxs-lookup"><span data-stu-id="20396-203">In this quickstart, you created a Batch account, a Batch pool, and a Batch job.</span></span> <span data-ttu-id="20396-204">The job ran sample tasks, and you viewed output created on one of the nodes.</span><span class="sxs-lookup"><span data-stu-id="20396-204">The job ran sample tasks, and you viewed output created on one of the nodes.</span></span> <span data-ttu-id="20396-205">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="20396-205">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span></span> <span data-ttu-id="20396-206">To learn more about Azure Batch, continue to the Azure Batch tutorials.</span><span class="sxs-lookup"><span data-stu-id="20396-206">To learn more about Azure Batch, continue to the Azure Batch tutorials.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="20396-207">Azure Batch tutorials</span><span class="sxs-lookup"><span data-stu-id="20396-207">Azure Batch tutorials</span></span>](./tutorial-parallel-dotnet.md)

[marketplace_portal]: ./media/quick-create-portal/marketplace-batch.png

[account_portal]: ./media/quick-create-portal/batch-account-portal.png

[account_keys]: ./media/quick-create-portal/batch-account-keys.png

[pool_os]: ./media/quick-create-portal/pool-operating-system.png

[pool_size]: ./media/quick-create-portal/pool-size.png

[pool_resizing]: ./media/quick-create-portal/pool-resizing.png

[job_create]: ./media/quick-create-portal/job-create.png

[task_create]: ./media/quick-create-portal/task-create.png

[task_output]: ./media/quick-create-portal/task-output.png