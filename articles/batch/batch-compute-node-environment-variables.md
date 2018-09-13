---
title: Azure Batch compute node environment variables | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3990f0c8-b627-432f-9551-5ce10f9bb0ca
caps.latest.revision: 14
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: e31f2a5e5186ea27d7da7d0d5d5837a2cda41a11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670921"
---
# <a name="azure-batch-compute-node-environment-variables"></a>Azure Batch compute node environment variables
The [Azure Batch service](https://azure.microsoft.com/services/batch/) sets the following environment variables on compute nodes. You can reference these environment variables in task command lines, and in the programs and scripts run by the command lines.

For additional information about using environment variables with Batch, see [Environment settings for tasks](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Environment variable visibility

These environment variables are visible only in the context of the **task user**, the user account on the node under which a task is executed. You will *not* see these if you [connect remotely](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) to a compute node via Remote Desktop Protocol (RDP) or Secure Shell (SSH) and list the environment variables. This is because the user account that is used for remote connection is not the same as the account that is used by the task.

## <a name="command-line-expansion-of-environment-variables"></a>Command-line expansion of environment variables

The command lines executed by tasks on compute nodes do not run under a shell. Therefore, these command lines cannot natively take advantage of shell features such as environment variable expansion (this includes the `PATH`). To take advantage of such features, you must **invoke the shell** in the command line. For example, by launching `cmd.exe` on Windows compute nodes or `/bin/sh` on Linux nodes:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Environment variables

| Variable name         | Description                                                              | Availability | Example |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| `AZ_BATCH_ACCOUNT_NAME`           | The name of the Batch account that the task belongs to. | All tasks. | `mybatchaccount` |
| `AZ_BATCH_CERTIFICATES_DIR`       | A directory within the [task working directory][files_dirs] in which certificates are stored for Linux compute nodes. Note that this environment variable does not apply to Windows compute nodes. | All tasks. | `/mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs` |
| `AZ_BATCH_JOB_ID`                 | The ID of the job that the task belongs to. | All tasks except start task. | `batchjob001` |
| `AZ_BATCH_JOB_PREP_DIR`           | The full path of the job preparation [task directory][files_dirs] on the node. | All tasks except start task and job preparation task. Only available if the job is configured with a job preparation task. | `C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation` |
| `AZ_BATCH_JOB_PREP_WORKING_DIR`   | The full path of the job preparation [task working directory][files_dirs] on the node. | All tasks except start task and job preparation task. Only available if the job is configured with a job preparation task. | `C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd` |
| `AZ_BATCH_NODE_ID`                | The ID of the node that the task is assigned to. | All tasks. | `tvm-1219235766_3-20160919t172711z` |
| `AZ_BATCH_NODE_ROOT_DIR`          | The full path of the root of all [Batch directories][files_dirs] on the node. | All tasks. | `C:\user\tasks` |
| `AZ_BATCH_NODE_SHARED_DIR`        | The full path of the [shared directory][files_dirs] on the node. All tasks that execute on a node have read/write access to this directory. Tasks that execute on other nodes do not have remote access to this directory (it is not a "shared" network directory). | All tasks. | `C:\user\tasks\shared` |
| `AZ_BATCH_NODE_STARTUP_DIR`       | The full path of the [start task directory][files_dirs] on the node. | All tasks. | `C:\user\tasks\startup` |
| `AZ_BATCH_POOL_ID`                | The ID of the pool that the task is running on. | All tasks. | `batchpool001` |
| `AZ_BATCH_TASK_DIR`               | The full path of the [task directory][files_dirs] on the node. This directory contains the `stdout.txt` and `stderr.txt` for the task, and the `AZ_BATCH_TASK_WORKING_DIR`. | All tasks. | `C:\user\tasks\workitems\batchjob001\job-1\task001` |
| `AZ_BATCH_TASK_ID`                | The ID of the current task. | All tasks except start task. | `task001` |
| `AZ_BATCH_TASK_WORKING_DIR`       | The full path of the [task working directory][files_dirs] on the node. The currently running task has read/write access to this directory. | All tasks. | `C:\user\tasks\workitems\batchjob001\job-1\task001\wd` |
| `CCP_NODES`                       | The list of nodes and number of cores per node that are allocated to a [multi-instance task][multi_instance]. Nodes and cores are listed in the format `numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, where the number of nodes is followed by one or more node IP addresses and the number of cores for each. |  Multi-instance primary and subtasks. |`2 10.0.0.4 1 10.0.0.5 1` |
| `AZ_BATCH_NODE_LIST`              | The list of nodes that are allocated to a [multi-instance task][multi_instance] in the format `nodeIP;nodeIP`. | Multi-instance primary and subtasks. | `10.0.0.4;10.0.0.5` |
| `AZ_BATCH_HOST_LIST`              | The list of nodes that are allocated to a [multi-instance task][multi_instance] in the format `nodeIP,nodeIP`. | Multi-instance primary and subtasks. | `10.0.0.4,10.0.0.5` |
| `AZ_BATCH_MASTER_NODE`            | The IP address and port of the compute node on which the primary task of a [multi-instance task][multi_instance] runs. | Multi-instance primary and subtasks. | `10.0.0.4:6000`|
| `AZ_BATCH_TASK_SHARED_DIR` | A directory path that is identical for the primary task and every subtask of a [multi-instance task][multi_instance]. The path exists on every node on which the multi-instance task runs, and is read/write accessible to the task commands running on that node (both the [coordination command][coord_cmd] and the [application command][app_cmd]). Subtasks or a primary task that execute on other nodes do not have remote access to this directory (it is not a “shared” network directory). | Multi-instance primary and subtasks. | `C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask` |
| `AZ_BATCH_IS_CURRENT_NODE_MASTER` | Specifies whether the current node is the master node for a [multi-instance task][multi_instance]. Possible values are `true` and `false`.| Multi-instance primary and subtasks. | `true` |


[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command