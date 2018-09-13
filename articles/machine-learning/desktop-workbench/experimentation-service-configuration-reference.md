---
title: Azure Machine Learning Experimentation Service configuration files
description: This document details the configuration settings for Azure ML Experimentation Service.
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
ms.openlocfilehash: 43bee297b917143c9014b28049c6dfa28727b757
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866850"
---
# <a name="azure-machine-learning-experimentation-service-configuration-files"></a><span data-ttu-id="780ca-103">Azure Machine Learning Experimentation Service configuration files</span><span class="sxs-lookup"><span data-stu-id="780ca-103">Azure Machine Learning Experimentation Service configuration files</span></span>

<span data-ttu-id="780ca-104">When you run a script in Azure Machine Learning (Azure ML) Workbench, the behavior of the execution is controlled by files in the **aml_config** folder.</span><span class="sxs-lookup"><span data-stu-id="780ca-104">When you run a script in Azure Machine Learning (Azure ML) Workbench, the behavior of the execution is controlled by files in the **aml_config** folder.</span></span> <span data-ttu-id="780ca-105">This folder is under your project folder root.</span><span class="sxs-lookup"><span data-stu-id="780ca-105">This folder is under your project folder root.</span></span> <span data-ttu-id="780ca-106">It is important to understand the contents of these files in order to achieve the desired outcome for your execution in an optimal way.</span><span class="sxs-lookup"><span data-stu-id="780ca-106">It is important to understand the contents of these files in order to achieve the desired outcome for your execution in an optimal way.</span></span>

<span data-ttu-id="780ca-107">Following are the relevant files under this folder:</span><span class="sxs-lookup"><span data-stu-id="780ca-107">Following are the relevant files under this folder:</span></span>
- <span data-ttu-id="780ca-108">conda_dependencies.yml</span><span class="sxs-lookup"><span data-stu-id="780ca-108">conda_dependencies.yml</span></span>
- <span data-ttu-id="780ca-109">spark_dependencies.yml</span><span class="sxs-lookup"><span data-stu-id="780ca-109">spark_dependencies.yml</span></span>
- <span data-ttu-id="780ca-110">compute target files</span><span class="sxs-lookup"><span data-stu-id="780ca-110">compute target files</span></span>
    - <span data-ttu-id="780ca-111">\<compute target name>.compute</span><span class="sxs-lookup"><span data-stu-id="780ca-111">\<compute target name>.compute</span></span>
- <span data-ttu-id="780ca-112">run configuration files</span><span class="sxs-lookup"><span data-stu-id="780ca-112">run configuration files</span></span>
    - <span data-ttu-id="780ca-113">\<run configuration name>.runconfig</span><span class="sxs-lookup"><span data-stu-id="780ca-113">\<run configuration name>.runconfig</span></span>

>[!NOTE]
><span data-ttu-id="780ca-114">You typically have a compute target file and run configuration file for each compute target you create.</span><span class="sxs-lookup"><span data-stu-id="780ca-114">You typically have a compute target file and run configuration file for each compute target you create.</span></span> <span data-ttu-id="780ca-115">However, you can create these files independently and have multiple run configuration files pointing to the same compute target.</span><span class="sxs-lookup"><span data-stu-id="780ca-115">However, you can create these files independently and have multiple run configuration files pointing to the same compute target.</span></span>

## <a name="condadependenciesyml"></a><span data-ttu-id="780ca-116">conda_dependencies.yml</span><span class="sxs-lookup"><span data-stu-id="780ca-116">conda_dependencies.yml</span></span>
<span data-ttu-id="780ca-117">This file is a [conda environment file](https://conda.io/docs/using/envs.html#create-environment-file-by-hand) that specifies the Python runtime version and packages that your code depends on.</span><span class="sxs-lookup"><span data-stu-id="780ca-117">This file is a [conda environment file](https://conda.io/docs/using/envs.html#create-environment-file-by-hand) that specifies the Python runtime version and packages that your code depends on.</span></span> <span data-ttu-id="780ca-118">When Azure ML Workbench executes a script in a Docker container or HDInsight cluster, it creates a [conda environment](https://conda.io/docs/using/envs.html) for your script to run on.</span><span class="sxs-lookup"><span data-stu-id="780ca-118">When Azure ML Workbench executes a script in a Docker container or HDInsight cluster, it creates a [conda environment](https://conda.io/docs/using/envs.html) for your script to run on.</span></span> 

<span data-ttu-id="780ca-119">In this file, you specify Python packages that your script needs for execution.</span><span class="sxs-lookup"><span data-stu-id="780ca-119">In this file, you specify Python packages that your script needs for execution.</span></span> <span data-ttu-id="780ca-120">Azure ML  Experimentation Service creates the conda environment according to your list of dependencies.</span><span class="sxs-lookup"><span data-stu-id="780ca-120">Azure ML  Experimentation Service creates the conda environment according to your list of dependencies.</span></span> <span data-ttu-id="780ca-121">Packages listed here must be reachable by the execution engine through channels such as:</span><span class="sxs-lookup"><span data-stu-id="780ca-121">Packages listed here must be reachable by the execution engine through channels such as:</span></span>

* [<span data-ttu-id="780ca-122">continuum.io</span><span class="sxs-lookup"><span data-stu-id="780ca-122">continuum.io</span></span>](https://anaconda.org/conda-forge/repo)
* [<span data-ttu-id="780ca-123">PyPI</span><span class="sxs-lookup"><span data-stu-id="780ca-123">PyPI</span></span>](https://pypi.python.org/pypi)
* <span data-ttu-id="780ca-124">a publicly accessible endpoint (URL)</span><span class="sxs-lookup"><span data-stu-id="780ca-124">a publicly accessible endpoint (URL)</span></span>
* <span data-ttu-id="780ca-125">or a local file path</span><span class="sxs-lookup"><span data-stu-id="780ca-125">or a local file path</span></span>
* <span data-ttu-id="780ca-126">others reachable by the execution engine</span><span class="sxs-lookup"><span data-stu-id="780ca-126">others reachable by the execution engine</span></span>

>[!NOTE]
><span data-ttu-id="780ca-127">When running on HDInsight cluster, Azure ML Workbench creates a conda environment for your specific run.</span><span class="sxs-lookup"><span data-stu-id="780ca-127">When running on HDInsight cluster, Azure ML Workbench creates a conda environment for your specific run.</span></span> <span data-ttu-id="780ca-128">This allows different users to run on different python environments on the same cluster.</span><span class="sxs-lookup"><span data-stu-id="780ca-128">This allows different users to run on different python environments on the same cluster.</span></span>  

<span data-ttu-id="780ca-129">Here is an example of a typical **conda_dependencies.yml** file.</span><span class="sxs-lookup"><span data-stu-id="780ca-129">Here is an example of a typical **conda_dependencies.yml** file.</span></span>
```yaml
name: project_environment
dependencies:
  # Python version
  - python=3.5.2
  
  # some conda packages
  - scikit-learn
  - cryptography
  
  # use pip to install some more packages
  - pip:
     # a package in PyPi
     - azure-storage
     
     # a package hosted in a public URL endpoint
     - https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
     
     # a wheel file available locally on disk (this only works if you are executing against local Docker target)
     - C:\temp\my_private_python_pkg.whl
```

<span data-ttu-id="780ca-130">Azure ML Workbench uses the same conda environment without rebuilding it as long as the **conda_dependencies.yml** remains the same.</span><span class="sxs-lookup"><span data-stu-id="780ca-130">Azure ML Workbench uses the same conda environment without rebuilding it as long as the **conda_dependencies.yml** remains the same.</span></span> <span data-ttu-id="780ca-131">It will rebuild your environment if your dependencies change.</span><span class="sxs-lookup"><span data-stu-id="780ca-131">It will rebuild your environment if your dependencies change.</span></span>

>[!NOTE]
><span data-ttu-id="780ca-132">If you target execution against _local_ compute context, **conda_dependencies.yml** file is **not** used.</span><span class="sxs-lookup"><span data-stu-id="780ca-132">If you target execution against _local_ compute context, **conda_dependencies.yml** file is **not** used.</span></span> <span data-ttu-id="780ca-133">Package dependencies for your local Azure ML Workbench Python environment need to be installed manually.</span><span class="sxs-lookup"><span data-stu-id="780ca-133">Package dependencies for your local Azure ML Workbench Python environment need to be installed manually.</span></span>

## <a name="sparkdependenciesyml"></a><span data-ttu-id="780ca-134">spark_dependencies.yml</span><span class="sxs-lookup"><span data-stu-id="780ca-134">spark_dependencies.yml</span></span>
<span data-ttu-id="780ca-135">This file specifies the Spark application name when you submit a PySpark script and Spark packages that need to be installed.</span><span class="sxs-lookup"><span data-stu-id="780ca-135">This file specifies the Spark application name when you submit a PySpark script and Spark packages that need to be installed.</span></span> <span data-ttu-id="780ca-136">You can also specify a public Maven repository as well as Spark packages that can be found in those Maven repositories.</span><span class="sxs-lookup"><span data-stu-id="780ca-136">You can also specify a public Maven repository as well as Spark packages that can be found in those Maven repositories.</span></span>

<span data-ttu-id="780ca-137">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="780ca-137">Here is an example:</span></span>

```yaml
configuration:
  # Spark application name
  "spark.app.name": "ClassifyingIris"
  
repositories:
  # Maven repository hosted in Azure CDN
  - "https://mmlspark.azureedge.net/maven"
  
  # Maven repository hosted in spark-packages.org
  - "https://spark-packages.org/packages"
  
packages:
  # MMLSpark package hosted in the Azure CDN Maven
  - group: "com.microsoft.ml.spark"
    artifact: "mmlspark_2.11"
    version: "0.5"
    
  # spark-sklearn packaged hosted in the spark-packages.org Maven
  - group: "databricks"
    artifact: "spark-sklearn"
    version: "0.2.0"
```

>[!NOTE]
><span data-ttu-id="780ca-138">Cluster tuning parameters such as worker size and cores should go into "configuration" section in the spark_dependecies.yml file</span><span class="sxs-lookup"><span data-stu-id="780ca-138">Cluster tuning parameters such as worker size and cores should go into "configuration" section in the spark_dependecies.yml file</span></span> 

>[!NOTE]
><span data-ttu-id="780ca-139">If you are executing the script in Python environment, *spark_dependencies.yml* file is ignored.</span><span class="sxs-lookup"><span data-stu-id="780ca-139">If you are executing the script in Python environment, *spark_dependencies.yml* file is ignored.</span></span> <span data-ttu-id="780ca-140">It is used only if you are running against Spark (either on Docker or HDInsight Cluster).</span><span class="sxs-lookup"><span data-stu-id="780ca-140">It is used only if you are running against Spark (either on Docker or HDInsight Cluster).</span></span>

## <a name="run-configuration"></a><span data-ttu-id="780ca-141">Run configuration</span><span class="sxs-lookup"><span data-stu-id="780ca-141">Run configuration</span></span>
<span data-ttu-id="780ca-142">To specify a particular run configuration, you need a .compute file and a .runconfig file.</span><span class="sxs-lookup"><span data-stu-id="780ca-142">To specify a particular run configuration, you need a .compute file and a .runconfig file.</span></span> <span data-ttu-id="780ca-143">These are typically generated using a CLI command.</span><span class="sxs-lookup"><span data-stu-id="780ca-143">These are typically generated using a CLI command.</span></span> <span data-ttu-id="780ca-144">You can also clone exiting ones, rename them, and edit them.</span><span class="sxs-lookup"><span data-stu-id="780ca-144">You can also clone exiting ones, rename them, and edit them.</span></span>

```azurecli
# create a compute target pointing to a VM via SSH
$ az ml computetarget attach remotedocker -n <compute target name> -a <IP address or FQDN of VM> -u <username> -w <password>

# create a compute context pointing to an HDI cluster head-node via SSH
$ az ml computetarget attach cluster -n <compute target name> -a <IP address or FQDN of HDI cluster> -u <username> -w <password> 
```

<span data-ttu-id="780ca-145">This command creates a pair of files based on the compute target specified.</span><span class="sxs-lookup"><span data-stu-id="780ca-145">This command creates a pair of files based on the compute target specified.</span></span> <span data-ttu-id="780ca-146">Let's say you named your compute target _foo_.</span><span class="sxs-lookup"><span data-stu-id="780ca-146">Let's say you named your compute target _foo_.</span></span> <span data-ttu-id="780ca-147">This command generates _foo.compute_ and _foo.runconfig_ in your **aml_config** folder.</span><span class="sxs-lookup"><span data-stu-id="780ca-147">This command generates _foo.compute_ and _foo.runconfig_ in your **aml_config** folder.</span></span>

>[!NOTE]
> <span data-ttu-id="780ca-148">_local_ or _docker_ names for the run configuration files are arbitrary.</span><span class="sxs-lookup"><span data-stu-id="780ca-148">_local_ or _docker_ names for the run configuration files are arbitrary.</span></span> <span data-ttu-id="780ca-149">Azure ML Workbench adds these two run configurations when you create a blank project for your convenience.</span><span class="sxs-lookup"><span data-stu-id="780ca-149">Azure ML Workbench adds these two run configurations when you create a blank project for your convenience.</span></span> <span data-ttu-id="780ca-150">You can rename "<run configuration name>.runconfig" files that come with the project template, or create new ones with any name you want.</span><span class="sxs-lookup"><span data-stu-id="780ca-150">You can rename "<run configuration name>.runconfig" files that come with the project template, or create new ones with any name you want.</span></span>

### <a name="compute-target-namecompute"></a><span data-ttu-id="780ca-151">\<compute target name>.compute</span><span class="sxs-lookup"><span data-stu-id="780ca-151">\<compute target name>.compute</span></span>
<span data-ttu-id="780ca-152">_\<compute target name>.compute_ file specifies connection and configuration information for the compute target.</span><span class="sxs-lookup"><span data-stu-id="780ca-152">_\<compute target name>.compute_ file specifies connection and configuration information for the compute target.</span></span> <span data-ttu-id="780ca-153">It is a list of name-value pairs.</span><span class="sxs-lookup"><span data-stu-id="780ca-153">It is a list of name-value pairs.</span></span> <span data-ttu-id="780ca-154">Following are the supported settings:</span><span class="sxs-lookup"><span data-stu-id="780ca-154">Following are the supported settings:</span></span>

<span data-ttu-id="780ca-155">**type**: Type of the compute environment.</span><span class="sxs-lookup"><span data-stu-id="780ca-155">**type**: Type of the compute environment.</span></span> <span data-ttu-id="780ca-156">Supported values are:</span><span class="sxs-lookup"><span data-stu-id="780ca-156">Supported values are:</span></span>
  - <span data-ttu-id="780ca-157">local</span><span class="sxs-lookup"><span data-stu-id="780ca-157">local</span></span>
  - <span data-ttu-id="780ca-158">remote</span><span class="sxs-lookup"><span data-stu-id="780ca-158">remote</span></span>
  - <span data-ttu-id="780ca-159">docker</span><span class="sxs-lookup"><span data-stu-id="780ca-159">docker</span></span>
  - <span data-ttu-id="780ca-160">remotedocker</span><span class="sxs-lookup"><span data-stu-id="780ca-160">remotedocker</span></span>
  - <span data-ttu-id="780ca-161">cluster</span><span class="sxs-lookup"><span data-stu-id="780ca-161">cluster</span></span>

<span data-ttu-id="780ca-162">**baseDockerImage**: The Docker image used to run the Python/PySpark script.</span><span class="sxs-lookup"><span data-stu-id="780ca-162">**baseDockerImage**: The Docker image used to run the Python/PySpark script.</span></span> <span data-ttu-id="780ca-163">The default value is _microsoft/mmlspark:plus-0.7.91_.</span><span class="sxs-lookup"><span data-stu-id="780ca-163">The default value is _microsoft/mmlspark:plus-0.7.91_.</span></span> <span data-ttu-id="780ca-164">We also support one other image: _microsoft/mmlspark:plus-gpu-0.7.91_, which gives you GPU access to the host machine (if GPU is present).</span><span class="sxs-lookup"><span data-stu-id="780ca-164">We also support one other image: _microsoft/mmlspark:plus-gpu-0.7.91_, which gives you GPU access to the host machine (if GPU is present).</span></span>

<span data-ttu-id="780ca-165">**address**: The IP address, or FQDN (fully qualified domain name) of the virtual machine, or HDInsight cluster head-node.</span><span class="sxs-lookup"><span data-stu-id="780ca-165">**address**: The IP address, or FQDN (fully qualified domain name) of the virtual machine, or HDInsight cluster head-node.</span></span>

<span data-ttu-id="780ca-166">**username**: The SSH username for accessing the virtual machine or the HDInsight head-node.</span><span class="sxs-lookup"><span data-stu-id="780ca-166">**username**: The SSH username for accessing the virtual machine or the HDInsight head-node.</span></span>

<span data-ttu-id="780ca-167">**password**: The encrypted password for the SSH connection.</span><span class="sxs-lookup"><span data-stu-id="780ca-167">**password**: The encrypted password for the SSH connection.</span></span>

<span data-ttu-id="780ca-168">**sharedVolumes**: Flag to signal that execution engine should use Docker shared volume feature to ship project files back and forth.</span><span class="sxs-lookup"><span data-stu-id="780ca-168">**sharedVolumes**: Flag to signal that execution engine should use Docker shared volume feature to ship project files back and forth.</span></span> <span data-ttu-id="780ca-169">Having this flag turned on can speed up execution since Docker can access projects directly without the need to copy them.</span><span class="sxs-lookup"><span data-stu-id="780ca-169">Having this flag turned on can speed up execution since Docker can access projects directly without the need to copy them.</span></span> <span data-ttu-id="780ca-170">It is best to set _false_ if the Docker engine is running on Windows since volume sharing for Docker on Windows can be flaky.</span><span class="sxs-lookup"><span data-stu-id="780ca-170">It is best to set _false_ if the Docker engine is running on Windows since volume sharing for Docker on Windows can be flaky.</span></span> <span data-ttu-id="780ca-171">Set it to _true_ if it is running on macOS or Linux.</span><span class="sxs-lookup"><span data-stu-id="780ca-171">Set it to _true_ if it is running on macOS or Linux.</span></span>

<span data-ttu-id="780ca-172">**nvidiaDocker**: This flag, when set to _true_, tells the Azure ML Experimentation Service to use _nvidia-docker_ command, as opposed to the regular _docker_ command, to launch the Docker image.</span><span class="sxs-lookup"><span data-stu-id="780ca-172">**nvidiaDocker**: This flag, when set to _true_, tells the Azure ML Experimentation Service to use _nvidia-docker_ command, as opposed to the regular _docker_ command, to launch the Docker image.</span></span> <span data-ttu-id="780ca-173">The _nvidia-docker_ engine allows the Docker container to access GPU hardware.</span><span class="sxs-lookup"><span data-stu-id="780ca-173">The _nvidia-docker_ engine allows the Docker container to access GPU hardware.</span></span> <span data-ttu-id="780ca-174">The setting is required if you want to run GPU execution in the Docker container.</span><span class="sxs-lookup"><span data-stu-id="780ca-174">The setting is required if you want to run GPU execution in the Docker container.</span></span> <span data-ttu-id="780ca-175">Only Linux host supports _nvidia-docker_.</span><span class="sxs-lookup"><span data-stu-id="780ca-175">Only Linux host supports _nvidia-docker_.</span></span> <span data-ttu-id="780ca-176">For example, Linux-based DSVM in Azure ships with _nvidia-docker_.</span><span class="sxs-lookup"><span data-stu-id="780ca-176">For example, Linux-based DSVM in Azure ships with _nvidia-docker_.</span></span> <span data-ttu-id="780ca-177">_nvidia-docker_ as of now is not supported on Windows.</span><span class="sxs-lookup"><span data-stu-id="780ca-177">_nvidia-docker_ as of now is not supported on Windows.</span></span>

<span data-ttu-id="780ca-178">**nativeSharedDirectory**: This property specifies the base directory (For example: _~/.azureml/share/_) where files can be saved in order to be shared across runs on the same compute target.</span><span class="sxs-lookup"><span data-stu-id="780ca-178">**nativeSharedDirectory**: This property specifies the base directory (For example: _~/.azureml/share/_) where files can be saved in order to be shared across runs on the same compute target.</span></span> <span data-ttu-id="780ca-179">If this setting is used when running on a Docker container, _sharedVolumes_ must be set to true.</span><span class="sxs-lookup"><span data-stu-id="780ca-179">If this setting is used when running on a Docker container, _sharedVolumes_ must be set to true.</span></span> <span data-ttu-id="780ca-180">Otherwise, execution fails.</span><span class="sxs-lookup"><span data-stu-id="780ca-180">Otherwise, execution fails.</span></span>

<span data-ttu-id="780ca-181">**userManagedEnvironment**: This property specifies whether this compute target is managed by the user directly or managed through experimentation service.</span><span class="sxs-lookup"><span data-stu-id="780ca-181">**userManagedEnvironment**: This property specifies whether this compute target is managed by the user directly or managed through experimentation service.</span></span>  

<span data-ttu-id="780ca-182">**pythonLocation**: This property specifies the location of the python runtime to be used on the compute target to execute user's program.</span><span class="sxs-lookup"><span data-stu-id="780ca-182">**pythonLocation**: This property specifies the location of the python runtime to be used on the compute target to execute user's program.</span></span> 

### <a name="run-configuration-namerunconfig"></a><span data-ttu-id="780ca-183">\<run configuration name>.runconfig</span><span class="sxs-lookup"><span data-stu-id="780ca-183">\<run configuration name>.runconfig</span></span>
<span data-ttu-id="780ca-184">_\<run configuration name>.runconfig_ specifies the Azure ML experiment execution behavior.</span><span class="sxs-lookup"><span data-stu-id="780ca-184">_\<run configuration name>.runconfig_ specifies the Azure ML experiment execution behavior.</span></span> <span data-ttu-id="780ca-185">You can configure execution behavior such as tracking run history or what compute target to use along with many others.</span><span class="sxs-lookup"><span data-stu-id="780ca-185">You can configure execution behavior such as tracking run history or what compute target to use along with many others.</span></span> <span data-ttu-id="780ca-186">The names of the run configuration files are used to populate the execution context dropdown in the Azure ML Workbench desktop application.</span><span class="sxs-lookup"><span data-stu-id="780ca-186">The names of the run configuration files are used to populate the execution context dropdown in the Azure ML Workbench desktop application.</span></span>

<span data-ttu-id="780ca-187">**ArgumentVector**: This section specifies the script to be run as part of this execution and the parameters for the script.</span><span class="sxs-lookup"><span data-stu-id="780ca-187">**ArgumentVector**: This section specifies the script to be run as part of this execution and the parameters for the script.</span></span> <span data-ttu-id="780ca-188">For example, if you have the following snippet in your "<run configuration name>.runconfig" file</span><span class="sxs-lookup"><span data-stu-id="780ca-188">For example, if you have the following snippet in your "<run configuration name>.runconfig" file</span></span> 

```
 "ArgumentVector":[
  - "myscript.py"
  - 234
  - "-v" 
 ] 
```
<span data-ttu-id="780ca-189">_"az ml experiment submit foo.runconfig"_  automatically runs the command with _myscript.py_ file passing in 234 as a parameter and sets the --verbose flag.</span><span class="sxs-lookup"><span data-stu-id="780ca-189">_"az ml experiment submit foo.runconfig"_  automatically runs the command with _myscript.py_ file passing in 234 as a parameter and sets the --verbose flag.</span></span>

<span data-ttu-id="780ca-190">**Target**: This parameter is the name of the _.compute_ file that the _runconfig_ file references.</span><span class="sxs-lookup"><span data-stu-id="780ca-190">**Target**: This parameter is the name of the _.compute_ file that the _runconfig_ file references.</span></span> <span data-ttu-id="780ca-191">It generally points the _foo.compute_ file but you can edit it to point to a different compute target.</span><span class="sxs-lookup"><span data-stu-id="780ca-191">It generally points the _foo.compute_ file but you can edit it to point to a different compute target.</span></span>

<span data-ttu-id="780ca-192">**Environment Variables**: This section enables users to set environment variables as part of their runs.</span><span class="sxs-lookup"><span data-stu-id="780ca-192">**Environment Variables**: This section enables users to set environment variables as part of their runs.</span></span> <span data-ttu-id="780ca-193">User can specify environment variables using name-value pairs in the following format:</span><span class="sxs-lookup"><span data-stu-id="780ca-193">User can specify environment variables using name-value pairs in the following format:</span></span>
```
EnvironmentVariables:
  "EXAMPLE_ENV_VAR1": "Example Value1"
  "EXAMPLE_ENV_VAR2": "Example Value2"
```

<span data-ttu-id="780ca-194">These environment variables can be accessed in user's code.</span><span class="sxs-lookup"><span data-stu-id="780ca-194">These environment variables can be accessed in user's code.</span></span> <span data-ttu-id="780ca-195">For example, this Python code prints the environment variable named "EXAMPLE_ENV_VAR"</span><span class="sxs-lookup"><span data-stu-id="780ca-195">For example, this Python code prints the environment variable named "EXAMPLE_ENV_VAR"</span></span>
```
print(os.environ.get("EXAMPLE_ENV_VAR1"))
```

<span data-ttu-id="780ca-196">**Framework**: This property specifies if Azure ML Workbench should launch a Spark session to run the script.</span><span class="sxs-lookup"><span data-stu-id="780ca-196">**Framework**: This property specifies if Azure ML Workbench should launch a Spark session to run the script.</span></span> <span data-ttu-id="780ca-197">The default value is _PySpark_.</span><span class="sxs-lookup"><span data-stu-id="780ca-197">The default value is _PySpark_.</span></span> <span data-ttu-id="780ca-198">Set it to _Python_ if you are not running PySpark code, which can help launching the job quicker with less overhead.</span><span class="sxs-lookup"><span data-stu-id="780ca-198">Set it to _Python_ if you are not running PySpark code, which can help launching the job quicker with less overhead.</span></span>

<span data-ttu-id="780ca-199">**CondaDependenciesFile**: This property points to the file that specifies the conda environment dependencies in the *aml_config* folder.</span><span class="sxs-lookup"><span data-stu-id="780ca-199">**CondaDependenciesFile**: This property points to the file that specifies the conda environment dependencies in the *aml_config* folder.</span></span> <span data-ttu-id="780ca-200">If set to _null_, it points to the default **conda_dependencies.yml** file.</span><span class="sxs-lookup"><span data-stu-id="780ca-200">If set to _null_, it points to the default **conda_dependencies.yml** file.</span></span>

<span data-ttu-id="780ca-201">**SparkDependenciesFile**: This property points to the file that specifies the Spark dependencies in the **aml_config** folder.</span><span class="sxs-lookup"><span data-stu-id="780ca-201">**SparkDependenciesFile**: This property points to the file that specifies the Spark dependencies in the **aml_config** folder.</span></span> <span data-ttu-id="780ca-202">It is set to _null_ by default and it points to the default **spark_dependencies.yml** file.</span><span class="sxs-lookup"><span data-stu-id="780ca-202">It is set to _null_ by default and it points to the default **spark_dependencies.yml** file.</span></span>

<span data-ttu-id="780ca-203">**PrepareEnvironment**: This property, when set to _true_, tells the Experimentation Service to prepare the conda environment based on the conda dependencies specified as part of your initial run.</span><span class="sxs-lookup"><span data-stu-id="780ca-203">**PrepareEnvironment**: This property, when set to _true_, tells the Experimentation Service to prepare the conda environment based on the conda dependencies specified as part of your initial run.</span></span> <span data-ttu-id="780ca-204">This property is effective only when you execute against a Docker environment.</span><span class="sxs-lookup"><span data-stu-id="780ca-204">This property is effective only when you execute against a Docker environment.</span></span> <span data-ttu-id="780ca-205">This setting has no effect if you are running against a _local_ environment.</span><span class="sxs-lookup"><span data-stu-id="780ca-205">This setting has no effect if you are running against a _local_ environment.</span></span> 

<span data-ttu-id="780ca-206">**TrackedRun**: This flag signals the Experimentation Service whether or not to track the run in Azure ML Workbench run history infrastructure.</span><span class="sxs-lookup"><span data-stu-id="780ca-206">**TrackedRun**: This flag signals the Experimentation Service whether or not to track the run in Azure ML Workbench run history infrastructure.</span></span> <span data-ttu-id="780ca-207">The default value is _true_.</span><span class="sxs-lookup"><span data-stu-id="780ca-207">The default value is _true_.</span></span> 

<span data-ttu-id="780ca-208">**UseSampling**: _UseSampling_ specifies whether the active sample datasets for data sources are used for the run.</span><span class="sxs-lookup"><span data-stu-id="780ca-208">**UseSampling**: _UseSampling_ specifies whether the active sample datasets for data sources are used for the run.</span></span> <span data-ttu-id="780ca-209">If set to _false_, data sources ingest and use the full data read from the data store.</span><span class="sxs-lookup"><span data-stu-id="780ca-209">If set to _false_, data sources ingest and use the full data read from the data store.</span></span> <span data-ttu-id="780ca-210">If set to _true_, active samples are used.</span><span class="sxs-lookup"><span data-stu-id="780ca-210">If set to _true_, active samples are used.</span></span> <span data-ttu-id="780ca-211">Users can use the **DataSourceSettings** to specify which specific sample datasets to use if they want to override the active sample.</span><span class="sxs-lookup"><span data-stu-id="780ca-211">Users can use the **DataSourceSettings** to specify which specific sample datasets to use if they want to override the active sample.</span></span> 

<span data-ttu-id="780ca-212">**DataSourceSettings**: This configuration section specifies the data source settings.</span><span class="sxs-lookup"><span data-stu-id="780ca-212">**DataSourceSettings**: This configuration section specifies the data source settings.</span></span> <span data-ttu-id="780ca-213">In this section, user specifies which existing data sample for a particular data source is used as part of the run.</span><span class="sxs-lookup"><span data-stu-id="780ca-213">In this section, user specifies which existing data sample for a particular data source is used as part of the run.</span></span> 

<span data-ttu-id="780ca-214">The following configuration setting specifies that sample named "MySample" is used for the data source named "MyDataSource"</span><span class="sxs-lookup"><span data-stu-id="780ca-214">The following configuration setting specifies that sample named "MySample" is used for the data source named "MyDataSource"</span></span>
```
DataSourceSettings:
    MyDataSource.dsource:
    Sampling:
    Sample: MySample
```

<span data-ttu-id="780ca-215">**DataSourceSubstitutions**: Data source substitutions can be used when the user wants to switch from one data source to another without changing their code.</span><span class="sxs-lookup"><span data-stu-id="780ca-215">**DataSourceSubstitutions**: Data source substitutions can be used when the user wants to switch from one data source to another without changing their code.</span></span> <span data-ttu-id="780ca-216">For example, users can switch from a sampled-down, local file to the original, larger dataset stored in Azure Blob by changing the data source reference.</span><span class="sxs-lookup"><span data-stu-id="780ca-216">For example, users can switch from a sampled-down, local file to the original, larger dataset stored in Azure Blob by changing the data source reference.</span></span> <span data-ttu-id="780ca-217">When a substitution is used, Azure ML Workbench runs your data sources and data preparation packages by referencing the substitute data source.</span><span class="sxs-lookup"><span data-stu-id="780ca-217">When a substitution is used, Azure ML Workbench runs your data sources and data preparation packages by referencing the substitute data source.</span></span>

<span data-ttu-id="780ca-218">The following example replaces the "mylocal.datasource" references in Azure ML data sources and data preparation packages with "myremote.dsource".</span><span class="sxs-lookup"><span data-stu-id="780ca-218">The following example replaces the "mylocal.datasource" references in Azure ML data sources and data preparation packages with "myremote.dsource".</span></span> 
 
```
DataSourceSubstitutions:
    mylocal.dsource: myremote.dsource
```

<span data-ttu-id="780ca-219">Based on the substitution above, the following code sample now reads from "myremote.dsource" instead of "mylocal.dsource" without users changing their code.</span><span class="sxs-lookup"><span data-stu-id="780ca-219">Based on the substitution above, the following code sample now reads from "myremote.dsource" instead of "mylocal.dsource" without users changing their code.</span></span>
```
df = datasource.load_datasource('mylocal.dsource')
```
## <a name="next-steps"></a><span data-ttu-id="780ca-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="780ca-220">Next steps</span></span>
<span data-ttu-id="780ca-221">Learn more about [Experimentation Service configuration](experimentation-service-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="780ca-221">Learn more about [Experimentation Service configuration](experimentation-service-configuration.md).</span></span>
