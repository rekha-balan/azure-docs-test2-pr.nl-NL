---
title: About Batch AI resources - Azure | Microsoft Docs
description: Overview of workspaces, clusters, file servers, experiments, and jobs in the Batch AI service in Microsoft Azure.
services: batch-ai
documentationcenter: na
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.custom: ''
ms.service: batch-ai
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2018
ms.author: danlep
ms.openlocfilehash: 4a9e3529f9d68ecdc614ea69cffc6897891f4548
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865720"
---
# <a name="overview-of-resources-in-batch-ai"></a><span data-ttu-id="be743-103">Overview of resources in Batch AI</span><span class="sxs-lookup"><span data-stu-id="be743-103">Overview of resources in Batch AI</span></span>

<span data-ttu-id="be743-104">When you first start using the Batch AI service, you'll want to understand the available Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="be743-104">When you first start using the Batch AI service, you'll want to understand the available Batch AI resources.</span></span> <span data-ttu-id="be743-105">As with other Azure services, you create Batch AI resources in one or more Azure *resource groups*.</span><span class="sxs-lookup"><span data-stu-id="be743-105">As with other Azure services, you create Batch AI resources in one or more Azure *resource groups*.</span></span> <span data-ttu-id="be743-106">Create one or more Batch AI *workspaces* in a resource group.</span><span class="sxs-lookup"><span data-stu-id="be743-106">Create one or more Batch AI *workspaces* in a resource group.</span></span> <span data-ttu-id="be743-107">Each workspace contains a mix of Batch AI *clusters*, *file servers*, and *experiments*.</span><span class="sxs-lookup"><span data-stu-id="be743-107">Each workspace contains a mix of Batch AI *clusters*, *file servers*, and *experiments*.</span></span> <span data-ttu-id="be743-108">A Batch AI experiment encapsulates a group of *jobs*.</span><span class="sxs-lookup"><span data-stu-id="be743-108">A Batch AI experiment encapsulates a group of *jobs*.</span></span>

<span data-ttu-id="be743-109">The following image shows an example resource hierarchy for Batch AI.</span><span class="sxs-lookup"><span data-stu-id="be743-109">The following image shows an example resource hierarchy for Batch AI.</span></span> 

![](./media/migrate-to-new-api/batch-ai-resource-hierarchy.png)

<span data-ttu-id="be743-110">The following sections go into more detail about the Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="be743-110">The following sections go into more detail about the Batch AI resources.</span></span>

## <a name="workspace"></a><span data-ttu-id="be743-111">Workspace</span><span class="sxs-lookup"><span data-stu-id="be743-111">Workspace</span></span>

<span data-ttu-id="be743-112">A workspace in Batch AI is a top-level collection of the rest of the Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="be743-112">A workspace in Batch AI is a top-level collection of the rest of the Batch AI resources.</span></span> <span data-ttu-id="be743-113">Workspaces help to separate work belonging to different groups or projects.</span><span class="sxs-lookup"><span data-stu-id="be743-113">Workspaces help to separate work belonging to different groups or projects.</span></span> <span data-ttu-id="be743-114">For example, you might create a development and a test workspace.</span><span class="sxs-lookup"><span data-stu-id="be743-114">For example, you might create a development and a test workspace.</span></span>

## <a name="cluster"></a><span data-ttu-id="be743-115">Cluster</span><span class="sxs-lookup"><span data-stu-id="be743-115">Cluster</span></span>

<span data-ttu-id="be743-116">A cluster in Batch AI contains the compute resources for running jobs.</span><span class="sxs-lookup"><span data-stu-id="be743-116">A cluster in Batch AI contains the compute resources for running jobs.</span></span> <span data-ttu-id="be743-117">All nodes in a cluster have same VM size and OS image.</span><span class="sxs-lookup"><span data-stu-id="be743-117">All nodes in a cluster have same VM size and OS image.</span></span> <span data-ttu-id="be743-118">Batch AI offers many options for creating clusters that are customized to different needs.</span><span class="sxs-lookup"><span data-stu-id="be743-118">Batch AI offers many options for creating clusters that are customized to different needs.</span></span> <span data-ttu-id="be743-119">Typically, you set up a different cluster for each category of processing power needed to complete a project.</span><span class="sxs-lookup"><span data-stu-id="be743-119">Typically, you set up a different cluster for each category of processing power needed to complete a project.</span></span> <span data-ttu-id="be743-120">Scale the Batch AI clusters up and down based on demand and budget.</span><span class="sxs-lookup"><span data-stu-id="be743-120">Scale the Batch AI clusters up and down based on demand and budget.</span></span> <span data-ttu-id="be743-121">For more information, see [Work with Batch AI clusters](clusters.md).</span><span class="sxs-lookup"><span data-stu-id="be743-121">For more information, see [Work with Batch AI clusters](clusters.md).</span></span>

## <a name="file-server"></a><span data-ttu-id="be743-122">File server</span><span class="sxs-lookup"><span data-stu-id="be743-122">File server</span></span>

<span data-ttu-id="be743-123">Optionally create a file server in Batch AI to store data, training scripts, and output logs.</span><span class="sxs-lookup"><span data-stu-id="be743-123">Optionally create a file server in Batch AI to store data, training scripts, and output logs.</span></span> <span data-ttu-id="be743-124">A Batch AI file server is a managed single-node NFS, which can be automatically mounted on cluster nodes to provide an easy and centrally accessible storage location for jobs.</span><span class="sxs-lookup"><span data-stu-id="be743-124">A Batch AI file server is a managed single-node NFS, which can be automatically mounted on cluster nodes to provide an easy and centrally accessible storage location for jobs.</span></span> <span data-ttu-id="be743-125">For most cases, only one file server is needed in a workspace, and you can separate data for your training jobs into different directories.</span><span class="sxs-lookup"><span data-stu-id="be743-125">For most cases, only one file server is needed in a workspace, and you can separate data for your training jobs into different directories.</span></span> <span data-ttu-id="be743-126">If NFS isn't appropriate for your workloads, Batch AI supports other storage options including [Azure Storage](use-azure-storage.md) or custom solutions such as a Gluster or Lustre file system.</span><span class="sxs-lookup"><span data-stu-id="be743-126">If NFS isn't appropriate for your workloads, Batch AI supports other storage options including [Azure Storage](use-azure-storage.md) or custom solutions such as a Gluster or Lustre file system.</span></span>

## <a name="experiment"></a><span data-ttu-id="be743-127">Experiment</span><span class="sxs-lookup"><span data-stu-id="be743-127">Experiment</span></span>

<span data-ttu-id="be743-128">An experiment groups a collection of related jobs that you query and manage together.</span><span class="sxs-lookup"><span data-stu-id="be743-128">An experiment groups a collection of related jobs that you query and manage together.</span></span> <span data-ttu-id="be743-129">Each workspace might have multiple experiments, where each experiment attempts to solve one specific problem.</span><span class="sxs-lookup"><span data-stu-id="be743-129">Each workspace might have multiple experiments, where each experiment attempts to solve one specific problem.</span></span>

## <a name="job"></a><span data-ttu-id="be743-130">Job</span><span class="sxs-lookup"><span data-stu-id="be743-130">Job</span></span>

<span data-ttu-id="be743-131">A job is a single task or script that needs to be executed, for example to train a deep learning model.</span><span class="sxs-lookup"><span data-stu-id="be743-131">A job is a single task or script that needs to be executed, for example to train a deep learning model.</span></span> <span data-ttu-id="be743-132">Each job executes a specific script on one cluster in the workspace.</span><span class="sxs-lookup"><span data-stu-id="be743-132">Each job executes a specific script on one cluster in the workspace.</span></span> <span data-ttu-id="be743-133">(The script might be stored on a Batch AI file server or other storage solution.) Each Batch AI job has a framework type associated with it: TensorFlow, Horovod, CNTK, Caffe, Caffe2, pyTorch, Chainer, custom MPI, or custom.</span><span class="sxs-lookup"><span data-stu-id="be743-133">(The script might be stored on a Batch AI file server or other storage solution.) Each Batch AI job has a framework type associated with it: TensorFlow, Horovod, CNTK, Caffe, Caffe2, pyTorch, Chainer, custom MPI, or custom.</span></span> <span data-ttu-id="be743-134">For each framework, the Batch AI service sets up the required infrastructure and manages the job processes.</span><span class="sxs-lookup"><span data-stu-id="be743-134">For each framework, the Batch AI service sets up the required infrastructure and manages the job processes.</span></span> <span data-ttu-id="be743-135">Each experiment can have multiple jobs that are similar, apart from a few changes to different parameters.</span><span class="sxs-lookup"><span data-stu-id="be743-135">Each experiment can have multiple jobs that are similar, apart from a few changes to different parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be743-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="be743-136">Next steps</span></span>

* <span data-ttu-id="be743-137">Run your first [Batch AI training job](quickstart-tensorflow-training-cli.md).</span><span class="sxs-lookup"><span data-stu-id="be743-137">Run your first [Batch AI training job](quickstart-tensorflow-training-cli.md).</span></span>

* <span data-ttu-id="be743-138">Check out sample [training recipes](https://github.com/Azure/BatchAI/tree/master/recipes) for different frameworks.</span><span class="sxs-lookup"><span data-stu-id="be743-138">Check out sample [training recipes](https://github.com/Azure/BatchAI/tree/master/recipes) for different frameworks.</span></span>