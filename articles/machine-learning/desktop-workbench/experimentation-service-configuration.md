---
title: Configuring Azure Machine Learning Experimentation Service | Microsoft Docs
description: This article provides a high-level overview of Azure Machine Learning Experimentation Service with instructions on how to configure it.
services: machine-learning
author: gokhanuluderya-msft
ms.author: gokhanu
manager: haining
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/28/2017
ms.openlocfilehash: e79817ffad139e0a3bcb0ba32b9bc6e5666319d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855735"
---
# <a name="configuring-azure-machine-learning-experimentation-service"></a><span data-ttu-id="d4b23-103">Configuring Azure Machine Learning Experimentation Service</span><span class="sxs-lookup"><span data-stu-id="d4b23-103">Configuring Azure Machine Learning Experimentation Service</span></span>

## <a name="overview"></a><span data-ttu-id="d4b23-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d4b23-104">Overview</span></span>
<span data-ttu-id="d4b23-105">Azure Machine Learning Experimentation Service enables data scientists to execute their experiments using the Azure Machine Learning execution and run management capabilities.</span><span class="sxs-lookup"><span data-stu-id="d4b23-105">Azure Machine Learning Experimentation Service enables data scientists to execute their experiments using the Azure Machine Learning execution and run management capabilities.</span></span> <span data-ttu-id="d4b23-106">It provides a framework for agile experimentation with fast iterations.</span><span class="sxs-lookup"><span data-stu-id="d4b23-106">It provides a framework for agile experimentation with fast iterations.</span></span> <span data-ttu-id="d4b23-107">Azure Machine Learning Workbench allows you to start with local runs on your machine and also an easy path for scaling up and out to other environments such as remote Data Science VMs with GPU or HDInsight Clusters running Spark.</span><span class="sxs-lookup"><span data-stu-id="d4b23-107">Azure Machine Learning Workbench allows you to start with local runs on your machine and also an easy path for scaling up and out to other environments such as remote Data Science VMs with GPU or HDInsight Clusters running Spark.</span></span>

<span data-ttu-id="d4b23-108">Experimentation Service is built for providing isolated, reproducible, and consistent runs of your experiments.</span><span class="sxs-lookup"><span data-stu-id="d4b23-108">Experimentation Service is built for providing isolated, reproducible, and consistent runs of your experiments.</span></span> <span data-ttu-id="d4b23-109">It helps you manage your compute targets, execution environments, and run configurations.</span><span class="sxs-lookup"><span data-stu-id="d4b23-109">It helps you manage your compute targets, execution environments, and run configurations.</span></span> <span data-ttu-id="d4b23-110">By using the Azure Machine Learning Workbench execution and run management capabilities, you can easily move  between different environments.</span><span class="sxs-lookup"><span data-stu-id="d4b23-110">By using the Azure Machine Learning Workbench execution and run management capabilities, you can easily move  between different environments.</span></span> 

<span data-ttu-id="d4b23-111">You can execute a Python or PySpark script in a Workbench project locally or at scale in the cloud.</span><span class="sxs-lookup"><span data-stu-id="d4b23-111">You can execute a Python or PySpark script in a Workbench project locally or at scale in the cloud.</span></span> 

<span data-ttu-id="d4b23-112">You can run your scripts on:</span><span class="sxs-lookup"><span data-stu-id="d4b23-112">You can run your scripts on:</span></span> 

* <span data-ttu-id="d4b23-113">Python (3.5.2) environment on your local computer installed by Workbench</span><span class="sxs-lookup"><span data-stu-id="d4b23-113">Python (3.5.2) environment on your local computer installed by Workbench</span></span>
* <span data-ttu-id="d4b23-114">Conda Python environment inside of a Docker container on local computer</span><span class="sxs-lookup"><span data-stu-id="d4b23-114">Conda Python environment inside of a Docker container on local computer</span></span>
* <span data-ttu-id="d4b23-115">On a Python environment that you own and manage on a remote Linux Machine</span><span class="sxs-lookup"><span data-stu-id="d4b23-115">On a Python environment that you own and manage on a remote Linux Machine</span></span>
* <span data-ttu-id="d4b23-116">Conda Python environment inside of a Docker container on a remote Linux machine.</span><span class="sxs-lookup"><span data-stu-id="d4b23-116">Conda Python environment inside of a Docker container on a remote Linux machine.</span></span> <span data-ttu-id="d4b23-117">For example, an [Ubuntu-based DSVM on Azure] (https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)</span><span class="sxs-lookup"><span data-stu-id="d4b23-117">For example, an [Ubuntu-based DSVM on Azure] (https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)</span></span>
* <span data-ttu-id="d4b23-118">[HDInsight for Spark](https://azure.microsoft.com/services/hdinsight/apache-spark/) on Azure</span><span class="sxs-lookup"><span data-stu-id="d4b23-118">[HDInsight for Spark](https://azure.microsoft.com/services/hdinsight/apache-spark/) on Azure</span></span>

>[!IMPORTANT]
><span data-ttu-id="d4b23-119">Azure Machine Learning Experimentation Service currently supports Python 3.5.2 and Spark 2.1.11 as Python and Spark runtime versions, respectively.</span><span class="sxs-lookup"><span data-stu-id="d4b23-119">Azure Machine Learning Experimentation Service currently supports Python 3.5.2 and Spark 2.1.11 as Python and Spark runtime versions, respectively.</span></span> 


### <a name="key-concepts-in-experimentation-service"></a><span data-ttu-id="d4b23-120">Key concepts in Experimentation Service</span><span class="sxs-lookup"><span data-stu-id="d4b23-120">Key concepts in Experimentation Service</span></span>
<span data-ttu-id="d4b23-121">It is important to understand the following concepts in Azure Machine Learning experiment execution.</span><span class="sxs-lookup"><span data-stu-id="d4b23-121">It is important to understand the following concepts in Azure Machine Learning experiment execution.</span></span> <span data-ttu-id="d4b23-122">In the subsequent sections, we discuss how to use these concepts in detail.</span><span class="sxs-lookup"><span data-stu-id="d4b23-122">In the subsequent sections, we discuss how to use these concepts in detail.</span></span> 

#### <a name="compute-target"></a><span data-ttu-id="d4b23-123">Compute target</span><span class="sxs-lookup"><span data-stu-id="d4b23-123">Compute target</span></span>
<span data-ttu-id="d4b23-124">A _compute target_ specifies where to execute your program such as your desktop, remote Docker on a VM, or a cluster.</span><span class="sxs-lookup"><span data-stu-id="d4b23-124">A _compute target_ specifies where to execute your program such as your desktop, remote Docker on a VM, or a cluster.</span></span> <span data-ttu-id="d4b23-125">A compute target needs to be addressable and accessible by you.</span><span class="sxs-lookup"><span data-stu-id="d4b23-125">A compute target needs to be addressable and accessible by you.</span></span> <span data-ttu-id="d4b23-126">Workbench gives you the ability to create compute targets and manage them using the Workbench application and the CLI.</span><span class="sxs-lookup"><span data-stu-id="d4b23-126">Workbench gives you the ability to create compute targets and manage them using the Workbench application and the CLI.</span></span> 

<span data-ttu-id="d4b23-127">_az ml computetarget attach_ command in CLI enables you to create a compute target that you can use in your runs.</span><span class="sxs-lookup"><span data-stu-id="d4b23-127">_az ml computetarget attach_ command in CLI enables you to create a compute target that you can use in your runs.</span></span>

<span data-ttu-id="d4b23-128">Supported compute targets are:</span><span class="sxs-lookup"><span data-stu-id="d4b23-128">Supported compute targets are:</span></span>
* <span data-ttu-id="d4b23-129">Local Python (3.5.2) environment on your computer installed by Workbench.</span><span class="sxs-lookup"><span data-stu-id="d4b23-129">Local Python (3.5.2) environment on your computer installed by Workbench.</span></span>
* <span data-ttu-id="d4b23-130">Local Docker on your computer</span><span class="sxs-lookup"><span data-stu-id="d4b23-130">Local Docker on your computer</span></span>
* <span data-ttu-id="d4b23-131">User-managed, Python environment on remote Linux-Ubuntu VMs.</span><span class="sxs-lookup"><span data-stu-id="d4b23-131">User-managed, Python environment on remote Linux-Ubuntu VMs.</span></span> <span data-ttu-id="d4b23-132">For example, an [Ubuntu-based DSVM on Azure](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)</span><span class="sxs-lookup"><span data-stu-id="d4b23-132">For example, an [Ubuntu-based DSVM on Azure](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)</span></span>
* <span data-ttu-id="d4b23-133">Remote Docker on Linux-Ubuntu VMs.</span><span class="sxs-lookup"><span data-stu-id="d4b23-133">Remote Docker on Linux-Ubuntu VMs.</span></span> <span data-ttu-id="d4b23-134">For example, an [Ubuntu-based DSVM on Azure](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)</span><span class="sxs-lookup"><span data-stu-id="d4b23-134">For example, an [Ubuntu-based DSVM on Azure](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)</span></span>
* <span data-ttu-id="d4b23-135">[HDInsight for Spark cluster](https://azure.microsoft.com/services/hdinsight/apache-spark/) on Azure</span><span class="sxs-lookup"><span data-stu-id="d4b23-135">[HDInsight for Spark cluster](https://azure.microsoft.com/services/hdinsight/apache-spark/) on Azure</span></span>

<span data-ttu-id="d4b23-136">Experimentation Service currently supports Python 3.5.2 and Spark 2.1.11 as Python and Spark runtime versions, respectively.</span><span class="sxs-lookup"><span data-stu-id="d4b23-136">Experimentation Service currently supports Python 3.5.2 and Spark 2.1.11 as Python and Spark runtime versions, respectively.</span></span> 

>[!IMPORTANT]
> <span data-ttu-id="d4b23-137">Windows VMs running Docker are **not** supported as remote compute targets.</span><span class="sxs-lookup"><span data-stu-id="d4b23-137">Windows VMs running Docker are **not** supported as remote compute targets.</span></span>

#### <a name="execution-environment"></a><span data-ttu-id="d4b23-138">Execution environment</span><span class="sxs-lookup"><span data-stu-id="d4b23-138">Execution environment</span></span>
<span data-ttu-id="d4b23-139">The _execution environment_ defines the run time configuration and the dependencies needed to run the program in Workbench.</span><span class="sxs-lookup"><span data-stu-id="d4b23-139">The _execution environment_ defines the run time configuration and the dependencies needed to run the program in Workbench.</span></span>

<span data-ttu-id="d4b23-140">You manage the local execution environment using your favorite tools and package managers if you're running on the Workbench default runtime.</span><span class="sxs-lookup"><span data-stu-id="d4b23-140">You manage the local execution environment using your favorite tools and package managers if you're running on the Workbench default runtime.</span></span> 

<span data-ttu-id="d4b23-141">Conda is used to manage local Docker and remote Docker executions as well as HDInsight-based executions.</span><span class="sxs-lookup"><span data-stu-id="d4b23-141">Conda is used to manage local Docker and remote Docker executions as well as HDInsight-based executions.</span></span> <span data-ttu-id="d4b23-142">For these compute targets, the execution environment configuration is managed through **Conda_dependencies.yml** and **Spark_dependencies.yml files**.</span><span class="sxs-lookup"><span data-stu-id="d4b23-142">For these compute targets, the execution environment configuration is managed through **Conda_dependencies.yml** and **Spark_dependencies.yml files**.</span></span> <span data-ttu-id="d4b23-143">These files are in the **aml_config** folder inside your project.</span><span class="sxs-lookup"><span data-stu-id="d4b23-143">These files are in the **aml_config** folder inside your project.</span></span>

<span data-ttu-id="d4b23-144">**Supported runtimes for execution environments are:**</span><span class="sxs-lookup"><span data-stu-id="d4b23-144">**Supported runtimes for execution environments are:**</span></span>
* <span data-ttu-id="d4b23-145">Python 3.5.2</span><span class="sxs-lookup"><span data-stu-id="d4b23-145">Python 3.5.2</span></span>
* <span data-ttu-id="d4b23-146">Spark 2.1.11</span><span class="sxs-lookup"><span data-stu-id="d4b23-146">Spark 2.1.11</span></span>

### <a name="run-configuration"></a><span data-ttu-id="d4b23-147">Run configuration</span><span class="sxs-lookup"><span data-stu-id="d4b23-147">Run configuration</span></span>
<span data-ttu-id="d4b23-148">In addition to the compute target and execution environment, Azure Machine Learning provides a framework to define and change *run configurations*.</span><span class="sxs-lookup"><span data-stu-id="d4b23-148">In addition to the compute target and execution environment, Azure Machine Learning provides a framework to define and change *run configurations*.</span></span> <span data-ttu-id="d4b23-149">Different executions of your experiment may require different configuration as part of iterative experimentation.</span><span class="sxs-lookup"><span data-stu-id="d4b23-149">Different executions of your experiment may require different configuration as part of iterative experimentation.</span></span> <span data-ttu-id="d4b23-150">You may be sweeping different parameter ranges, using different data sources, and tuning spark parameters.</span><span class="sxs-lookup"><span data-stu-id="d4b23-150">You may be sweeping different parameter ranges, using different data sources, and tuning spark parameters.</span></span> <span data-ttu-id="d4b23-151">Experimentation Service provides a framework for managing run configurations.</span><span class="sxs-lookup"><span data-stu-id="d4b23-151">Experimentation Service provides a framework for managing run configurations.</span></span>

<span data-ttu-id="d4b23-152">Running _az ml computetarget attach_ command produces two files in your **aml_config** folder in your project: a ".compute" and  a ".runconfig" following this convention: _<your_computetarget_name>.compute_ and _<your_computetarget_name>.runconfig_.</span><span class="sxs-lookup"><span data-stu-id="d4b23-152">Running _az ml computetarget attach_ command produces two files in your **aml_config** folder in your project: a ".compute" and  a ".runconfig" following this convention: _<your_computetarget_name>.compute_ and _<your_computetarget_name>.runconfig_.</span></span> <span data-ttu-id="d4b23-153">The .runconfig file is automatically created for your convenience when you create a compute target.</span><span class="sxs-lookup"><span data-stu-id="d4b23-153">The .runconfig file is automatically created for your convenience when you create a compute target.</span></span> <span data-ttu-id="d4b23-154">You can create and manage other run configurations using _az ml runconfigurations_ command in CLI.</span><span class="sxs-lookup"><span data-stu-id="d4b23-154">You can create and manage other run configurations using _az ml runconfigurations_ command in CLI.</span></span> <span data-ttu-id="d4b23-155">You can also create and edit them on your file system.</span><span class="sxs-lookup"><span data-stu-id="d4b23-155">You can also create and edit them on your file system.</span></span>

<span data-ttu-id="d4b23-156">Run configuration in Workbench also enables you to specify environment variables.</span><span class="sxs-lookup"><span data-stu-id="d4b23-156">Run configuration in Workbench also enables you to specify environment variables.</span></span> <span data-ttu-id="d4b23-157">You can specify environment variables and use them in your code by adding the following section in your .runconfig file.</span><span class="sxs-lookup"><span data-stu-id="d4b23-157">You can specify environment variables and use them in your code by adding the following section in your .runconfig file.</span></span> 

```
EnvironmentVariables:
    "EXAMPLE_ENV_VAR1": "Example Value1"
    "EXAMPLE_ENV_VAR2": "Example Value2"
```

<span data-ttu-id="d4b23-158">These environment variables can be accessed in your code.</span><span class="sxs-lookup"><span data-stu-id="d4b23-158">These environment variables can be accessed in your code.</span></span> <span data-ttu-id="d4b23-159">For example, this phyton code snippet prints the environment variable named "EXAMPLE_ENV_VAR1"</span><span class="sxs-lookup"><span data-stu-id="d4b23-159">For example, this phyton code snippet prints the environment variable named "EXAMPLE_ENV_VAR1"</span></span>
```
print(os.environ.get("EXAMPLE_ENV_VAR1"))
```

<span data-ttu-id="d4b23-160">_**The following figure shows the high-level flow for initial experiment run.**_
![](media/experimentation-service-configuration/experiment-execution-flow.png)</span><span class="sxs-lookup"><span data-stu-id="d4b23-160">_**The following figure shows the high-level flow for initial experiment run.**_
![](media/experimentation-service-configuration/experiment-execution-flow.png)</span></span>

## <a name="experiment-execution-scenarios"></a><span data-ttu-id="d4b23-161">Experiment execution scenarios</span><span class="sxs-lookup"><span data-stu-id="d4b23-161">Experiment execution scenarios</span></span>
<span data-ttu-id="d4b23-162">In this section, we dive into execution scenarios and learn about how Azure Machine Learning runs experiments, specifically running an experiment locally, on a remote VM, and on an HDInsight Cluster.</span><span class="sxs-lookup"><span data-stu-id="d4b23-162">In this section, we dive into execution scenarios and learn about how Azure Machine Learning runs experiments, specifically running an experiment locally, on a remote VM, and on an HDInsight Cluster.</span></span> <span data-ttu-id="d4b23-163">This section is a walkthrough starting from creating a compute target to executing your experiments.</span><span class="sxs-lookup"><span data-stu-id="d4b23-163">This section is a walkthrough starting from creating a compute target to executing your experiments.</span></span>

>[!NOTE]
><span data-ttu-id="d4b23-164">For the rest of this article, we are using the CLI (Command-line interface) commands to show the concepts and the capabilities.</span><span class="sxs-lookup"><span data-stu-id="d4b23-164">For the rest of this article, we are using the CLI (Command-line interface) commands to show the concepts and the capabilities.</span></span> <span data-ttu-id="d4b23-165">Capabilities described here can also be used from Workbench.</span><span class="sxs-lookup"><span data-stu-id="d4b23-165">Capabilities described here can also be used from Workbench.</span></span>

## <a name="launching-the-cli"></a><span data-ttu-id="d4b23-166">Launching the CLI</span><span class="sxs-lookup"><span data-stu-id="d4b23-166">Launching the CLI</span></span>
<span data-ttu-id="d4b23-167">An easy way to launch the CLI is opening a project in Workbench and navigating to **File-->Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="d4b23-167">An easy way to launch the CLI is opening a project in Workbench and navigating to **File-->Open Command Prompt**.</span></span>

![](media/experimentation-service-configuration/opening-cli.png)

<span data-ttu-id="d4b23-168">This command launches a terminal window in which you can enter commands to execute scripts in the current project folder.</span><span class="sxs-lookup"><span data-stu-id="d4b23-168">This command launches a terminal window in which you can enter commands to execute scripts in the current project folder.</span></span> <span data-ttu-id="d4b23-169">This terminal window is configured with the Python 3.5.2 environment, which is installed by Workbench.</span><span class="sxs-lookup"><span data-stu-id="d4b23-169">This terminal window is configured with the Python 3.5.2 environment, which is installed by Workbench.</span></span>

>[!NOTE]
> <span data-ttu-id="d4b23-170">When you execute any _az ml_ command from the command window, you need to be authenticated against Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b23-170">When you execute any _az ml_ command from the command window, you need to be authenticated against Azure.</span></span> <span data-ttu-id="d4b23-171">CLI uses an independent authentication cache then the desktop app and so logging in to Workbench doesn't mean you are authenticated in your CLI environment.</span><span class="sxs-lookup"><span data-stu-id="d4b23-171">CLI uses an independent authentication cache then the desktop app and so logging in to Workbench doesn't mean you are authenticated in your CLI environment.</span></span> <span data-ttu-id="d4b23-172">To authenticate, use the following the steps.</span><span class="sxs-lookup"><span data-stu-id="d4b23-172">To authenticate, use the following the steps.</span></span> <span data-ttu-id="d4b23-173">Authentication token is cached locally for a period of time so you only need to repeat these steps when the token expires.</span><span class="sxs-lookup"><span data-stu-id="d4b23-173">Authentication token is cached locally for a period of time so you only need to repeat these steps when the token expires.</span></span> <span data-ttu-id="d4b23-174">When the token expires or if you are seeing authentication errors, execute the following commands:</span><span class="sxs-lookup"><span data-stu-id="d4b23-174">When the token expires or if you are seeing authentication errors, execute the following commands:</span></span>

```
# to authenticate 
$ az login

# to list subscriptions
$ az account list -o table

# to set current subscription to a particular subscription ID 
$ az account set -s <subscription_id>

# to verify your current Azure subscription
$ az account show
```

>[!NOTE] 
><span data-ttu-id="d4b23-175">When you run _az ml_ command within a project folder, make sure that the project belongs to an Azure Machine Learning Experimentation account on the _current_ Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d4b23-175">When you run _az ml_ command within a project folder, make sure that the project belongs to an Azure Machine Learning Experimentation account on the _current_ Azure subscription.</span></span> <span data-ttu-id="d4b23-176">Otherwise you may encounter execution errors.</span><span class="sxs-lookup"><span data-stu-id="d4b23-176">Otherwise you may encounter execution errors.</span></span>


## <a name="running-scripts-and-experiments"></a><span data-ttu-id="d4b23-177">Running scripts and experiments</span><span class="sxs-lookup"><span data-stu-id="d4b23-177">Running scripts and experiments</span></span>
<span data-ttu-id="d4b23-178">With Workbench, you can execute your Python and PySpark scripts on various compute targets using the _az ml experiment submit_ command.</span><span class="sxs-lookup"><span data-stu-id="d4b23-178">With Workbench, you can execute your Python and PySpark scripts on various compute targets using the _az ml experiment submit_ command.</span></span> <span data-ttu-id="d4b23-179">This command requires a run configuration definition.</span><span class="sxs-lookup"><span data-stu-id="d4b23-179">This command requires a run configuration definition.</span></span> 

<span data-ttu-id="d4b23-180">Workbench creates a corresponding runconfig file when you create a compute target, but you can create additional run configurations using _az ml runconfiguration  create_ command.</span><span class="sxs-lookup"><span data-stu-id="d4b23-180">Workbench creates a corresponding runconfig file when you create a compute target, but you can create additional run configurations using _az ml runconfiguration  create_ command.</span></span> <span data-ttu-id="d4b23-181">You can also manually edit the run configuration files.</span><span class="sxs-lookup"><span data-stu-id="d4b23-181">You can also manually edit the run configuration files.</span></span>

<span data-ttu-id="d4b23-182">Run configurations show up as part of experiment run experience in Workbench.</span><span class="sxs-lookup"><span data-stu-id="d4b23-182">Run configurations show up as part of experiment run experience in Workbench.</span></span> 

>[!NOTE]
><span data-ttu-id="d4b23-183">You can learn more about the run configuration file in the [Experiment Execution Configuration Reference](experimentation-service-configuration-reference.md) Section.</span><span class="sxs-lookup"><span data-stu-id="d4b23-183">You can learn more about the run configuration file in the [Experiment Execution Configuration Reference](experimentation-service-configuration-reference.md) Section.</span></span>

## <a name="running-a-script-locally-on-workbench-installed-runtime"></a><span data-ttu-id="d4b23-184">Running a script locally on Workbench-installed runtime</span><span class="sxs-lookup"><span data-stu-id="d4b23-184">Running a script locally on Workbench-installed runtime</span></span>
<span data-ttu-id="d4b23-185">Workbench enables you to run your scripts directly against the Workbench-installed Python 3.5.2 runtime.</span><span class="sxs-lookup"><span data-stu-id="d4b23-185">Workbench enables you to run your scripts directly against the Workbench-installed Python 3.5.2 runtime.</span></span> <span data-ttu-id="d4b23-186">This default runtime is installed at Workbench set-up time and includes Azure Machine Learning libraries and dependencies.</span><span class="sxs-lookup"><span data-stu-id="d4b23-186">This default runtime is installed at Workbench set-up time and includes Azure Machine Learning libraries and dependencies.</span></span> <span data-ttu-id="d4b23-187">Run results and artifacts for local executions are still saved in Run History Service in the cloud.</span><span class="sxs-lookup"><span data-stu-id="d4b23-187">Run results and artifacts for local executions are still saved in Run History Service in the cloud.</span></span>

<span data-ttu-id="d4b23-188">Unlike Docker-based executions, this configuration is _not_ managed by Conda.</span><span class="sxs-lookup"><span data-stu-id="d4b23-188">Unlike Docker-based executions, this configuration is _not_ managed by Conda.</span></span> <span data-ttu-id="d4b23-189">You need to manually provision package dependencies for your local Workbench Python environment.</span><span class="sxs-lookup"><span data-stu-id="d4b23-189">You need to manually provision package dependencies for your local Workbench Python environment.</span></span>

<span data-ttu-id="d4b23-190">You can execute the following command to run your script locally in the Workbench-installed Python environment.</span><span class="sxs-lookup"><span data-stu-id="d4b23-190">You can execute the following command to run your script locally in the Workbench-installed Python environment.</span></span> 

```
$az ml experiment submit -c local myscript.py
```

<span data-ttu-id="d4b23-191">You can find the path to the default Python environment by typing the following command in the Workbench CLI window.</span><span class="sxs-lookup"><span data-stu-id="d4b23-191">You can find the path to the default Python environment by typing the following command in the Workbench CLI window.</span></span>
```
$ conda env list
```

>[!NOTE]
><span data-ttu-id="d4b23-192">Running PySpark locally directly against local Spark environments is currently **not** supported.</span><span class="sxs-lookup"><span data-stu-id="d4b23-192">Running PySpark locally directly against local Spark environments is currently **not** supported.</span></span> <span data-ttu-id="d4b23-193">Workbench does support PySpark scripts running on local Docker.</span><span class="sxs-lookup"><span data-stu-id="d4b23-193">Workbench does support PySpark scripts running on local Docker.</span></span> <span data-ttu-id="d4b23-194">Azure Machine Learning base Docker image comes with Spark 2.1.11 pre-installed.</span><span class="sxs-lookup"><span data-stu-id="d4b23-194">Azure Machine Learning base Docker image comes with Spark 2.1.11 pre-installed.</span></span> 

<span data-ttu-id="d4b23-195">_**Overview of local execution for a Python script:**_
![](media/experimentation-service-configuration/local-native-run.png)</span><span class="sxs-lookup"><span data-stu-id="d4b23-195">_**Overview of local execution for a Python script:**_
![](media/experimentation-service-configuration/local-native-run.png)</span></span>

## <a name="running-a-script-on-local-docker"></a><span data-ttu-id="d4b23-196">Running a script on local Docker</span><span class="sxs-lookup"><span data-stu-id="d4b23-196">Running a script on local Docker</span></span>
<span data-ttu-id="d4b23-197">You can also run your projects on a Docker container on your local machine through Experimentation Service.</span><span class="sxs-lookup"><span data-stu-id="d4b23-197">You can also run your projects on a Docker container on your local machine through Experimentation Service.</span></span> <span data-ttu-id="d4b23-198">Workbench provides a base Docker image that comes with Azure Machine Learning libraries and as well as Spark 2.1.11 runtime to make local Spark executions easy.</span><span class="sxs-lookup"><span data-stu-id="d4b23-198">Workbench provides a base Docker image that comes with Azure Machine Learning libraries and as well as Spark 2.1.11 runtime to make local Spark executions easy.</span></span> <span data-ttu-id="d4b23-199">Docker needs to be already running on the local machine.</span><span class="sxs-lookup"><span data-stu-id="d4b23-199">Docker needs to be already running on the local machine.</span></span>

<span data-ttu-id="d4b23-200">For running your Python or PySpark script on local Docker, you can execute the following commands in CLI.</span><span class="sxs-lookup"><span data-stu-id="d4b23-200">For running your Python or PySpark script on local Docker, you can execute the following commands in CLI.</span></span>

```
$az ml experiment submit -c docker myscript.py
```
<span data-ttu-id="d4b23-201">or</span><span class="sxs-lookup"><span data-stu-id="d4b23-201">or</span></span>
```
az ml experiment submit --run-configuration docker myscript.py
```

<span data-ttu-id="d4b23-202">The execution environment on local Docker is prepared using the Azure Machine Learning base Docker image.</span><span class="sxs-lookup"><span data-stu-id="d4b23-202">The execution environment on local Docker is prepared using the Azure Machine Learning base Docker image.</span></span> <span data-ttu-id="d4b23-203">Workbench downloads this image when running for the first time and overlays it with packages specified in your conda_dependencies.yml file.</span><span class="sxs-lookup"><span data-stu-id="d4b23-203">Workbench downloads this image when running for the first time and overlays it with packages specified in your conda_dependencies.yml file.</span></span> <span data-ttu-id="d4b23-204">This operation makes the initial run slower but subsequent runs are considerably faster thanks to Workbench reusing cached layers.</span><span class="sxs-lookup"><span data-stu-id="d4b23-204">This operation makes the initial run slower but subsequent runs are considerably faster thanks to Workbench reusing cached layers.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="d4b23-205">You need to run _az ml experiment prepare -c docker_ command first to prepare the Docker image for your first run.</span><span class="sxs-lookup"><span data-stu-id="d4b23-205">You need to run _az ml experiment prepare -c docker_ command first to prepare the Docker image for your first run.</span></span> <span data-ttu-id="d4b23-206">You can also set the **PrepareEnvironment** parameter to true in your docker.runconfig file.</span><span class="sxs-lookup"><span data-stu-id="d4b23-206">You can also set the **PrepareEnvironment** parameter to true in your docker.runconfig file.</span></span> <span data-ttu-id="d4b23-207">This action automatically prepares your environment as part of your run execution.</span><span class="sxs-lookup"><span data-stu-id="d4b23-207">This action automatically prepares your environment as part of your run execution.</span></span>  

>[!NOTE]
><span data-ttu-id="d4b23-208">If running a PySpark script on Spark, spark_dependencies.yml is also used in addition to conda_dependencies.yml.</span><span class="sxs-lookup"><span data-stu-id="d4b23-208">If running a PySpark script on Spark, spark_dependencies.yml is also used in addition to conda_dependencies.yml.</span></span>

<span data-ttu-id="d4b23-209">Running your scripts on a Docker image gives you the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d4b23-209">Running your scripts on a Docker image gives you the following benefits:</span></span>

1. <span data-ttu-id="d4b23-210">It ensures that your script can be reliably executed in other execution environments.</span><span class="sxs-lookup"><span data-stu-id="d4b23-210">It ensures that your script can be reliably executed in other execution environments.</span></span> <span data-ttu-id="d4b23-211">Running on a Docker container helps you discover and avoid any local references that may impact portability.</span><span class="sxs-lookup"><span data-stu-id="d4b23-211">Running on a Docker container helps you discover and avoid any local references that may impact portability.</span></span> 

2. <span data-ttu-id="d4b23-212">It allows you to quickly test code on runtimes and frameworks that are complex to install and configure, such as Apache Spark, without having to install them yourself.</span><span class="sxs-lookup"><span data-stu-id="d4b23-212">It allows you to quickly test code on runtimes and frameworks that are complex to install and configure, such as Apache Spark, without having to install them yourself.</span></span>


<span data-ttu-id="d4b23-213">_**Overview of local Docker execution for a Python script:**_
![](media/experimentation-service-configuration/local-docker-run.png)</span><span class="sxs-lookup"><span data-stu-id="d4b23-213">_**Overview of local Docker execution for a Python script:**_
![](media/experimentation-service-configuration/local-docker-run.png)</span></span>

## <a name="running-a-script-on-a-remote-docker"></a><span data-ttu-id="d4b23-214">Running a script on a remote Docker</span><span class="sxs-lookup"><span data-stu-id="d4b23-214">Running a script on a remote Docker</span></span>
<span data-ttu-id="d4b23-215">In some cases, resources available on your local machine may not be enough to train the desired model.</span><span class="sxs-lookup"><span data-stu-id="d4b23-215">In some cases, resources available on your local machine may not be enough to train the desired model.</span></span> <span data-ttu-id="d4b23-216">In this situation, Experimentation Service allows an easy way to run your Python or PySpark scripts on more powerful VMs using remote Docker execution.</span><span class="sxs-lookup"><span data-stu-id="d4b23-216">In this situation, Experimentation Service allows an easy way to run your Python or PySpark scripts on more powerful VMs using remote Docker execution.</span></span> 

<span data-ttu-id="d4b23-217">Remote VM should satisfy the following requirements:</span><span class="sxs-lookup"><span data-stu-id="d4b23-217">Remote VM should satisfy the following requirements:</span></span>
* <span data-ttu-id="d4b23-218">Remote VM needs to be running Linux-Ubuntu and should be accessible through SSH.</span><span class="sxs-lookup"><span data-stu-id="d4b23-218">Remote VM needs to be running Linux-Ubuntu and should be accessible through SSH.</span></span> 
* <span data-ttu-id="d4b23-219">Remote VM needs to have Docker running.</span><span class="sxs-lookup"><span data-stu-id="d4b23-219">Remote VM needs to have Docker running.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="d4b23-220">Windows VMs running Docker is **not** supported as remote compute targets</span><span class="sxs-lookup"><span data-stu-id="d4b23-220">Windows VMs running Docker is **not** supported as remote compute targets</span></span>


<span data-ttu-id="d4b23-221">You can use the following command to create both the compute target definition and run configuration for remote Docker-based executions.</span><span class="sxs-lookup"><span data-stu-id="d4b23-221">You can use the following command to create both the compute target definition and run configuration for remote Docker-based executions.</span></span>

```
az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --password "sshpassword" 
```

<span data-ttu-id="d4b23-222">Once you configure the compute target, you can use the following command to run your script.</span><span class="sxs-lookup"><span data-stu-id="d4b23-222">Once you configure the compute target, you can use the following command to run your script.</span></span>
```
$ az ml experiment submit -c remotevm myscript.py
```
>[!NOTE]
><span data-ttu-id="d4b23-223">Keep in mind that execution environment is configured using the specifications in conda_dependencies.yml.</span><span class="sxs-lookup"><span data-stu-id="d4b23-223">Keep in mind that execution environment is configured using the specifications in conda_dependencies.yml.</span></span> <span data-ttu-id="d4b23-224">spark_dependencies.yml is also used if PySpark framework is specified in .runconfig file.</span><span class="sxs-lookup"><span data-stu-id="d4b23-224">spark_dependencies.yml is also used if PySpark framework is specified in .runconfig file.</span></span> 

<span data-ttu-id="d4b23-225">The Docker construction process for remote VMs is exactly the same as the process for local Docker runs so you should expect a similar execution experience.</span><span class="sxs-lookup"><span data-stu-id="d4b23-225">The Docker construction process for remote VMs is exactly the same as the process for local Docker runs so you should expect a similar execution experience.</span></span>

>[!TIP]
><span data-ttu-id="d4b23-226">If you prefer to avoid the latency introduced by building the Docker image for your first run, you can use the following command to prepare the compute target before executing your script.</span><span class="sxs-lookup"><span data-stu-id="d4b23-226">If you prefer to avoid the latency introduced by building the Docker image for your first run, you can use the following command to prepare the compute target before executing your script.</span></span> <span data-ttu-id="d4b23-227">az ml experiment prepare -c remotedocker</span><span class="sxs-lookup"><span data-stu-id="d4b23-227">az ml experiment prepare -c remotedocker</span></span>

<span data-ttu-id="d4b23-228">_**Overview of remote vm execution for a Python script:**_
![](media/experimentation-service-configuration/remote-vm-run.png)</span><span class="sxs-lookup"><span data-stu-id="d4b23-228">_**Overview of remote vm execution for a Python script:**_
![](media/experimentation-service-configuration/remote-vm-run.png)</span></span>

## <a name="running-a-script-on-a-remote-vm-targeting-user-managed-environments"></a><span data-ttu-id="d4b23-229">Running a script on a remote VM targeting user-managed environments</span><span class="sxs-lookup"><span data-stu-id="d4b23-229">Running a script on a remote VM targeting user-managed environments</span></span>
<span data-ttu-id="d4b23-230">Experimentation service also supports running a script on user's own Python environment inside a remote Ubuntu virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d4b23-230">Experimentation service also supports running a script on user's own Python environment inside a remote Ubuntu virtual machine.</span></span> <span data-ttu-id="d4b23-231">This allows you to manage your own environment for execution and still use Azure Machine Learning capabilities.</span><span class="sxs-lookup"><span data-stu-id="d4b23-231">This allows you to manage your own environment for execution and still use Azure Machine Learning capabilities.</span></span> 

<span data-ttu-id="d4b23-232">Follow the following steps to run your script on your own environment.</span><span class="sxs-lookup"><span data-stu-id="d4b23-232">Follow the following steps to run your script on your own environment.</span></span>
* <span data-ttu-id="d4b23-233">Prepare your Python environment on a remote Ubuntu VM or a DSVM installing your dependencies.</span><span class="sxs-lookup"><span data-stu-id="d4b23-233">Prepare your Python environment on a remote Ubuntu VM or a DSVM installing your dependencies.</span></span>
* <span data-ttu-id="d4b23-234">Install Azure Machine Learning requirements using the following command.</span><span class="sxs-lookup"><span data-stu-id="d4b23-234">Install Azure Machine Learning requirements using the following command.</span></span>

```
pip install -I --index-url https://azuremldownloads.azureedge.net/python-repository/preview --extra-index-url https://pypi.python.org/simple azureml-requirements
```

>[!TIP]
><span data-ttu-id="d4b23-235">In some cases, you may need to run this command in sudo mode depending on your privileges.</span><span class="sxs-lookup"><span data-stu-id="d4b23-235">In some cases, you may need to run this command in sudo mode depending on your privileges.</span></span> 
```
sudo pip install -I --index-url https://azuremldownloads.azureedge.net/python-repository/preview --extra-index-url https://pypi.python.org/simple azureml-requirements
```
 
* <span data-ttu-id="d4b23-236">Use the following command to create both the compute target definition and run configuration for user-managed runs on remote VM executions.</span><span class="sxs-lookup"><span data-stu-id="d4b23-236">Use the following command to create both the compute target definition and run configuration for user-managed runs on remote VM executions.</span></span>
```
az ml computetarget attach remote --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --password "sshpassword" 
```
>[!NOTE]
><span data-ttu-id="d4b23-237">This will set "userManagedEnvironment" parameter in your .compute configuration file to true.</span><span class="sxs-lookup"><span data-stu-id="d4b23-237">This will set "userManagedEnvironment" parameter in your .compute configuration file to true.</span></span>

* <span data-ttu-id="d4b23-238">Set location of your Python runtime executable in your .compute file.</span><span class="sxs-lookup"><span data-stu-id="d4b23-238">Set location of your Python runtime executable in your .compute file.</span></span> <span data-ttu-id="d4b23-239">You should refer to the full path of your python executable.</span><span class="sxs-lookup"><span data-stu-id="d4b23-239">You should refer to the full path of your python executable.</span></span> 
```
pythonLocation: python3
```

<span data-ttu-id="d4b23-240">Once you configure the compute target, you can use the following command to run your script.</span><span class="sxs-lookup"><span data-stu-id="d4b23-240">Once you configure the compute target, you can use the following command to run your script.</span></span>
```
$ az ml experiment submit -c remotevm myscript.py
```

>[!NOTE]
> <span data-ttu-id="d4b23-241">When you are running on a DSVM, you should use the following commands</span><span class="sxs-lookup"><span data-stu-id="d4b23-241">When you are running on a DSVM, you should use the following commands</span></span>

<span data-ttu-id="d4b23-242">If you would like to run directly on DSVM's global python environment, run this command.</span><span class="sxs-lookup"><span data-stu-id="d4b23-242">If you would like to run directly on DSVM's global python environment, run this command.</span></span>
```
sudo /anaconda/envs/py35/bin/pip install <package>
```


## <a name="running-a-script-on-an-hdinsight-cluster"></a><span data-ttu-id="d4b23-243">Running a script on an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="d4b23-243">Running a script on an HDInsight cluster</span></span>
<span data-ttu-id="d4b23-244">HDInsight is a popular platform for big-data analytics supporting Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d4b23-244">HDInsight is a popular platform for big-data analytics supporting Apache Spark.</span></span> <span data-ttu-id="d4b23-245">Workbench enables experimentation on big data using HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="d4b23-245">Workbench enables experimentation on big data using HDInsight Spark clusters.</span></span> 

>[!NOTE]
><span data-ttu-id="d4b23-246">The HDInsight cluster must use Azure Blob as the primary storage.</span><span class="sxs-lookup"><span data-stu-id="d4b23-246">The HDInsight cluster must use Azure Blob as the primary storage.</span></span> <span data-ttu-id="d4b23-247">Using Azure Data Lake storage is not supported yet.</span><span class="sxs-lookup"><span data-stu-id="d4b23-247">Using Azure Data Lake storage is not supported yet.</span></span>

<span data-ttu-id="d4b23-248">You can create a compute target and run configuration for an HDInsight Spark cluster using the following command:</span><span class="sxs-lookup"><span data-stu-id="d4b23-248">You can create a compute target and run configuration for an HDInsight Spark cluster using the following command:</span></span>

```
$ az ml computetarget attach cluster --name "myhdi" --address "<FQDN or IP address>" --username "sshuser" --password "sshpassword"  
```

>[!NOTE]
><span data-ttu-id="d4b23-249">If you use FQDN instead of an IP address and your HDI Spark cluster is named _foo_, the SSH endpoint is on the driver node named _foo-ssh.azurehdinsight.net_.</span><span class="sxs-lookup"><span data-stu-id="d4b23-249">If you use FQDN instead of an IP address and your HDI Spark cluster is named _foo_, the SSH endpoint is on the driver node named _foo-ssh.azurehdinsight.net_.</span></span> <span data-ttu-id="d4b23-250">Don't forget the **-ssh** postfix in the server name when using FQDN for _--address_ parameter.</span><span class="sxs-lookup"><span data-stu-id="d4b23-250">Don't forget the **-ssh** postfix in the server name when using FQDN for _--address_ parameter.</span></span>


<span data-ttu-id="d4b23-251">Once you have the compute context, you can run the following command to execute your PySpark script.</span><span class="sxs-lookup"><span data-stu-id="d4b23-251">Once you have the compute context, you can run the following command to execute your PySpark script.</span></span>

```
$ az ml experiment submit -c myhdi myscript.py
```

<span data-ttu-id="d4b23-252">Workbench prepares and manages execution environment on HDInsight cluster using Conda.</span><span class="sxs-lookup"><span data-stu-id="d4b23-252">Workbench prepares and manages execution environment on HDInsight cluster using Conda.</span></span> <span data-ttu-id="d4b23-253">Configuration is managed by _conda_dependencies.yml_ and _spark_dependencies.yml_ configuration files.</span><span class="sxs-lookup"><span data-stu-id="d4b23-253">Configuration is managed by _conda_dependencies.yml_ and _spark_dependencies.yml_ configuration files.</span></span> 

<span data-ttu-id="d4b23-254">You need SSH access to the HDInsight cluster in order to execute experiments in this mode.</span><span class="sxs-lookup"><span data-stu-id="d4b23-254">You need SSH access to the HDInsight cluster in order to execute experiments in this mode.</span></span> 

>[!NOTE]
><span data-ttu-id="d4b23-255">Supported configuration is HDInsight Spark clusters running Linux (Ubuntu with Python/PySpark 3.5.2 and Spark 2.1.11).</span><span class="sxs-lookup"><span data-stu-id="d4b23-255">Supported configuration is HDInsight Spark clusters running Linux (Ubuntu with Python/PySpark 3.5.2 and Spark 2.1.11).</span></span>

<span data-ttu-id="d4b23-256">_**Overview of HDInsight-based execution for a PySpark script**_
![](media/experimentation-service-configuration/hdinsight-run.png)</span><span class="sxs-lookup"><span data-stu-id="d4b23-256">_**Overview of HDInsight-based execution for a PySpark script**_
![](media/experimentation-service-configuration/hdinsight-run.png)</span></span>


## <a name="running-a-script-on-gpu"></a><span data-ttu-id="d4b23-257">Running a script on GPU</span><span class="sxs-lookup"><span data-stu-id="d4b23-257">Running a script on GPU</span></span>
<span data-ttu-id="d4b23-258">To run your scripts on GPU, you can follow the guidance in this article:[How to use GPU in Azure Machine Learning](how-to-use-gpu.md)</span><span class="sxs-lookup"><span data-stu-id="d4b23-258">To run your scripts on GPU, you can follow the guidance in this article:[How to use GPU in Azure Machine Learning](how-to-use-gpu.md)</span></span>

## <a name="using-ssh-key-based-authentication-for-creating-and-using-compute-targets"></a><span data-ttu-id="d4b23-259">Using SSH Key-based authentication for creating and using compute targets</span><span class="sxs-lookup"><span data-stu-id="d4b23-259">Using SSH Key-based authentication for creating and using compute targets</span></span>
<span data-ttu-id="d4b23-260">Azure Machine Learning Workbench allows you to create and use compute targets using SSH Key-based authentication in addition to the username/password-based scheme.</span><span class="sxs-lookup"><span data-stu-id="d4b23-260">Azure Machine Learning Workbench allows you to create and use compute targets using SSH Key-based authentication in addition to the username/password-based scheme.</span></span> <span data-ttu-id="d4b23-261">You can use this capability when using remotedocker or cluster as your compute target.</span><span class="sxs-lookup"><span data-stu-id="d4b23-261">You can use this capability when using remotedocker or cluster as your compute target.</span></span> <span data-ttu-id="d4b23-262">When you use this scheme, the Workbench creates a public/private key pair and reports back the public key.</span><span class="sxs-lookup"><span data-stu-id="d4b23-262">When you use this scheme, the Workbench creates a public/private key pair and reports back the public key.</span></span> <span data-ttu-id="d4b23-263">You append the public key to the ~/.ssh/authorized_keys files for your username.</span><span class="sxs-lookup"><span data-stu-id="d4b23-263">You append the public key to the ~/.ssh/authorized_keys files for your username.</span></span> <span data-ttu-id="d4b23-264">Azure Machine Learning Workbench then uses ssh key-based authentication for accessing and executing on this compute target.</span><span class="sxs-lookup"><span data-stu-id="d4b23-264">Azure Machine Learning Workbench then uses ssh key-based authentication for accessing and executing on this compute target.</span></span> <span data-ttu-id="d4b23-265">Since the private key for the compute target is saved in the key store for the workspace, other users of the workspace can use the compute target the same way by providing the username provided for creating the compute target.</span><span class="sxs-lookup"><span data-stu-id="d4b23-265">Since the private key for the compute target is saved in the key store for the workspace, other users of the workspace can use the compute target the same way by providing the username provided for creating the compute target.</span></span>  

<span data-ttu-id="d4b23-266">You follow these steps to use this functionality.</span><span class="sxs-lookup"><span data-stu-id="d4b23-266">You follow these steps to use this functionality.</span></span> 

- <span data-ttu-id="d4b23-267">Create a compute target using one of the following commands.</span><span class="sxs-lookup"><span data-stu-id="d4b23-267">Create a compute target using one of the following commands.</span></span>

```
az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --use-azureml-ssh-key
```
<span data-ttu-id="d4b23-268">or</span><span class="sxs-lookup"><span data-stu-id="d4b23-268">or</span></span>
```
az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" -k
```
- <span data-ttu-id="d4b23-269">Append the public key generated by the Workbench to the ~/.ssh/authorized_keys file on the attached compute target.</span><span class="sxs-lookup"><span data-stu-id="d4b23-269">Append the public key generated by the Workbench to the ~/.ssh/authorized_keys file on the attached compute target.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="d4b23-270">You need to log on the compute target using the same username you used to create the compute target.</span><span class="sxs-lookup"><span data-stu-id="d4b23-270">You need to log on the compute target using the same username you used to create the compute target.</span></span> 

- <span data-ttu-id="d4b23-271">You can now prepare and use the compute target using SSH key-based authentication.</span><span class="sxs-lookup"><span data-stu-id="d4b23-271">You can now prepare and use the compute target using SSH key-based authentication.</span></span>

```
az ml experiment prepare -c remotevm
```

## <a name="next-steps"></a><span data-ttu-id="d4b23-272">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4b23-272">Next steps</span></span>
* [<span data-ttu-id="d4b23-273">Create and Install Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d4b23-273">Create and Install Azure Machine Learning</span></span>](../service/quickstart-installation.md)
* [<span data-ttu-id="d4b23-274">Model Management</span><span class="sxs-lookup"><span data-stu-id="d4b23-274">Model Management</span></span>](model-management-overview.md)
