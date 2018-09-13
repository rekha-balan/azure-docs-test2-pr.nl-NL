---
title: How to Use GPU for Azure Machine Learning | Microsoft Docs
description: This article describes how to use Graphical Processing Units (GPU) to train deep neural networks in Azure Machine Learning Workbench.
services: machine-learning
author: rastala
ms.author: roastala
manager: jhubbard
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/14/2017
ms.openlocfilehash: 09d8e3da543cdf4433d986b321697abcad88eb22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871278"
---
# <a name="how-to-use-gpu-in-azure-machine-learning"></a><span data-ttu-id="81850-103">How to use GPU in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81850-103">How to use GPU in Azure Machine Learning</span></span>
<span data-ttu-id="81850-104">Graphical Processing Unit (GPU) is widely used to process computationally intensive tasks that can typically happen when training certain deep neural network models.</span><span class="sxs-lookup"><span data-stu-id="81850-104">Graphical Processing Unit (GPU) is widely used to process computationally intensive tasks that can typically happen when training certain deep neural network models.</span></span> <span data-ttu-id="81850-105">By using GPUs, you can reduce the training time of the models significantly.</span><span class="sxs-lookup"><span data-stu-id="81850-105">By using GPUs, you can reduce the training time of the models significantly.</span></span> <span data-ttu-id="81850-106">In this document, you learn how to configure Azure ML Workbench to use  [DSVM (Data Science Virtual Machine)](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview) equipped with GPUs as execution target.</span><span class="sxs-lookup"><span data-stu-id="81850-106">In this document, you learn how to configure Azure ML Workbench to use  [DSVM (Data Science Virtual Machine)](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview) equipped with GPUs as execution target.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="81850-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="81850-107">Prerequisites</span></span>
- <span data-ttu-id="81850-108">To step through this how-to guide, you need to first [install Azure ML Workbench](../service/quickstart-installation.md).</span><span class="sxs-lookup"><span data-stu-id="81850-108">To step through this how-to guide, you need to first [install Azure ML Workbench](../service/quickstart-installation.md).</span></span>
- <span data-ttu-id="81850-109">You need to have access to computers equipped with NVidia GPUs.</span><span class="sxs-lookup"><span data-stu-id="81850-109">You need to have access to computers equipped with NVidia GPUs.</span></span>
    - <span data-ttu-id="81850-110">You can run your scripts directly on local machine (Windows or macOS) with GPUs.</span><span class="sxs-lookup"><span data-stu-id="81850-110">You can run your scripts directly on local machine (Windows or macOS) with GPUs.</span></span>
    - <span data-ttu-id="81850-111">You can also run scripts in a Docker container on a Linux machine with GPUs..</span><span class="sxs-lookup"><span data-stu-id="81850-111">You can also run scripts in a Docker container on a Linux machine with GPUs..</span></span>

## <a name="execute-in-local-environment-with-gpus"></a><span data-ttu-id="81850-112">Execute in _local_ Environment with GPUs</span><span class="sxs-lookup"><span data-stu-id="81850-112">Execute in _local_ Environment with GPUs</span></span>
<span data-ttu-id="81850-113">You can install Azure ML Workbench on a computer equipped with GPUs and execute against _local_ environment.</span><span class="sxs-lookup"><span data-stu-id="81850-113">You can install Azure ML Workbench on a computer equipped with GPUs and execute against _local_ environment.</span></span> <span data-ttu-id="81850-114">This can be:</span><span class="sxs-lookup"><span data-stu-id="81850-114">This can be:</span></span>
- <span data-ttu-id="81850-115">A physical Windows or macOS machine.</span><span class="sxs-lookup"><span data-stu-id="81850-115">A physical Windows or macOS machine.</span></span>
- <span data-ttu-id="81850-116">A Windows VM (Virtual Machine) such as a Windows DSVM provisioned using Azure NC-series VMs template.</span><span class="sxs-lookup"><span data-stu-id="81850-116">A Windows VM (Virtual Machine) such as a Windows DSVM provisioned using Azure NC-series VMs template.</span></span>

<span data-ttu-id="81850-117">In this case, there are no special configuration required in Azure ML Workbench.</span><span class="sxs-lookup"><span data-stu-id="81850-117">In this case, there are no special configuration required in Azure ML Workbench.</span></span> <span data-ttu-id="81850-118">Just make sure you have all the necessary drivers, toolkits, and GPU-enabled machine learning libraries installed locally.</span><span class="sxs-lookup"><span data-stu-id="81850-118">Just make sure you have all the necessary drivers, toolkits, and GPU-enabled machine learning libraries installed locally.</span></span> <span data-ttu-id="81850-119">Simply execute against _local_ environment where the Python runtime can directly access the local GPU hardware.</span><span class="sxs-lookup"><span data-stu-id="81850-119">Simply execute against _local_ environment where the Python runtime can directly access the local GPU hardware.</span></span>

1. <span data-ttu-id="81850-120">Open AML Workbench.</span><span class="sxs-lookup"><span data-stu-id="81850-120">Open AML Workbench.</span></span> <span data-ttu-id="81850-121">go to **File** and **Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="81850-121">go to **File** and **Open Command Prompt**.</span></span> 
2. <span data-ttu-id="81850-122">From command line, install GPU-enabled deep learning framework such as the Microsoft Cognitive Toolkit, TensorFlow, and etc. For example:</span><span class="sxs-lookup"><span data-stu-id="81850-122">From command line, install GPU-enabled deep learning framework such as the Microsoft Cognitive Toolkit, TensorFlow, and etc. For example:</span></span>

```batch
REM install latest TensorFlow with GPU support
C:\MyProj> pip install tensorflow-gpu

REM install Microsoft Cognitive Toolkit 2.5 with GPU support on Windows
C:\MyProj> pip install https://cntk.ai/PythonWheel/GPU/cntk_gpu-2.5.1-cp35-cp35m-win_amd64.whl
```

3. <span data-ttu-id="81850-123">Write Python code that leverages the deep learning libraries.</span><span class="sxs-lookup"><span data-stu-id="81850-123">Write Python code that leverages the deep learning libraries.</span></span>
4. <span data-ttu-id="81850-124">Choose _local_ as compute environment and execute the Python code.</span><span class="sxs-lookup"><span data-stu-id="81850-124">Choose _local_ as compute environment and execute the Python code.</span></span>

```batch
REM execute Python script in local environment
C:\MyProj> az ml experiment submit -c local my-deep-learning-script.py
```

## <a name="execute-in-docker-environment-on-linux-vm-with-gpus"></a><span data-ttu-id="81850-125">Execute in _docker_ Environment on Linux VM with GPUs</span><span class="sxs-lookup"><span data-stu-id="81850-125">Execute in _docker_ Environment on Linux VM with GPUs</span></span>
<span data-ttu-id="81850-126">Azure ML Workbench also support execution in Docker in an Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="81850-126">Azure ML Workbench also support execution in Docker in an Azure Linux VM.</span></span> <span data-ttu-id="81850-127">Here you have a great option to run computationally intensive jobs on a piece of powerful virtual hardware, and pay only for the usage by turning it off when done.</span><span class="sxs-lookup"><span data-stu-id="81850-127">Here you have a great option to run computationally intensive jobs on a piece of powerful virtual hardware, and pay only for the usage by turning it off when done.</span></span> <span data-ttu-id="81850-128">While in principle it is possible to use GPUs on any Linux virtual machine, the Ubuntu-based DSVM comes with the required CUDA drivers and libraries pre-installed, making the set-up much easier.</span><span class="sxs-lookup"><span data-stu-id="81850-128">While in principle it is possible to use GPUs on any Linux virtual machine, the Ubuntu-based DSVM comes with the required CUDA drivers and libraries pre-installed, making the set-up much easier.</span></span> <span data-ttu-id="81850-129">Follow the below steps:</span><span class="sxs-lookup"><span data-stu-id="81850-129">Follow the below steps:</span></span>

### <a name="create-a-ubuntu-based-linux-data-science-virtual-machine-in-azure"></a><span data-ttu-id="81850-130">Create a Ubuntu-based Linux Data Science Virtual Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="81850-130">Create a Ubuntu-based Linux Data Science Virtual Machine in Azure</span></span>
1. <span data-ttu-id="81850-131">Open your web browser and go to the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="81850-131">Open your web browser and go to the [Azure portal](https://portal.azure.com)</span></span>

2. <span data-ttu-id="81850-132">Select **+ New** on the left of the portal.</span><span class="sxs-lookup"><span data-stu-id="81850-132">Select **+ New** on the left of the portal.</span></span>

3. <span data-ttu-id="81850-133">Search for "Data Science Virtual Machine for Linux (Ubuntu)" in the marketplace.</span><span class="sxs-lookup"><span data-stu-id="81850-133">Search for "Data Science Virtual Machine for Linux (Ubuntu)" in the marketplace.</span></span>

4. <span data-ttu-id="81850-134">Click **Create** to create an Ubuntu DSVM.</span><span class="sxs-lookup"><span data-stu-id="81850-134">Click **Create** to create an Ubuntu DSVM.</span></span>

5. <span data-ttu-id="81850-135">Fill in the **Basics** form with the required information.</span><span class="sxs-lookup"><span data-stu-id="81850-135">Fill in the **Basics** form with the required information.</span></span>
<span data-ttu-id="81850-136">When selecting the location for your VM, note that GPU VMs are only available in certain Azure regions, for example, **South Central US**.</span><span class="sxs-lookup"><span data-stu-id="81850-136">When selecting the location for your VM, note that GPU VMs are only available in certain Azure regions, for example, **South Central US**.</span></span> <span data-ttu-id="81850-137">See [compute products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="81850-137">See [compute products available by region](https://azure.microsoft.com/regions/services/).</span></span>
<span data-ttu-id="81850-138">Click OK to save the **Basics** information.</span><span class="sxs-lookup"><span data-stu-id="81850-138">Click OK to save the **Basics** information.</span></span>

6. <span data-ttu-id="81850-139">Choose the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="81850-139">Choose the size of the virtual machine.</span></span> <span data-ttu-id="81850-140">Select one of the sizes with NC-prefixed VMs, which are equipped with NVidia GPU chips.</span><span class="sxs-lookup"><span data-stu-id="81850-140">Select one of the sizes with NC-prefixed VMs, which are equipped with NVidia GPU chips.</span></span>  <span data-ttu-id="81850-141">Click **View All** to see the full list as needed.</span><span class="sxs-lookup"><span data-stu-id="81850-141">Click **View All** to see the full list as needed.</span></span> <span data-ttu-id="81850-142">Learn more about [GPU-equipped Azure VMs](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).</span><span class="sxs-lookup"><span data-stu-id="81850-142">Learn more about [GPU-equipped Azure VMs](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).</span></span>

7. <span data-ttu-id="81850-143">Finish the remaining settings and review the purchase information.</span><span class="sxs-lookup"><span data-stu-id="81850-143">Finish the remaining settings and review the purchase information.</span></span> <span data-ttu-id="81850-144">Click Purchase to Create the VM.</span><span class="sxs-lookup"><span data-stu-id="81850-144">Click Purchase to Create the VM.</span></span> <span data-ttu-id="81850-145">Take note of the IP address allocated to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="81850-145">Take note of the IP address allocated to the virtual machine.</span></span> 

### <a name="create-a-new-project-in-azure-ml-workbench"></a><span data-ttu-id="81850-146">Create a New Project in Azure ML Workbench</span><span class="sxs-lookup"><span data-stu-id="81850-146">Create a New Project in Azure ML Workbench</span></span> 
<span data-ttu-id="81850-147">You can use the _Classifying MNIST using TensorFlow_ example, or the _Classifying MNIST dataset with CNTK_ example.</span><span class="sxs-lookup"><span data-stu-id="81850-147">You can use the _Classifying MNIST using TensorFlow_ example, or the _Classifying MNIST dataset with CNTK_ example.</span></span>

### <a name="create-a-new-compute-target"></a><span data-ttu-id="81850-148">Create a new Compute Target</span><span class="sxs-lookup"><span data-stu-id="81850-148">Create a new Compute Target</span></span>
<span data-ttu-id="81850-149">Launch the command line from Azure ML Workbench.</span><span class="sxs-lookup"><span data-stu-id="81850-149">Launch the command line from Azure ML Workbench.</span></span> <span data-ttu-id="81850-150">Enter the following command.</span><span class="sxs-lookup"><span data-stu-id="81850-150">Enter the following command.</span></span> <span data-ttu-id="81850-151">Replace the placeholder text from the example below with your own values for the name, IP address, username, and password.</span><span class="sxs-lookup"><span data-stu-id="81850-151">Replace the placeholder text from the example below with your own values for the name, IP address, username, and password.</span></span> 

```batch
C:\MyProj> az ml computetarget attach remotedocker --name "my_dsvm" --address "my_dsvm_ip_address" --username "my_name" --password "my_password" 
```

### <a name="configure-azure-ml-workbench-to-access-gpu"></a><span data-ttu-id="81850-152">Configure Azure ML Workbench to Access GPU</span><span class="sxs-lookup"><span data-stu-id="81850-152">Configure Azure ML Workbench to Access GPU</span></span>
<span data-ttu-id="81850-153">Go back to the project and open **File View**, and hit the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="81850-153">Go back to the project and open **File View**, and hit the **Refresh** button.</span></span> <span data-ttu-id="81850-154">Now you see two new configuration files `my_dsvm.compute` and `my_dsvm.runconfig`.</span><span class="sxs-lookup"><span data-stu-id="81850-154">Now you see two new configuration files `my_dsvm.compute` and `my_dsvm.runconfig`.</span></span>
 
<span data-ttu-id="81850-155">Open the `my_dsvm.compute`.</span><span class="sxs-lookup"><span data-stu-id="81850-155">Open the `my_dsvm.compute`.</span></span> <span data-ttu-id="81850-156">Change the `baseDockerImage` to `microsoft/mmlspark:plus-gpu-0.9.9` and add a new line `nvidiaDocker: true`.</span><span class="sxs-lookup"><span data-stu-id="81850-156">Change the `baseDockerImage` to `microsoft/mmlspark:plus-gpu-0.9.9` and add a new line `nvidiaDocker: true`.</span></span> <span data-ttu-id="81850-157">So the file should have these two lines:</span><span class="sxs-lookup"><span data-stu-id="81850-157">So the file should have these two lines:</span></span>
 
```yaml
...
baseDockerImage: microsoft/mmlspark:plus-gpu-0.9.9
nvidiaDocker: true
```
 
<span data-ttu-id="81850-158">Now open `my_dsvm.runconfig`, change `Framework` value from `PySpark` to `Python`.</span><span class="sxs-lookup"><span data-stu-id="81850-158">Now open `my_dsvm.runconfig`, change `Framework` value from `PySpark` to `Python`.</span></span> <span data-ttu-id="81850-159">If you don't see this line, add it, since the default value would be `PySpark`.</span><span class="sxs-lookup"><span data-stu-id="81850-159">If you don't see this line, add it, since the default value would be `PySpark`.</span></span>

```yaml
"Framework": "Python"
```
### <a name="reference-deep-learning-framework"></a><span data-ttu-id="81850-160">Reference Deep Learning Framework</span><span class="sxs-lookup"><span data-stu-id="81850-160">Reference Deep Learning Framework</span></span> 
<span data-ttu-id="81850-161">Open `conda_dependencies.yml` file, and make sure you are using the GPU version of the deep learning framework Python packages.</span><span class="sxs-lookup"><span data-stu-id="81850-161">Open `conda_dependencies.yml` file, and make sure you are using the GPU version of the deep learning framework Python packages.</span></span> <span data-ttu-id="81850-162">The sample projects list CPU versions so you need to make this change.</span><span class="sxs-lookup"><span data-stu-id="81850-162">The sample projects list CPU versions so you need to make this change.</span></span>

<span data-ttu-id="81850-163">Example for TensorFlow:</span><span class="sxs-lookup"><span data-stu-id="81850-163">Example for TensorFlow:</span></span> 
```
name: project_environment
dependencies:
  - python=3.5.2
  # latest TensorFlow library with GPU support
  - tensorflow-gpu
```

<span data-ttu-id="81850-164">Example for Microsoft Cognitive Toolkit:</span><span class="sxs-lookup"><span data-stu-id="81850-164">Example for Microsoft Cognitive Toolkit:</span></span>
```yaml
name: project_environment
dependencies:
  - python=3.5.2
  - pip: 
    # use the Linux build of Microsoft Cognitive Toolkit 2.5 with GPU support
    - https://cntk.ai/PythonWheel/GPU/cntk_gpu-2.5.1-cp35-cp35m-win_amd64.whl
```

### <a name="execute"></a><span data-ttu-id="81850-165">Execute</span><span class="sxs-lookup"><span data-stu-id="81850-165">Execute</span></span>
<span data-ttu-id="81850-166">You are now ready to run your Python scripts.</span><span class="sxs-lookup"><span data-stu-id="81850-166">You are now ready to run your Python scripts.</span></span> <span data-ttu-id="81850-167">You can run them within the Azure ML Workbench using the `my_dsvm` context, or you can launch it from the command line:</span><span class="sxs-lookup"><span data-stu-id="81850-167">You can run them within the Azure ML Workbench using the `my_dsvm` context, or you can launch it from the command line:</span></span>
 
```batch
C:\myProj> az ml experiment submit -c my_dsvm my_tensorflow_or_cntk_script.py
```
 
<span data-ttu-id="81850-168">To verify that the GPU is used, examine the run output to see something like the following:</span><span class="sxs-lookup"><span data-stu-id="81850-168">To verify that the GPU is used, examine the run output to see something like the following:</span></span>

```
name: Tesla K80
major: 3 minor: 7 memoryClockRate (GHz) 0.8235
pciBusID 06c3:00:00.0
Total memory: 11.17GiB
Free memory: 11.11GiB
```

<span data-ttu-id="81850-169">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="81850-169">Congratulations!</span></span> <span data-ttu-id="81850-170">Your script just harnessed the power of GPU through a Docker container!</span><span class="sxs-lookup"><span data-stu-id="81850-170">Your script just harnessed the power of GPU through a Docker container!</span></span>

## <a name="next-steps"></a><span data-ttu-id="81850-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="81850-171">Next steps</span></span>
<span data-ttu-id="81850-172">See an example of using GPU to accelerate deep neural network training at Azure ML Gallery.</span><span class="sxs-lookup"><span data-stu-id="81850-172">See an example of using GPU to accelerate deep neural network training at Azure ML Gallery.</span></span>
