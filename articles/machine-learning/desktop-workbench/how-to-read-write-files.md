---
title: Read and write large data files | Microsoft Docs
description: Read and write large files in Azure Machine Learning experiments.
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/10/2017
ms.openlocfilehash: 5a772f8792c02139e45977e207b5be4bebc63a9c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866325"
---
# <a name="persisting-changes-and-working-with-large-files"></a><span data-ttu-id="78499-103">Persisting changes and working with large files</span><span class="sxs-lookup"><span data-stu-id="78499-103">Persisting changes and working with large files</span></span>
<span data-ttu-id="78499-104">With the Azure Machine Learning Experimentation service, you can configure a variety of execution targets.</span><span class="sxs-lookup"><span data-stu-id="78499-104">With the Azure Machine Learning Experimentation service, you can configure a variety of execution targets.</span></span> <span data-ttu-id="78499-105">Some targets are local, such as a local computer or a Docker container on a local computer.</span><span class="sxs-lookup"><span data-stu-id="78499-105">Some targets are local, such as a local computer or a Docker container on a local computer.</span></span> <span data-ttu-id="78499-106">Others are remote, such as a Docker container on a remote machine or an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78499-106">Others are remote, such as a Docker container on a remote machine or an HDInsight cluster.</span></span> <span data-ttu-id="78499-107">For more information, see [Overview of Azure Machine Learning experiment execution service](experimentation-service-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="78499-107">For more information, see [Overview of Azure Machine Learning experiment execution service](experimentation-service-configuration.md).</span></span> 

<span data-ttu-id="78499-108">Before you can execute on a target, you must copy the project folder to the compute target.</span><span class="sxs-lookup"><span data-stu-id="78499-108">Before you can execute on a target, you must copy the project folder to the compute target.</span></span> <span data-ttu-id="78499-109">You must do so even with a local execution that uses a local temp folder for this purpose.</span><span class="sxs-lookup"><span data-stu-id="78499-109">You must do so even with a local execution that uses a local temp folder for this purpose.</span></span> 

## <a name="execution-isolation-portability-and-reproducibility"></a><span data-ttu-id="78499-110">Execution isolation, portability, and reproducibility</span><span class="sxs-lookup"><span data-stu-id="78499-110">Execution isolation, portability, and reproducibility</span></span>
<span data-ttu-id="78499-111">The purpose of this design is to ensure the isolation, reproducibility, and portability of the execution.</span><span class="sxs-lookup"><span data-stu-id="78499-111">The purpose of this design is to ensure the isolation, reproducibility, and portability of the execution.</span></span> <span data-ttu-id="78499-112">If you execute the same script twice, on the same or another compute target, you receive the same results.</span><span class="sxs-lookup"><span data-stu-id="78499-112">If you execute the same script twice, on the same or another compute target, you receive the same results.</span></span> <span data-ttu-id="78499-113">The changes made during the first execution shouldn't affect those in the second execution.</span><span class="sxs-lookup"><span data-stu-id="78499-113">The changes made during the first execution shouldn't affect those in the second execution.</span></span> <span data-ttu-id="78499-114">With this design, you can treat compute targets as stateless computation resources, each having no affinity to the jobs that are executed after they are finished.</span><span class="sxs-lookup"><span data-stu-id="78499-114">With this design, you can treat compute targets as stateless computation resources, each having no affinity to the jobs that are executed after they are finished.</span></span>

## <a name="challenges"></a><span data-ttu-id="78499-115">Challenges</span><span class="sxs-lookup"><span data-stu-id="78499-115">Challenges</span></span>
<span data-ttu-id="78499-116">Even though this design provides the benefits of portability and repeatability, it also brings some unique challenges.</span><span class="sxs-lookup"><span data-stu-id="78499-116">Even though this design provides the benefits of portability and repeatability, it also brings some unique challenges.</span></span>

### <a name="persisting-state-changes"></a><span data-ttu-id="78499-117">Persisting state changes</span><span class="sxs-lookup"><span data-stu-id="78499-117">Persisting state changes</span></span>
<span data-ttu-id="78499-118">If your script modifies the state of the compute context, the changes are not persisted for your next execution, and they're not propagated back to the client machine automatically.</span><span class="sxs-lookup"><span data-stu-id="78499-118">If your script modifies the state of the compute context, the changes are not persisted for your next execution, and they're not propagated back to the client machine automatically.</span></span> 

<span data-ttu-id="78499-119">More specifically, if your script creates a subfolder or writes a file, that folder or file will not be present in your project directory after execution.</span><span class="sxs-lookup"><span data-stu-id="78499-119">More specifically, if your script creates a subfolder or writes a file, that folder or file will not be present in your project directory after execution.</span></span> <span data-ttu-id="78499-120">The files are stored in a temp folder in the compute target environment.</span><span class="sxs-lookup"><span data-stu-id="78499-120">The files are stored in a temp folder in the compute target environment.</span></span> <span data-ttu-id="78499-121">You might use them for debugging purposes, but you cannot rely on their permanent existence.</span><span class="sxs-lookup"><span data-stu-id="78499-121">You might use them for debugging purposes, but you cannot rely on their permanent existence.</span></span>

### <a name="working-with-large-files-in-the-project-folder"></a><span data-ttu-id="78499-122">Working with large files in the project folder</span><span class="sxs-lookup"><span data-stu-id="78499-122">Working with large files in the project folder</span></span>

<span data-ttu-id="78499-123">If your project folder contains any large files, you incur latency when the folder is copied to the target compute environment at the beginning of an execution.</span><span class="sxs-lookup"><span data-stu-id="78499-123">If your project folder contains any large files, you incur latency when the folder is copied to the target compute environment at the beginning of an execution.</span></span> <span data-ttu-id="78499-124">Even if the execution happens locally, there is still unnecessary disk traffic to avoid.</span><span class="sxs-lookup"><span data-stu-id="78499-124">Even if the execution happens locally, there is still unnecessary disk traffic to avoid.</span></span> <span data-ttu-id="78499-125">For this reason, we currently cap the maximum project size at 25 MB.</span><span class="sxs-lookup"><span data-stu-id="78499-125">For this reason, we currently cap the maximum project size at 25 MB.</span></span>

## <a name="option-1-use-the-outputs-folder"></a><span data-ttu-id="78499-126">Option 1: Use the *outputs* folder</span><span class="sxs-lookup"><span data-stu-id="78499-126">Option 1: Use the *outputs* folder</span></span>
<span data-ttu-id="78499-127">This option is preferable if all the following conditions apply:</span><span class="sxs-lookup"><span data-stu-id="78499-127">This option is preferable if all the following conditions apply:</span></span>
* <span data-ttu-id="78499-128">Your script produces files.</span><span class="sxs-lookup"><span data-stu-id="78499-128">Your script produces files.</span></span>
* <span data-ttu-id="78499-129">You expect the files to change with every experiment.</span><span class="sxs-lookup"><span data-stu-id="78499-129">You expect the files to change with every experiment.</span></span>
* <span data-ttu-id="78499-130">You want to keep a history of these files.</span><span class="sxs-lookup"><span data-stu-id="78499-130">You want to keep a history of these files.</span></span> 

<span data-ttu-id="78499-131">The common use cases are:</span><span class="sxs-lookup"><span data-stu-id="78499-131">The common use cases are:</span></span>
* <span data-ttu-id="78499-132">Training a model</span><span class="sxs-lookup"><span data-stu-id="78499-132">Training a model</span></span>
* <span data-ttu-id="78499-133">Creating a dataset</span><span class="sxs-lookup"><span data-stu-id="78499-133">Creating a dataset</span></span>
* <span data-ttu-id="78499-134">Plotting a graph as an image file as part of your model-training execution</span><span class="sxs-lookup"><span data-stu-id="78499-134">Plotting a graph as an image file as part of your model-training execution</span></span> 

<span data-ttu-id="78499-135">Additionally, you want to compare the outputs across runs, select an output file (such as a model) that was produced by a previous run, and then use it for a subsequent task (such as scoring).</span><span class="sxs-lookup"><span data-stu-id="78499-135">Additionally, you want to compare the outputs across runs, select an output file (such as a model) that was produced by a previous run, and then use it for a subsequent task (such as scoring).</span></span>

<span data-ttu-id="78499-136">You can write files to a folder named *outputs* that's relative to the root directory.</span><span class="sxs-lookup"><span data-stu-id="78499-136">You can write files to a folder named *outputs* that's relative to the root directory.</span></span> <span data-ttu-id="78499-137">The folder receives special treatment by the Experimentation service.</span><span class="sxs-lookup"><span data-stu-id="78499-137">The folder receives special treatment by the Experimentation service.</span></span> <span data-ttu-id="78499-138">Anything your script creates in the folder during the execution, such as a model file, data file, or plotted image file (collectively known as _artifacts_), is copied to the Azure Blob storage account that's associated with your experimentation account after the run is finished.</span><span class="sxs-lookup"><span data-stu-id="78499-138">Anything your script creates in the folder during the execution, such as a model file, data file, or plotted image file (collectively known as _artifacts_), is copied to the Azure Blob storage account that's associated with your experimentation account after the run is finished.</span></span> <span data-ttu-id="78499-139">The files become part of your run history record.</span><span class="sxs-lookup"><span data-stu-id="78499-139">The files become part of your run history record.</span></span>

<span data-ttu-id="78499-140">Here is a short example of code for storing a model in the *outputs* folder:</span><span class="sxs-lookup"><span data-stu-id="78499-140">Here is a short example of code for storing a model in the *outputs* folder:</span></span>
```python
import os
import pickle

# m is a scikit-learn model. 
# we serialize it into a mode.plk file under the ./outputs folder.
with open(os.path.join('.', 'outputs', 'model.pkl'), 'wb') as f:    
    pickle.dump(m, f)
```
<span data-ttu-id="78499-141">You can download any artifact by browsing to the **Output Files** section of the run detail page of a particular run in Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="78499-141">You can download any artifact by browsing to the **Output Files** section of the run detail page of a particular run in Azure Machine Learning Workbench.</span></span> <span data-ttu-id="78499-142">Simply select the run, and then select the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="78499-142">Simply select the run, and then select the **Download** button.</span></span> <span data-ttu-id="78499-143">Alternatively, you can enter the `az ml asset download` command in the command-line interface (CLI) window.</span><span class="sxs-lookup"><span data-stu-id="78499-143">Alternatively, you can enter the `az ml asset download` command in the command-line interface (CLI) window.</span></span>

<span data-ttu-id="78499-144">For a more complete example, see the `iris_sklearn.py` Python script in the _Classifying Iris_ sample project.</span><span class="sxs-lookup"><span data-stu-id="78499-144">For a more complete example, see the `iris_sklearn.py` Python script in the _Classifying Iris_ sample project.</span></span>

## <a name="option-2-use-the-shared-folder"></a><span data-ttu-id="78499-145">Option 2: Use the shared folder</span><span class="sxs-lookup"><span data-stu-id="78499-145">Option 2: Use the shared folder</span></span>
<span data-ttu-id="78499-146">If you don't need to keep a history of each run's files, using a shared folder that can be accessed across independent runs can be a great option for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="78499-146">If you don't need to keep a history of each run's files, using a shared folder that can be accessed across independent runs can be a great option for the following scenarios:</span></span> 
- <span data-ttu-id="78499-147">Your script needs to load data from local files, such as .csv files or a directory of text or image files, as training or test data.</span><span class="sxs-lookup"><span data-stu-id="78499-147">Your script needs to load data from local files, such as .csv files or a directory of text or image files, as training or test data.</span></span> 
- <span data-ttu-id="78499-148">Your script processes raw data and writes out intermediate results, such as featurized training data from text or image files, which are used in a subsequent training run.</span><span class="sxs-lookup"><span data-stu-id="78499-148">Your script processes raw data and writes out intermediate results, such as featurized training data from text or image files, which are used in a subsequent training run.</span></span> 
- <span data-ttu-id="78499-149">Your script spits out a model, and your subsequent scoring script must pick up the model and use it for evaluation.</span><span class="sxs-lookup"><span data-stu-id="78499-149">Your script spits out a model, and your subsequent scoring script must pick up the model and use it for evaluation.</span></span> 

<span data-ttu-id="78499-150">It is important to note that the shared folder lives locally on your chosen compute target.</span><span class="sxs-lookup"><span data-stu-id="78499-150">It is important to note that the shared folder lives locally on your chosen compute target.</span></span> <span data-ttu-id="78499-151">Therefore, this option works only if all your script runs that reference this shared folder are executed on the same compute target, and the compute target is not recycled between runs.</span><span class="sxs-lookup"><span data-stu-id="78499-151">Therefore, this option works only if all your script runs that reference this shared folder are executed on the same compute target, and the compute target is not recycled between runs.</span></span>

<span data-ttu-id="78499-152">By taking advantage of the shared-folder feature, you can read from or write to a special folder that's identified by an environment variable, `AZUREML_NATIVE_SHARE_DIRECTORY`.</span><span class="sxs-lookup"><span data-stu-id="78499-152">By taking advantage of the shared-folder feature, you can read from or write to a special folder that's identified by an environment variable, `AZUREML_NATIVE_SHARE_DIRECTORY`.</span></span> 

### <a name="example"></a><span data-ttu-id="78499-153">Example</span><span class="sxs-lookup"><span data-stu-id="78499-153">Example</span></span>
<span data-ttu-id="78499-154">Here is some sample Python code for using this share folder to read and write to a text file:</span><span class="sxs-lookup"><span data-stu-id="78499-154">Here is some sample Python code for using this share folder to read and write to a text file:</span></span>
```python
import os

# write to the shared folder
with open(os.environ['AZUREML_NATIVE_SHARE_DIRECTORY'] + 'test.txt', "w") as f1:
    f1.write(“Hello World”)

# read from the shared folder
with open(os.environ['AZUREML_NATIVE_SHARE_DIRECTORY'] + 'test.txt', "r") as f2:
    text = f2.read()
```

<span data-ttu-id="78499-155">For a more complete example, see the *iris_sklearn_shared_folder.py* file in the _Classifying Iris_ sample project.</span><span class="sxs-lookup"><span data-stu-id="78499-155">For a more complete example, see the *iris_sklearn_shared_folder.py* file in the _Classifying Iris_ sample project.</span></span>

<span data-ttu-id="78499-156">Before you can use this feature, you have to set in the *.compute* file some simple configurations that represent the targeted execution context in the *aml_config* folder.</span><span class="sxs-lookup"><span data-stu-id="78499-156">Before you can use this feature, you have to set in the *.compute* file some simple configurations that represent the targeted execution context in the *aml_config* folder.</span></span> <span data-ttu-id="78499-157">The actual path to the folder can vary depending on the compute target you choose and the value you configure.</span><span class="sxs-lookup"><span data-stu-id="78499-157">The actual path to the folder can vary depending on the compute target you choose and the value you configure.</span></span>

### <a name="configure-local-compute-context"></a><span data-ttu-id="78499-158">Configure local compute context</span><span class="sxs-lookup"><span data-stu-id="78499-158">Configure local compute context</span></span>

<span data-ttu-id="78499-159">To enable this feature in a local compute context, simply add to your *.compute* file the following line, which represents the _local_ environment (usually named *local.compute*).</span><span class="sxs-lookup"><span data-stu-id="78499-159">To enable this feature in a local compute context, simply add to your *.compute* file the following line, which represents the _local_ environment (usually named *local.compute*).</span></span>
```
# local.runconfig
...
nativeSharedDirectory: ~/.azureml/share
...
```

<span data-ttu-id="78499-160">The path ~/.azureml/share is the default base folder path.</span><span class="sxs-lookup"><span data-stu-id="78499-160">The path ~/.azureml/share is the default base folder path.</span></span> <span data-ttu-id="78499-161">You can change it to any local absolute path that's accessible by the script run.</span><span class="sxs-lookup"><span data-stu-id="78499-161">You can change it to any local absolute path that's accessible by the script run.</span></span> <span data-ttu-id="78499-162">The experimentation account name, workspace name, and project name are automatically appended to the base directory name, which becomes the full path of the shared directory.</span><span class="sxs-lookup"><span data-stu-id="78499-162">The experimentation account name, workspace name, and project name are automatically appended to the base directory name, which becomes the full path of the shared directory.</span></span> <span data-ttu-id="78499-163">For example, the files can be written to (and retrieved from) the following path if you use the preceding default value:</span><span class="sxs-lookup"><span data-stu-id="78499-163">For example, the files can be written to (and retrieved from) the following path if you use the preceding default value:</span></span>

```
# on Windows
C:\users\<username>\.azureml\share\<exp_acct_name>\<workspace_name>\<proj_name>\

# on macOS
/Users/<username>/.azureml/share/<exp_acct_name>/<workspace_name>/<proj_name>/
```

### <a name="configure-the-docker-compute-context-local-or-remote"></a><span data-ttu-id="78499-164">Configure the Docker compute context (local or remote)</span><span class="sxs-lookup"><span data-stu-id="78499-164">Configure the Docker compute context (local or remote)</span></span>
<span data-ttu-id="78499-165">To enable this feature on a Docker compute context, you must add the following two lines to your local or remote Docker *.compute* file.</span><span class="sxs-lookup"><span data-stu-id="78499-165">To enable this feature on a Docker compute context, you must add the following two lines to your local or remote Docker *.compute* file.</span></span>

```
# docker.compute
...
sharedVolumes: true
nativeSharedDirectory: ~/.azureml/share
...
```
>[!IMPORTANT]
><span data-ttu-id="78499-166">The **sharedVolumes** property must be set to *true* when you use the `AZUREML_NATIVE_SHARE_DIRECTORY` environment variable to access the shared folder.</span><span class="sxs-lookup"><span data-stu-id="78499-166">The **sharedVolumes** property must be set to *true* when you use the `AZUREML_NATIVE_SHARE_DIRECTORY` environment variable to access the shared folder.</span></span> <span data-ttu-id="78499-167">Otherwise, the execution fails.</span><span class="sxs-lookup"><span data-stu-id="78499-167">Otherwise, the execution fails.</span></span>

<span data-ttu-id="78499-168">The code running in the Docker container always sees this shared folder as */azureml-share/*.</span><span class="sxs-lookup"><span data-stu-id="78499-168">The code running in the Docker container always sees this shared folder as */azureml-share/*.</span></span> <span data-ttu-id="78499-169">The folder path, as seen by the Docker container, is not configurable.</span><span class="sxs-lookup"><span data-stu-id="78499-169">The folder path, as seen by the Docker container, is not configurable.</span></span> <span data-ttu-id="78499-170">Do not use this folder name in your code.</span><span class="sxs-lookup"><span data-stu-id="78499-170">Do not use this folder name in your code.</span></span> <span data-ttu-id="78499-171">Instead, always use the environment variable name `AZUREML_NATIVE_SHARE_DIRECTORY` to refer to this folder.</span><span class="sxs-lookup"><span data-stu-id="78499-171">Instead, always use the environment variable name `AZUREML_NATIVE_SHARE_DIRECTORY` to refer to this folder.</span></span> <span data-ttu-id="78499-172">It is mapped to a local folder on the Docker host machine or compute context.</span><span class="sxs-lookup"><span data-stu-id="78499-172">It is mapped to a local folder on the Docker host machine or compute context.</span></span> <span data-ttu-id="78499-173">The base directory of this local folder is the configurable value of the `nativeSharedDirectory` setting in the *.compute* file.</span><span class="sxs-lookup"><span data-stu-id="78499-173">The base directory of this local folder is the configurable value of the `nativeSharedDirectory` setting in the *.compute* file.</span></span> <span data-ttu-id="78499-174">The local path of the shared folder on the host machine, if you use the default value, is the following:</span><span class="sxs-lookup"><span data-stu-id="78499-174">The local path of the shared folder on the host machine, if you use the default value, is the following:</span></span>
```
# Windows
C:\users\<username>\.azureml\share\<exp_acct_name>\<workspace_name>\<proj_name>\

# macOS
/Users/<username>/.azureml/share/<exp_acct_name>/<workspace_name>/<proj_name>/

# Ubuntu Linux
/home/<username>/.azureml/share/<exp_acct_name>/<workspace_name>/<proj_name>/
```

>[!NOTE]
><span data-ttu-id="78499-175">The path of the shared folder on the local disk is the same whether it's a local compute context or a local Docker compute context.</span><span class="sxs-lookup"><span data-stu-id="78499-175">The path of the shared folder on the local disk is the same whether it's a local compute context or a local Docker compute context.</span></span> <span data-ttu-id="78499-176">This means you can even share files between a local run and a local Docker run.</span><span class="sxs-lookup"><span data-stu-id="78499-176">This means you can even share files between a local run and a local Docker run.</span></span>

<span data-ttu-id="78499-177">You can place input data directly in these folders and expect that your local or Docker runs on the machine can pick it up.</span><span class="sxs-lookup"><span data-stu-id="78499-177">You can place input data directly in these folders and expect that your local or Docker runs on the machine can pick it up.</span></span> <span data-ttu-id="78499-178">You can also write files to this folder from your local or Docker runs, and expect files get persisted in that folder, surviving the execution lifecycle.</span><span class="sxs-lookup"><span data-stu-id="78499-178">You can also write files to this folder from your local or Docker runs, and expect files get persisted in that folder, surviving the execution lifecycle.</span></span>

<span data-ttu-id="78499-179">For more information, see [Azure Machine Learning Workbench execution configuration files](experimentation-service-configuration-reference.md).</span><span class="sxs-lookup"><span data-stu-id="78499-179">For more information, see [Azure Machine Learning Workbench execution configuration files](experimentation-service-configuration-reference.md).</span></span>

>[!NOTE]
><span data-ttu-id="78499-180">The `AZUREML_NATIVE_SHARE_DIRECTORY` environment variable is not supported in an HDInsight compute context.</span><span class="sxs-lookup"><span data-stu-id="78499-180">The `AZUREML_NATIVE_SHARE_DIRECTORY` environment variable is not supported in an HDInsight compute context.</span></span> <span data-ttu-id="78499-181">However, it is easy to achieve the same result by explicitly using an absolute Azure Blob storage path to read from and write to the attached blob storage.</span><span class="sxs-lookup"><span data-stu-id="78499-181">However, it is easy to achieve the same result by explicitly using an absolute Azure Blob storage path to read from and write to the attached blob storage.</span></span>

## <a name="option-3-use-external-durable-storage"></a><span data-ttu-id="78499-182">Option 3: Use external durable storage</span><span class="sxs-lookup"><span data-stu-id="78499-182">Option 3: Use external durable storage</span></span>

<span data-ttu-id="78499-183">You can use external durable storage to persist state during execution.</span><span class="sxs-lookup"><span data-stu-id="78499-183">You can use external durable storage to persist state during execution.</span></span> <span data-ttu-id="78499-184">This option is useful in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="78499-184">This option is useful in the following scenarios:</span></span>
- <span data-ttu-id="78499-185">Your input data is already stored in durable storage that's accessible from the target compute environment.</span><span class="sxs-lookup"><span data-stu-id="78499-185">Your input data is already stored in durable storage that's accessible from the target compute environment.</span></span>
- <span data-ttu-id="78499-186">The files don't need to be part of the run history records.</span><span class="sxs-lookup"><span data-stu-id="78499-186">The files don't need to be part of the run history records.</span></span>
- <span data-ttu-id="78499-187">The files must be shared by executions across various compute environments.</span><span class="sxs-lookup"><span data-stu-id="78499-187">The files must be shared by executions across various compute environments.</span></span>
- <span data-ttu-id="78499-188">The files must be able to survive the compute context itself.</span><span class="sxs-lookup"><span data-stu-id="78499-188">The files must be able to survive the compute context itself.</span></span>

<span data-ttu-id="78499-189">One such approach is to use Azure Blob storage from your Python or PySpark code.</span><span class="sxs-lookup"><span data-stu-id="78499-189">One such approach is to use Azure Blob storage from your Python or PySpark code.</span></span> <span data-ttu-id="78499-190">Here is a short example:</span><span class="sxs-lookup"><span data-stu-id="78499-190">Here is a short example:</span></span>

```python
from azure.storage.blob import BlockBlobService
from azure.storage.blob.models import PublicAccess
import glob
import os

ACCOUNT_NAME = "<your blob storage account name>"
ACCOUNT_KEY = "<account key>"
CONTAINER_NAME = "<container name>"

blob_service = BlockBlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

## Create a new container if necessary, or use an existing one
blob_service.create_container(CONTAINER_NAME, fail_on_exist=False, public_access=PublicAccess.Container)

# df is a pandas DataFrame
df.to_csv('mydata.csv', sep='\t', index=False)

# Export the mydata.csv file to Blob storage.
for name in glob.iglob('mydata.csv'):
    blob_service.create_blob_from_path(CONTAINER_NAME, 'single_file.csv', name)
```

<span data-ttu-id="78499-191">Here is a short example for attaching any arbitrary Azure Blob storage to an HDI Spark runtime:</span><span class="sxs-lookup"><span data-stu-id="78499-191">Here is a short example for attaching any arbitrary Azure Blob storage to an HDI Spark runtime:</span></span>
```python
def attach_storage_container(spark, account, key):
    config = spark._sc._jsc.hadoopConfiguration()
    setting = "fs.azure.account.key." + account + ".blob.core.windows.net"
    if not config.get(setting):
        config.set(setting, key)
 
attach_storage_container(spark, "<storage account name>", "<storage key>”)
```

## <a name="conclusion"></a><span data-ttu-id="78499-192">Conclusion</span><span class="sxs-lookup"><span data-stu-id="78499-192">Conclusion</span></span>
<span data-ttu-id="78499-193">Because Azure Machine Learning executes scripts by copying the entire project folder to the target compute context, take special care with large input, output, and intermediary files.</span><span class="sxs-lookup"><span data-stu-id="78499-193">Because Azure Machine Learning executes scripts by copying the entire project folder to the target compute context, take special care with large input, output, and intermediary files.</span></span> <span data-ttu-id="78499-194">For large file transactions, you can use the special outputs folder, the shared folder that's accessible through the `AZUREML_NATIVE_SHARE_DIRECTORY` environment variable, or external durable storage.</span><span class="sxs-lookup"><span data-stu-id="78499-194">For large file transactions, you can use the special outputs folder, the shared folder that's accessible through the `AZUREML_NATIVE_SHARE_DIRECTORY` environment variable, or external durable storage.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="78499-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="78499-195">Next steps</span></span>
- <span data-ttu-id="78499-196">Review the [Azure Machine Learning Workbench execution configuration files](experimentation-service-configuration-reference.md) article.</span><span class="sxs-lookup"><span data-stu-id="78499-196">Review the [Azure Machine Learning Workbench execution configuration files](experimentation-service-configuration-reference.md) article.</span></span>
- <span data-ttu-id="78499-197">See how the [Classifying Iris](tutorial-classifying-iris-part-1.md) tutorial project uses the outputs folder to persist a trained model.</span><span class="sxs-lookup"><span data-stu-id="78499-197">See how the [Classifying Iris](tutorial-classifying-iris-part-1.md) tutorial project uses the outputs folder to persist a trained model.</span></span>
