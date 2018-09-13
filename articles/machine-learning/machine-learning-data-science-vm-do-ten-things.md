---
title: Ten things you can do on the Data science Virtual Machine  | Microsoft Docs
description: Perform various data exploration and modeling task on the Data science Virtual Machine.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 95fe838b033e823686bb163350325a8acd3c4250
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549637"
---
# <a name="ten-things-you-can-do-on-the-data-science-virtual-machine"></a><span data-ttu-id="15da3-103">Ten things you can do on the Data science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="15da3-103">Ten things you can do on the Data science Virtual Machine</span></span>
<span data-ttu-id="15da3-104">The Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks.</span><span class="sxs-lookup"><span data-stu-id="15da3-104">The Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks.</span></span> <span data-ttu-id="15da3-105">The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span><span class="sxs-lookup"><span data-stu-id="15da3-105">The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="15da3-106">The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="15da3-106">The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in DocumentDB.</span></span> <span data-ttu-id="15da3-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="15da3-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="15da3-108">In this article we walk you through how to use your DSVM to perform various data science tasks and interact with other Azure services.</span><span class="sxs-lookup"><span data-stu-id="15da3-108">In this article we walk you through how to use your DSVM to perform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="15da3-109">Here are some of the things you can do on the DSVM:</span><span class="sxs-lookup"><span data-stu-id="15da3-109">Here are some of the things you can do on the DSVM:</span></span>

1. <span data-ttu-id="15da3-110">Explore data and develop models locally on the DSVM using Microsoft R Server, Python</span><span class="sxs-lookup"><span data-stu-id="15da3-110">Explore data and develop models locally on the DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="15da3-111">Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span><span class="sxs-lookup"><span data-stu-id="15da3-111">Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="15da3-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span><span class="sxs-lookup"><span data-stu-id="15da3-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="15da3-113">Administer your Azure resources using  Azure portal or Powershell</span><span class="sxs-lookup"><span data-stu-id="15da3-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="15da3-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File Storage as a mountable drive on your DSVM</span><span class="sxs-lookup"><span data-stu-id="15da3-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File Storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="15da3-115">Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.</span><span class="sxs-lookup"><span data-stu-id="15da3-115">Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="15da3-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure DocumentDB, Azure SQL Data Warehouse & databases</span><span class="sxs-lookup"><span data-stu-id="15da3-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure DocumentDB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="15da3-117">Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud</span><span class="sxs-lookup"><span data-stu-id="15da3-117">Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud</span></span>
9. <span data-ttu-id="15da3-118">Dynamically scale your DSVM to meet your project needs</span><span class="sxs-lookup"><span data-stu-id="15da3-118">Dynamically scale your DSVM to meet your project needs</span></span>
10. <span data-ttu-id="15da3-119">Install additional tools on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="15da3-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="15da3-120">Additional usage charges will apply for many of the additional data storage and analytics services listed in this article.</span><span class="sxs-lookup"><span data-stu-id="15da3-120">Additional usage charges will apply for many of the additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="15da3-121">Please refer to the [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span><span class="sxs-lookup"><span data-stu-id="15da3-121">Please refer to the [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="15da3-122">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="15da3-122">**Prerequisites**</span></span>

* <span data-ttu-id="15da3-123">You will need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="15da3-123">You will need an Azure subscription.</span></span> <span data-ttu-id="15da3-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="15da3-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="15da3-125">Instructions for provisioning a Data Science Virtual Machine on the Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="15da3-125">Instructions for provisioning a Data Science Virtual Machine on the Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="15da3-126">1. Explore data and develop models using Microsoft R Server or Python</span><span class="sxs-lookup"><span data-stu-id="15da3-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="15da3-127">You can use languages like R and Python to do your data analytics right on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="15da3-127">You can use languages like R and Python to do your data analytics right on the DSVM.</span></span>

<span data-ttu-id="15da3-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on the start menu or the desktop.</span><span class="sxs-lookup"><span data-stu-id="15da3-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on the start menu or the desktop.</span></span> <span data-ttu-id="15da3-129">Microsoft has provided additional libraries on top of the Open source/CRAN-R to enable scalable analytics and the ability to analyze data larger than the memory size allowed by doing parallel chunked analysis.</span><span class="sxs-lookup"><span data-stu-id="15da3-129">Microsoft has provided additional libraries on top of the Open source/CRAN-R to enable scalable analytics and the ability to analyze data larger than the memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="15da3-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="15da3-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="15da3-131">For Python, you can use an IDE like Visual Studio Community Edition which has the Python Tools for Visual Studio (PTVS) extension pre-installed.</span><span class="sxs-lookup"><span data-stu-id="15da3-131">For Python, you can use an IDE like Visual Studio Community Edition which has the Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="15da3-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span><span class="sxs-lookup"><span data-stu-id="15da3-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="15da3-133">In order to enable Anaconda Python 2.7 and 3.5, you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="15da3-133">In order to enable Anaconda Python 2.7 and 3.5, you need to do the following:</span></span>

* <span data-ttu-id="15da3-134">Create custom environments for each version by navigating to **Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in the Visual Studio 2015 Community Edition</span><span class="sxs-lookup"><span data-stu-id="15da3-134">Create custom environments for each version by navigating to **Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in the Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="15da3-135">Give a description and set the environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="15da3-135">Give a description and set the environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="15da3-136">Click **Auto Detect** and then **Apply** to save the environment.</span><span class="sxs-lookup"><span data-stu-id="15da3-136">Click **Auto Detect** and then **Apply** to save the environment.</span></span>

<span data-ttu-id="15da3-137">Here is what the custom environment setup looks like in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15da3-137">Here is what the custom environment setup looks like in Visual Studio.</span></span>

![PTVS Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="15da3-139">See the [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how to create Python Environments.</span><span class="sxs-lookup"><span data-stu-id="15da3-139">See the [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how to create Python Environments.</span></span>

<span data-ttu-id="15da3-140">Now you are set up to create a new Python project.</span><span class="sxs-lookup"><span data-stu-id="15da3-140">Now you are set up to create a new Python project.</span></span> <span data-ttu-id="15da3-141">Navigate to **File** -> **New** -> **Project** -> **Python** and select the type of Python application you are building.</span><span class="sxs-lookup"><span data-stu-id="15da3-141">Navigate to **File** -> **New** -> **Project** -> **Python** and select the type of Python application you are building.</span></span> <span data-ttu-id="15da3-142">You can set the Python environment for the current project to the desired version (Anaconda 2.7 or 3.5): right-click the **Python environment**, select **Add/Remove Python Environments**, and then select the desired environment to associate with the project.</span><span class="sxs-lookup"><span data-stu-id="15da3-142">You can set the Python environment for the current project to the desired version (Anaconda 2.7 or 3.5): right-click the **Python environment**, select **Add/Remove Python Environments**, and then select the desired environment to associate with the project.</span></span> <span data-ttu-id="15da3-143">You can find more information about working with PTVS on the product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span><span class="sxs-lookup"><span data-stu-id="15da3-143">You can find more information about working with PTVS on the product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-to-explore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="15da3-144">2. Using a Jupyter Notebook to explore and model your data with Python or R</span><span class="sxs-lookup"><span data-stu-id="15da3-144">2. Using a Jupyter Notebook to explore and model your data with Python or R</span></span>
<span data-ttu-id="15da3-145">The Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span><span class="sxs-lookup"><span data-stu-id="15da3-145">The Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="15da3-146">You can use Python 2, Python 3 or R (both Open Source and the Microsoft R Server) in a Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="15da3-146">You can use Python 2, Python 3 or R (both Open Source and the Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="15da3-147">To launch the Jupyter Notebook click on the start menu icon / desktop icon titled **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="15da3-147">To launch the Jupyter Notebook click on the start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="15da3-148">On the DSVM you can also browse to "https://localhost:9999/" to access the Jupiter Notebook.</span><span class="sxs-lookup"><span data-stu-id="15da3-148">On the DSVM you can also browse to "https://localhost:9999/" to access the Jupiter Notebook.</span></span> <span data-ttu-id="15da3-149">If it prompts you for a password, use instructions provided in the ***How to create a strong password on the Jupyter notebook server*** section of the [Provision the Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic to create a strong password to access the Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="15da3-149">If it prompts you for a password, use instructions provided in the ***How to create a strong password on the Jupyter notebook server*** section of the [Provision the Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic to create a strong password to access the Jupyter notebook.</span></span> 

<span data-ttu-id="15da3-150">Once you have opened the notebook, you will see a directory that contains a few example notebooks that are pre-packaged into the DSVM.</span><span class="sxs-lookup"><span data-stu-id="15da3-150">Once you have opened the notebook, you will see a directory that contains a few example notebooks that are pre-packaged into the DSVM.</span></span> <span data-ttu-id="15da3-151">Now you can:</span><span class="sxs-lookup"><span data-stu-id="15da3-151">Now you can:</span></span>

* <span data-ttu-id="15da3-152">click on the notebook to see the code.</span><span class="sxs-lookup"><span data-stu-id="15da3-152">click on the notebook to see the code.</span></span>
* <span data-ttu-id="15da3-153">execute each cell by pressing **SHIFT-ENTER**.</span><span class="sxs-lookup"><span data-stu-id="15da3-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="15da3-154">run the entire notebook by clicking on **Cell** -> **Run**</span><span class="sxs-lookup"><span data-stu-id="15da3-154">run the entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="15da3-155">create a new notebook by clicking on the Jupyter Icon (left top corner) and then clicking **New** button on the right and then choosing the notebook language (also known as kernels).</span><span class="sxs-lookup"><span data-stu-id="15da3-155">create a new notebook by clicking on the Jupyter Icon (left top corner) and then clicking **New** button on the right and then choosing the notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="15da3-156">Currently we support Python 2.7, Python 3.5 and R. The R kernel supports programming in both Open source R as well as the enterprise scalable Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="15da3-156">Currently we support Python 2.7, Python 3.5 and R. The R kernel supports programming in both Open source R as well as the enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="15da3-157">Once you are in the notebook you can explore your data, build the model, test the model using your choice of libraries.</span><span class="sxs-lookup"><span data-stu-id="15da3-157">Once you are in the notebook you can explore your data, build the model, test the model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="15da3-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15da3-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="15da3-159">Once you have built and validated your model the next step is usually to deploy it into production.</span><span class="sxs-lookup"><span data-stu-id="15da3-159">Once you have built and validated your model the next step is usually to deploy it into production.</span></span> <span data-ttu-id="15da3-160">This allows your client applications to invoke the model predictions on a real time or on a batch mode basis.</span><span class="sxs-lookup"><span data-stu-id="15da3-160">This allows your client applications to invoke the model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="15da3-161">Azure Machine Learning provides a mechanism to operationalize a model built in either R or Python.</span><span class="sxs-lookup"><span data-stu-id="15da3-161">Azure Machine Learning provides a mechanism to operationalize a model built in either R or Python.</span></span>

<span data-ttu-id="15da3-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients to make REST calls that pass in input parameters and receive predictions from the model as outputs.</span><span class="sxs-lookup"><span data-stu-id="15da3-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients to make REST calls that pass in input parameters and receive predictions from the model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="15da3-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting the [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span><span class="sxs-lookup"><span data-stu-id="15da3-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting the [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="15da3-164">Build and Operationalize Python models</span><span class="sxs-lookup"><span data-stu-id="15da3-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="15da3-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using the SciKit-learn library.</span><span class="sxs-lookup"><span data-stu-id="15da3-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using the SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="15da3-166">The method used to deploy your python models to Azure Machine Learning wraps the prediction of the model into a function and decorates it with attributes provided by the pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and the input and return parameters.</span><span class="sxs-lookup"><span data-stu-id="15da3-166">The method used to deploy your python models to Azure Machine Learning wraps the prediction of the model into a function and decorates it with attributes provided by the pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and the input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="15da3-167">A client can now make calls to the web service.</span><span class="sxs-lookup"><span data-stu-id="15da3-167">A client can now make calls to the web service.</span></span> <span data-ttu-id="15da3-168">There are convenience wrappers that construct the REST API requests.</span><span class="sxs-lookup"><span data-stu-id="15da3-168">There are convenience wrappers that construct the REST API requests.</span></span> <span data-ttu-id="15da3-169">Here is a sample code to consume the web service.</span><span class="sxs-lookup"><span data-stu-id="15da3-169">Here is a sample code to consume the web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="15da3-170">The Azure Machine Learning library is only supported on Python 2.7 currently.</span><span class="sxs-lookup"><span data-stu-id="15da3-170">The Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="15da3-171">Build and Operationalize R models</span><span class="sxs-lookup"><span data-stu-id="15da3-171">Build and Operationalize R models</span></span>
<span data-ttu-id="15da3-172">You can deploy R models built on the Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar to how it is done for Python.</span><span class="sxs-lookup"><span data-stu-id="15da3-172">You can deploy R models built on the Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar to how it is done for Python.</span></span> <span data-ttu-id="15da3-173">Her are the steps:</span><span class="sxs-lookup"><span data-stu-id="15da3-173">Her are the steps:</span></span>

* <span data-ttu-id="15da3-174">create a settings.json file as below to provide your workspace ID and auth token.</span><span class="sxs-lookup"><span data-stu-id="15da3-174">create a settings.json file as below to provide your workspace ID and auth token.</span></span>
* <span data-ttu-id="15da3-175">write a wrapper for the model's predict function.</span><span class="sxs-lookup"><span data-stu-id="15da3-175">write a wrapper for the model's predict function.</span></span>
* <span data-ttu-id="15da3-176">call ```publishWebService``` in the Azure Machine Learning library to pass in the function wrapper.</span><span class="sxs-lookup"><span data-stu-id="15da3-176">call ```publishWebService``` in the Azure Machine Learning library to pass in the function wrapper.</span></span>  

<span data-ttu-id="15da3-177">Here is the procedure and code snippets that can be used to set up, build, publish, and consume a model as a web service in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15da3-177">Here is the procedure and code snippets that can be used to set up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="15da3-178">Setup</span><span class="sxs-lookup"><span data-stu-id="15da3-178">Setup</span></span>
1. <span data-ttu-id="15da3-179">Install the Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span><span class="sxs-lookup"><span data-stu-id="15da3-179">Install the Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="15da3-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="15da3-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="15da3-181">You need the zip utility in the path (and named zip.exe) to operationalize your R package into Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15da3-181">You need the zip utility in the path (and named zip.exe) to operationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="15da3-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter the parameters from your Azure Machine Learning workspace:</span><span class="sxs-lookup"><span data-stu-id="15da3-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter the parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="15da3-183">settings.json File structure:</span><span class="sxs-lookup"><span data-stu-id="15da3-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="15da3-184">Build a model in R and publish it in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15da3-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function to publish based on the model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-the-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="15da3-185">Consume the model deployed in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15da3-185">Consume the model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="15da3-186">To consume the model from a client application, we use the Azure Machine Learning library to look up the published web service by name using the `services` API call to determine the endpoint.</span><span class="sxs-lookup"><span data-stu-id="15da3-186">To consume the model from a client application, we use the Azure Machine Learning library to look up the published web service by name using the `services` API call to determine the endpoint.</span></span> <span data-ttu-id="15da3-187">Then you just call the `consume` function and pass in the data frame to be predicted.</span><span class="sxs-lookup"><span data-stu-id="15da3-187">Then you just call the `consume` function and pass in the data frame to be predicted.</span></span>
<span data-ttu-id="15da3-188">The following code is used to consume the model published as an Azure Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="15da3-188">The following code is used to consume the model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use the last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="15da3-189">More information about the Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="15da3-189">More information about the Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="15da3-190">4. Administer your Azure resources using Azure portal or Powershell</span><span class="sxs-lookup"><span data-stu-id="15da3-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="15da3-191">The DSVM not only allows you to build your analytics solution locally on the virtual machine, but also allows you to access services on Microsoft's Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="15da3-191">The DSVM not only allows you to build your analytics solution locally on the virtual machine, but also allows you to access services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="15da3-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span><span class="sxs-lookup"><span data-stu-id="15da3-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="15da3-193">To administer your Azure subscription and cloud resources you can use your browser and point to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15da3-193">To administer your Azure subscription and cloud resources you can use your browser and point to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="15da3-194">You can also use Azure Powershell to administer your Azure subscription and resources via a script.</span><span class="sxs-lookup"><span data-stu-id="15da3-194">You can also use Azure Powershell to administer your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="15da3-195">You can run Azure Powershell from a shortcut on the desktop or from the start menu titled "Microsoft Azure Powershell".</span><span class="sxs-lookup"><span data-stu-id="15da3-195">You can run Azure Powershell from a shortcut on the desktop or from the start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="15da3-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span><span class="sxs-lookup"><span data-stu-id="15da3-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="15da3-197">5. Extend your storage space with a shared file system</span><span class="sxs-lookup"><span data-stu-id="15da3-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="15da3-198">Data scientists can share large datasets, code or other resources within the team.</span><span class="sxs-lookup"><span data-stu-id="15da3-198">Data scientists can share large datasets, code or other resources within the team.</span></span> <span data-ttu-id="15da3-199">The DSVM itself has about 70GB of space available.</span><span class="sxs-lookup"><span data-stu-id="15da3-199">The DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="15da3-200">To extend your storage, you can use the Azure File Service and either mount it on the DSVM or access it via a REST API.</span><span class="sxs-lookup"><span data-stu-id="15da3-200">To extend your storage, you can use the Azure File Service and either mount it on the DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="15da3-201">The maximum space of the Azure File Service share is 5TB and individual file size limit is 1TB.</span><span class="sxs-lookup"><span data-stu-id="15da3-201">The maximum space of the Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="15da3-202">You can use Azure Powershell to create an Azure File Service share.</span><span class="sxs-lookup"><span data-stu-id="15da3-202">You can use Azure Powershell to create an Azure File Service share.</span></span> <span data-ttu-id="15da3-203">Here is the script to run under Azure PowerShell to create an Azure File service share.</span><span class="sxs-lookup"><span data-stu-id="15da3-203">Here is the script to run under Azure PowerShell to create an Azure File service share.</span></span>

    # Authenticate to Azure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under the FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List the share to confirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="15da3-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="15da3-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="15da3-205">It is highly recommended that the VM is in same Azure data center as the storage account to avoid latency and data transfer charges.</span><span class="sxs-lookup"><span data-stu-id="15da3-205">It is highly recommended that the VM is in same Azure data center as the storage account to avoid latency and data transfer charges.</span></span> <span data-ttu-id="15da3-206">Here is the commands to mount the drive on the DSVM that you can run on Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="15da3-206">Here is the commands to mount the drive on the DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of the storage account that has the Azure file share from Azure portal. Store it securely on the VM to avoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount the Azure file share as Z: drive on the VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="15da3-207">Now you can access this drive as you would any normal drive on the VM.</span><span class="sxs-lookup"><span data-stu-id="15da3-207">Now you can access this drive as you would any normal drive on the VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="15da3-208">6. Share code with your team using GitHub</span><span class="sxs-lookup"><span data-stu-id="15da3-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="15da3-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by the developer community.</span><span class="sxs-lookup"><span data-stu-id="15da3-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by the developer community.</span></span> <span data-ttu-id="15da3-210">It uses Git as the technology to track and store versions of the code files.</span><span class="sxs-lookup"><span data-stu-id="15da3-210">It uses Git as the technology to track and store versions of the code files.</span></span> <span data-ttu-id="15da3-211">GitHub is also a platform where you can create your own repository to store your team's shared code and documentation, implement version control and also control who have access to view and contribute code.</span><span class="sxs-lookup"><span data-stu-id="15da3-211">GitHub is also a platform where you can create your own repository to store your team's shared code and documentation, implement version control and also control who have access to view and contribute code.</span></span> <span data-ttu-id="15da3-212">Please visit the [GitHub help pages](https://help.github.com/) for more information on using Git.</span><span class="sxs-lookup"><span data-stu-id="15da3-212">Please visit the [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="15da3-213">You can use GitHub as one of the ways to collaborate with your team, use code developed by the community and contribute code back to the community.</span><span class="sxs-lookup"><span data-stu-id="15da3-213">You can use GitHub as one of the ways to collaborate with your team, use code developed by the community and contribute code back to the community.</span></span>

<span data-ttu-id="15da3-214">The DSVM already comes loaded with client tools on both command line as well GUI to access GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="15da3-214">The DSVM already comes loaded with client tools on both command line as well GUI to access GitHub repository.</span></span> <span data-ttu-id="15da3-215">The command line tool to work with Git and GitHub is called Git Bash.</span><span class="sxs-lookup"><span data-stu-id="15da3-215">The command line tool to work with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="15da3-216">Visual Studio installed on the DSVM has the Git extensions.</span><span class="sxs-lookup"><span data-stu-id="15da3-216">Visual Studio installed on the DSVM has the Git extensions.</span></span> <span data-ttu-id="15da3-217">You can find start-up icons for these tools on the start menu and the desktop.</span><span class="sxs-lookup"><span data-stu-id="15da3-217">You can find start-up icons for these tools on the start menu and the desktop.</span></span>

<span data-ttu-id="15da3-218">To download code from a GitHub repository you will use the ```git clone``` command.</span><span class="sxs-lookup"><span data-stu-id="15da3-218">To download code from a GitHub repository you will use the ```git clone``` command.</span></span> <span data-ttu-id="15da3-219">For example to download data science repository published by Microsoft into the current directory you can run the following command once you are in ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="15da3-219">For example to download data science repository published by Microsoft into the current directory you can run the following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="15da3-220">In Visual Studio, you can do the same clone operation.</span><span class="sxs-lookup"><span data-stu-id="15da3-220">In Visual Studio, you can do the same clone operation.</span></span> <span data-ttu-id="15da3-221">The screen-shot below shows how to access Git and GitHub tools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15da3-221">The screen-shot below shows how to access Git and GitHub tools in Visual Studio.</span></span>

![Git in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="15da3-223">You can find more information on using Git to work with your GitHub repository from several resources available on github.com.</span><span class="sxs-lookup"><span data-stu-id="15da3-223">You can find more information on using Git to work with your GitHub repository from several resources available on github.com.</span></span> <span data-ttu-id="15da3-224">The [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span><span class="sxs-lookup"><span data-stu-id="15da3-224">The [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="15da3-225">7. Access various Azure data and analytics services</span><span class="sxs-lookup"><span data-stu-id="15da3-225">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="15da3-226">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="15da3-226">Azure Blob</span></span>
<span data-ttu-id="15da3-227">Azure blob is a reliable, economical cloud storage for data big and small.</span><span class="sxs-lookup"><span data-stu-id="15da3-227">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="15da3-228">Let us look at how you can move data to Azure Blob and access data stored in an Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="15da3-228">Let us look at how you can move data to Azure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="15da3-229">**Prerequisite**</span><span class="sxs-lookup"><span data-stu-id="15da3-229">**Prerequisite**</span></span>

* <span data-ttu-id="15da3-230">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="15da3-230">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="15da3-232">Confirm that the pre-installed command line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="15da3-232">Confirm that the pre-installed command line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="15da3-233">You can add the directory containing the azcopy.exe to your PATH environment variable to avoid typing the full command path when running this tool.</span><span class="sxs-lookup"><span data-stu-id="15da3-233">You can add the directory containing the azcopy.exe to your PATH environment variable to avoid typing the full command path when running this tool.</span></span> <span data-ttu-id="15da3-234">For more info on AzCopy tool please refer to [AzCopy documentation](../storage/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="15da3-234">For more info on AzCopy tool please refer to [AzCopy documentation](../storage/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="15da3-235">Start the Azure Storage Explorer tool.</span><span class="sxs-lookup"><span data-stu-id="15da3-235">Start the Azure Storage Explorer tool.</span></span> <span data-ttu-id="15da3-236">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="15da3-236">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="15da3-238">**Move data from VM to Azure Blob: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="15da3-238">**Move data from VM to Azure Blob: AzCopy**</span></span>

<span data-ttu-id="15da3-239">To move data between your local files and blob storage, you can use AzCopy in command line or PowerShell:</span><span class="sxs-lookup"><span data-stu-id="15da3-239">To move data between your local files and blob storage, you can use AzCopy in command line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="15da3-240">Replace **C:\myfolder** to the path where your file is stored, **mystorageaccount** to your blob storage account name, **mycontainer** to the container name, **storage account key** to your blob storage access key.</span><span class="sxs-lookup"><span data-stu-id="15da3-240">Replace **C:\myfolder** to the path where your file is stored, **mystorageaccount** to your blob storage account name, **mycontainer** to the container name, **storage account key** to your blob storage access key.</span></span> <span data-ttu-id="15da3-241">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15da3-241">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="15da3-243">Run AzCopy command in PowerShell or from a command prompt.</span><span class="sxs-lookup"><span data-stu-id="15da3-243">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="15da3-244">Here is some example usage of AzCopy command:</span><span class="sxs-lookup"><span data-stu-id="15da3-244">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine to a Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container to Local machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="15da3-245">Once you run your AzCopy command to copy to an Azure blob you see your file shows up in Azure Storage Explorer shortly.</span><span class="sxs-lookup"><span data-stu-id="15da3-245">Once you run your AzCopy command to copy to an Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="15da3-247">**Move data from VM to Azure Blob: Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="15da3-247">**Move data from VM to Azure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="15da3-248">You can also upload data from the local file in your VM using Azure Storage Explorer:</span><span class="sxs-lookup"><span data-stu-id="15da3-248">You can also upload data from the local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="15da3-249">To upload data to a container, select the target container and click the **Upload** button.![Upload in Storage Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="15da3-249">To upload data to a container, select the target container and click the **Upload** button.![Upload in Storage Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="15da3-250">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files to blob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="15da3-250">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files to blob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="15da3-251">**Read data from Azure Blob: Machine Learning reader module**</span><span class="sxs-lookup"><span data-stu-id="15da3-251">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="15da3-252">In Azure Machine Learning Studio you can use an **Import Data module** to read data from your blob.</span><span class="sxs-lookup"><span data-stu-id="15da3-252">In Azure Machine Learning Studio you can use an **Import Data module** to read data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="15da3-254">**Read data from Azure Blob: Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="15da3-254">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="15da3-255">You can use **BlobService** library to read data directly from blob in a Jupyter Notebook or Python program.</span><span class="sxs-lookup"><span data-stu-id="15da3-255">You can use **BlobService** library to read data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="15da3-256">First, import required packages:</span><span class="sxs-lookup"><span data-stu-id="15da3-256">First, import required packages:</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

<span data-ttu-id="15da3-257">Then plug in your Azure Blob account credentials and read data from Blob:</span><span class="sxs-lookup"><span data-stu-id="15da3-257">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds to download "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'the size of the data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="15da3-258">The data is read in as a data frame:</span><span class="sxs-lookup"><span data-stu-id="15da3-258">The data is read in as a data frame:</span></span>

![IPNB_data_readin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="15da3-260">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="15da3-260">Azure Data Lake</span></span>
<span data-ttu-id="15da3-261">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="15da3-261">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="15da3-262">It works with both the Hadoop ecosystem and the Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="15da3-262">It works with both the Hadoop ecosystem and the Azure Data Lake Analytics.</span></span> <span data-ttu-id="15da3-263">We show how you can move data into the Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="15da3-263">We show how you can move data into the Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="15da3-264">**Prerequisite**</span><span class="sxs-lookup"><span data-stu-id="15da3-264">**Prerequisite**</span></span>

* <span data-ttu-id="15da3-265">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15da3-265">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="15da3-267">The  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on the Visual Studio Community Edition which is on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="15da3-267">The  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on the Visual Studio Community Edition which is on the virtual machine.</span></span> <span data-ttu-id="15da3-268">After starting Visual Studio and logging in your Azure subscription, you will see your Azure Data Analytics account and storage in the left panel of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15da3-268">After starting Visual Studio and logging in your Azure subscription, you will see your Azure Data Analytics account and storage in the left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="15da3-270">**Move data from VM to Data Lake: Azure Data Lake Explorer**</span><span class="sxs-lookup"><span data-stu-id="15da3-270">**Move data from VM to Data Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="15da3-271">You can use **Azure Data Lake Explorer** to upload data from the local files in your Virtual Machine to Data Lake storage.</span><span class="sxs-lookup"><span data-stu-id="15da3-271">You can use **Azure Data Lake Explorer** to upload data from the local files in your Virtual Machine to Data Lake storage.</span></span>

![Azure_Data_Lake_UploadData](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="15da3-273">You can also build a data pipeline to productionize your data movement to or from Azure Data Lake using the [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="15da3-273">You can also build a data pipeline to productionize your data movement to or from Azure Data Lake using the [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="15da3-274">We refer you to this [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) to guide you through the steps to build the data pipelines.</span><span class="sxs-lookup"><span data-stu-id="15da3-274">We refer you to this [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) to guide you through the steps to build the data pipelines.</span></span>

<span data-ttu-id="15da3-275">**Read data from Azure Blob to Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="15da3-275">**Read data from Azure Blob to Data Lake: U-SQL**</span></span>

<span data-ttu-id="15da3-276">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span><span class="sxs-lookup"><span data-stu-id="15da3-276">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="15da3-277">Before composing your U-SQL query, make sure your blob storage account is linked to your Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="15da3-277">Before composing your U-SQL query, make sure your blob storage account is linked to your Azure Data Lake.</span></span> <span data-ttu-id="15da3-278">Go to **Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type to **Azure Storage** and plug in your Azure Storage Account Name and Key.</span><span class="sxs-lookup"><span data-stu-id="15da3-278">Go to **Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type to **Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="15da3-279">Then you will be able to reference the data stored in the storage account.</span><span class="sxs-lookup"><span data-stu-id="15da3-279">Then you will be able to reference the data stored in the storage account.</span></span>

![Enter storage account and key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="15da3-281">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output the resulting data to either Azure Data Lake or Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="15da3-281">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output the resulting data to either Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="15da3-282">When you reference the data in blob storage, use **wasb://**; when you reference the data in Azure Data Lake, use **swbhdfs://**</span><span class="sxs-lookup"><span data-stu-id="15da3-282">When you reference the data in blob storage, use **wasb://**; when you reference the data in Azure Data Lake, use **swbhdfs://**</span></span>

![Data frame](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="15da3-284">You may use the following U-SQL queries in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="15da3-284">You may use the following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    TO "swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    TO "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="15da3-285">After your query is submitted to the server, a diagram showing the status of your job will be displayed.</span><span class="sxs-lookup"><span data-stu-id="15da3-285">After your query is submitted to the server, a diagram showing the status of your job will be displayed.</span></span>

![Job status diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="15da3-287">**Query data in Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="15da3-287">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="15da3-288">After the dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) to query and explore the data.</span><span class="sxs-lookup"><span data-stu-id="15da3-288">After the dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) to query and explore the data.</span></span> <span data-ttu-id="15da3-289">U-SQL language is similar to T-SQL, but combines some features from C# so that users can write customized modules, User Defined Functions, and etc. You can use the scripts in the previous step.</span><span class="sxs-lookup"><span data-stu-id="15da3-289">U-SQL language is similar to T-SQL, but combines some features from C# so that users can write customized modules, User Defined Functions, and etc. You can use the scripts in the previous step.</span></span>

<span data-ttu-id="15da3-290">After the query is submitted to server, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview the data by right-click the file.</span><span class="sxs-lookup"><span data-stu-id="15da3-290">After the query is submitted to server, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview the data by right-click the file.</span></span>

![File in Azure Data Lake Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="15da3-292">To see the file information:</span><span class="sxs-lookup"><span data-stu-id="15da3-292">To see the file information:</span></span>

![File summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="15da3-294">HDInsight Hadoop Clusters</span><span class="sxs-lookup"><span data-stu-id="15da3-294">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="15da3-295">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on the cloud.</span><span class="sxs-lookup"><span data-stu-id="15da3-295">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on the cloud.</span></span> <span data-ttu-id="15da3-296">You can work easily with Azure HDInsight clusters from the data science virtual machine.</span><span class="sxs-lookup"><span data-stu-id="15da3-296">You can work easily with Azure HDInsight clusters from the data science virtual machine.</span></span>

<span data-ttu-id="15da3-297">**Prerequisite**</span><span class="sxs-lookup"><span data-stu-id="15da3-297">**Prerequisite**</span></span>

* <span data-ttu-id="15da3-298">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15da3-298">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="15da3-299">This storage account is used to store data for HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="15da3-299">This storage account is used to store data for HDInsight clusters.</span></span>

![Create Azure Blob storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="15da3-301">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="15da3-301">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="15da3-302">You must link the storage account created with your HDInsight cluster when it is created.</span><span class="sxs-lookup"><span data-stu-id="15da3-302">You must link the storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="15da3-303">This storage account is used for accessing data that can be processed within the cluster.</span><span class="sxs-lookup"><span data-stu-id="15da3-303">This storage account is used for accessing data that can be processed within the cluster.</span></span>

![Link to storage account created with HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="15da3-305">You must enable **Remote Access** to the head node of the cluster after it is created.</span><span class="sxs-lookup"><span data-stu-id="15da3-305">You must enable **Remote Access** to the head node of the cluster after it is created.</span></span> <span data-ttu-id="15da3-306">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you will need them below.</span><span class="sxs-lookup"><span data-stu-id="15da3-306">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you will need them below.</span></span>

![Enable remote access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="15da3-308">Create an Azure Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="15da3-308">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="15da3-309">Your Machine Learning Experiments will be stored in this Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="15da3-309">Your Machine Learning Experiments will be stored in this Machine Learning workspace.</span></span> <span data-ttu-id="15da3-310">Select the highlighted options in Portal as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="15da3-310">Select the highlighted options in Portal as shown in the screenshot below.</span></span>

![Create an Azure Machine Learning workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="15da3-312">Then enter the parameters for your workspace</span><span class="sxs-lookup"><span data-stu-id="15da3-312">Then enter the parameters for your workspace</span></span>

![Enter Machine Learning workspace parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="15da3-314">Upload data using IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="15da3-314">Upload data using IPython Notebook.</span></span> <span data-ttu-id="15da3-315">First import required packages, plug in credentials, create a db in your storage account, then load data to HDI clusters.</span><span class="sxs-lookup"><span data-stu-id="15da3-315">First import required packages, plug in credentials, create a db in your storage account, then load data to HDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create the connection to Hive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage to HDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="15da3-316">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) to upload NYC Taxi data to HDI cluster.</span><span class="sxs-lookup"><span data-stu-id="15da3-316">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) to upload NYC Taxi data to HDI cluster.</span></span> <span data-ttu-id="15da3-317">Major steps include:</span><span class="sxs-lookup"><span data-stu-id="15da3-317">Major steps include:</span></span>
  
  * <span data-ttu-id="15da3-318">AzCopy: download zipped CSV's from public blob to your local folder</span><span class="sxs-lookup"><span data-stu-id="15da3-318">AzCopy: download zipped CSV's from public blob to your local folder</span></span>
  * <span data-ttu-id="15da3-319">AzCopy: upload unzipped CSV's from local folder to HDI cluster</span><span class="sxs-lookup"><span data-stu-id="15da3-319">AzCopy: upload unzipped CSV's from local folder to HDI cluster</span></span>
  * <span data-ttu-id="15da3-320">Log into the head node of Hadoop cluster and prepare for exploratory data analysis</span><span class="sxs-lookup"><span data-stu-id="15da3-320">Log into the head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="15da3-321">After the data is loaded to HDI cluster, you can check your data in Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="15da3-321">After the data is loaded to HDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="15da3-322">And you have a database nyctaxidb created in HDI cluster.</span><span class="sxs-lookup"><span data-stu-id="15da3-322">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="15da3-323">**Data exploration: Hive Queries in Python**</span><span class="sxs-lookup"><span data-stu-id="15da3-323">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="15da3-324">Since the data is in Hadoop cluster, you can use the pyodbc package to connect to Hadoop Clusters and query database using Hive to do exploration and feature engineering.</span><span class="sxs-lookup"><span data-stu-id="15da3-324">Since the data is in Hadoop cluster, you can use the pyodbc package to connect to Hadoop Clusters and query database using Hive to do exploration and feature engineering.</span></span> <span data-ttu-id="15da3-325">You can view the existing tables we created in the prerequisite step.</span><span class="sxs-lookup"><span data-stu-id="15da3-325">You can view the existing tables we created in the prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![View existing tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="15da3-327">Let's look at the number of records in each month and the frequencies of tipped or not in the trip table:</span><span class="sxs-lookup"><span data-stu-id="15da3-327">Let's look at the number of records in each month and the frequencies of tipped or not in the trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Plot of number of records in each month](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Plot of tip frequencies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="15da3-330">We can also compute the distance between pickup location and dropoff location and then compare it to the trip distance.</span><span class="sxs-lookup"><span data-stu-id="15da3-330">We can also compute the distance between pickup location and dropoff location and then compare it to the trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Pickup and dropoff table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Plot of pickup/dropoff distance to trip distance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="15da3-333">Now let's prepare a down-sampled (1%) set of data for modeling.</span><span class="sxs-lookup"><span data-stu-id="15da3-333">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="15da3-334">We can use this data in Machine Learning reader module.</span><span class="sxs-lookup"><span data-stu-id="15da3-334">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of the join into the above internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="15da3-335">After a while, you can see the data has been loaded in Hadoop clusters:</span><span class="sxs-lookup"><span data-stu-id="15da3-335">After a while, you can see the data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Table of data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="15da3-337">**Read data from HDI using Machine Learning: reader module**</span><span class="sxs-lookup"><span data-stu-id="15da3-337">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="15da3-338">You may also use the **reader** module in Machine Learning Studio to access the database in Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="15da3-338">You may also use the **reader** module in Machine Learning Studio to access the database in Hadoop cluster.</span></span> <span data-ttu-id="15da3-339">Plug in the credentials of your HDI clusters and Azure Storage Account and you will be able to build machine learning models using database in HDI clusters.</span><span class="sxs-lookup"><span data-stu-id="15da3-339">Plug in the credentials of your HDI clusters and Azure Storage Account and you will be able to build machine learning models using database in HDI clusters.</span></span>

![Reader module properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="15da3-341">The scored dataset can then be viewed:</span><span class="sxs-lookup"><span data-stu-id="15da3-341">The scored dataset can then be viewed:</span></span>

![View scored dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="15da3-343">Azure SQL Data Warehouse & databases</span><span class="sxs-lookup"><span data-stu-id="15da3-343">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="15da3-344">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span><span class="sxs-lookup"><span data-stu-id="15da3-344">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="15da3-345">You can provision your Azure SQL Data Warehouse by following the instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="15da3-345">You can provision your Azure SQL Data Warehouse by following the instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="15da3-346">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) to do data upload, exploration and modeling using data within the SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="15da3-346">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) to do data upload, exploration and modeling using data within the SQL Data Warehouse.</span></span>

#### <a name="azure-documentdb"></a><span data-ttu-id="15da3-347">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="15da3-347">Azure DocumentDB</span></span>
<span data-ttu-id="15da3-348">Azure DocumentDB is a NoSQL database in the cloud.</span><span class="sxs-lookup"><span data-stu-id="15da3-348">Azure DocumentDB is a NoSQL database in the cloud.</span></span> <span data-ttu-id="15da3-349">It allows you to work with documents like JSON and allows you to store and query the documents.</span><span class="sxs-lookup"><span data-stu-id="15da3-349">It allows you to work with documents like JSON and allows you to store and query the documents.</span></span>

<span data-ttu-id="15da3-350">You need to do the following per-requisites steps to access DocumentDB from the DSVM.</span><span class="sxs-lookup"><span data-stu-id="15da3-350">You need to do the following per-requisites steps to access DocumentDB from the DSVM.</span></span>

1. <span data-ttu-id="15da3-351">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span><span class="sxs-lookup"><span data-stu-id="15da3-351">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="15da3-352">Create DocumentDB account and Document DB database from [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="15da3-352">Create DocumentDB account and Document DB database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="15da3-353">Download "DocumentDB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract to a directory of your choice</span><span class="sxs-lookup"><span data-stu-id="15da3-353">Download "DocumentDB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract to a directory of your choice</span></span>
4. <span data-ttu-id="15da3-354">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into DocumentDB with following command parameters to the migration tool (dtui.exe from the directory where you installed the DocumentDB Migration Tool).</span><span class="sxs-lookup"><span data-stu-id="15da3-354">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into DocumentDB with following command parameters to the migration tool (dtui.exe from the directory where you installed the DocumentDB Migration Tool).</span></span> <span data-ttu-id="15da3-355">Enter the source and target location parameters from below.</span><span class="sxs-lookup"><span data-stu-id="15da3-355">Enter the source and target location parameters from below.</span></span>
   
    <span data-ttu-id="15da3-356">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="15da3-356">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="15da3-357">Once you import the data, you can go to Jupyter and open the notebook titled *DocumentDBSample* which contains python code to access DocumentDB and do some basic querying.</span><span class="sxs-lookup"><span data-stu-id="15da3-357">Once you import the data, you can go to Jupyter and open the notebook titled *DocumentDBSample* which contains python code to access DocumentDB and do some basic querying.</span></span> <span data-ttu-id="15da3-358">You can learn more about DocumentDB by visiting the service [documentation page](https://azure.microsoft.com/documentation/learning-paths/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="15da3-358">You can learn more about DocumentDB by visiting the service [documentation page](https://azure.microsoft.com/documentation/learning-paths/documentdb/)</span></span>

## <a name="8-build-reports-and-dashboard-using-the-power-bi-desktop"></a><span data-ttu-id="15da3-359">8. Build reports and dashboard using the Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="15da3-359">8. Build reports and dashboard using the Power BI Desktop</span></span>
<span data-ttu-id="15da3-360">Let us visualize the Volcano JSON file we saw in the DocumentDB example above in Power BI to gain visual insights into the data.</span><span class="sxs-lookup"><span data-stu-id="15da3-360">Let us visualize the Volcano JSON file we saw in the DocumentDB example above in Power BI to gain visual insights into the data.</span></span> <span data-ttu-id="15da3-361">Detailed steps are available in the [Power BI article](../documentdb/documentdb-powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="15da3-361">Detailed steps are available in the [Power BI article](../documentdb/documentdb-powerbi-visualize.md).</span></span> <span data-ttu-id="15da3-362">The high level steps are below :</span><span class="sxs-lookup"><span data-stu-id="15da3-362">The high level steps are below :</span></span>

1. <span data-ttu-id="15da3-363">Open Power BI Desktop and do "Get Data".</span><span class="sxs-lookup"><span data-stu-id="15da3-363">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="15da3-364">Specify the URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="15da3-364">Specify the URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="15da3-365">You should see the JSON records imported as a list</span><span class="sxs-lookup"><span data-stu-id="15da3-365">You should see the JSON records imported as a list</span></span>
3. <span data-ttu-id="15da3-366">Convert the list to a table so Power BI can work with the same</span><span class="sxs-lookup"><span data-stu-id="15da3-366">Convert the list to a table so Power BI can work with the same</span></span>
4. <span data-ttu-id="15da3-367">Expand the columns by clicking on the expand icon (the one with the "left arrow and a right arrow" icon on the right of the column)</span><span class="sxs-lookup"><span data-stu-id="15da3-367">Expand the columns by clicking on the expand icon (the one with the "left arrow and a right arrow" icon on the right of the column)</span></span>
5. <span data-ttu-id="15da3-368">Notice that location is a "Record" field.</span><span class="sxs-lookup"><span data-stu-id="15da3-368">Notice that location is a "Record" field.</span></span> <span data-ttu-id="15da3-369">Expand the record and select only the coordinates.</span><span class="sxs-lookup"><span data-stu-id="15da3-369">Expand the record and select only the coordinates.</span></span> <span data-ttu-id="15da3-370">Coordinate is a list column</span><span class="sxs-lookup"><span data-stu-id="15da3-370">Coordinate is a list column</span></span>
6. <span data-ttu-id="15da3-371">Add a new column to convert the list coordinate column into a comma separate LatLong column concatenating the two elements in the coordinate list field using the formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="15da3-371">Add a new column to convert the list coordinate column into a comma separate LatLong column concatenating the two elements in the coordinate list field using the formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="15da3-372">Finally convert the ```Elevation``` column to Decimal and select the **Close** and **Apply**.</span><span class="sxs-lookup"><span data-stu-id="15da3-372">Finally convert the ```Elevation``` column to Decimal and select the **Close** and **Apply**.</span></span>

<span data-ttu-id="15da3-373">Instead of steps above, you can paste the following code that scripts out the steps above in the Advanced Editor in Power BI that allows you to write the data transformations in a query language.</span><span class="sxs-lookup"><span data-stu-id="15da3-373">Instead of steps above, you can paste the following code that scripts out the steps above in the Advanced Editor in Power BI that allows you to write the data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="15da3-374">You now have the data in your Power BI data model.</span><span class="sxs-lookup"><span data-stu-id="15da3-374">You now have the data in your Power BI data model.</span></span> <span data-ttu-id="15da3-375">Your Power BI desktop should look as shown below.</span><span class="sxs-lookup"><span data-stu-id="15da3-375">Your Power BI desktop should look as shown below.</span></span>

![Power BI desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="15da3-377">You can start building reports and visualizations using the data model.</span><span class="sxs-lookup"><span data-stu-id="15da3-377">You can start building reports and visualizations using the data model.</span></span> <span data-ttu-id="15da3-378">You can follow the steps in this [Power BI article](../documentdb/documentdb-powerbi-visualize.md#build-the-reports) to build a report.</span><span class="sxs-lookup"><span data-stu-id="15da3-378">You can follow the steps in this [Power BI article](../documentdb/documentdb-powerbi-visualize.md#build-the-reports) to build a report.</span></span> <span data-ttu-id="15da3-379">The end result will be a report that looks like the following.</span><span class="sxs-lookup"><span data-stu-id="15da3-379">The end result will be a report that looks like the following.</span></span>

![Power BI Desktop Report View - Power BI connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-to-meet-your-project-needs"></a><span data-ttu-id="15da3-381">9. Dynamically scale your DSVM to meet your project needs</span><span class="sxs-lookup"><span data-stu-id="15da3-381">9. Dynamically scale your DSVM to meet your project needs</span></span>
<span data-ttu-id="15da3-382">You can scale up and down the DSVM to meet your project needs.</span><span class="sxs-lookup"><span data-stu-id="15da3-382">You can scale up and down the DSVM to meet your project needs.</span></span> <span data-ttu-id="15da3-383">If you don't need to use the VM in the evening or weekends, you can just shut down the VM from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15da3-383">If you don't need to use the VM in the evening or weekends, you can just shut down the VM from the [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="15da3-384">You will incur compute charges if you use just the Operating system shutdown button on the VM.</span><span class="sxs-lookup"><span data-stu-id="15da3-384">You will incur compute charges if you use just the Operating system shutdown button on the VM.</span></span>  
> 
> 

<span data-ttu-id="15da3-385">If you need to handle some large scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span><span class="sxs-lookup"><span data-stu-id="15da3-385">If you need to handle some large scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="15da3-386">The full list of VMs along with their hourly compute pricing is available on the [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span><span class="sxs-lookup"><span data-stu-id="15da3-386">The full list of VMs along with their hourly compute pricing is available on the [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="15da3-387">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload to a Hadoop or a Spark cluster), you can scale down the cluster from the [Azure portal](https://portal.azure.com) and going to the settings of your VM instance.</span><span class="sxs-lookup"><span data-stu-id="15da3-387">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload to a Hadoop or a Spark cluster), you can scale down the cluster from the [Azure portal](https://portal.azure.com) and going to the settings of your VM instance.</span></span> <span data-ttu-id="15da3-388">Here is a screenshot.</span><span class="sxs-lookup"><span data-stu-id="15da3-388">Here is a screenshot.</span></span>

![VM instance settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="15da3-390">10. Install additional tools on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="15da3-390">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="15da3-391">We have packaged several tools that we believe will be able to address many of the common data analytics needs and that should save you time by avoiding having to install and configure your environments one by one and save you money by paying only for resources that you use.</span><span class="sxs-lookup"><span data-stu-id="15da3-391">We have packaged several tools that we believe will be able to address many of the common data analytics needs and that should save you time by avoiding having to install and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="15da3-392">You can leverage other Azure data and analytics services profiled in this article to enhance your analytics environment.</span><span class="sxs-lookup"><span data-stu-id="15da3-392">You can leverage other Azure data and analytics services profiled in this article to enhance your analytics environment.</span></span> <span data-ttu-id="15da3-393">We understand that in some cases your needs may require additional tools, including some proprietary third party tools.</span><span class="sxs-lookup"><span data-stu-id="15da3-393">We understand that in some cases your needs may require additional tools, including some proprietary third party tools.</span></span> <span data-ttu-id="15da3-394">You have full administrative access on the virtual machine to install new tools you need.</span><span class="sxs-lookup"><span data-stu-id="15da3-394">You have full administrative access on the virtual machine to install new tools you need.</span></span> <span data-ttu-id="15da3-395">You can also install additional packages in Python and R that are not pre-installed.</span><span class="sxs-lookup"><span data-stu-id="15da3-395">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="15da3-396">For Python you can use either ```conda``` or ```pip```.</span><span class="sxs-lookup"><span data-stu-id="15da3-396">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="15da3-397">For R you can use the ```install.packages()``` in the R console or use the IDE and choose "**Packages** -> **Install Packages...**".</span><span class="sxs-lookup"><span data-stu-id="15da3-397">For R you can use the ```install.packages()``` in the R console or use the IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="15da3-398">Summary</span><span class="sxs-lookup"><span data-stu-id="15da3-398">Summary</span></span>
<span data-ttu-id="15da3-399">These are just some of the things you can do on the Microsoft Data Science Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="15da3-399">These are just some of the things you can do on the Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="15da3-400">There are many more things you can do to make it an effective analytics environment.</span><span class="sxs-lookup"><span data-stu-id="15da3-400">There are many more things you can do to make it an effective analytics environment.</span></span>



































