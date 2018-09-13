---
title: Customer Churn Prediction using Azure Machine Learning | Microsoft Docs
description: How to perform churn analytics using Azure ML Workbench.
services: machine-learning
documentationcenter: ''
author: miprasad
manager: kristin.tolle
editor: miprasad
ms.assetid: ''
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/17/2017
ms.author: miprasad
ms.openlocfilehash: 7c7b50098cfd1bcac534156dd905b37affab80bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867690"
---
# <a name="customer-churn-prediction-using-azure-machine-learning"></a><span data-ttu-id="8a518-103">Customer churn prediction using Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8a518-103">Customer churn prediction using Azure Machine Learning</span></span>

<span data-ttu-id="8a518-104">On average, keeping existing customers is five times cheaper than the cost of recruiting new ones.</span><span class="sxs-lookup"><span data-stu-id="8a518-104">On average, keeping existing customers is five times cheaper than the cost of recruiting new ones.</span></span> <span data-ttu-id="8a518-105">As a result, marketing executives often find themselves trying to estimate the likelihood of customer churn and finding the necessary actions to minimize the churn rate.</span><span class="sxs-lookup"><span data-stu-id="8a518-105">As a result, marketing executives often find themselves trying to estimate the likelihood of customer churn and finding the necessary actions to minimize the churn rate.</span></span>

<span data-ttu-id="8a518-106">The aim of this solution is to demonstrate predictive churn analytics using Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="8a518-106">The aim of this solution is to demonstrate predictive churn analytics using Azure Machine Learning Workbench.</span></span> <span data-ttu-id="8a518-107">This solution provides an easy to use template to develop churn predictive data pipelines for retailers.</span><span class="sxs-lookup"><span data-stu-id="8a518-107">This solution provides an easy to use template to develop churn predictive data pipelines for retailers.</span></span> <span data-ttu-id="8a518-108">The template can be used with different datasets and different definitions of churn.</span><span class="sxs-lookup"><span data-stu-id="8a518-108">The template can be used with different datasets and different definitions of churn.</span></span> <span data-ttu-id="8a518-109">The aim of the hands-on example is to:</span><span class="sxs-lookup"><span data-stu-id="8a518-109">The aim of the hands-on example is to:</span></span>

1. <span data-ttu-id="8a518-110">Understand Azure Machine Learning Workbench's Data Preparation tools to clean and ingest customer relationship data for churn analytics.</span><span class="sxs-lookup"><span data-stu-id="8a518-110">Understand Azure Machine Learning Workbench's Data Preparation tools to clean and ingest customer relationship data for churn analytics.</span></span>

2. <span data-ttu-id="8a518-111">Perform feature transformation to handle noisy heterogeneous data.</span><span class="sxs-lookup"><span data-stu-id="8a518-111">Perform feature transformation to handle noisy heterogeneous data.</span></span>

3. <span data-ttu-id="8a518-112">Integrate third-party libraries (such as `scikit-learn` and `azureml`) to develop Bayesian and Tree-based classifiers for predicting churn.</span><span class="sxs-lookup"><span data-stu-id="8a518-112">Integrate third-party libraries (such as `scikit-learn` and `azureml`) to develop Bayesian and Tree-based classifiers for predicting churn.</span></span>

4. <span data-ttu-id="8a518-113">Deploy.</span><span class="sxs-lookup"><span data-stu-id="8a518-113">Deploy.</span></span>

## <a name="link-of-the-gallery-github-repository"></a><span data-ttu-id="8a518-114">Link of the gallery GitHub repository</span><span class="sxs-lookup"><span data-stu-id="8a518-114">Link of the gallery GitHub repository</span></span>
<span data-ttu-id="8a518-115">Following is the link to the public GitHub repository where all the code is hosted:</span><span class="sxs-lookup"><span data-stu-id="8a518-115">Following is the link to the public GitHub repository where all the code is hosted:</span></span>

[https://github.com/Azure/MachineLearningSamples-ChurnPrediction](https://github.com/Azure/MachineLearningSamples-ChurnPrediction)

## <a name="use-case-overview"></a><span data-ttu-id="8a518-116">Use case overview</span><span class="sxs-lookup"><span data-stu-id="8a518-116">Use case overview</span></span>
<span data-ttu-id="8a518-117">Companies need an effective strategy for managing customer churn.</span><span class="sxs-lookup"><span data-stu-id="8a518-117">Companies need an effective strategy for managing customer churn.</span></span> <span data-ttu-id="8a518-118">Customer churn includes customers stopping the use of a service, switching to a competitor service, switching to a lower-tier experience in the service or reducing engagement with the service.</span><span class="sxs-lookup"><span data-stu-id="8a518-118">Customer churn includes customers stopping the use of a service, switching to a competitor service, switching to a lower-tier experience in the service or reducing engagement with the service.</span></span>

<span data-ttu-id="8a518-119">In this use case, we look at data from French telecom company Orange to identify customers who are likely to churn in the near term in order to improve the service and create custom outreach campaigns that help retain customers.</span><span class="sxs-lookup"><span data-stu-id="8a518-119">In this use case, we look at data from French telecom company Orange to identify customers who are likely to churn in the near term in order to improve the service and create custom outreach campaigns that help retain customers.</span></span>

<span data-ttu-id="8a518-120">Telecom companies face a competitive market.</span><span class="sxs-lookup"><span data-stu-id="8a518-120">Telecom companies face a competitive market.</span></span> <span data-ttu-id="8a518-121">Many carriers lose revenue from postpaid customers due to churn.</span><span class="sxs-lookup"><span data-stu-id="8a518-121">Many carriers lose revenue from postpaid customers due to churn.</span></span> <span data-ttu-id="8a518-122">Hence the ability to accurately identify customer churn can be a huge competitive advantage.</span><span class="sxs-lookup"><span data-stu-id="8a518-122">Hence the ability to accurately identify customer churn can be a huge competitive advantage.</span></span>

<span data-ttu-id="8a518-123">Some of the factors contributing to telecom customer churn include:</span><span class="sxs-lookup"><span data-stu-id="8a518-123">Some of the factors contributing to telecom customer churn include:</span></span>

* <span data-ttu-id="8a518-124">Perceived frequent service disruptions</span><span class="sxs-lookup"><span data-stu-id="8a518-124">Perceived frequent service disruptions</span></span>
* <span data-ttu-id="8a518-125">Poor customer service experiences in online/retail stores</span><span class="sxs-lookup"><span data-stu-id="8a518-125">Poor customer service experiences in online/retail stores</span></span>
* <span data-ttu-id="8a518-126">Offers from other competing carriers (better family plan, data plan, etc.).</span><span class="sxs-lookup"><span data-stu-id="8a518-126">Offers from other competing carriers (better family plan, data plan, etc.).</span></span>

<span data-ttu-id="8a518-127">In this solution, we will use a concrete example of building a predictive customer churn model for telecom companies.</span><span class="sxs-lookup"><span data-stu-id="8a518-127">In this solution, we will use a concrete example of building a predictive customer churn model for telecom companies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a518-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a518-128">Prerequisites</span></span>

* <span data-ttu-id="8a518-129">An [Azure account](https://azure.microsoft.com/free/) (free trials are available)</span><span class="sxs-lookup"><span data-stu-id="8a518-129">An [Azure account](https://azure.microsoft.com/free/) (free trials are available)</span></span>

* <span data-ttu-id="8a518-130">An installed copy of [Azure Machine Learning Workbench](../service/overview-what-is-azure-ml.md) following the [quick start installation guide](../service/quickstart-installation.md) to install the program and create a workspace</span><span class="sxs-lookup"><span data-stu-id="8a518-130">An installed copy of [Azure Machine Learning Workbench](../service/overview-what-is-azure-ml.md) following the [quick start installation guide](../service/quickstart-installation.md) to install the program and create a workspace</span></span>

* <span data-ttu-id="8a518-131">For operationalization, it is best if you have Docker engine installed and running locally.</span><span class="sxs-lookup"><span data-stu-id="8a518-131">For operationalization, it is best if you have Docker engine installed and running locally.</span></span> <span data-ttu-id="8a518-132">If not, you can use the cluster option but be aware that running an Azure Container Service (ACS) can be expensive.</span><span class="sxs-lookup"><span data-stu-id="8a518-132">If not, you can use the cluster option but be aware that running an Azure Container Service (ACS) can be expensive.</span></span>

* <span data-ttu-id="8a518-133">This Solution assumes that you are running Azure Machine Learning Workbench on Windows 10 with Docker engine locally installed.</span><span class="sxs-lookup"><span data-stu-id="8a518-133">This Solution assumes that you are running Azure Machine Learning Workbench on Windows 10 with Docker engine locally installed.</span></span> <span data-ttu-id="8a518-134">If you are using macOS the instruction is largely the same.</span><span class="sxs-lookup"><span data-stu-id="8a518-134">If you are using macOS the instruction is largely the same.</span></span>

## <a name="create-a-new-workbench-project"></a><span data-ttu-id="8a518-135">Create a new Workbench project</span><span class="sxs-lookup"><span data-stu-id="8a518-135">Create a new Workbench project</span></span>

<span data-ttu-id="8a518-136">Create a new project using this example as a template:</span><span class="sxs-lookup"><span data-stu-id="8a518-136">Create a new project using this example as a template:</span></span>
1.  <span data-ttu-id="8a518-137">Open Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="8a518-137">Open Azure Machine Learning Workbench</span></span>
2.  <span data-ttu-id="8a518-138">On the **Projects** page, click the **+** sign and select **New Project**</span><span class="sxs-lookup"><span data-stu-id="8a518-138">On the **Projects** page, click the **+** sign and select **New Project**</span></span>
3.  <span data-ttu-id="8a518-139">In the **Create New Project** pane, fill in the information for your new project</span><span class="sxs-lookup"><span data-stu-id="8a518-139">In the **Create New Project** pane, fill in the information for your new project</span></span>
4.  <span data-ttu-id="8a518-140">In the **Search Project Templates** search box, type "Customer Churn Prediction" and select the template</span><span class="sxs-lookup"><span data-stu-id="8a518-140">In the **Search Project Templates** search box, type "Customer Churn Prediction" and select the template</span></span>
5.  <span data-ttu-id="8a518-141">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="8a518-141">Click **Create**</span></span>

## <a name="data-description"></a><span data-ttu-id="8a518-142">Data description</span><span class="sxs-lookup"><span data-stu-id="8a518-142">Data description</span></span>

<span data-ttu-id="8a518-143">The data set used in the solution is from the SIDKDD 2009 competition.</span><span class="sxs-lookup"><span data-stu-id="8a518-143">The data set used in the solution is from the SIDKDD 2009 competition.</span></span> <span data-ttu-id="8a518-144">It is called `CATelcoCustomerChurnTrainingSample.csv` and is located in the [`data`](https://github.com/Azure/MachineLearningSamples-ChurnPrediction/tree/master/data) folder.</span><span class="sxs-lookup"><span data-stu-id="8a518-144">It is called `CATelcoCustomerChurnTrainingSample.csv` and is located in the [`data`](https://github.com/Azure/MachineLearningSamples-ChurnPrediction/tree/master/data) folder.</span></span> <span data-ttu-id="8a518-145">The dataset consists of heterogeneous noisy data (numerical/categorical variables) from French Telecom company Orange and is anonymized.</span><span class="sxs-lookup"><span data-stu-id="8a518-145">The dataset consists of heterogeneous noisy data (numerical/categorical variables) from French Telecom company Orange and is anonymized.</span></span>

<span data-ttu-id="8a518-146">The variables capture customer demographic information, call statistics (such as average call duration, call failure rate, etc.), contract information, complaint statistics.</span><span class="sxs-lookup"><span data-stu-id="8a518-146">The variables capture customer demographic information, call statistics (such as average call duration, call failure rate, etc.), contract information, complaint statistics.</span></span> <span data-ttu-id="8a518-147">Churn variable is binary (0 - did not churn, 1 - did churn).</span><span class="sxs-lookup"><span data-stu-id="8a518-147">Churn variable is binary (0 - did not churn, 1 - did churn).</span></span>

## <a name="scenario-structure"></a><span data-ttu-id="8a518-148">Scenario structure</span><span class="sxs-lookup"><span data-stu-id="8a518-148">Scenario structure</span></span>

<span data-ttu-id="8a518-149">The folder structure is arranged as follows:</span><span class="sxs-lookup"><span data-stu-id="8a518-149">The folder structure is arranged as follows:</span></span>

<span data-ttu-id="8a518-150">__data__: Contains the dataset used in the solution</span><span class="sxs-lookup"><span data-stu-id="8a518-150">__data__: Contains the dataset used in the solution</span></span>  

<span data-ttu-id="8a518-151">__docs__: Contains all the hands-on labs</span><span class="sxs-lookup"><span data-stu-id="8a518-151">__docs__: Contains all the hands-on labs</span></span>

<span data-ttu-id="8a518-152">The order of Hands-on Labs to carry out the solution is as follows:</span><span class="sxs-lookup"><span data-stu-id="8a518-152">The order of Hands-on Labs to carry out the solution is as follows:</span></span>
1. <span data-ttu-id="8a518-153">Data Preparation: The main file related to Data Preparation in the data folder is `CATelcoCustomerChurnTrainingSample.csv`</span><span class="sxs-lookup"><span data-stu-id="8a518-153">Data Preparation: The main file related to Data Preparation in the data folder is `CATelcoCustomerChurnTrainingSample.csv`</span></span>
2. <span data-ttu-id="8a518-154">Modeling and Evaluation: The main file related to modeling and evaluation in the root folder is `CATelcoCustomerChurnModeling.py`</span><span class="sxs-lookup"><span data-stu-id="8a518-154">Modeling and Evaluation: The main file related to modeling and evaluation in the root folder is `CATelcoCustomerChurnModeling.py`</span></span>
3. <span data-ttu-id="8a518-155">Modeling and Evaluation without .dprep: The main file for this task in the root folder is `CATelcoCustomerChurnModelingWithoutDprep.py`</span><span class="sxs-lookup"><span data-stu-id="8a518-155">Modeling and Evaluation without .dprep: The main file for this task in the root folder is `CATelcoCustomerChurnModelingWithoutDprep.py`</span></span>
4. <span data-ttu-id="8a518-156">Operationalization: The main files for deloyment are the model (`model.pkl`) and `churn_schema_gen.py`</span><span class="sxs-lookup"><span data-stu-id="8a518-156">Operationalization: The main files for deloyment are the model (`model.pkl`) and `churn_schema_gen.py`</span></span>

| <span data-ttu-id="8a518-157">Order</span><span class="sxs-lookup"><span data-stu-id="8a518-157">Order</span></span>| <span data-ttu-id="8a518-158">File Name</span><span class="sxs-lookup"><span data-stu-id="8a518-158">File Name</span></span> | <span data-ttu-id="8a518-159">Realted Files</span><span class="sxs-lookup"><span data-stu-id="8a518-159">Realted Files</span></span> |
|--|-----------|------|
| <span data-ttu-id="8a518-160">1</span><span class="sxs-lookup"><span data-stu-id="8a518-160">1</span></span> | [`DataPreparation.md`](https://github.com/Azure/MachineLearningSamples-ChurnPrediction/blob/master/docs/DataPreparation.md) | <span data-ttu-id="8a518-161">'data/CATelcoCustomerChurnTrainingSample.csv'</span><span class="sxs-lookup"><span data-stu-id="8a518-161">'data/CATelcoCustomerChurnTrainingSample.csv'</span></span> |
| <span data-ttu-id="8a518-162">2</span><span class="sxs-lookup"><span data-stu-id="8a518-162">2</span></span> | [`ModelingAndEvaluation.md`](https://github.com/Azure/MachineLearningSamples-ChurnPrediction/blob/master/docs/ModelingAndEvaluation.md) | <span data-ttu-id="8a518-163">'CATelcoCustomerChurnModeling.py'</span><span class="sxs-lookup"><span data-stu-id="8a518-163">'CATelcoCustomerChurnModeling.py'</span></span> |
| <span data-ttu-id="8a518-164">3</span><span class="sxs-lookup"><span data-stu-id="8a518-164">3</span></span> | [`ModelingAndEvaluationWithoutDprep.md`](https://github.com/Azure/MachineLearningSamples-ChurnPrediction/blob/master/docs/ModelingAndEvaluationWithoutDprep.md) | <span data-ttu-id="8a518-165">'CATelcoCustomerChurnModelingWithoutDprep.py'</span><span class="sxs-lookup"><span data-stu-id="8a518-165">'CATelcoCustomerChurnModelingWithoutDprep.py'</span></span> |
| <span data-ttu-id="8a518-166">4</span><span class="sxs-lookup"><span data-stu-id="8a518-166">4</span></span> | [`Operationalization.md`](https://github.com/Azure/MachineLearningSamples-ChurnPrediction/blob/master/docs/Operationalization.md) | <span data-ttu-id="8a518-167">'model.pkl'</span><span class="sxs-lookup"><span data-stu-id="8a518-167">'model.pkl'</span></span><br><span data-ttu-id="8a518-168">'churn_schema_gen.py'</span><span class="sxs-lookup"><span data-stu-id="8a518-168">'churn_schema_gen.py'</span></span> |

<span data-ttu-id="8a518-169">Follow the Labs in the sequential manner described above.</span><span class="sxs-lookup"><span data-stu-id="8a518-169">Follow the Labs in the sequential manner described above.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8a518-170">Conclusion</span><span class="sxs-lookup"><span data-stu-id="8a518-170">Conclusion</span></span>
<span data-ttu-id="8a518-171">This hands on scenario demonstrated how to perform churn prediction using Azure Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="8a518-171">This hands on scenario demonstrated how to perform churn prediction using Azure Machine Learning Workbench.</span></span> <span data-ttu-id="8a518-172">We first performed data cleaning to handle noisy and heterogeneous data, followed by feature engineering using Data Preparation tools.</span><span class="sxs-lookup"><span data-stu-id="8a518-172">We first performed data cleaning to handle noisy and heterogeneous data, followed by feature engineering using Data Preparation tools.</span></span> <span data-ttu-id="8a518-173">We then used open source machine learning tools to create and evaluate a classification model, then used local docker container to deploy the model making it ready for production.</span><span class="sxs-lookup"><span data-stu-id="8a518-173">We then used open source machine learning tools to create and evaluate a classification model, then used local docker container to deploy the model making it ready for production.</span></span>
