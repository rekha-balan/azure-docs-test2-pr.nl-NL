---
title: How to use Jupyter Notebooks in Azure Machine Learning Workbench | Microsoft Docs
description: A guide for using the Jupyter Notebook feature of Azure Machine Learning Workbench
services: machine-learning
author: rastala
ms.author: roastala
manager: haining
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 11/09/2017
ms.openlocfilehash: 712cdaa65487620b2f8af4a0ad57c01c24b9a965
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870442"
---
# <a name="use-jupyter-notebooks-in-azure-machine-learning-workbench"></a><span data-ttu-id="cf7f0-103">Use Jupyter Notebooks in Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="cf7f0-103">Use Jupyter Notebooks in Azure Machine Learning Workbench</span></span>

<span data-ttu-id="cf7f0-104">Azure Machine Learning Workbench supports interactive data science experimentation through its integration with Jupyter Notebooks.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-104">Azure Machine Learning Workbench supports interactive data science experimentation through its integration with Jupyter Notebooks.</span></span> <span data-ttu-id="cf7f0-105">This article describes how to make effective use of this feature to increase the rate and quality of your interactive data science experimentation.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-105">This article describes how to make effective use of this feature to increase the rate and quality of your interactive data science experimentation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf7f0-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cf7f0-106">Prerequisites</span></span>
- <span data-ttu-id="cf7f0-107">[Create Azure Machine Learning accounts and install Azure Machine Learning Workbench](../service/quickstart-installation.md).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-107">[Create Azure Machine Learning accounts and install Azure Machine Learning Workbench](../service/quickstart-installation.md).</span></span>
- <span data-ttu-id="cf7f0-108">Be familiar with the [Jupyter Notebook](http://jupyter.org/).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-108">Be familiar with the [Jupyter Notebook](http://jupyter.org/).</span></span> <span data-ttu-id="cf7f0-109">This article is not about learning how to use Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-109">This article is not about learning how to use Jupyter.</span></span>

## <a name="jupyter-notebook-architecture"></a><span data-ttu-id="cf7f0-110">Jupyter Notebook architecture</span><span class="sxs-lookup"><span data-stu-id="cf7f0-110">Jupyter Notebook architecture</span></span>
<span data-ttu-id="cf7f0-111">At a high level, Jupyter Notebook architecture includes three components.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-111">At a high level, Jupyter Notebook architecture includes three components.</span></span> <span data-ttu-id="cf7f0-112">Each can run in different compute environments:</span><span class="sxs-lookup"><span data-stu-id="cf7f0-112">Each can run in different compute environments:</span></span>

- <span data-ttu-id="cf7f0-113">**Client**: Receives user input and displays rendered output.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-113">**Client**: Receives user input and displays rendered output.</span></span>
- <span data-ttu-id="cf7f0-114">**Server**: Web server that hosts the notebook files (.ipynb files).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-114">**Server**: Web server that hosts the notebook files (.ipynb files).</span></span>
- <span data-ttu-id="cf7f0-115">**Kernel**: Runtime environment in which execution of the notebook cells happens.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-115">**Kernel**: Runtime environment in which execution of the notebook cells happens.</span></span>

<span data-ttu-id="cf7f0-116">For more information, see the official [Jupyter documentation](http://jupyter.readthedocs.io/en/latest/architecture/how_jupyter_ipython_work.html).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-116">For more information, see the official [Jupyter documentation](http://jupyter.readthedocs.io/en/latest/architecture/how_jupyter_ipython_work.html).</span></span> <span data-ttu-id="cf7f0-117">The following diagram depicts how this client, server, and kernel architecture maps to the components in Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="cf7f0-117">The following diagram depicts how this client, server, and kernel architecture maps to the components in Azure Machine Learning:</span></span>

![Jupyter Notebook architecture](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-architecture.png)

## <a name="kernels-in-azure-machine-learning-workbench-notebooks"></a><span data-ttu-id="cf7f0-119">Kernels in Azure Machine Learning Workbench notebooks</span><span class="sxs-lookup"><span data-stu-id="cf7f0-119">Kernels in Azure Machine Learning Workbench notebooks</span></span>
<span data-ttu-id="cf7f0-120">You can access different kernels in Azure Machine Learning Workbench by defining run configurations and compute targets in the `aml_config` folder in your project.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-120">You can access different kernels in Azure Machine Learning Workbench by defining run configurations and compute targets in the `aml_config` folder in your project.</span></span> <span data-ttu-id="cf7f0-121">Adding a new compute target by issuing the `az ml computetarget attach` command is the equivalent of adding a new kernel.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-121">Adding a new compute target by issuing the `az ml computetarget attach` command is the equivalent of adding a new kernel.</span></span>

>[!NOTE]
><span data-ttu-id="cf7f0-122">Review [Configuring Azure Machine Learning Experimentation Service](experimentation-service-configuration.md) for more details on run configurations and compute targets.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-122">Review [Configuring Azure Machine Learning Experimentation Service](experimentation-service-configuration.md) for more details on run configurations and compute targets.</span></span>

### <a name="kernel-naming-convention"></a><span data-ttu-id="cf7f0-123">Kernel naming convention</span><span class="sxs-lookup"><span data-stu-id="cf7f0-123">Kernel naming convention</span></span>
<span data-ttu-id="cf7f0-124">Azure Machine Learning Workbench generates custom Jupyter kernels.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-124">Azure Machine Learning Workbench generates custom Jupyter kernels.</span></span> <span data-ttu-id="cf7f0-125">These kernels are named *\<project name> \<run config name>*.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-125">These kernels are named *\<project name> \<run config name>*.</span></span> <span data-ttu-id="cf7f0-126">For example, if you have a run configuration named _docker-python_ in a project named _myIris_,  Azure Machine Learning makes available a kernel named *myIris docker-python.*</span><span class="sxs-lookup"><span data-stu-id="cf7f0-126">For example, if you have a run configuration named _docker-python_ in a project named _myIris_,  Azure Machine Learning makes available a kernel named *myIris docker-python.*</span></span> <span data-ttu-id="cf7f0-127">You set the running kernel in the Jupyter Notebook **Kernel** menu, in the **Change kernel** submenu.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-127">You set the running kernel in the Jupyter Notebook **Kernel** menu, in the **Change kernel** submenu.</span></span> <span data-ttu-id="cf7f0-128">The name of the running kernel appears on the far right of the menu bar.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-128">The name of the running kernel appears on the far right of the menu bar.</span></span>
 
<span data-ttu-id="cf7f0-129">Currently, Azure Machine Learning Workbench supports the following types of kernels.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-129">Currently, Azure Machine Learning Workbench supports the following types of kernels.</span></span>

### <a name="local-python-kernel"></a><span data-ttu-id="cf7f0-130">Local Python kernel</span><span class="sxs-lookup"><span data-stu-id="cf7f0-130">Local Python kernel</span></span>
<span data-ttu-id="cf7f0-131">This Python kernel supports execution on local machines.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-131">This Python kernel supports execution on local machines.</span></span> <span data-ttu-id="cf7f0-132">It's integrated with Azure Machine Learning Run History support.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-132">It's integrated with Azure Machine Learning Run History support.</span></span> <span data-ttu-id="cf7f0-133">The name of the kernel is typically *my_project_name local.*</span><span class="sxs-lookup"><span data-stu-id="cf7f0-133">The name of the kernel is typically *my_project_name local.*</span></span>

>[!NOTE]
><span data-ttu-id="cf7f0-134">Do not use the Python 3 kernel.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-134">Do not use the Python 3 kernel.</span></span> <span data-ttu-id="cf7f0-135">It is a standalone kernel provided by Jupyter by default and is not integrated with Azure Machine Learning capabilities.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-135">It is a standalone kernel provided by Jupyter by default and is not integrated with Azure Machine Learning capabilities.</span></span> <span data-ttu-id="cf7f0-136">For example, the `%azureml` Jupyter magic functions return "not found" errors.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-136">For example, the `%azureml` Jupyter magic functions return "not found" errors.</span></span> 

### <a name="python-kernel-in-docker-local-or-remote"></a><span data-ttu-id="cf7f0-137">Python kernel in Docker (local or remote)</span><span class="sxs-lookup"><span data-stu-id="cf7f0-137">Python kernel in Docker (local or remote)</span></span>
<span data-ttu-id="cf7f0-138">This Python kernel runs in a Docker container either on your local machine or in a remote Linux virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-138">This Python kernel runs in a Docker container either on your local machine or in a remote Linux virtual machine (VM).</span></span> <span data-ttu-id="cf7f0-139">The name of the kernel is typically *my_project docker.*</span><span class="sxs-lookup"><span data-stu-id="cf7f0-139">The name of the kernel is typically *my_project docker.*</span></span> <span data-ttu-id="cf7f0-140">The associated `docker.runconfig` file has the `Framework` field set to `Python`.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-140">The associated `docker.runconfig` file has the `Framework` field set to `Python`.</span></span>

### <a name="pyspark-kernel-in-docker-local-or-remote"></a><span data-ttu-id="cf7f0-141">PySpark kernel in Docker (local or remote)</span><span class="sxs-lookup"><span data-stu-id="cf7f0-141">PySpark kernel in Docker (local or remote)</span></span>
<span data-ttu-id="cf7f0-142">This PySpark kernel executes scripts in a Spark context running inside a Docker container, either on your local machine or on a remote Linux VM.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-142">This PySpark kernel executes scripts in a Spark context running inside a Docker container, either on your local machine or on a remote Linux VM.</span></span> <span data-ttu-id="cf7f0-143">The kernel name is typically *my_project docker.*</span><span class="sxs-lookup"><span data-stu-id="cf7f0-143">The kernel name is typically *my_project docker.*</span></span> <span data-ttu-id="cf7f0-144">The associated `docker.runconfig` file has the `Framework` field set to `PySpark`.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-144">The associated `docker.runconfig` file has the `Framework` field set to `PySpark`.</span></span>

### <a name="pyspark-kernel-in-an-azure-hdinsight-cluster"></a><span data-ttu-id="cf7f0-145">PySpark kernel in an Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="cf7f0-145">PySpark kernel in an Azure HDInsight cluster</span></span>
<span data-ttu-id="cf7f0-146">This kernel runs in the remote Azure HDInsight cluster that you attached as a compute target for your project.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-146">This kernel runs in the remote Azure HDInsight cluster that you attached as a compute target for your project.</span></span> <span data-ttu-id="cf7f0-147">The kernel name is typically *my_project my_hdi.*</span><span class="sxs-lookup"><span data-stu-id="cf7f0-147">The kernel name is typically *my_project my_hdi.*</span></span> 

>[!IMPORTANT]
><span data-ttu-id="cf7f0-148">In the `.compute` file for the HDI compute target, you must change the `yarnDeployMode` field to `client` (the default value is `cluster`) to use this kernel.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-148">In the `.compute` file for the HDI compute target, you must change the `yarnDeployMode` field to `client` (the default value is `cluster`) to use this kernel.</span></span> 

## <a name="start-a-jupyter-server-from-azure-machine-learning-workbench"></a><span data-ttu-id="cf7f0-149">Start a Jupyter server from Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="cf7f0-149">Start a Jupyter server from Azure Machine Learning Workbench</span></span>
<span data-ttu-id="cf7f0-150">From Azure Machine Learning Workbench, you can access notebooks via the **Notebooks** tab. The _Classifying Iris_ sample project includes an `iris.ipynb` sample notebook.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-150">From Azure Machine Learning Workbench, you can access notebooks via the **Notebooks** tab. The _Classifying Iris_ sample project includes an `iris.ipynb` sample notebook.</span></span>

![Notebooks tab](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-01.png)

<span data-ttu-id="cf7f0-152">When you open a notebook in Azure Machine Learning Workbench, it's displayed in its own document tab in **Preview Mode**.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-152">When you open a notebook in Azure Machine Learning Workbench, it's displayed in its own document tab in **Preview Mode**.</span></span> <span data-ttu-id="cf7f0-153">This is a read-only view that doesn't require a running Jupyter server and kernel.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-153">This is a read-only view that doesn't require a running Jupyter server and kernel.</span></span>

![Notebook preview](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-02.png)

<span data-ttu-id="cf7f0-155">Selecting the **Start Notebook Server** button starts the Jupyter server and switches the notebook into **Edit Mode**.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-155">Selecting the **Start Notebook Server** button starts the Jupyter server and switches the notebook into **Edit Mode**.</span></span> <span data-ttu-id="cf7f0-156">The familiar Jupyter Notebook user interface appears embedded in Workbench.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-156">The familiar Jupyter Notebook user interface appears embedded in Workbench.</span></span> <span data-ttu-id="cf7f0-157">You can now set a kernel from the **Kernel**  menu and start your interactive notebook session.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-157">You can now set a kernel from the **Kernel**  menu and start your interactive notebook session.</span></span> 

>[!NOTE]
><span data-ttu-id="cf7f0-158">With non-local kernels, it can take a minute or two to start if you're using it for the first time.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-158">With non-local kernels, it can take a minute or two to start if you're using it for the first time.</span></span> <span data-ttu-id="cf7f0-159">You can execute the `az ml experiment prepare` command from the CLI window to prepare the compute target so the kernel starts much faster after the compute target is prepared.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-159">You can execute the `az ml experiment prepare` command from the CLI window to prepare the compute target so the kernel starts much faster after the compute target is prepared.</span></span>

![Edit Mode](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-04.png)

<span data-ttu-id="cf7f0-161">This is a fully interactive Jupyter Notebook experience.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-161">This is a fully interactive Jupyter Notebook experience.</span></span> <span data-ttu-id="cf7f0-162">All regular notebook operations and keyboard shortcuts are supported from this window, except for some file operations that can be done via the Workbench **Notebooks** tab and **File** tab.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-162">All regular notebook operations and keyboard shortcuts are supported from this window, except for some file operations that can be done via the Workbench **Notebooks** tab and **File** tab.</span></span>

## <a name="start-a-jupyter-server-from-the-command-line"></a><span data-ttu-id="cf7f0-163">Start a Jupyter server from the command line</span><span class="sxs-lookup"><span data-stu-id="cf7f0-163">Start a Jupyter server from the command line</span></span>
<span data-ttu-id="cf7f0-164">You can also start a notebook session by issuing `az ml notebook start` from the command-line window:</span><span class="sxs-lookup"><span data-stu-id="cf7f0-164">You can also start a notebook session by issuing `az ml notebook start` from the command-line window:</span></span>
```
$ az ml notebook start
[I 10:14:25.455 NotebookApp] The port 8888 is already in use, trying another port.
[I 10:14:25.464 NotebookApp] Serving notebooks from local directory: /Users/johnpelak/Desktop/IrisDemo
[I 10:14:25.465 NotebookApp] 0 active kernels 
[I 10:14:25.465 NotebookApp] The Jupyter Notebook is running at: http://localhost:8889/?token=1f0161ab88b22fc83f2083a93879ec5e8d0ec18490f0b953
[I 10:14:25.465 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 10:14:25.466 NotebookApp] 
    
Copy and paste this URL into your browser when you connect for the first time, to login with a token: http://localhost:8889/?token=1f0161ab88b22fc83f2083a93879ec5e8d0ec18490f0b953
[I 10:14:25.759 NotebookApp] Accepting one-time-token-authenticated connection from ::1
[I 10:16:52.970 NotebookApp] Kernel started: 7f8932e0-89b9-48b4-b5d0-e8f48d1da159
[I 10:16:53.854 NotebookApp] Adapting to protocol v5.1 for kernel 7f8932e0-89b9-48b4-b5d0-e8f48d1da159
```
<span data-ttu-id="cf7f0-165">Your default browser automatically opens with the Jupyter server pointing to the project home directory.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-165">Your default browser automatically opens with the Jupyter server pointing to the project home directory.</span></span> <span data-ttu-id="cf7f0-166">You can also use the URL and token displayed in the CLI window to open other browser windows locally.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-166">You can also use the URL and token displayed in the CLI window to open other browser windows locally.</span></span> 

![Project dashboard](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-07.png)

<span data-ttu-id="cf7f0-168">You can now select an `.ipynb` notebook file, open it, set the kernel (if it hasn't been set), and start your interactive session.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-168">You can now select an `.ipynb` notebook file, open it, set the kernel (if it hasn't been set), and start your interactive session.</span></span>

![Project dashboard](media/how-to-use-jupyter-notebooks/how-to-use-jupyter-notebooks-08.png)

## <a name="use-magic-commands-to-manage-experiments"></a><span data-ttu-id="cf7f0-170">Use magic commands to manage experiments</span><span class="sxs-lookup"><span data-stu-id="cf7f0-170">Use magic commands to manage experiments</span></span>

<span data-ttu-id="cf7f0-171">You can use [magic commands](http://ipython.readthedocs.io/en/stable/interactive/magics.html) within your notebook cells to track your run history and save outputs such as models or datasets.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-171">You can use [magic commands](http://ipython.readthedocs.io/en/stable/interactive/magics.html) within your notebook cells to track your run history and save outputs such as models or datasets.</span></span>

<span data-ttu-id="cf7f0-172">To track individual notebook cell runs, use the `%azureml history on` magic command.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-172">To track individual notebook cell runs, use the `%azureml history on` magic command.</span></span> <span data-ttu-id="cf7f0-173">After you turn on the history, each cell run appears as an entry in the run history:</span><span class="sxs-lookup"><span data-stu-id="cf7f0-173">After you turn on the history, each cell run appears as an entry in the run history:</span></span>

```
%azureml history on
from azureml.logging import get_azureml_logger
logger = get_azureml_logger()
logger.log("Cell","Load Data")
```

<span data-ttu-id="cf7f0-174">To turn off cell run tracking, use the `%azureml history off` magic command.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-174">To turn off cell run tracking, use the `%azureml history off` magic command.</span></span>

<span data-ttu-id="cf7f0-175">You can use the `%azureml upload` magic command to save model and data files from your run.</span><span class="sxs-lookup"><span data-stu-id="cf7f0-175">You can use the `%azureml upload` magic command to save model and data files from your run.</span></span> <span data-ttu-id="cf7f0-176">The saved objects appear as outputs in the run history view:</span><span class="sxs-lookup"><span data-stu-id="cf7f0-176">The saved objects appear as outputs in the run history view:</span></span>

```
modelpath = os.path.join("outputs","model.pkl")
with open(modelpath,"wb") as f:
    pickle.dump(model,f)
%azureml upload outputs/model.pkl
```

>[!NOTE]
><span data-ttu-id="cf7f0-177">The outputs must be saved to a folder named *outputs.*</span><span class="sxs-lookup"><span data-stu-id="cf7f0-177">The outputs must be saved to a folder named *outputs.*</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf7f0-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf7f0-178">Next steps</span></span>
- <span data-ttu-id="cf7f0-179">To learn how to use Jupyter Notebook, see the [Jupyter official documentation](http://jupyter-notebook.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-179">To learn how to use Jupyter Notebook, see the [Jupyter official documentation](http://jupyter-notebook.readthedocs.io/en/latest/).</span></span>    
- <span data-ttu-id="cf7f0-180">To gain a deeper understanding of the Azure Machine Learning experimentation execution environment, see [Configuring Azure Machine Learning Experimentation Service](experimentation-service-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="cf7f0-180">To gain a deeper understanding of the Azure Machine Learning experimentation execution environment, see [Configuring Azure Machine Learning Experimentation Service](experimentation-service-configuration.md).</span></span>

