---
title: Distributed Tuning of Hyperparameters using Azure Machine Learning Workbench | Microsoft Docs
description: This scenario shows how to do distributed tuning of hyperparameters using Azure Machine Learning Workbench
services: machine-learning
author: pechyony
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.author: dmpechyo
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.date: 09/20/2017
ms.openlocfilehash: 6347500b8968394a922969dd3dd2f00dd51cb6dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866862"
---
# <a name="distributed-tuning-of-hyperparameters-using-azure-machine-learning-workbench"></a><span data-ttu-id="e46db-103">Distributed tuning of hyperparameters using Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="e46db-103">Distributed tuning of hyperparameters using Azure Machine Learning Workbench</span></span>

<span data-ttu-id="e46db-104">This scenario shows how to use Azure Machine Learning Workbench to scale out tuning of hyperparameters of machine learning algorithms that implement scikit-learn API.</span><span class="sxs-lookup"><span data-stu-id="e46db-104">This scenario shows how to use Azure Machine Learning Workbench to scale out tuning of hyperparameters of machine learning algorithms that implement scikit-learn API.</span></span> <span data-ttu-id="e46db-105">We show how to configure and use a remote Docker container and Spark cluster as an execution backend for tuning hyperparameters.</span><span class="sxs-lookup"><span data-stu-id="e46db-105">We show how to configure and use a remote Docker container and Spark cluster as an execution backend for tuning hyperparameters.</span></span>

## <a name="link-of-the-gallery-github-repository"></a><span data-ttu-id="e46db-106">Link of the Gallery GitHub repository</span><span class="sxs-lookup"><span data-stu-id="e46db-106">Link of the Gallery GitHub repository</span></span>
<span data-ttu-id="e46db-107">Following is the link to the public GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="e46db-107">Following is the link to the public GitHub repository:</span></span> 

[https://github.com/Azure/MachineLearningSamples-DistributedHyperParameterTuning](https://github.com/Azure/MachineLearningSamples-DistributedHyperParameterTuning)

## <a name="use-case-overview"></a><span data-ttu-id="e46db-108">Use case overview</span><span class="sxs-lookup"><span data-stu-id="e46db-108">Use case overview</span></span>

<span data-ttu-id="e46db-109">Many machine learning algorithms have one or more knobs, called hyperparameters.</span><span class="sxs-lookup"><span data-stu-id="e46db-109">Many machine learning algorithms have one or more knobs, called hyperparameters.</span></span> <span data-ttu-id="e46db-110">These knobs allow tuning of algorithms to optimize their performance over future data, measured according to user-specified metrics (for example, accuracy, AUC, RMSE).</span><span class="sxs-lookup"><span data-stu-id="e46db-110">These knobs allow tuning of algorithms to optimize their performance over future data, measured according to user-specified metrics (for example, accuracy, AUC, RMSE).</span></span> <span data-ttu-id="e46db-111">Data scientist needs to provide values of hyperparameters when building a model over training data and before seeing the future test data.</span><span class="sxs-lookup"><span data-stu-id="e46db-111">Data scientist needs to provide values of hyperparameters when building a model over training data and before seeing the future test data.</span></span> <span data-ttu-id="e46db-112">How based on the known training data can we set up the values of hyperparameters so that the model has a good performance over the unknown test data?</span><span class="sxs-lookup"><span data-stu-id="e46db-112">How based on the known training data can we set up the values of hyperparameters so that the model has a good performance over the unknown test data?</span></span> 
    
<span data-ttu-id="e46db-113">A popular technique for tuning hyperparameters is a *grid search* combined with *cross-validation*.</span><span class="sxs-lookup"><span data-stu-id="e46db-113">A popular technique for tuning hyperparameters is a *grid search* combined with *cross-validation*.</span></span> <span data-ttu-id="e46db-114">Cross-validation is a technique that assesses how well a model, trained on a training set, predicts over the test set.</span><span class="sxs-lookup"><span data-stu-id="e46db-114">Cross-validation is a technique that assesses how well a model, trained on a training set, predicts over the test set.</span></span> <span data-ttu-id="e46db-115">Using this technique, we first divide the dataset into K folds and then train the algorithm K times in a round-robin fashion.</span><span class="sxs-lookup"><span data-stu-id="e46db-115">Using this technique, we first divide the dataset into K folds and then train the algorithm K times in a round-robin fashion.</span></span> <span data-ttu-id="e46db-116">We do this on all but one of the folds called the "held-out fold".</span><span class="sxs-lookup"><span data-stu-id="e46db-116">We do this on all but one of the folds called the "held-out fold".</span></span> <span data-ttu-id="e46db-117">We compute the average value of the metrics of K models over K held-out folds.</span><span class="sxs-lookup"><span data-stu-id="e46db-117">We compute the average value of the metrics of K models over K held-out folds.</span></span> <span data-ttu-id="e46db-118">This average value, called *cross-validated performance estimate*, depends on the values of hyperparameters used when creating K models.</span><span class="sxs-lookup"><span data-stu-id="e46db-118">This average value, called *cross-validated performance estimate*, depends on the values of hyperparameters used when creating K models.</span></span> <span data-ttu-id="e46db-119">When tuning hyperparameters, we search through the space of candidate hyperparameter values to find the ones that optimize cross-validation performance estimate.</span><span class="sxs-lookup"><span data-stu-id="e46db-119">When tuning hyperparameters, we search through the space of candidate hyperparameter values to find the ones that optimize cross-validation performance estimate.</span></span> <span data-ttu-id="e46db-120">Grid search is a common search technique.</span><span class="sxs-lookup"><span data-stu-id="e46db-120">Grid search is a common search technique.</span></span> <span data-ttu-id="e46db-121">In grid search, the space of candidate values of multiple hyperparameters is a cross-product of sets of candidate values of individual hyperparameters.</span><span class="sxs-lookup"><span data-stu-id="e46db-121">In grid search, the space of candidate values of multiple hyperparameters is a cross-product of sets of candidate values of individual hyperparameters.</span></span> 

<span data-ttu-id="e46db-122">Grid search using cross-validation can be time-consuming.</span><span class="sxs-lookup"><span data-stu-id="e46db-122">Grid search using cross-validation can be time-consuming.</span></span> <span data-ttu-id="e46db-123">If an algorithm has five hyperparameters each with five candidate values, we use K=5 folds.</span><span class="sxs-lookup"><span data-stu-id="e46db-123">If an algorithm has five hyperparameters each with five candidate values, we use K=5 folds.</span></span> <span data-ttu-id="e46db-124">We then complete a grid search by training 5<sup>6</sup>=15625 models.</span><span class="sxs-lookup"><span data-stu-id="e46db-124">We then complete a grid search by training 5<sup>6</sup>=15625 models.</span></span> <span data-ttu-id="e46db-125">Fortunately, grid-search using cross-validation is an embarrassingly parallel procedure and all these models can be trained in parallel.</span><span class="sxs-lookup"><span data-stu-id="e46db-125">Fortunately, grid-search using cross-validation is an embarrassingly parallel procedure and all these models can be trained in parallel.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e46db-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e46db-126">Prerequisites</span></span>

* <span data-ttu-id="e46db-127">An [Azure account](https://azure.microsoft.com/free/) (free trials are available).</span><span class="sxs-lookup"><span data-stu-id="e46db-127">An [Azure account](https://azure.microsoft.com/free/) (free trials are available).</span></span>
* <span data-ttu-id="e46db-128">An installed copy of [Azure Machine Learning Workbench](../service/overview-what-is-azure-ml.md) following the [Install and create Quickstart](../service/quickstart-installation.md) to install the Workbench and create accounts.</span><span class="sxs-lookup"><span data-stu-id="e46db-128">An installed copy of [Azure Machine Learning Workbench](../service/overview-what-is-azure-ml.md) following the [Install and create Quickstart](../service/quickstart-installation.md) to install the Workbench and create accounts.</span></span>
* <span data-ttu-id="e46db-129">This scenario assumes that you are running Azure ML Workbench on Windows 10 or MacOS with Docker engine locally installed.</span><span class="sxs-lookup"><span data-stu-id="e46db-129">This scenario assumes that you are running Azure ML Workbench on Windows 10 or MacOS with Docker engine locally installed.</span></span> 
* <span data-ttu-id="e46db-130">To run the scenario with a remote Docker container, provision Ubuntu Data Science Virtual Machine (DSVM) by following the [instructions](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-provision-vm).</span><span class="sxs-lookup"><span data-stu-id="e46db-130">To run the scenario with a remote Docker container, provision Ubuntu Data Science Virtual Machine (DSVM) by following the [instructions](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-provision-vm).</span></span> <span data-ttu-id="e46db-131">We recommend using a virtual machine with at least 8 cores and 28 Gb of memory.</span><span class="sxs-lookup"><span data-stu-id="e46db-131">We recommend using a virtual machine with at least 8 cores and 28 Gb of memory.</span></span> <span data-ttu-id="e46db-132">D4 instances of virtual machines have such capacity.</span><span class="sxs-lookup"><span data-stu-id="e46db-132">D4 instances of virtual machines have such capacity.</span></span> 
* <span data-ttu-id="e46db-133">To run this scenario with a Spark cluster, provision Spark HDInsight cluster by following these [instructions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="e46db-133">To run this scenario with a Spark cluster, provision Spark HDInsight cluster by following these [instructions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters).</span></span> <span data-ttu-id="e46db-134">We recommend having a cluster with the following configuration in both header and worker nodes:</span><span class="sxs-lookup"><span data-stu-id="e46db-134">We recommend having a cluster with the following configuration in both header and worker nodes:</span></span>
    - <span data-ttu-id="e46db-135">four worker nodes</span><span class="sxs-lookup"><span data-stu-id="e46db-135">four worker nodes</span></span>
    - <span data-ttu-id="e46db-136">eight cores</span><span class="sxs-lookup"><span data-stu-id="e46db-136">eight cores</span></span>
    - <span data-ttu-id="e46db-137">28 Gb of memory</span><span class="sxs-lookup"><span data-stu-id="e46db-137">28 Gb of memory</span></span>  
      
  <span data-ttu-id="e46db-138">D4 instances of virtual machines have such capacity.</span><span class="sxs-lookup"><span data-stu-id="e46db-138">D4 instances of virtual machines have such capacity.</span></span> 

     <span data-ttu-id="e46db-139">**Troubleshooting**: Your Azure subscription might have a quota on the number of cores that can be used.</span><span class="sxs-lookup"><span data-stu-id="e46db-139">**Troubleshooting**: Your Azure subscription might have a quota on the number of cores that can be used.</span></span> <span data-ttu-id="e46db-140">The Azure portal does not allow the creation of cluster with the total number of cores exceeding the quota.</span><span class="sxs-lookup"><span data-stu-id="e46db-140">The Azure portal does not allow the creation of cluster with the total number of cores exceeding the quota.</span></span> <span data-ttu-id="e46db-141">To find you quota, go in the Azure portal to the Subscriptions section, click on the subscription used to deploy a cluster and then click on **Usage+quotas**.</span><span class="sxs-lookup"><span data-stu-id="e46db-141">To find you quota, go in the Azure portal to the Subscriptions section, click on the subscription used to deploy a cluster and then click on **Usage+quotas**.</span></span> <span data-ttu-id="e46db-142">Usually quotas are defined per Azure region and you can choose to deploy the Spark cluster in a region where you have enough free cores.</span><span class="sxs-lookup"><span data-stu-id="e46db-142">Usually quotas are defined per Azure region and you can choose to deploy the Spark cluster in a region where you have enough free cores.</span></span> 

* <span data-ttu-id="e46db-143">Create an Azure storage account that is used for storing the dataset.</span><span class="sxs-lookup"><span data-stu-id="e46db-143">Create an Azure storage account that is used for storing the dataset.</span></span> <span data-ttu-id="e46db-144">Follow the [instructions](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account) to create a storage account.</span><span class="sxs-lookup"><span data-stu-id="e46db-144">Follow the [instructions](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account) to create a storage account.</span></span>

## <a name="data-description"></a><span data-ttu-id="e46db-145">Data description</span><span class="sxs-lookup"><span data-stu-id="e46db-145">Data description</span></span>

<span data-ttu-id="e46db-146">We use [TalkingData dataset](https://www.kaggle.com/c/talkingdata-mobile-user-demographics/data).</span><span class="sxs-lookup"><span data-stu-id="e46db-146">We use [TalkingData dataset](https://www.kaggle.com/c/talkingdata-mobile-user-demographics/data).</span></span> <span data-ttu-id="e46db-147">This dataset has events from the apps in cell phones.</span><span class="sxs-lookup"><span data-stu-id="e46db-147">This dataset has events from the apps in cell phones.</span></span> <span data-ttu-id="e46db-148">The goal is to predict gender and age category of cell phone user given the type of the phone and the events that the user generated recently.</span><span class="sxs-lookup"><span data-stu-id="e46db-148">The goal is to predict gender and age category of cell phone user given the type of the phone and the events that the user generated recently.</span></span>  

## <a name="scenario-structure"></a><span data-ttu-id="e46db-149">Scenario structure</span><span class="sxs-lookup"><span data-stu-id="e46db-149">Scenario structure</span></span>
<span data-ttu-id="e46db-150">This scenario has multiple folders in GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="e46db-150">This scenario has multiple folders in GitHub repository.</span></span> <span data-ttu-id="e46db-151">Code and configuration files are in **Code** folder, all documentation is in **Docs** folder and all images are **Images** folder.</span><span class="sxs-lookup"><span data-stu-id="e46db-151">Code and configuration files are in **Code** folder, all documentation is in **Docs** folder and all images are **Images** folder.</span></span> <span data-ttu-id="e46db-152">The root folder has README file that contains a brief summary of this scenario.</span><span class="sxs-lookup"><span data-stu-id="e46db-152">The root folder has README file that contains a brief summary of this scenario.</span></span>

### <a name="getting-started"></a><span data-ttu-id="e46db-153">Getting started</span><span class="sxs-lookup"><span data-stu-id="e46db-153">Getting started</span></span>
<span data-ttu-id="e46db-154">Click on the Azure Machine Learning Workbench icon to run Azure Machine Learning Workbench and create a project from the  "Distributed Tuning of Hyperparameters" template.</span><span class="sxs-lookup"><span data-stu-id="e46db-154">Click on the Azure Machine Learning Workbench icon to run Azure Machine Learning Workbench and create a project from the  "Distributed Tuning of Hyperparameters" template.</span></span> <span data-ttu-id="e46db-155">You can find detailed instructions on how to create a new project in [Install and create Quickstart](quickstart-installation.md).</span><span class="sxs-lookup"><span data-stu-id="e46db-155">You can find detailed instructions on how to create a new project in [Install and create Quickstart](quickstart-installation.md).</span></span>   

### <a name="configuration-of-execution-environments"></a><span data-ttu-id="e46db-156">Configuration of execution environments</span><span class="sxs-lookup"><span data-stu-id="e46db-156">Configuration of execution environments</span></span>
<span data-ttu-id="e46db-157">We show how to run our code in a remote Docker container and in a Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e46db-157">We show how to run our code in a remote Docker container and in a Spark cluster.</span></span> <span data-ttu-id="e46db-158">We start with the description of the settings that are common to both environments.</span><span class="sxs-lookup"><span data-stu-id="e46db-158">We start with the description of the settings that are common to both environments.</span></span> 

<span data-ttu-id="e46db-159">We use [scikit-learn](https://anaconda.org/conda-forge/scikit-learn), [xgboost](https://anaconda.org/conda-forge/xgboost), and [azure-storage](https://pypi.python.org/pypi/azure-storage) packages that are not provided in the default Docker container of Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="e46db-159">We use [scikit-learn](https://anaconda.org/conda-forge/scikit-learn), [xgboost](https://anaconda.org/conda-forge/xgboost), and [azure-storage](https://pypi.python.org/pypi/azure-storage) packages that are not provided in the default Docker container of Azure Machine Learning Workbench.</span></span> <span data-ttu-id="e46db-160">azure-storage package requires installation of [cryptography](https://pypi.python.org/pypi/cryptography) and [azure](https://pypi.python.org/pypi/azure) packages.</span><span class="sxs-lookup"><span data-stu-id="e46db-160">azure-storage package requires installation of [cryptography](https://pypi.python.org/pypi/cryptography) and [azure](https://pypi.python.org/pypi/azure) packages.</span></span> <span data-ttu-id="e46db-161">To install these packages in the Docker container and in the nodes of Spark cluster, we modify conda_dependencies.yml file:</span><span class="sxs-lookup"><span data-stu-id="e46db-161">To install these packages in the Docker container and in the nodes of Spark cluster, we modify conda_dependencies.yml file:</span></span>

    name: project_environment
    channels:
      - conda-forge
    dependencies:
      - python=3.5.2
      - scikit-learn
      - xgboost
      - pip:
        - cryptography
        - azure
        - azure-storage

<span data-ttu-id="e46db-162">The modified conda\_dependencies.yml file is stored in aml_config directory of tutorial.</span><span class="sxs-lookup"><span data-stu-id="e46db-162">The modified conda\_dependencies.yml file is stored in aml_config directory of tutorial.</span></span> 

<span data-ttu-id="e46db-163">In the next steps, we connect execution environment to Azure account.</span><span class="sxs-lookup"><span data-stu-id="e46db-163">In the next steps, we connect execution environment to Azure account.</span></span> <span data-ttu-id="e46db-164">Click File Menu from the top left corner of AML Workbench.</span><span class="sxs-lookup"><span data-stu-id="e46db-164">Click File Menu from the top left corner of AML Workbench.</span></span> <span data-ttu-id="e46db-165">And choose "Open Command Prompt".</span><span class="sxs-lookup"><span data-stu-id="e46db-165">And choose "Open Command Prompt".</span></span> <span data-ttu-id="e46db-166">Then run in CLI</span><span class="sxs-lookup"><span data-stu-id="e46db-166">Then run in CLI</span></span>

    az login

<span data-ttu-id="e46db-167">You get a message</span><span class="sxs-lookup"><span data-stu-id="e46db-167">You get a message</span></span>

    To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the code <code> to authenticate.

<span data-ttu-id="e46db-168">Go to this web page, enter the code and sign into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="e46db-168">Go to this web page, enter the code and sign into your Azure account.</span></span> <span data-ttu-id="e46db-169">After this step, run in CLI</span><span class="sxs-lookup"><span data-stu-id="e46db-169">After this step, run in CLI</span></span>

    az account list -o table

<span data-ttu-id="e46db-170">and find the Azure subscription ID that has your AML Workbench Workspace account.</span><span class="sxs-lookup"><span data-stu-id="e46db-170">and find the Azure subscription ID that has your AML Workbench Workspace account.</span></span> <span data-ttu-id="e46db-171">Finally, run in CLI</span><span class="sxs-lookup"><span data-stu-id="e46db-171">Finally, run in CLI</span></span>

    az account set -s <subscription ID>

<span data-ttu-id="e46db-172">to complete the connection to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e46db-172">to complete the connection to your Azure subscription.</span></span>

<span data-ttu-id="e46db-173">In the next two sections, we show how to complete configuration of remote docker and Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e46db-173">In the next two sections, we show how to complete configuration of remote docker and Spark cluster.</span></span>

#### <a name="configuration-of-remote-docker-container"></a><span data-ttu-id="e46db-174">Configuration of remote Docker container</span><span class="sxs-lookup"><span data-stu-id="e46db-174">Configuration of remote Docker container</span></span>

 <span data-ttu-id="e46db-175">To set up a remote Docker container, run in CLI</span><span class="sxs-lookup"><span data-stu-id="e46db-175">To set up a remote Docker container, run in CLI</span></span>

    az ml computetarget attach remotedocker --name dsvm --address <IP address> --username <username> --password <password> 

<span data-ttu-id="e46db-176">with IP address, user name and password in DSVM.</span><span class="sxs-lookup"><span data-stu-id="e46db-176">with IP address, user name and password in DSVM.</span></span> <span data-ttu-id="e46db-177">IP address of DSVM can be found in Overview section of your DSVM page in Azure portal:</span><span class="sxs-lookup"><span data-stu-id="e46db-177">IP address of DSVM can be found in Overview section of your DSVM page in Azure portal:</span></span>

![VM IP](media/scenario-distributed-tuning-of-hyperparameters/vm_ip.png)

#### <a name="configuration-of-spark-cluster"></a><span data-ttu-id="e46db-179">Configuration of Spark cluster</span><span class="sxs-lookup"><span data-stu-id="e46db-179">Configuration of Spark cluster</span></span>

<span data-ttu-id="e46db-180">To set up Spark environment, run in CLI</span><span class="sxs-lookup"><span data-stu-id="e46db-180">To set up Spark environment, run in CLI</span></span>

    az ml computetarget attach cluster --name spark --address <cluster name>-ssh.azurehdinsight.net  --username <username> --password <password> 

<span data-ttu-id="e46db-181">with the name of the cluster, cluster's SSH user name and password.</span><span class="sxs-lookup"><span data-stu-id="e46db-181">with the name of the cluster, cluster's SSH user name and password.</span></span> <span data-ttu-id="e46db-182">The default value of SSH user name is `sshuser`, unless you changed it during provisioning of the cluster.</span><span class="sxs-lookup"><span data-stu-id="e46db-182">The default value of SSH user name is `sshuser`, unless you changed it during provisioning of the cluster.</span></span> <span data-ttu-id="e46db-183">The name of the cluster can be found in Properties section of your cluster page in Azure portal:</span><span class="sxs-lookup"><span data-stu-id="e46db-183">The name of the cluster can be found in Properties section of your cluster page in Azure portal:</span></span>

![Cluster name](media/scenario-distributed-tuning-of-hyperparameters/cluster_name.png)

<span data-ttu-id="e46db-185">We use spark-sklearn package to have Spark as an execution environment for distributed tuning of hyperparameters.</span><span class="sxs-lookup"><span data-stu-id="e46db-185">We use spark-sklearn package to have Spark as an execution environment for distributed tuning of hyperparameters.</span></span> <span data-ttu-id="e46db-186">We modified spark_dependencies.yml file to install this package when Spark execution environment is used:</span><span class="sxs-lookup"><span data-stu-id="e46db-186">We modified spark_dependencies.yml file to install this package when Spark execution environment is used:</span></span>

    configuration: 
      #"spark.driver.cores": "8"
      #"spark.driver.memory": "5200m"
      #"spark.executor.instances": "128"
      #"spark.executor.memory": "5200m"  
      #"spark.executor.cores": "2"
  
    repositories:
      - "https://mmlspark.azureedge.net/maven"
      - "https://spark-packages.org/packages"
    packages:
      - group: "com.microsoft.ml.spark"
        artifact: "mmlspark_2.11"
        version: "0.7.91"
      - group: "databricks"
        artifact: "spark-sklearn"
        version: "0.2.0"

<span data-ttu-id="e46db-187">The modified spark\_dependencies.yml file is stored in aml_config directory of tutorial.</span><span class="sxs-lookup"><span data-stu-id="e46db-187">The modified spark\_dependencies.yml file is stored in aml_config directory of tutorial.</span></span> 

### <a name="data-ingestion"></a><span data-ttu-id="e46db-188">Data ingestion</span><span class="sxs-lookup"><span data-stu-id="e46db-188">Data ingestion</span></span>
<span data-ttu-id="e46db-189">The code in this scenario assumes that the data is stored in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="e46db-189">The code in this scenario assumes that the data is stored in Azure blob storage.</span></span> <span data-ttu-id="e46db-190">We show initially how to download data from Kaggle site to your computer and upload it to the blob storage.</span><span class="sxs-lookup"><span data-stu-id="e46db-190">We show initially how to download data from Kaggle site to your computer and upload it to the blob storage.</span></span> <span data-ttu-id="e46db-191">Then we show how to read the data from blob storage.</span><span class="sxs-lookup"><span data-stu-id="e46db-191">Then we show how to read the data from blob storage.</span></span> 

<span data-ttu-id="e46db-192">To download data from Kaggle, go to [dataset page](https://www.kaggle.com/c/talkingdata-mobile-user-demographics/data) and click Download button.</span><span class="sxs-lookup"><span data-stu-id="e46db-192">To download data from Kaggle, go to [dataset page](https://www.kaggle.com/c/talkingdata-mobile-user-demographics/data) and click Download button.</span></span> <span data-ttu-id="e46db-193">You will be asked to log in to Kaggle.</span><span class="sxs-lookup"><span data-stu-id="e46db-193">You will be asked to log in to Kaggle.</span></span> <span data-ttu-id="e46db-194">After logging in, you will be redirected back to dataset page.</span><span class="sxs-lookup"><span data-stu-id="e46db-194">After logging in, you will be redirected back to dataset page.</span></span> <span data-ttu-id="e46db-195">Then download the first seven files in the left column by selecting them and clicking Download button.</span><span class="sxs-lookup"><span data-stu-id="e46db-195">Then download the first seven files in the left column by selecting them and clicking Download button.</span></span> <span data-ttu-id="e46db-196">The total size of the downloaded files is 289 Mb.</span><span class="sxs-lookup"><span data-stu-id="e46db-196">The total size of the downloaded files is 289 Mb.</span></span> <span data-ttu-id="e46db-197">To upload these files to blob storage, create blob storage container 'dataset' in your storage account.</span><span class="sxs-lookup"><span data-stu-id="e46db-197">To upload these files to blob storage, create blob storage container 'dataset' in your storage account.</span></span> <span data-ttu-id="e46db-198">You can do that by going to Azure page of your storage account, clicking Blobs and then clicking +Container.</span><span class="sxs-lookup"><span data-stu-id="e46db-198">You can do that by going to Azure page of your storage account, clicking Blobs and then clicking +Container.</span></span> <span data-ttu-id="e46db-199">Enter 'dataset' as Name and click OK.</span><span class="sxs-lookup"><span data-stu-id="e46db-199">Enter 'dataset' as Name and click OK.</span></span> <span data-ttu-id="e46db-200">The following screenshots illustrate these steps:</span><span class="sxs-lookup"><span data-stu-id="e46db-200">The following screenshots illustrate these steps:</span></span>

<span data-ttu-id="e46db-201">![Open blob](media/scenario-distributed-tuning-of-hyperparameters/open_blob.png)
![Open container](media/scenario-distributed-tuning-of-hyperparameters/open_container.png)</span><span class="sxs-lookup"><span data-stu-id="e46db-201">![Open blob](media/scenario-distributed-tuning-of-hyperparameters/open_blob.png)
![Open container](media/scenario-distributed-tuning-of-hyperparameters/open_container.png)</span></span>

<span data-ttu-id="e46db-202">After that, select dataset container from the list and click Upload button.</span><span class="sxs-lookup"><span data-stu-id="e46db-202">After that, select dataset container from the list and click Upload button.</span></span> <span data-ttu-id="e46db-203">Azure portal allows you to upload multiple files concurrently.</span><span class="sxs-lookup"><span data-stu-id="e46db-203">Azure portal allows you to upload multiple files concurrently.</span></span> <span data-ttu-id="e46db-204">In "Upload blob" section click folder button, select all files from the dataset, click Open, and then click Upload.</span><span class="sxs-lookup"><span data-stu-id="e46db-204">In "Upload blob" section click folder button, select all files from the dataset, click Open, and then click Upload.</span></span> <span data-ttu-id="e46db-205">The following screenshot illustrates these steps:</span><span class="sxs-lookup"><span data-stu-id="e46db-205">The following screenshot illustrates these steps:</span></span>

![Upload blob](media/scenario-distributed-tuning-of-hyperparameters/upload_blob.png) 

<span data-ttu-id="e46db-207">Upload of the files takes several minutes, depending on your Internet connection.</span><span class="sxs-lookup"><span data-stu-id="e46db-207">Upload of the files takes several minutes, depending on your Internet connection.</span></span> 

<span data-ttu-id="e46db-208">In our code, we use [Azure Storage SDK](https://docs.microsoft.com/en-us/python/azure/) to download the dataset from blob storage to the current execution environment.</span><span class="sxs-lookup"><span data-stu-id="e46db-208">In our code, we use [Azure Storage SDK](https://docs.microsoft.com/en-us/python/azure/) to download the dataset from blob storage to the current execution environment.</span></span> <span data-ttu-id="e46db-209">The download is performed in load\_data() function from load_data.py file.</span><span class="sxs-lookup"><span data-stu-id="e46db-209">The download is performed in load\_data() function from load_data.py file.</span></span> <span data-ttu-id="e46db-210">To use this code, you need to replace <ACCOUNT_NAME> and <ACCOUNT_KEY> with the name and primary key of your storage account that hosts the dataset.</span><span class="sxs-lookup"><span data-stu-id="e46db-210">To use this code, you need to replace <ACCOUNT_NAME> and <ACCOUNT_KEY> with the name and primary key of your storage account that hosts the dataset.</span></span> <span data-ttu-id="e46db-211">You can see the account name in the top left corner of your storage account's Azure page.</span><span class="sxs-lookup"><span data-stu-id="e46db-211">You can see the account name in the top left corner of your storage account's Azure page.</span></span> <span data-ttu-id="e46db-212">To get account key, select Access Keys in Azure page of storage account (see the first screenshot in Data Ingestion section) and then copy the long string in the first row of key column:</span><span class="sxs-lookup"><span data-stu-id="e46db-212">To get account key, select Access Keys in Azure page of storage account (see the first screenshot in Data Ingestion section) and then copy the long string in the first row of key column:</span></span>
 
![access key](media/scenario-distributed-tuning-of-hyperparameters/access_key.png)

<span data-ttu-id="e46db-214">The following code from load_data() function downloads a single file:</span><span class="sxs-lookup"><span data-stu-id="e46db-214">The following code from load_data() function downloads a single file:</span></span>

    from azure.storage.blob import BlockBlobService

    # Define storage parameters 
    ACCOUNT_NAME = "<ACCOUNT_NAME>"
    ACCOUNT_KEY = "<ACCOUNT_KEY>"
    CONTAINER_NAME = "dataset"

    # Define blob service     
    my_service = BlockBlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # Load blob
    my_service.get_blob_to_path(CONTAINER_NAME, 'app_events.csv.zip', 'app_events.csv.zip')

<span data-ttu-id="e46db-215">Notice that you do not need to run load_data.py file manually.</span><span class="sxs-lookup"><span data-stu-id="e46db-215">Notice that you do not need to run load_data.py file manually.</span></span> <span data-ttu-id="e46db-216">It is called from other files later on.</span><span class="sxs-lookup"><span data-stu-id="e46db-216">It is called from other files later on.</span></span>

### <a name="feature-engineering"></a><span data-ttu-id="e46db-217">Feature engineering</span><span class="sxs-lookup"><span data-stu-id="e46db-217">Feature engineering</span></span>
<span data-ttu-id="e46db-218">The code for computing all features is in feature\_engineering.py file.</span><span class="sxs-lookup"><span data-stu-id="e46db-218">The code for computing all features is in feature\_engineering.py file.</span></span> <span data-ttu-id="e46db-219">You do not need to run feature_engineering.py file manually.</span><span class="sxs-lookup"><span data-stu-id="e46db-219">You do not need to run feature_engineering.py file manually.</span></span> <span data-ttu-id="e46db-220">Later on it will be called from other files.</span><span class="sxs-lookup"><span data-stu-id="e46db-220">Later on it will be called from other files.</span></span>

<span data-ttu-id="e46db-221">We create multiple feature sets:</span><span class="sxs-lookup"><span data-stu-id="e46db-221">We create multiple feature sets:</span></span>
* <span data-ttu-id="e46db-222">One-hot encoding of brand and model of the cell phone (one\_hot\_brand_model function)</span><span class="sxs-lookup"><span data-stu-id="e46db-222">One-hot encoding of brand and model of the cell phone (one\_hot\_brand_model function)</span></span>
* <span data-ttu-id="e46db-223">Fraction of events generated by user in each weekday (weekday\_hour_features function)</span><span class="sxs-lookup"><span data-stu-id="e46db-223">Fraction of events generated by user in each weekday (weekday\_hour_features function)</span></span>
* <span data-ttu-id="e46db-224">Fraction of events generated by user in each hour (weekday\_hour_features function)</span><span class="sxs-lookup"><span data-stu-id="e46db-224">Fraction of events generated by user in each hour (weekday\_hour_features function)</span></span>
* <span data-ttu-id="e46db-225">Fraction of events generated by user in each combination of weekday and hour (weekday\_hour_features function)</span><span class="sxs-lookup"><span data-stu-id="e46db-225">Fraction of events generated by user in each combination of weekday and hour (weekday\_hour_features function)</span></span>
* <span data-ttu-id="e46db-226">Fraction of events generated by user in each app (one\_hot\_app_labels function)</span><span class="sxs-lookup"><span data-stu-id="e46db-226">Fraction of events generated by user in each app (one\_hot\_app_labels function)</span></span>
* <span data-ttu-id="e46db-227">Fraction of events generated by user in each app label (one\_hot\_app_labels function)</span><span class="sxs-lookup"><span data-stu-id="e46db-227">Fraction of events generated by user in each app label (one\_hot\_app_labels function)</span></span>
* <span data-ttu-id="e46db-228">Fraction of events generated by user in each app category (text\_category_features function)</span><span class="sxs-lookup"><span data-stu-id="e46db-228">Fraction of events generated by user in each app category (text\_category_features function)</span></span>
* <span data-ttu-id="e46db-229">Indicator features for categories of apps that were used to generated events (one\_hot_category function)</span><span class="sxs-lookup"><span data-stu-id="e46db-229">Indicator features for categories of apps that were used to generated events (one\_hot_category function)</span></span>

<span data-ttu-id="e46db-230">These features were inspired by Kaggle kernel [A linear model on apps and labels](https://www.kaggle.com/dvasyukova/a-linear-model-on-apps-and-labels).</span><span class="sxs-lookup"><span data-stu-id="e46db-230">These features were inspired by Kaggle kernel [A linear model on apps and labels](https://www.kaggle.com/dvasyukova/a-linear-model-on-apps-and-labels).</span></span>

<span data-ttu-id="e46db-231">The computation of these features requires significant amount of memory.</span><span class="sxs-lookup"><span data-stu-id="e46db-231">The computation of these features requires significant amount of memory.</span></span> <span data-ttu-id="e46db-232">Initially we tried to compute features in the local environment with 16-GB RAM.</span><span class="sxs-lookup"><span data-stu-id="e46db-232">Initially we tried to compute features in the local environment with 16-GB RAM.</span></span> <span data-ttu-id="e46db-233">We were able to compute the first four sets of features, but received 'Out of memory' error when computing the fifth feature set.</span><span class="sxs-lookup"><span data-stu-id="e46db-233">We were able to compute the first four sets of features, but received 'Out of memory' error when computing the fifth feature set.</span></span> <span data-ttu-id="e46db-234">The computation of the first four feature sets is in singleVMsmall.py file and it can be executed in the local environment by running</span><span class="sxs-lookup"><span data-stu-id="e46db-234">The computation of the first four feature sets is in singleVMsmall.py file and it can be executed in the local environment by running</span></span> 

     az ml experiment submit -c local .\singleVMsmall.py   

<span data-ttu-id="e46db-235">in CLI window.</span><span class="sxs-lookup"><span data-stu-id="e46db-235">in CLI window.</span></span>

<span data-ttu-id="e46db-236">Since local environment is too small for computing all feature sets, we switch to remote DSVM that has larger memory.</span><span class="sxs-lookup"><span data-stu-id="e46db-236">Since local environment is too small for computing all feature sets, we switch to remote DSVM that has larger memory.</span></span> <span data-ttu-id="e46db-237">The execution inside DSVM is done inside Docker container that is managed by AML Workbench.</span><span class="sxs-lookup"><span data-stu-id="e46db-237">The execution inside DSVM is done inside Docker container that is managed by AML Workbench.</span></span> <span data-ttu-id="e46db-238">Using this DSVM we are able to compute all features and train models and tune hyperparameters (see the next section).</span><span class="sxs-lookup"><span data-stu-id="e46db-238">Using this DSVM we are able to compute all features and train models and tune hyperparameters (see the next section).</span></span> <span data-ttu-id="e46db-239">singleVM.py file has complete feature computation and modeling code.</span><span class="sxs-lookup"><span data-stu-id="e46db-239">singleVM.py file has complete feature computation and modeling code.</span></span> <span data-ttu-id="e46db-240">In the next section, we will show how to run singleVM.py in remote DSVM.</span><span class="sxs-lookup"><span data-stu-id="e46db-240">In the next section, we will show how to run singleVM.py in remote DSVM.</span></span> 

### <a name="tuning-hyperparameters-using-remote-dsvm"></a><span data-ttu-id="e46db-241">Tuning hyperparameters using remote DSVM</span><span class="sxs-lookup"><span data-stu-id="e46db-241">Tuning hyperparameters using remote DSVM</span></span>
<span data-ttu-id="e46db-242">We use [xgboost](https://anaconda.org/conda-forge/xgboost) implementation [1] of gradient tree boosting.</span><span class="sxs-lookup"><span data-stu-id="e46db-242">We use [xgboost](https://anaconda.org/conda-forge/xgboost) implementation [1] of gradient tree boosting.</span></span> <span data-ttu-id="e46db-243">We also use [scikit-learn](http://scikit-learn.org/) package to tune hyperparameters of xgboost.</span><span class="sxs-lookup"><span data-stu-id="e46db-243">We also use [scikit-learn](http://scikit-learn.org/) package to tune hyperparameters of xgboost.</span></span> <span data-ttu-id="e46db-244">Although xgboost is not part of scikit-learn package, it implements scikit-learn API and hence can be used together with hyperparameter tuning functions of scikit-learn.</span><span class="sxs-lookup"><span data-stu-id="e46db-244">Although xgboost is not part of scikit-learn package, it implements scikit-learn API and hence can be used together with hyperparameter tuning functions of scikit-learn.</span></span> 

<span data-ttu-id="e46db-245">Xgboost has eight hyperparameters, described [here](https://github.com/dmlc/xgboost/blob/master/doc/parameter.md):</span><span class="sxs-lookup"><span data-stu-id="e46db-245">Xgboost has eight hyperparameters, described [here](https://github.com/dmlc/xgboost/blob/master/doc/parameter.md):</span></span>
* <span data-ttu-id="e46db-246">n_estimators</span><span class="sxs-lookup"><span data-stu-id="e46db-246">n_estimators</span></span>
* <span data-ttu-id="e46db-247">max_depth</span><span class="sxs-lookup"><span data-stu-id="e46db-247">max_depth</span></span>
* <span data-ttu-id="e46db-248">reg_alpha</span><span class="sxs-lookup"><span data-stu-id="e46db-248">reg_alpha</span></span>
* <span data-ttu-id="e46db-249">reg_lambda</span><span class="sxs-lookup"><span data-stu-id="e46db-249">reg_lambda</span></span>
* <span data-ttu-id="e46db-250">colsample\_by_tree</span><span class="sxs-lookup"><span data-stu-id="e46db-250">colsample\_by_tree</span></span>
* <span data-ttu-id="e46db-251">learning_rate</span><span class="sxs-lookup"><span data-stu-id="e46db-251">learning_rate</span></span>
* <span data-ttu-id="e46db-252">colsample\_by_level</span><span class="sxs-lookup"><span data-stu-id="e46db-252">colsample\_by_level</span></span>
* <span data-ttu-id="e46db-253">subsample</span><span class="sxs-lookup"><span data-stu-id="e46db-253">subsample</span></span>
* <span data-ttu-id="e46db-254">objective</span><span class="sxs-lookup"><span data-stu-id="e46db-254">objective</span></span>  
 
<span data-ttu-id="e46db-255">Initially, we use remote DSVM and tune hyperparameters from a small grid of candidate values:</span><span class="sxs-lookup"><span data-stu-id="e46db-255">Initially, we use remote DSVM and tune hyperparameters from a small grid of candidate values:</span></span>

    tuned_parameters = [{'n_estimators': [300,400], 'max_depth': [3,4], 'objective': ['multi:softprob'], 'reg_alpha': [1], 'reg_lambda': [1], 'colsample_bytree': [1],'learning_rate': [0.1], 'colsample_bylevel': [0.1,], 'subsample': [0.5]}]  

<span data-ttu-id="e46db-256">This grid has four combinations of values of hyperparameters.</span><span class="sxs-lookup"><span data-stu-id="e46db-256">This grid has four combinations of values of hyperparameters.</span></span> <span data-ttu-id="e46db-257">We use 5-fold cross validation, resulting in 4x5=20 runs of xgboost.</span><span class="sxs-lookup"><span data-stu-id="e46db-257">We use 5-fold cross validation, resulting in 4x5=20 runs of xgboost.</span></span> <span data-ttu-id="e46db-258">To measure performance of the models, we use negative log loss metric.</span><span class="sxs-lookup"><span data-stu-id="e46db-258">To measure performance of the models, we use negative log loss metric.</span></span> <span data-ttu-id="e46db-259">The following code finds the values of hyperparameters from the grid that maximize the cross-validated negative log loss.</span><span class="sxs-lookup"><span data-stu-id="e46db-259">The following code finds the values of hyperparameters from the grid that maximize the cross-validated negative log loss.</span></span> <span data-ttu-id="e46db-260">The code also uses these values to train the final model over the full training set:</span><span class="sxs-lookup"><span data-stu-id="e46db-260">The code also uses these values to train the final model over the full training set:</span></span>

    clf = XGBClassifier(seed=0)
    metric = 'neg_log_loss'
    
    clf_cv = GridSearchCV(clf, tuned_parameters, scoring=metric, cv=5, n_jobs=8)
    model = clf_cv.fit(X_train,y_train)

<span data-ttu-id="e46db-261">After creating the model, we save the results of the hyperparameter tuning.</span><span class="sxs-lookup"><span data-stu-id="e46db-261">After creating the model, we save the results of the hyperparameter tuning.</span></span> <span data-ttu-id="e46db-262">We use logging API of AML Workbench to save the best values of hyperparameters and corresponding cross-validated estimate of the negative log loss:</span><span class="sxs-lookup"><span data-stu-id="e46db-262">We use logging API of AML Workbench to save the best values of hyperparameters and corresponding cross-validated estimate of the negative log loss:</span></span>

    from azureml.logging import get_azureml_logger

    # initialize logger
    run_logger = get_azureml_logger()

    ...

    run_logger.log(metric, float(clf_cv.best_score_))

    for key in clf_cv.best_params_.keys():
        run_logger.log(key, clf_cv.best_params_[key]) 

<span data-ttu-id="e46db-263">We also create sweeping_results.txt file with cross-validated, negative log losses of all combinations of hyperparameter values in the grid.</span><span class="sxs-lookup"><span data-stu-id="e46db-263">We also create sweeping_results.txt file with cross-validated, negative log losses of all combinations of hyperparameter values in the grid.</span></span>

    if not path.exists('./outputs'):
        makedirs('./outputs')
    outfile = open('./outputs/sweeping_results.txt','w')

    print("metric = ", metric, file=outfile)
    for i in range(len(model.grid_scores_)):
        print(model.grid_scores_[i], file=outfile)
    outfile.close()

This file is stored in a special ./outputs directory. <span data-ttu-id="e46db-265">Later on we show how to download it.</span><span class="sxs-lookup"><span data-stu-id="e46db-265">Later on we show how to download it.</span></span>  

 <span data-ttu-id="e46db-266">Before running singleVM.py in remote DSVM for the first time, we create a Docker container there by running</span><span class="sxs-lookup"><span data-stu-id="e46db-266">Before running singleVM.py in remote DSVM for the first time, we create a Docker container there by running</span></span> 

    az ml experiment prepare -c dsvm

<span data-ttu-id="e46db-267">in CLI windows.</span><span class="sxs-lookup"><span data-stu-id="e46db-267">in CLI windows.</span></span> <span data-ttu-id="e46db-268">Creation of Docker container takes several minutes.</span><span class="sxs-lookup"><span data-stu-id="e46db-268">Creation of Docker container takes several minutes.</span></span> <span data-ttu-id="e46db-269">After that we run singleVM.py in DSVM:</span><span class="sxs-lookup"><span data-stu-id="e46db-269">After that we run singleVM.py in DSVM:</span></span>

    az ml experiment submit -c dsvm .\singleVM.py

<span data-ttu-id="e46db-270">This command finishes in 1 hour 38 minutes when DSVM has 8 cores and 28 Gb of memory.</span><span class="sxs-lookup"><span data-stu-id="e46db-270">This command finishes in 1 hour 38 minutes when DSVM has 8 cores and 28 Gb of memory.</span></span> <span data-ttu-id="e46db-271">The logged values can be viewed in Run History window of AML Workbench:</span><span class="sxs-lookup"><span data-stu-id="e46db-271">The logged values can be viewed in Run History window of AML Workbench:</span></span>

![run history](media/scenario-distributed-tuning-of-hyperparameters/run_history.png)

<span data-ttu-id="e46db-273">By default Run History window shows values and graphs of the first 1-2 logged values.</span><span class="sxs-lookup"><span data-stu-id="e46db-273">By default Run History window shows values and graphs of the first 1-2 logged values.</span></span> <span data-ttu-id="e46db-274">To see the full list of the chosen values of hyperparameters, click on the settings icon marked with red circle in the previous screenshot.</span><span class="sxs-lookup"><span data-stu-id="e46db-274">To see the full list of the chosen values of hyperparameters, click on the settings icon marked with red circle in the previous screenshot.</span></span> <span data-ttu-id="e46db-275">Then, select the hyperparameters to be shown in the table.</span><span class="sxs-lookup"><span data-stu-id="e46db-275">Then, select the hyperparameters to be shown in the table.</span></span> <span data-ttu-id="e46db-276">Also, to select the graphs that are shown in the top part of Run History window, click on the setting icon marked with blue circle and select the graphs from the list.</span><span class="sxs-lookup"><span data-stu-id="e46db-276">Also, to select the graphs that are shown in the top part of Run History window, click on the setting icon marked with blue circle and select the graphs from the list.</span></span> 

<span data-ttu-id="e46db-277">The chosen values of hyperparameters can also be examined in Run Properties window:</span><span class="sxs-lookup"><span data-stu-id="e46db-277">The chosen values of hyperparameters can also be examined in Run Properties window:</span></span> 

![run properties](media/scenario-distributed-tuning-of-hyperparameters/run_properties.png)

<span data-ttu-id="e46db-279">In the top right corner of Run Properties window, there is a section Output Files with the list of all files that were created in '.\output' folder.</span><span class="sxs-lookup"><span data-stu-id="e46db-279">In the top right corner of Run Properties window, there is a section Output Files with the list of all files that were created in '.\output' folder.</span></span> <span data-ttu-id="e46db-280">sweeping\_results.txt can be downloaded from there by selecting it and clicking Download button.</span><span class="sxs-lookup"><span data-stu-id="e46db-280">sweeping\_results.txt can be downloaded from there by selecting it and clicking Download button.</span></span> <span data-ttu-id="e46db-281">sweeping_results.txt should have the following output:</span><span class="sxs-lookup"><span data-stu-id="e46db-281">sweeping_results.txt should have the following output:</span></span>

    metric =  neg_log_loss
    mean: -2.29096, std: 0.03748, params: {'colsample_bytree': 1, 'learning_rate': 0.1, 'subsample': 0.5, 'n_estimators': 300, 'reg_alpha': 1, 'objective': 'multi:softprob', 'colsample_bylevel': 0.1, 'reg_lambda': 1, 'max_depth': 3}
    mean: -2.28712, std: 0.03822, params: {'colsample_bytree': 1, 'learning_rate': 0.1, 'subsample': 0.5, 'n_estimators': 400, 'reg_alpha': 1, 'objective': 'multi:softprob', 'colsample_bylevel': 0.1, 'reg_lambda': 1, 'max_depth': 3}
    mean: -2.28706, std: 0.03863, params: {'colsample_bytree': 1, 'learning_rate': 0.1, 'subsample': 0.5, 'n_estimators': 300, 'reg_alpha': 1, 'objective': 'multi:softprob', 'colsample_bylevel': 0.1, 'reg_lambda': 1, 'max_depth': 4}
    mean: -2.28530, std: 0.03927, params: {'colsample_bytree': 1, 'learning_rate': 0.1, 'subsample': 0.5, 'n_estimators': 400, 'reg_alpha': 1, 'objective': 'multi:softprob', 'colsample_bylevel': 0.1, 'reg_lambda': 1, 'max_depth': 4}

### <a name="tuning-hyperparameters-using-spark-cluster"></a><span data-ttu-id="e46db-282">Tuning hyperparameters using Spark cluster</span><span class="sxs-lookup"><span data-stu-id="e46db-282">Tuning hyperparameters using Spark cluster</span></span>
<span data-ttu-id="e46db-283">We use Spark cluster to scale out tuning hyperparameters and use larger grid.</span><span class="sxs-lookup"><span data-stu-id="e46db-283">We use Spark cluster to scale out tuning hyperparameters and use larger grid.</span></span> <span data-ttu-id="e46db-284">Our new grid is</span><span class="sxs-lookup"><span data-stu-id="e46db-284">Our new grid is</span></span>

    tuned_parameters = [{'n_estimators': [300,400], 'max_depth': [3,4], 'objective': ['multi:softprob'], 'reg_alpha': [1], 'reg_lambda': [1], 'colsample_bytree': [1], 'learning_rate': [0.1], 'colsample_bylevel': [0.01, 0.1], 'subsample': [0.5, 0.7]}]

<span data-ttu-id="e46db-285">This grid has 16 combinations of values of hyperparameters.</span><span class="sxs-lookup"><span data-stu-id="e46db-285">This grid has 16 combinations of values of hyperparameters.</span></span> <span data-ttu-id="e46db-286">Since we use 5-fold cross validation, we run xgboost 16x5=80 times.</span><span class="sxs-lookup"><span data-stu-id="e46db-286">Since we use 5-fold cross validation, we run xgboost 16x5=80 times.</span></span>

<span data-ttu-id="e46db-287">scikit-learn package does not have a native support of tuning hyperparameters using Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e46db-287">scikit-learn package does not have a native support of tuning hyperparameters using Spark cluster.</span></span> <span data-ttu-id="e46db-288">Fortunately, [spark-sklearn](https://spark-packages.org/package/databricks/spark-sklearn) package from Databricks fills this gap.</span><span class="sxs-lookup"><span data-stu-id="e46db-288">Fortunately, [spark-sklearn](https://spark-packages.org/package/databricks/spark-sklearn) package from Databricks fills this gap.</span></span> <span data-ttu-id="e46db-289">This package provides GridSearchCV function that has almost the same API as GridSearchCV function in scikit-learn.</span><span class="sxs-lookup"><span data-stu-id="e46db-289">This package provides GridSearchCV function that has almost the same API as GridSearchCV function in scikit-learn.</span></span> <span data-ttu-id="e46db-290">To use spark-sklearn and tune hyperparameters using Spark we need to create a Spark context</span><span class="sxs-lookup"><span data-stu-id="e46db-290">To use spark-sklearn and tune hyperparameters using Spark we need to create a Spark context</span></span>

    from pyspark import SparkContext
    sc = SparkContext.getOrCreate()

<span data-ttu-id="e46db-291">Then we replace</span><span class="sxs-lookup"><span data-stu-id="e46db-291">Then we replace</span></span> 

    from sklearn.model_selection import GridSearchCV

<span data-ttu-id="e46db-292">with</span><span class="sxs-lookup"><span data-stu-id="e46db-292">with</span></span> 

    from spark_sklearn import GridSearchCV

<span data-ttu-id="e46db-293">Also we replace the call to GridSearchCV from scikit-learn to the one from spark-sklearn:</span><span class="sxs-lookup"><span data-stu-id="e46db-293">Also we replace the call to GridSearchCV from scikit-learn to the one from spark-sklearn:</span></span>

    clf_cv = GridSearchCV(sc = sc, param_grid = tuned_parameters, estimator = clf, scoring=metric, cv=5)

<span data-ttu-id="e46db-294">The final code for tuning hyperparameters using Spark is in distributed\_sweep.py file.</span><span class="sxs-lookup"><span data-stu-id="e46db-294">The final code for tuning hyperparameters using Spark is in distributed\_sweep.py file.</span></span> <span data-ttu-id="e46db-295">The difference between singleVM.py and distributed_sweep.py is in definition of grid and additional four lines of code.</span><span class="sxs-lookup"><span data-stu-id="e46db-295">The difference between singleVM.py and distributed_sweep.py is in definition of grid and additional four lines of code.</span></span> <span data-ttu-id="e46db-296">Notice also that due to AML Workbench services, the logging code does not change when changing execution environment from remote DSVM to Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e46db-296">Notice also that due to AML Workbench services, the logging code does not change when changing execution environment from remote DSVM to Spark cluster.</span></span>

<span data-ttu-id="e46db-297">Before running distributed_sweep.py in Spark cluster for the first time, we need to install Python packages there.</span><span class="sxs-lookup"><span data-stu-id="e46db-297">Before running distributed_sweep.py in Spark cluster for the first time, we need to install Python packages there.</span></span> <span data-ttu-id="e46db-298">This can be achieved by running</span><span class="sxs-lookup"><span data-stu-id="e46db-298">This can be achieved by running</span></span> 

    az ml experiment prepare -c spark

<span data-ttu-id="e46db-299">in CLI windows.</span><span class="sxs-lookup"><span data-stu-id="e46db-299">in CLI windows.</span></span> <span data-ttu-id="e46db-300">This installation takes several minutes.</span><span class="sxs-lookup"><span data-stu-id="e46db-300">This installation takes several minutes.</span></span> <span data-ttu-id="e46db-301">After that we run distributed_sweep.py in Spark cluster:</span><span class="sxs-lookup"><span data-stu-id="e46db-301">After that we run distributed_sweep.py in Spark cluster:</span></span>

    az ml experiment submit -c spark .\distributed_sweep.py

<span data-ttu-id="e46db-302">This command finishes in 1 hour 6 minutes when Spark cluster has 6 worker nodes with 28 Gb of memory.</span><span class="sxs-lookup"><span data-stu-id="e46db-302">This command finishes in 1 hour 6 minutes when Spark cluster has 6 worker nodes with 28 Gb of memory.</span></span> <span data-ttu-id="e46db-303">The results of hyperparameter-tuning can be accessed in Azure Machine Learning Workbench the same way as remote DSVM execution.</span><span class="sxs-lookup"><span data-stu-id="e46db-303">The results of hyperparameter-tuning can be accessed in Azure Machine Learning Workbench the same way as remote DSVM execution.</span></span> <span data-ttu-id="e46db-304">(namely logs, best values of hyperparameters, and sweeping_results.txt file)</span><span class="sxs-lookup"><span data-stu-id="e46db-304">(namely logs, best values of hyperparameters, and sweeping_results.txt file)</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="e46db-305">Architecture diagram</span><span class="sxs-lookup"><span data-stu-id="e46db-305">Architecture diagram</span></span>

<span data-ttu-id="e46db-306">The following diagram shows the overall workflow: ![architecture](media/scenario-distributed-tuning-of-hyperparameters/architecture.png)</span><span class="sxs-lookup"><span data-stu-id="e46db-306">The following diagram shows the overall workflow: ![architecture](media/scenario-distributed-tuning-of-hyperparameters/architecture.png)</span></span> 

## <a name="conclusion"></a><span data-ttu-id="e46db-307">Conclusion</span><span class="sxs-lookup"><span data-stu-id="e46db-307">Conclusion</span></span> 

<span data-ttu-id="e46db-308">In this scenario, we showed how to use Azure Machine Learning Workbench to perform tuning of hyperparameters in remote virtual machines and Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="e46db-308">In this scenario, we showed how to use Azure Machine Learning Workbench to perform tuning of hyperparameters in remote virtual machines and Spark clusters.</span></span> <span data-ttu-id="e46db-309">We saw that Azure Machine Learning Workbench provides tools for easy configuration of execution environments.</span><span class="sxs-lookup"><span data-stu-id="e46db-309">We saw that Azure Machine Learning Workbench provides tools for easy configuration of execution environments.</span></span> <span data-ttu-id="e46db-310">It also allows easily switching between them.</span><span class="sxs-lookup"><span data-stu-id="e46db-310">It also allows easily switching between them.</span></span> 

## <a name="references"></a><span data-ttu-id="e46db-311">References</span><span class="sxs-lookup"><span data-stu-id="e46db-311">References</span></span>

<span data-ttu-id="e46db-312">[1] T. Chen and C. Guestrin.</span><span class="sxs-lookup"><span data-stu-id="e46db-312">[1] T. Chen and C. Guestrin.</span></span> <span data-ttu-id="e46db-313">[XGBoost: A Scalable Tree Boosting System](https://arxiv.org/abs/1603.02754).</span><span class="sxs-lookup"><span data-stu-id="e46db-313">[XGBoost: A Scalable Tree Boosting System](https://arxiv.org/abs/1603.02754).</span></span> <span data-ttu-id="e46db-314">KDD 2016.</span><span class="sxs-lookup"><span data-stu-id="e46db-314">KDD 2016.</span></span>




