---
title: Azure Batch AI service - AI training | Microsoft Docs
description: Learn about using the managed Azure Batch AI service to train artificial intelligence (AI) and other machine learning models on clusters of GPUs and CPUs.
services: batch-ai
documentationcenter: ''
author: alexsuttonms
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch-ai
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 08/01/2018
ms.author: danlep
ms.openlocfilehash: 98497812e75d07fc153e0e351331c05484164fdd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870035"
---
# <a name="what-is-azure-batch-ai"></a><span data-ttu-id="8c1c3-103">What is Azure Batch AI?</span><span class="sxs-lookup"><span data-stu-id="8c1c3-103">What is Azure Batch AI?</span></span>

<span data-ttu-id="8c1c3-104">Azure Batch AI is a managed service to help data scientists and AI researchers train and test machine learning and AI models at scale in Azure - without having to manage complex infrastructure.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-104">Azure Batch AI is a managed service to help data scientists and AI researchers train and test machine learning and AI models at scale in Azure - without having to manage complex infrastructure.</span></span> <span data-ttu-id="8c1c3-105">Describe the compute resources, the jobs you want to run, where to store the model inputs and the outputs, and Batch AI takes care of the rest.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-105">Describe the compute resources, the jobs you want to run, where to store the model inputs and the outputs, and Batch AI takes care of the rest.</span></span>

<span data-ttu-id="8c1c3-106">You can use Batch AI either standalone or to perform model training as part of a larger development workflow:</span><span class="sxs-lookup"><span data-stu-id="8c1c3-106">You can use Batch AI either standalone or to perform model training as part of a larger development workflow:</span></span>

* <span data-ttu-id="8c1c3-107">Use Batch AI by itself to train, test, and batch score machine learning and AI models on clusters of [GPUs](../virtual-machines/linux/sizes-gpu.md) or CPUs.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-107">Use Batch AI by itself to train, test, and batch score machine learning and AI models on clusters of [GPUs](../virtual-machines/linux/sizes-gpu.md) or CPUs.</span></span> 

* <span data-ttu-id="8c1c3-108">Target a Batch AI cluster in a workflow with [Azure Machine Learning](../machine-learning/service/overview-what-is-azure-ml.md) or other [Azure AI Platform tools](https://azure.microsoft.com/overview/ai-platform/).</span><span class="sxs-lookup"><span data-stu-id="8c1c3-108">Target a Batch AI cluster in a workflow with [Azure Machine Learning](../machine-learning/service/overview-what-is-azure-ml.md) or other [Azure AI Platform tools](https://azure.microsoft.com/overview/ai-platform/).</span></span> <span data-ttu-id="8c1c3-109">Azure ML provides a rich experience for data preparation, experimentation, and job history.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-109">Azure ML provides a rich experience for data preparation, experimentation, and job history.</span></span> <span data-ttu-id="8c1c3-110">Azure ML can also package a trained model into a container, and deploy a model for inference or to IoT devices.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-110">Azure ML can also package a trained model into a container, and deploy a model for inference or to IoT devices.</span></span>  

## <a name="train-machine-learning-and-ai-models"></a><span data-ttu-id="8c1c3-111">Train machine learning and AI models</span><span class="sxs-lookup"><span data-stu-id="8c1c3-111">Train machine learning and AI models</span></span>

<span data-ttu-id="8c1c3-112">Use Batch AI to train machine learning models as well as deep neural networks (deep learning) and other AI approaches.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-112">Use Batch AI to train machine learning models as well as deep neural networks (deep learning) and other AI approaches.</span></span> <span data-ttu-id="8c1c3-113">Batch AI has built-in support for popular open-source AI libraries and frameworks including [TensorFlow](https://github.com/tensorflow/tensorflow), [PyTorch](https://github.com/pytorch/pytorch), [Chainer](https://github.com/chainer/chainer), and [Microsoft Cognitive Toolkit (CNTK)](https://github.com/Microsoft/CNTK).</span><span class="sxs-lookup"><span data-stu-id="8c1c3-113">Batch AI has built-in support for popular open-source AI libraries and frameworks including [TensorFlow](https://github.com/tensorflow/tensorflow), [PyTorch](https://github.com/pytorch/pytorch), [Chainer](https://github.com/chainer/chainer), and [Microsoft Cognitive Toolkit (CNTK)](https://github.com/Microsoft/CNTK).</span></span>

<span data-ttu-id="8c1c3-114">After you've identified your problem area and prepared your data, work interactively with Batch AI to test model ideas.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-114">After you've identified your problem area and prepared your data, work interactively with Batch AI to test model ideas.</span></span> <span data-ttu-id="8c1c3-115">Then when you’re ready to experiment at scale, start jobs across multiple GPUs with MPI or other communication libraries, and run more experiments in parallel.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-115">Then when you’re ready to experiment at scale, start jobs across multiple GPUs with MPI or other communication libraries, and run more experiments in parallel.</span></span>

<span data-ttu-id="8c1c3-116">Batch AI helps you train models at scale in several ways.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-116">Batch AI helps you train models at scale in several ways.</span></span> <span data-ttu-id="8c1c3-117">For example:</span><span class="sxs-lookup"><span data-stu-id="8c1c3-117">For example:</span></span> 

|  |  |
|---------|---------|
| <span data-ttu-id="8c1c3-118">**Distribute training**</span><span class="sxs-lookup"><span data-stu-id="8c1c3-118">**Distribute training**</span></span><br/><span data-ttu-id="8c1c3-119">![Distributed training](./media/overview/distributed-training.png)</span><span class="sxs-lookup"><span data-stu-id="8c1c3-119">![Distributed training](./media/overview/distributed-training.png)</span></span>  | <span data-ttu-id="8c1c3-120">Scale up training for a single job across many network-connected GPUs, to train larger networks with high volumes of data.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-120">Scale up training for a single job across many network-connected GPUs, to train larger networks with high volumes of data.</span></span>|
| <span data-ttu-id="8c1c3-121">**Experiment**</span><span class="sxs-lookup"><span data-stu-id="8c1c3-121">**Experiment**</span></span><br/><span data-ttu-id="8c1c3-122">![Experimentation](./media/overview/experimentation.png)</span><span class="sxs-lookup"><span data-stu-id="8c1c3-122">![Experimentation](./media/overview/experimentation.png)</span></span> | <span data-ttu-id="8c1c3-123">Scale out training with multiple jobs.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-123">Scale out training with multiple jobs.</span></span> <span data-ttu-id="8c1c3-124">Run parameter sweeps to test out new ideas, or tune hyperparameters to optimize accuracy and performance.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-124">Run parameter sweeps to test out new ideas, or tune hyperparameters to optimize accuracy and performance.</span></span> |
| <span data-ttu-id="8c1c3-125">**Execute in parallel**![Parallel execution](./media/overview/parallel-execution.png)</span><span class="sxs-lookup"><span data-stu-id="8c1c3-125">**Execute in parallel**![Parallel execution](./media/overview/parallel-execution.png)</span></span> | <span data-ttu-id="8c1c3-126">Train or score many models at a time, running in parallel across a fleet of servers to get the jobs done faster.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-126">Train or score many models at a time, running in parallel across a fleet of servers to get the jobs done faster.</span></span>|

<span data-ttu-id="8c1c3-127">When you've trained a model, use Batch AI to test the model if this wasn’t part of your training script, or perform batch scoring.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-127">When you've trained a model, use Batch AI to test the model if this wasn’t part of your training script, or perform batch scoring.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="8c1c3-128">How it works</span><span class="sxs-lookup"><span data-stu-id="8c1c3-128">How it works</span></span>

<span data-ttu-id="8c1c3-129">Use Batch AI SDKs, command-line scripts, or the Azure portal to manage compute resources and schedule jobs for AI training and testing:</span><span class="sxs-lookup"><span data-stu-id="8c1c3-129">Use Batch AI SDKs, command-line scripts, or the Azure portal to manage compute resources and schedule jobs for AI training and testing:</span></span> 

* <span data-ttu-id="8c1c3-130">**Provision and scale clusters of VMs** - Choose the number of nodes (VMs), and select a GPU-enabled or other VM size that meets your training needs.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-130">**Provision and scale clusters of VMs** - Choose the number of nodes (VMs), and select a GPU-enabled or other VM size that meets your training needs.</span></span> <span data-ttu-id="8c1c3-131">Scale the number of nodes up or down automatically or manually so that you only use resources when needed.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-131">Scale the number of nodes up or down automatically or manually so that you only use resources when needed.</span></span> 

* <span data-ttu-id="8c1c3-132">**Manage dependencies and containers** - By default, Batch AI clusters run Linux VM images that have dependencies pre-installed to run container-based training frameworks either on GPUs or CPUs.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-132">**Manage dependencies and containers** - By default, Batch AI clusters run Linux VM images that have dependencies pre-installed to run container-based training frameworks either on GPUs or CPUs.</span></span> <span data-ttu-id="8c1c3-133">For additional configuration, bring custom images or run start-up scripts.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-133">For additional configuration, bring custom images or run start-up scripts.</span></span>

* <span data-ttu-id="8c1c3-134">**Distribute data** - Choose one or several storage options to manage input data and scripts and job output: Azure Files, Azure Blob storage, or a managed NFS server.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-134">**Distribute data** - Choose one or several storage options to manage input data and scripts and job output: Azure Files, Azure Blob storage, or a managed NFS server.</span></span> <span data-ttu-id="8c1c3-135">Batch AI also supports custom storage solutions including high-performance parallel file systems.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-135">Batch AI also supports custom storage solutions including high-performance parallel file systems.</span></span> <span data-ttu-id="8c1c3-136">Mount storage file systems to the cluster nodes and job containers using simple configuration files.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-136">Mount storage file systems to the cluster nodes and job containers using simple configuration files.</span></span>

* <span data-ttu-id="8c1c3-137">**Schedule jobs** - Submit jobs to a priority-based job queue to share cluster resources and take advantage of low-priority VMs and reserved instances.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-137">**Schedule jobs** - Submit jobs to a priority-based job queue to share cluster resources and take advantage of low-priority VMs and reserved instances.</span></span>

* <span data-ttu-id="8c1c3-138">**Handle failures** - Monitor job status and restart jobs in case of VM failures during potentially long-running jobs.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-138">**Handle failures** - Monitor job status and restart jobs in case of VM failures during potentially long-running jobs.</span></span>

* <span data-ttu-id="8c1c3-139">**Gather results** - Easily access output logs, Stdout, Stderr, and trained models.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-139">**Gather results** - Easily access output logs, Stdout, Stderr, and trained models.</span></span> <span data-ttu-id="8c1c3-140">Configure your Batch AI jobs to push output directly to mounted storage.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-140">Configure your Batch AI jobs to push output directly to mounted storage.</span></span>

<span data-ttu-id="8c1c3-141">As an Azure service, Batch AI supports common tools such as role-based access control (RBAC) and Azure virtual networks for security.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-141">As an Azure service, Batch AI supports common tools such as role-based access control (RBAC) and Azure virtual networks for security.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="8c1c3-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c1c3-142">Next steps</span></span>

* <span data-ttu-id="8c1c3-143">Learn more about the [Batch AI resources](resource-concepts.md) for training a machine learning or AI model.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-143">Learn more about the [Batch AI resources](resource-concepts.md) for training a machine learning or AI model.</span></span>

* <span data-ttu-id="8c1c3-144">Get started [training a sample deep learning model](quickstart-tensorflow-training-cli.md) with Batch AI.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-144">Get started [training a sample deep learning model](quickstart-tensorflow-training-cli.md) with Batch AI.</span></span>

* <span data-ttu-id="8c1c3-145">Check out sample [training recipes](https://github.com/Azure/BatchAI/blob/master/recipes) for popular AI frameworks.</span><span class="sxs-lookup"><span data-stu-id="8c1c3-145">Check out sample [training recipes](https://github.com/Azure/BatchAI/blob/master/recipes) for popular AI frameworks.</span></span>
