---
title: Run tasks under user accounts in Azure Batch | Microsoft Docs
description: Configure user accounts for running tasks in Azure Batch
services: batch
author: tamram
manager: timlt
editor: ''
tags: ''
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/18/2017
ms.author: tamram
ms.openlocfilehash: 8c18a6898aa25bbc04040cf2b5c3d05ce0af035e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662486"
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="9d5d8-103">Run tasks under user accounts in Batch</span><span class="sxs-lookup"><span data-stu-id="9d5d8-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="9d5d8-104">A task in Azure Batch always runs under a user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="9d5d8-105">By default, tasks run under standard user accounts, without administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="9d5d8-106">These default user account settings are typically sufficient.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="9d5d8-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="9d5d8-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="9d5d8-109">Types of user accounts</span><span class="sxs-lookup"><span data-stu-id="9d5d8-109">Types of user accounts</span></span>

<span data-ttu-id="9d5d8-110">Azure Batch provides two types of user accounts for running tasks:</span><span class="sxs-lookup"><span data-stu-id="9d5d8-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="9d5d8-111">**Auto-user accounts.**</span><span class="sxs-lookup"><span data-stu-id="9d5d8-111">**Auto-user accounts.**</span></span> <span data-ttu-id="9d5d8-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="9d5d8-113">By default, tasks run under an auto-user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="9d5d8-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="9d5d8-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="9d5d8-116">**A named user account.**</span><span class="sxs-lookup"><span data-stu-id="9d5d8-116">**A named user account.**</span></span> <span data-ttu-id="9d5d8-117">You can specify one or more named user accounts for a pool when you create the pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="9d5d8-118">Each user account is created on each node of the pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="9d5d8-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="9d5d8-120">When you add a task, you can specify the named user account under which that task should run.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="9d5d8-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="9d5d8-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="9d5d8-123">Use the new **userIdentity** property of a task to specify elevation level.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="9d5d8-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="9d5d8-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="9d5d8-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="9d5d8-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="9d5d8-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="9d5d8-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="9d5d8-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d5d8-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="9d5d8-129">User account access to files and directories</span><span class="sxs-lookup"><span data-stu-id="9d5d8-129">User account access to files and directories</span></span>

<span data-ttu-id="9d5d8-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="9d5d8-131">Both types of accounts have read access to the startup and job preparation directories.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="9d5d8-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="9d5d8-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="9d5d8-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="9d5d8-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="9d5d8-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="9d5d8-136">Elevated access for tasks</span><span class="sxs-lookup"><span data-stu-id="9d5d8-136">Elevated access for tasks</span></span> 

<span data-ttu-id="9d5d8-137">The user account's elevation level indicates whether a task runs with elevated access.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="9d5d8-138">Both an auto-user account and a named user account can run with elevated access.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="9d5d8-139">The two options for elevation level are:</span><span class="sxs-lookup"><span data-stu-id="9d5d8-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="9d5d8-140">**NonAdmin:** The task runs as a standard user without elevated access.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="9d5d8-141">The default elevation level for a Batch user account is always **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="9d5d8-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="9d5d8-143">Auto-user accounts</span><span class="sxs-lookup"><span data-stu-id="9d5d8-143">Auto-user accounts</span></span>

<span data-ttu-id="9d5d8-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="9d5d8-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="9d5d8-146">The alternative to task scope is pool scope.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="9d5d8-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="9d5d8-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="9d5d8-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="9d5d8-149">The default scope is different on Windows and Linux nodes:</span><span class="sxs-lookup"><span data-stu-id="9d5d8-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="9d5d8-150">On Windows nodes, tasks run under task scope by default.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="9d5d8-151">Linux nodes always run under pool scope.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="9d5d8-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span><span class="sxs-lookup"><span data-stu-id="9d5d8-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="9d5d8-153">Non-admin access with task scope (the default auto-user specification)</span><span class="sxs-lookup"><span data-stu-id="9d5d8-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="9d5d8-154">Admin (elevated) access with task scope</span><span class="sxs-lookup"><span data-stu-id="9d5d8-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="9d5d8-155">Non-admin access with pool scope</span><span class="sxs-lookup"><span data-stu-id="9d5d8-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="9d5d8-156">Admin access with pool scope</span><span class="sxs-lookup"><span data-stu-id="9d5d8-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="9d5d8-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="9d5d8-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="9d5d8-159">A malicious user could also use RDP or SSH to connect to a node.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="9d5d8-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="9d5d8-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="9d5d8-162">Run a task as an auto-user with elevated access</span><span class="sxs-lookup"><span data-stu-id="9d5d8-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="9d5d8-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="9d5d8-164">For example, a start task may need elevated access to install software on the node.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="9d5d8-165">In general, it's best to use elevated access only when necessary.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="9d5d8-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="9d5d8-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="9d5d8-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="9d5d8-169">The following code snippets show how to configure the auto-user specification.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="9d5d8-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="9d5d8-171">Task scope is the default setting, but is included here for the sake of example.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="9d5d8-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="9d5d8-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="9d5d8-173">Batch Java</span><span class="sxs-lookup"><span data-stu-id="9d5d8-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="9d5d8-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="9d5d8-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="9d5d8-175">Run a task as an auto-user with pool scope</span><span class="sxs-lookup"><span data-stu-id="9d5d8-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="9d5d8-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="9d5d8-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="9d5d8-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="9d5d8-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="9d5d8-180">The two pool-wide auto-user accounts are separate accounts.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="9d5d8-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="9d5d8-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="9d5d8-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="9d5d8-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="9d5d8-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="9d5d8-186">Instead, you can protect the secret at the user level.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="9d5d8-187">Tasks running under the same user account can access the secret without elevated access.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="9d5d8-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="9d5d8-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="9d5d8-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="9d5d8-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="9d5d8-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="9d5d8-193">Named user accounts</span><span class="sxs-lookup"><span data-stu-id="9d5d8-193">Named user accounts</span></span>

<span data-ttu-id="9d5d8-194">You can define named user accounts when you create a pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="9d5d8-195">A named user account has a name and password that you provide.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="9d5d8-196">You can specify the elevation level for a named user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="9d5d8-197">For Linux nodes, you can also provide an SSH private key.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="9d5d8-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="9d5d8-199">You may define any number of named users for a pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="9d5d8-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="9d5d8-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="9d5d8-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="9d5d8-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="9d5d8-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="9d5d8-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="9d5d8-206">Named user accounts enable password-less SSH between Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="9d5d8-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="9d5d8-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="9d5d8-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="9d5d8-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="9d5d8-210">Create named user accounts</span><span class="sxs-lookup"><span data-stu-id="9d5d8-210">Create named user accounts</span></span>

<span data-ttu-id="9d5d8-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="9d5d8-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="9d5d8-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="9d5d8-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example"></a><span data-ttu-id="9d5d8-215">Batch .NET example</span><span class="sxs-lookup"><span data-stu-id="9d5d8-215">Batch .NET example</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicated: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(AdminUserAccountName, AdminPassword, ElevationLevel.Admin),
    new UserAccount(NonAdminUserAccountName, NonAdminPassword, ElevationLevel.NonAdmin),
};
 
pool.Commit();
```

#### <a name="batch-java-example"></a><span data-ttu-id="9d5d8-216">Batch Java example</span><span class="sxs-lookup"><span data-stu-id="9d5d8-216">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="9d5d8-217">Batch Python example</span><span class="sxs-lookup"><span data-stu-id="9d5d8-217">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="9d5d8-218">Run a task under a named user account with elevated access</span><span class="sxs-lookup"><span data-stu-id="9d5d8-218">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="9d5d8-219">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-219">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="9d5d8-220">This code snippet specifies that the task should run under a named user account.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-220">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="9d5d8-221">This named user account was defined on the pool when the pool was created.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-221">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="9d5d8-222">In this case, the named user account was created with admin permissions:</span><span class="sxs-lookup"><span data-stu-id="9d5d8-222">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="9d5d8-223">Update your code to the latest Batch client library</span><span class="sxs-lookup"><span data-stu-id="9d5d8-223">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="9d5d8-224">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-224">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="9d5d8-225">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-225">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="9d5d8-226">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="9d5d8-226">Batch .NET</span></span>

| <span data-ttu-id="9d5d8-227">If your code uses...</span><span class="sxs-lookup"><span data-stu-id="9d5d8-227">If your code uses...</span></span>                  | <span data-ttu-id="9d5d8-228">Update it to....</span><span class="sxs-lookup"><span data-stu-id="9d5d8-228">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="9d5d8-229">`CloudTask.RunElevated` not specified</span><span class="sxs-lookup"><span data-stu-id="9d5d8-229">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="9d5d8-230">No update required</span><span class="sxs-lookup"><span data-stu-id="9d5d8-230">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="9d5d8-231">Batch Java</span><span class="sxs-lookup"><span data-stu-id="9d5d8-231">Batch Java</span></span>

| <span data-ttu-id="9d5d8-232">If your code uses...</span><span class="sxs-lookup"><span data-stu-id="9d5d8-232">If your code uses...</span></span>                      | <span data-ttu-id="9d5d8-233">Update it to....</span><span class="sxs-lookup"><span data-stu-id="9d5d8-233">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="9d5d8-234">`CloudTask.withRunElevated` not specified</span><span class="sxs-lookup"><span data-stu-id="9d5d8-234">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="9d5d8-235">No update required</span><span class="sxs-lookup"><span data-stu-id="9d5d8-235">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="9d5d8-236">Batch Python</span><span class="sxs-lookup"><span data-stu-id="9d5d8-236">Batch Python</span></span>

| <span data-ttu-id="9d5d8-237">If your code uses...</span><span class="sxs-lookup"><span data-stu-id="9d5d8-237">If your code uses...</span></span>                      | <span data-ttu-id="9d5d8-238">Update it to....</span><span class="sxs-lookup"><span data-stu-id="9d5d8-238">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="9d5d8-239">`user_identity=user`, where</span><span class="sxs-lookup"><span data-stu-id="9d5d8-239">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="9d5d8-240">`user_identity=user`, where</span><span class="sxs-lookup"><span data-stu-id="9d5d8-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="9d5d8-241">`run_elevated` not specified</span><span class="sxs-lookup"><span data-stu-id="9d5d8-241">`run_elevated` not specified</span></span> | <span data-ttu-id="9d5d8-242">No update required</span><span class="sxs-lookup"><span data-stu-id="9d5d8-242">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="9d5d8-243">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d5d8-243">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="9d5d8-244">Batch Forum</span><span class="sxs-lookup"><span data-stu-id="9d5d8-244">Batch Forum</span></span>

<span data-ttu-id="9d5d8-245">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-245">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="9d5d8-246">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="9d5d8-246">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>