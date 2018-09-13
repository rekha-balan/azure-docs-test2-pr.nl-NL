---
title: Access datasets with Machine Learning Python client library | Microsoft Docs
description: Install and use the Python client library to access and manage Azure Machine Learning data securely from a local Python environment.
services: machine-learning
documentationcenter: python
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 9f84686f8689a40cf002035053236b415481488f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869633"
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="8d912-103">Access datasets with Python using the Azure Machine Learning Python client library</span><span class="sxs-lookup"><span data-stu-id="8d912-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="8d912-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span><span class="sxs-lookup"><span data-stu-id="8d912-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="8d912-105">This topic provides instructions on how to:</span><span class="sxs-lookup"><span data-stu-id="8d912-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="8d912-106">install the Machine Learning Python client library</span><span class="sxs-lookup"><span data-stu-id="8d912-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="8d912-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span><span class="sxs-lookup"><span data-stu-id="8d912-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="8d912-108">access intermediate datasets from experiments</span><span class="sxs-lookup"><span data-stu-id="8d912-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="8d912-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span><span class="sxs-lookup"><span data-stu-id="8d912-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a><span data-ttu-id="8d912-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d912-110">Prerequisites</span></span>
<span data-ttu-id="8d912-111">The Python client library has been tested under the following environments:</span><span class="sxs-lookup"><span data-stu-id="8d912-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="8d912-112">Windows, Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="8d912-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="8d912-113">Python 2.7, 3.3 and 3.4</span><span class="sxs-lookup"><span data-stu-id="8d912-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="8d912-114">It has a dependency on the following packages:</span><span class="sxs-lookup"><span data-stu-id="8d912-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="8d912-115">requests</span><span class="sxs-lookup"><span data-stu-id="8d912-115">requests</span></span>
* <span data-ttu-id="8d912-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="8d912-116">python-dateutil</span></span>
* <span data-ttu-id="8d912-117">pandas</span><span class="sxs-lookup"><span data-stu-id="8d912-117">pandas</span></span>

<span data-ttu-id="8d912-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span><span class="sxs-lookup"><span data-stu-id="8d912-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="8d912-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span><span class="sxs-lookup"><span data-stu-id="8d912-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <a name="installation"></a><span data-ttu-id="8d912-120">How to install the Azure Machine Learning Python client library</span><span class="sxs-lookup"><span data-stu-id="8d912-120">How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="8d912-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span><span class="sxs-lookup"><span data-stu-id="8d912-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="8d912-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="8d912-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="8d912-123">To install it in your Python environment, run the following command from your local Python environment:</span><span class="sxs-lookup"><span data-stu-id="8d912-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="8d912-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="8d912-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="8d912-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span><span class="sxs-lookup"><span data-stu-id="8d912-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a><span data-ttu-id="8d912-126">Use Studio Code snippets to access datasets</span><span class="sxs-lookup"><span data-stu-id="8d912-126">Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="8d912-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span><span class="sxs-lookup"><span data-stu-id="8d912-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="8d912-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span><span class="sxs-lookup"><span data-stu-id="8d912-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <a name="security"></a><span data-ttu-id="8d912-129">Security for data access</span><span class="sxs-lookup"><span data-stu-id="8d912-129">Security for data access</span></span>
<span data-ttu-id="8d912-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span><span class="sxs-lookup"><span data-stu-id="8d912-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="8d912-131">These provide full access to your workspace and must be protected, like a password.</span><span class="sxs-lookup"><span data-stu-id="8d912-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="8d912-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span><span class="sxs-lookup"><span data-stu-id="8d912-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="8d912-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span><span class="sxs-lookup"><span data-stu-id="8d912-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Security][security]

<span data-ttu-id="8d912-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span><span class="sxs-lookup"><span data-stu-id="8d912-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="8d912-136">To obtain the authorization token, you can do one of the following:</span><span class="sxs-lookup"><span data-stu-id="8d912-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="8d912-137">Ask for a token from an owner.</span><span class="sxs-lookup"><span data-stu-id="8d912-137">Ask for a token from an owner.</span></span> <span data-ttu-id="8d912-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span><span class="sxs-lookup"><span data-stu-id="8d912-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="8d912-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span><span class="sxs-lookup"><span data-stu-id="8d912-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="8d912-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span><span class="sxs-lookup"><span data-stu-id="8d912-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Authorization tokens](./media/python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="8d912-142">Ask to be promoted to role of owner.</span><span class="sxs-lookup"><span data-stu-id="8d912-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="8d912-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span><span class="sxs-lookup"><span data-stu-id="8d912-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="8d912-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span><span class="sxs-lookup"><span data-stu-id="8d912-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="8d912-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="8d912-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="8d912-146">You can regenerate them, but this procedure revokes access to the previous token.</span><span class="sxs-lookup"><span data-stu-id="8d912-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <a name="accessingDatasets"></a><span data-ttu-id="8d912-147">Access datasets from a local Python application</span><span class="sxs-lookup"><span data-stu-id="8d912-147">Access datasets from a local Python application</span></span>
1. <span data-ttu-id="8d912-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span><span class="sxs-lookup"><span data-stu-id="8d912-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="8d912-149">Select the dataset you would like to access.</span><span class="sxs-lookup"><span data-stu-id="8d912-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="8d912-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span><span class="sxs-lookup"><span data-stu-id="8d912-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="8d912-151">From the bottom toolbar, click **Generate Data Access Code**.</span><span class="sxs-lookup"><span data-stu-id="8d912-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="8d912-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span><span class="sxs-lookup"><span data-stu-id="8d912-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![Datasets][datasets]
4. <span data-ttu-id="8d912-154">Select the code snippet from the window that appears and copy it to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="8d912-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Access Code][dataset-access-code]
5. <span data-ttu-id="8d912-156">Paste the code into the notebook of your local Python application.</span><span class="sxs-lookup"><span data-stu-id="8d912-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Notebook][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a><span data-ttu-id="8d912-158">Access intermediate datasets from Machine Learning experiments</span><span class="sxs-lookup"><span data-stu-id="8d912-158">Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="8d912-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span><span class="sxs-lookup"><span data-stu-id="8d912-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="8d912-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span><span class="sxs-lookup"><span data-stu-id="8d912-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="8d912-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span><span class="sxs-lookup"><span data-stu-id="8d912-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="8d912-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span><span class="sxs-lookup"><span data-stu-id="8d912-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="8d912-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="8d912-163">PlainText</span></span>
* <span data-ttu-id="8d912-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="8d912-164">GenericCSV</span></span>
* <span data-ttu-id="8d912-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="8d912-165">GenericTSV</span></span>
* <span data-ttu-id="8d912-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d912-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="8d912-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d912-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="8d912-168">You can determine the format by hovering over a module output node.</span><span class="sxs-lookup"><span data-stu-id="8d912-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="8d912-169">It is displayed along with the node name, in a tooltip.</span><span class="sxs-lookup"><span data-stu-id="8d912-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="8d912-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span><span class="sxs-lookup"><span data-stu-id="8d912-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Dataset Format][dataset-format]

<span data-ttu-id="8d912-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span><span class="sxs-lookup"><span data-stu-id="8d912-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![GenericCSV Format][csv-format]

<span data-ttu-id="8d912-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span><span class="sxs-lookup"><span data-stu-id="8d912-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="8d912-175">Create a new experiment.</span><span class="sxs-lookup"><span data-stu-id="8d912-175">Create a new experiment.</span></span>
2. <span data-ttu-id="8d912-176">Insert an **Adult Census Income Binary Classification dataset** module.</span><span class="sxs-lookup"><span data-stu-id="8d912-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="8d912-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span><span class="sxs-lookup"><span data-stu-id="8d912-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="8d912-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span><span class="sxs-lookup"><span data-stu-id="8d912-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="8d912-179">Save the experiment, run it, and wait for it to finish running.</span><span class="sxs-lookup"><span data-stu-id="8d912-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="8d912-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span><span class="sxs-lookup"><span data-stu-id="8d912-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="8d912-181">When the context menu appears, select **Generate Data Access Code**.</span><span class="sxs-lookup"><span data-stu-id="8d912-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Context Menu][experiment]
8. <span data-ttu-id="8d912-183">Select the code snippet and copy it to your clipboard from the window that appears.</span><span class="sxs-lookup"><span data-stu-id="8d912-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Access Code][intermediate-dataset-access-code]
9. <span data-ttu-id="8d912-185">Paste the code in your notebook.</span><span class="sxs-lookup"><span data-stu-id="8d912-185">Paste the code in your notebook.</span></span>
   
    ![Notebook][ipython-intermediate-dataset]
10. <span data-ttu-id="8d912-187">You can visualize the data using matplotlib.</span><span class="sxs-lookup"><span data-stu-id="8d912-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="8d912-188">This displays in a histogram for the age column:</span><span class="sxs-lookup"><span data-stu-id="8d912-188">This displays in a histogram for the age column:</span></span>
    
    ![Histogram][ipython-histogram]

## <a name="clientApis"></a><span data-ttu-id="8d912-190">Use the Machine Learning Python client library to access, read, create, and manage datasets</span><span class="sxs-lookup"><span data-stu-id="8d912-190">Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="8d912-191">Workspace</span><span class="sxs-lookup"><span data-stu-id="8d912-191">Workspace</span></span>
<span data-ttu-id="8d912-192">The workspace is the entry point for the Python client library.</span><span class="sxs-lookup"><span data-stu-id="8d912-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="8d912-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span><span class="sxs-lookup"><span data-stu-id="8d912-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="8d912-194">Enumerate datasets</span><span class="sxs-lookup"><span data-stu-id="8d912-194">Enumerate datasets</span></span>
<span data-ttu-id="8d912-195">To enumerate all datasets in a given workspace:</span><span class="sxs-lookup"><span data-stu-id="8d912-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="8d912-196">To enumerate just the user-created datasets:</span><span class="sxs-lookup"><span data-stu-id="8d912-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="8d912-197">To enumerate just the example datasets:</span><span class="sxs-lookup"><span data-stu-id="8d912-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="8d912-198">You can access a dataset by name (which is case-sensitive):</span><span class="sxs-lookup"><span data-stu-id="8d912-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="8d912-199">Or you can access it by index:</span><span class="sxs-lookup"><span data-stu-id="8d912-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="8d912-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="8d912-200">Metadata</span></span>
<span data-ttu-id="8d912-201">Datasets have metadata, in addition to content.</span><span class="sxs-lookup"><span data-stu-id="8d912-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="8d912-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span><span class="sxs-lookup"><span data-stu-id="8d912-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="8d912-203">Some metadata values are assigned by the user at creation time:</span><span class="sxs-lookup"><span data-stu-id="8d912-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="8d912-204">Others are values assigned by Azure ML:</span><span class="sxs-lookup"><span data-stu-id="8d912-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="8d912-205">See the `SourceDataset` class for more on the available metadata.</span><span class="sxs-lookup"><span data-stu-id="8d912-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="8d912-206">Read contents</span><span class="sxs-lookup"><span data-stu-id="8d912-206">Read contents</span></span>
<span data-ttu-id="8d912-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span><span class="sxs-lookup"><span data-stu-id="8d912-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="8d912-208">This is done with the `to_dataframe` method:</span><span class="sxs-lookup"><span data-stu-id="8d912-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="8d912-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span><span class="sxs-lookup"><span data-stu-id="8d912-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="8d912-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span><span class="sxs-lookup"><span data-stu-id="8d912-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="8d912-211">To read the contents as text:</span><span class="sxs-lookup"><span data-stu-id="8d912-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="8d912-212">To read the contents as binary:</span><span class="sxs-lookup"><span data-stu-id="8d912-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="8d912-213">You can also just open a stream to the contents:</span><span class="sxs-lookup"><span data-stu-id="8d912-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="8d912-214">Create a new dataset</span><span class="sxs-lookup"><span data-stu-id="8d912-214">Create a new dataset</span></span>
<span data-ttu-id="8d912-215">The Python client library allows you to upload datasets from your Python program.</span><span class="sxs-lookup"><span data-stu-id="8d912-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="8d912-216">These datasets are then available for use in your workspace.</span><span class="sxs-lookup"><span data-stu-id="8d912-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="8d912-217">If you have your data in a Pandas DataFrame, use the following code:</span><span class="sxs-lookup"><span data-stu-id="8d912-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="8d912-218">If your data is already serialized, you can use:</span><span class="sxs-lookup"><span data-stu-id="8d912-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="8d912-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span><span class="sxs-lookup"><span data-stu-id="8d912-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="8d912-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="8d912-220">PlainText</span></span>
* <span data-ttu-id="8d912-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="8d912-221">GenericCSV</span></span>
* <span data-ttu-id="8d912-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="8d912-222">GenericTSV</span></span>
* <span data-ttu-id="8d912-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d912-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="8d912-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d912-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="8d912-225">Update an existing dataset</span><span class="sxs-lookup"><span data-stu-id="8d912-225">Update an existing dataset</span></span>
<span data-ttu-id="8d912-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span><span class="sxs-lookup"><span data-stu-id="8d912-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="8d912-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span><span class="sxs-lookup"><span data-stu-id="8d912-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="8d912-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span><span class="sxs-lookup"><span data-stu-id="8d912-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="8d912-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d912-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="8d912-230">You can optionally set a new description by specifying a value for the `description` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d912-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="8d912-231">You can optionally set a new name by specifying a value for the `name` parameter.</span><span class="sxs-lookup"><span data-stu-id="8d912-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="8d912-232">From now on, you'll retrieve the dataset using the new name only.</span><span class="sxs-lookup"><span data-stu-id="8d912-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="8d912-233">The following code updates the data, name and description.</span><span class="sxs-lookup"><span data-stu-id="8d912-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="8d912-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span><span class="sxs-lookup"><span data-stu-id="8d912-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="8d912-235">The `dataframe` parameter is always required.</span><span class="sxs-lookup"><span data-stu-id="8d912-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="8d912-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="8d912-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="8d912-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span><span class="sxs-lookup"><span data-stu-id="8d912-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/python-data-access/security.png
[dataset-format]:./media/python-data-access/dataset-format.png
[csv-format]:./media/python-data-access/csv-format.png
[datasets]:./media/python-data-access/datasets.png
[dataset-access-code]:./media/python-data-access/dataset-access-code.png
[ipython-dataset]:./media/python-data-access/ipython-dataset.png
[experiment]:./media/python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

