---
title: What is an FPGA? – Project Brainwave – Azure Machine Learning
description: Learn how to accelerate models and deep neural networks with FPGAs.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: tedway
author: tedway
ms.date: 05/31/2018
ms.openlocfilehash: 0d960df0d12f9c31e32ee95666ea9bb61f609bde
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857725"
---
# <a name="what-is-fpga-and-project-brainwave"></a><span data-ttu-id="327be-104">What is FPGA and Project Brainwave?</span><span class="sxs-lookup"><span data-stu-id="327be-104">What is FPGA and Project Brainwave?</span></span>

<span data-ttu-id="327be-105">This article provides an introduction to field-programmable gate arrays (FPGA) and how FPGA is integrated with Azure machine learning to provide real-time AI.</span><span class="sxs-lookup"><span data-stu-id="327be-105">This article provides an introduction to field-programmable gate arrays (FPGA) and how FPGA is integrated with Azure machine learning to provide real-time AI.</span></span>

## <a name="fpgas-vs-cpu-gpu-and-asic"></a><span data-ttu-id="327be-106">FPGAs vs. CPU, GPU, and ASIC</span><span class="sxs-lookup"><span data-stu-id="327be-106">FPGAs vs. CPU, GPU, and ASIC</span></span>

<span data-ttu-id="327be-107">FPGAs contain an array of programmable logic blocks, and a hierarchy of reconfigurable interconnects that allow the blocks to be configured in different ways after manufacturing.</span><span class="sxs-lookup"><span data-stu-id="327be-107">FPGAs contain an array of programmable logic blocks, and a hierarchy of reconfigurable interconnects that allow the blocks to be configured in different ways after manufacturing.</span></span>

<span data-ttu-id="327be-108">FPGAs provide a combination of programmability and performance comparing to other chips:</span><span class="sxs-lookup"><span data-stu-id="327be-108">FPGAs provide a combination of programmability and performance comparing to other chips:</span></span>

![Azure Machine Learning FPGA comparison](./media/concept-accelerate-with-fpgas/azure-machine-learning-fpga-comparison.png)

- <span data-ttu-id="327be-110">**Central processing units (CPU)** are general-purpose processors.</span><span class="sxs-lookup"><span data-stu-id="327be-110">**Central processing units (CPU)** are general-purpose processors.</span></span> <span data-ttu-id="327be-111">CPU performance is not ideal for graphics and video processing.</span><span class="sxs-lookup"><span data-stu-id="327be-111">CPU performance is not ideal for graphics and video processing.</span></span>
- <span data-ttu-id="327be-112">**Graphics processing units (GPU)** offer parallel processing and are a popular choice for AI computations.</span><span class="sxs-lookup"><span data-stu-id="327be-112">**Graphics processing units (GPU)** offer parallel processing and are a popular choice for AI computations.</span></span> <span data-ttu-id="327be-113">The parallel processing with GPUs result in faster image rendering than CPUs.</span><span class="sxs-lookup"><span data-stu-id="327be-113">The parallel processing with GPUs result in faster image rendering than CPUs.</span></span>
- <span data-ttu-id="327be-114">**Application-specific integrated circuits (ASIC)**, such as Google’s TensorFlow Processor Units, are customized circuits.</span><span class="sxs-lookup"><span data-stu-id="327be-114">**Application-specific integrated circuits (ASIC)**, such as Google’s TensorFlow Processor Units, are customized circuits.</span></span> <span data-ttu-id="327be-115">While these chips provide the highest efficiency, ASICs are inflexible.</span><span class="sxs-lookup"><span data-stu-id="327be-115">While these chips provide the highest efficiency, ASICs are inflexible.</span></span>
- <span data-ttu-id="327be-116">**FPGAs**, such as those available on Azure, provide the performance close to ASIC, but offer the flexibility to be reconfigured later.</span><span class="sxs-lookup"><span data-stu-id="327be-116">**FPGAs**, such as those available on Azure, provide the performance close to ASIC, but offer the flexibility to be reconfigured later.</span></span>

<span data-ttu-id="327be-117">FPGAs are now in every new Azure server.</span><span class="sxs-lookup"><span data-stu-id="327be-117">FPGAs are now in every new Azure server.</span></span> <span data-ttu-id="327be-118">Microsoft is already using FPGAs for Bing search ranking, deep neural network (DNN) evaluation, and software defined networking (SDN) acceleration.</span><span class="sxs-lookup"><span data-stu-id="327be-118">Microsoft is already using FPGAs for Bing search ranking, deep neural network (DNN) evaluation, and software defined networking (SDN) acceleration.</span></span> <span data-ttu-id="327be-119">These FPGA implementations reduce latency while freeing CPUs for other tasks.</span><span class="sxs-lookup"><span data-stu-id="327be-119">These FPGA implementations reduce latency while freeing CPUs for other tasks.</span></span>

## <a name="project-brainwave-on-azure"></a><span data-ttu-id="327be-120">Project Brainwave on Azure</span><span class="sxs-lookup"><span data-stu-id="327be-120">Project Brainwave on Azure</span></span>

<span data-ttu-id="327be-121">Project Brainwave is a hardware architecture that is designed based on Intel's FPGA devices and used to accelerate real-time AI calculations.</span><span class="sxs-lookup"><span data-stu-id="327be-121">Project Brainwave is a hardware architecture that is designed based on Intel's FPGA devices and used to accelerate real-time AI calculations.</span></span> <span data-ttu-id="327be-122">With this economical FPGA-enabled architecture, a trained neural network can be run as quickly as possible and with lower latency.</span><span class="sxs-lookup"><span data-stu-id="327be-122">With this economical FPGA-enabled architecture, a trained neural network can be run as quickly as possible and with lower latency.</span></span> <span data-ttu-id="327be-123">Project Brainwave can parallelize pre-trained DNNs across FPGAs to scale out your service.</span><span class="sxs-lookup"><span data-stu-id="327be-123">Project Brainwave can parallelize pre-trained DNNs across FPGAs to scale out your service.</span></span>

- <span data-ttu-id="327be-124">Performance</span><span class="sxs-lookup"><span data-stu-id="327be-124">Performance</span></span>

    <span data-ttu-id="327be-125">FPGAs make it possible to achieve low latency for real-time inferencing requests.</span><span class="sxs-lookup"><span data-stu-id="327be-125">FPGAs make it possible to achieve low latency for real-time inferencing requests.</span></span> <span data-ttu-id="327be-126">Batching means breaking up a request into smaller pieces and feeding them to a processor to improve hardware utilization.</span><span class="sxs-lookup"><span data-stu-id="327be-126">Batching means breaking up a request into smaller pieces and feeding them to a processor to improve hardware utilization.</span></span> <span data-ttu-id="327be-127">Batching is not efficient and can cause latency.</span><span class="sxs-lookup"><span data-stu-id="327be-127">Batching is not efficient and can cause latency.</span></span> <span data-ttu-id="327be-128">Brainwave doesn't require batching; therefore the latency is 10 times lower compared to CPU and GPU.</span><span class="sxs-lookup"><span data-stu-id="327be-128">Brainwave doesn't require batching; therefore the latency is 10 times lower compared to CPU and GPU.</span></span>

- <span data-ttu-id="327be-129">Flexibility</span><span class="sxs-lookup"><span data-stu-id="327be-129">Flexibility</span></span>

    <span data-ttu-id="327be-130">FPGAs can be reconfigured for different types of machine learning models.</span><span class="sxs-lookup"><span data-stu-id="327be-130">FPGAs can be reconfigured for different types of machine learning models.</span></span> <span data-ttu-id="327be-131">This flexibility makes it easier to accelerate the applications based on the most optimal numerical precision and memory model being used.</span><span class="sxs-lookup"><span data-stu-id="327be-131">This flexibility makes it easier to accelerate the applications based on the most optimal numerical precision and memory model being used.</span></span>

    <span data-ttu-id="327be-132">New machine learning techniques are being developed on a regular basis, and Project Brainwave's hardware design is also evolving rapidly.</span><span class="sxs-lookup"><span data-stu-id="327be-132">New machine learning techniques are being developed on a regular basis, and Project Brainwave's hardware design is also evolving rapidly.</span></span> <span data-ttu-id="327be-133">Since FPGAs are reconfigurable, it is possible to stay current with the requirements of the rapidly changing AI algorithms.</span><span class="sxs-lookup"><span data-stu-id="327be-133">Since FPGAs are reconfigurable, it is possible to stay current with the requirements of the rapidly changing AI algorithms.</span></span>

- <span data-ttu-id="327be-134">Scale</span><span class="sxs-lookup"><span data-stu-id="327be-134">Scale</span></span>

    <span data-ttu-id="327be-135">Microsoft Azure is the world's largest cloud investment in FPGAs.</span><span class="sxs-lookup"><span data-stu-id="327be-135">Microsoft Azure is the world's largest cloud investment in FPGAs.</span></span> <span data-ttu-id="327be-136">You can run Brainwave on Azure's scale infrastructure.</span><span class="sxs-lookup"><span data-stu-id="327be-136">You can run Brainwave on Azure's scale infrastructure.</span></span>

<span data-ttu-id="327be-137">A preview of Project Brainwave integrated with Azure Machine Learning is currently available.</span><span class="sxs-lookup"><span data-stu-id="327be-137">A preview of Project Brainwave integrated with Azure Machine Learning is currently available.</span></span> <span data-ttu-id="327be-138">And a limited preview is also available to bring Project Brainwave to the edge so that you can take advantage of that computing speed in your own businesses and facilities.</span><span class="sxs-lookup"><span data-stu-id="327be-138">And a limited preview is also available to bring Project Brainwave to the edge so that you can take advantage of that computing speed in your own businesses and facilities.</span></span>

<span data-ttu-id="327be-139">In current preview, Brainwave is limited to the TensorFlow deployment and the ResNet50-based neural networks on Intel FPGA hardware for image classification and recognition.</span><span class="sxs-lookup"><span data-stu-id="327be-139">In current preview, Brainwave is limited to the TensorFlow deployment and the ResNet50-based neural networks on Intel FPGA hardware for image classification and recognition.</span></span> <span data-ttu-id="327be-140">There are plans to support more gallery models and other frameworks.</span><span class="sxs-lookup"><span data-stu-id="327be-140">There are plans to support more gallery models and other frameworks.</span></span>

<span data-ttu-id="327be-141">The following scenarios use FPGA on Project Brainwave architecture:</span><span class="sxs-lookup"><span data-stu-id="327be-141">The following scenarios use FPGA on Project Brainwave architecture:</span></span>

- <span data-ttu-id="327be-142">Automated optical inspection system.</span><span class="sxs-lookup"><span data-stu-id="327be-142">Automated optical inspection system.</span></span> <span data-ttu-id="327be-143">See [Real-time AI: Microsoft announces preview of Project Brainwave](https://blogs.microsoft.com/ai/build-2018-project-brainwave/).</span><span class="sxs-lookup"><span data-stu-id="327be-143">See [Real-time AI: Microsoft announces preview of Project Brainwave](https://blogs.microsoft.com/ai/build-2018-project-brainwave/).</span></span>
- <span data-ttu-id="327be-144">Land cover mapping.</span><span class="sxs-lookup"><span data-stu-id="327be-144">Land cover mapping.</span></span> <span data-ttu-id="327be-145">See [How to Use FPGAs for Deep Learning Inference to Perform Land Cover Mapping on Terabytes of Aerial Images](https://blogs.technet.microsoft.com/machinelearning/2018/05/29/how-to-use-fpgas-for-deep-learning-inference-to-perform-land-cover-mapping-on-terabytes-of-aerial-images/).</span><span class="sxs-lookup"><span data-stu-id="327be-145">See [How to Use FPGAs for Deep Learning Inference to Perform Land Cover Mapping on Terabytes of Aerial Images](https://blogs.technet.microsoft.com/machinelearning/2018/05/29/how-to-use-fpgas-for-deep-learning-inference-to-perform-land-cover-mapping-on-terabytes-of-aerial-images/).</span></span>

## <a name="how-to-deploy-a-web-service-to-an-fpga"></a><span data-ttu-id="327be-146">How to deploy a web service to an FPGA?</span><span class="sxs-lookup"><span data-stu-id="327be-146">How to deploy a web service to an FPGA?</span></span>

<span data-ttu-id="327be-147">The high-level flow for creating an image recognition service in Azure using ResNet50 as a featurizer is as follows:</span><span class="sxs-lookup"><span data-stu-id="327be-147">The high-level flow for creating an image recognition service in Azure using ResNet50 as a featurizer is as follows:</span></span>

1. <span data-ttu-id="327be-148">ResNet50 is already deployed in Brainwave.</span><span class="sxs-lookup"><span data-stu-id="327be-148">ResNet50 is already deployed in Brainwave.</span></span> <span data-ttu-id="327be-149">You can build other graphs (date input, classification, and so on) with TensorFlow, and define a pipeline (input -> featurize -> classify) using a service definition json file.</span><span class="sxs-lookup"><span data-stu-id="327be-149">You can build other graphs (date input, classification, and so on) with TensorFlow, and define a pipeline (input -> featurize -> classify) using a service definition json file.</span></span> <span data-ttu-id="327be-150">Compress the definition and graphs into a zip file, and upload the zip file to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="327be-150">Compress the definition and graphs into a zip file, and upload the zip file to Azure Blob storage.</span></span>
2. <span data-ttu-id="327be-151">Register the model using Azure ML Model Management API with the zip file in the Blob storage.</span><span class="sxs-lookup"><span data-stu-id="327be-151">Register the model using Azure ML Model Management API with the zip file in the Blob storage.</span></span>
3. <span data-ttu-id="327be-152">Deploy the service with the registered model using Azure ML Model Management API.</span><span class="sxs-lookup"><span data-stu-id="327be-152">Deploy the service with the registered model using Azure ML Model Management API.</span></span>

<span data-ttu-id="327be-153">Learn more about this process in the article, [Deploy a model as a web service on an FPGA with Azure Machine Learning](how-to-deploy-fpga-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="327be-153">Learn more about this process in the article, [Deploy a model as a web service on an FPGA with Azure Machine Learning](how-to-deploy-fpga-web-service.md).</span></span>


## <a name="start-using-fpga"></a><span data-ttu-id="327be-154">Start using FPGA</span><span class="sxs-lookup"><span data-stu-id="327be-154">Start using FPGA</span></span>

<span data-ttu-id="327be-155">Azure Machine Learning Hardware Accelerated Models allow you to deploy trained DNN models to FPGAs in the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="327be-155">Azure Machine Learning Hardware Accelerated Models allow you to deploy trained DNN models to FPGAs in the Azure cloud.</span></span> <span data-ttu-id="327be-156">To get started, see:</span><span class="sxs-lookup"><span data-stu-id="327be-156">To get started, see:</span></span>

- [<span data-ttu-id="327be-157">Deploy a model as a web service on an FPGA</span><span class="sxs-lookup"><span data-stu-id="327be-157">Deploy a model as a web service on an FPGA</span></span>](how-to-deploy-fpga-web-service.md)
- <span data-ttu-id="327be-158">[Microsoft Azure Machine Learning Hardware Accelerated Models Powered by Project Brainwave](https://github.com/azure/aml-real-time-ai).</span><span class="sxs-lookup"><span data-stu-id="327be-158">[Microsoft Azure Machine Learning Hardware Accelerated Models Powered by Project Brainwave](https://github.com/azure/aml-real-time-ai).</span></span>

## <a name="next-steps"></a><span data-ttu-id="327be-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="327be-159">Next steps</span></span>

[<span data-ttu-id="327be-160">Deploy a model as a web service on an FPGA</span><span class="sxs-lookup"><span data-stu-id="327be-160">Deploy a model as a web service on an FPGA</span></span>](how-to-deploy-fpga-web-service.md)

[<span data-ttu-id="327be-161">Learn how to install the FPGA SDK</span><span class="sxs-lookup"><span data-stu-id="327be-161">Learn how to install the FPGA SDK</span></span>](reference-fpga-package-overview.md)

[<span data-ttu-id="327be-162">Hyperscale hardware: ML at scale on top of Azure + FPGA : Build 2018 (video)</span><span class="sxs-lookup"><span data-stu-id="327be-162">Hyperscale hardware: ML at scale on top of Azure + FPGA : Build 2018 (video)</span></span>](https://www.youtube.com/watch?v=BMgQAHIx2eY)

[<span data-ttu-id="327be-163">Inside the Microsoft FPGA-based configurable cloud (video)</span><span class="sxs-lookup"><span data-stu-id="327be-163">Inside the Microsoft FPGA-based configurable cloud (video)</span></span>](https://channel9.msdn.com/Events/Build/2017/B8063)

[<span data-ttu-id="327be-164">Microsoft unveils Project Brainwave for real-time AI</span><span class="sxs-lookup"><span data-stu-id="327be-164">Microsoft unveils Project Brainwave for real-time AI</span></span>](https://www.microsoft.com/research/blog/microsoft-unveils-project-brainwave/)