---
title: How to prepare your model for deployment in Azure Machine Learning Studio | Microsoft Docs
description: How to prepare your trained model for deployment as a web service by converting your Machine Learning Studio training experiment to a predictive experiment.
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.openlocfilehash: 4bfbe22ba04f154c9f24daa13231d18e73316f9c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868818"
---
# <a name="how-to-prepare-your-model-for-deployment-in-azure-machine-learning-studio"></a><span data-ttu-id="d461a-103">How to prepare your model for deployment in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d461a-103">How to prepare your model for deployment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="d461a-104">Azure Machine Learning Studio gives you the tools you need to develop a predictive analytics model and then operationalize it by deploying it as an Azure web service.</span><span class="sxs-lookup"><span data-stu-id="d461a-104">Azure Machine Learning Studio gives you the tools you need to develop a predictive analytics model and then operationalize it by deploying it as an Azure web service.</span></span>

<span data-ttu-id="d461a-105">To do this, you use Studio to create an experiment - called a *training experiment* - where you train, score, and edit your model.</span><span class="sxs-lookup"><span data-stu-id="d461a-105">To do this, you use Studio to create an experiment - called a *training experiment* - where you train, score, and edit your model.</span></span> <span data-ttu-id="d461a-106">Once you're satisfied, you get your model ready to deploy by converting your training experiment to a *predictive experiment* that's configured to score user data.</span><span class="sxs-lookup"><span data-stu-id="d461a-106">Once you're satisfied, you get your model ready to deploy by converting your training experiment to a *predictive experiment* that's configured to score user data.</span></span>

<span data-ttu-id="d461a-107">You can see an example of this process in [Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning](walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="d461a-107">You can see an example of this process in [Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning](walkthrough-develop-predictive-solution.md).</span></span>

<span data-ttu-id="d461a-108">This article takes a deep dive into the details of how a training experiment gets converted into a predictive experiment, and how that predictive experiment is deployed.</span><span class="sxs-lookup"><span data-stu-id="d461a-108">This article takes a deep dive into the details of how a training experiment gets converted into a predictive experiment, and how that predictive experiment is deployed.</span></span> <span data-ttu-id="d461a-109">By understanding these details, you can learn how to configure your deployed model to make it more effective.</span><span class="sxs-lookup"><span data-stu-id="d461a-109">By understanding these details, you can learn how to configure your deployed model to make it more effective.</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="d461a-110">Overview</span><span class="sxs-lookup"><span data-stu-id="d461a-110">Overview</span></span> 

<span data-ttu-id="d461a-111">The process of converting a training experiment to a predictive experiment involves three steps:</span><span class="sxs-lookup"><span data-stu-id="d461a-111">The process of converting a training experiment to a predictive experiment involves three steps:</span></span>

1. <span data-ttu-id="d461a-112">Replace the machine learning algorithm modules with your trained model.</span><span class="sxs-lookup"><span data-stu-id="d461a-112">Replace the machine learning algorithm modules with your trained model.</span></span>
2. <span data-ttu-id="d461a-113">Trim the experiment to only those modules that are needed for scoring.</span><span class="sxs-lookup"><span data-stu-id="d461a-113">Trim the experiment to only those modules that are needed for scoring.</span></span> <span data-ttu-id="d461a-114">A training experiment includes a number of modules that are necessary for training but are not needed once the model is trained.</span><span class="sxs-lookup"><span data-stu-id="d461a-114">A training experiment includes a number of modules that are necessary for training but are not needed once the model is trained.</span></span>
3. <span data-ttu-id="d461a-115">Define how your model will accept data from the web service user, and what data will be returned.</span><span class="sxs-lookup"><span data-stu-id="d461a-115">Define how your model will accept data from the web service user, and what data will be returned.</span></span>

> [!TIP]
> <span data-ttu-id="d461a-116">In your training experiment, you've been concerned with training and scoring your model using your own data.</span><span class="sxs-lookup"><span data-stu-id="d461a-116">In your training experiment, you've been concerned with training and scoring your model using your own data.</span></span> <span data-ttu-id="d461a-117">But once deployed, users will send new data to your model and it will return prediction results.</span><span class="sxs-lookup"><span data-stu-id="d461a-117">But once deployed, users will send new data to your model and it will return prediction results.</span></span> <span data-ttu-id="d461a-118">So, as you convert your training experiment to a predictive experiment to get it ready for deployment, keep in mind how the model will be used by others.</span><span class="sxs-lookup"><span data-stu-id="d461a-118">So, as you convert your training experiment to a predictive experiment to get it ready for deployment, keep in mind how the model will be used by others.</span></span>
> 
> 

## <a name="set-up-web-service-button"></a><span data-ttu-id="d461a-119">Set Up Web Service button</span><span class="sxs-lookup"><span data-stu-id="d461a-119">Set Up Web Service button</span></span>
<span data-ttu-id="d461a-120">After you run your experiment (click **RUN** at the bottom of the experiment canvas), click the **Set Up Web Service** button (select the **Predictive Web Service** option).</span><span class="sxs-lookup"><span data-stu-id="d461a-120">After you run your experiment (click **RUN** at the bottom of the experiment canvas), click the **Set Up Web Service** button (select the **Predictive Web Service** option).</span></span> <span data-ttu-id="d461a-121">**Set Up Web Service** performs for you the three steps of converting your training experiment to a predictive experiment:</span><span class="sxs-lookup"><span data-stu-id="d461a-121">**Set Up Web Service** performs for you the three steps of converting your training experiment to a predictive experiment:</span></span>

1. <span data-ttu-id="d461a-122">It saves your trained model in the **Trained Models** section of the module palette (to the left of the experiment canvas).</span><span class="sxs-lookup"><span data-stu-id="d461a-122">It saves your trained model in the **Trained Models** section of the module palette (to the left of the experiment canvas).</span></span> <span data-ttu-id="d461a-123">It then replaces the machine learning algorithm and [Train Model][train-model] modules with the saved trained model.</span><span class="sxs-lookup"><span data-stu-id="d461a-123">It then replaces the machine learning algorithm and [Train Model][train-model] modules with the saved trained model.</span></span>
2. <span data-ttu-id="d461a-124">It analyzes your experiment and removes modules that were clearly used only for training and are no longer needed.</span><span class="sxs-lookup"><span data-stu-id="d461a-124">It analyzes your experiment and removes modules that were clearly used only for training and are no longer needed.</span></span>
3. <span data-ttu-id="d461a-125">It inserts _Web service input_ and _output_ modules into default locations in your experiment (these modules accept and return user data).</span><span class="sxs-lookup"><span data-stu-id="d461a-125">It inserts _Web service input_ and _output_ modules into default locations in your experiment (these modules accept and return user data).</span></span>

<span data-ttu-id="d461a-126">For example, the following experiment trains a two-class boosted decision tree model using sample census data:</span><span class="sxs-lookup"><span data-stu-id="d461a-126">For example, the following experiment trains a two-class boosted decision tree model using sample census data:</span></span>

![Training experiment][figure1]

<span data-ttu-id="d461a-128">The modules in this experiment perform basically four different functions:</span><span class="sxs-lookup"><span data-stu-id="d461a-128">The modules in this experiment perform basically four different functions:</span></span>

![Module functions][figure2]

<span data-ttu-id="d461a-130">When you convert this training experiment to a predictive experiment, some of these modules are no longer needed, or they now serve a different purpose:</span><span class="sxs-lookup"><span data-stu-id="d461a-130">When you convert this training experiment to a predictive experiment, some of these modules are no longer needed, or they now serve a different purpose:</span></span>

* <span data-ttu-id="d461a-131">**Data** - The data in this sample dataset is not used during scoring - the user of the web service will supply the data to be scored.</span><span class="sxs-lookup"><span data-stu-id="d461a-131">**Data** - The data in this sample dataset is not used during scoring - the user of the web service will supply the data to be scored.</span></span> <span data-ttu-id="d461a-132">However, the metadata from this dataset, such as data types, is used by the trained model.</span><span class="sxs-lookup"><span data-stu-id="d461a-132">However, the metadata from this dataset, such as data types, is used by the trained model.</span></span> <span data-ttu-id="d461a-133">So you need to keep the dataset in the predictive experiment so that it can provide this metadata.</span><span class="sxs-lookup"><span data-stu-id="d461a-133">So you need to keep the dataset in the predictive experiment so that it can provide this metadata.</span></span>

* <span data-ttu-id="d461a-134">**Prep** - Depending on the user data that will be submitted for scoring, these modules may or may not be necessary to process the incoming data.</span><span class="sxs-lookup"><span data-stu-id="d461a-134">**Prep** - Depending on the user data that will be submitted for scoring, these modules may or may not be necessary to process the incoming data.</span></span> <span data-ttu-id="d461a-135">The **Set Up Web Service** button doesn't touch these - you need to decide how you want to handle them.</span><span class="sxs-lookup"><span data-stu-id="d461a-135">The **Set Up Web Service** button doesn't touch these - you need to decide how you want to handle them.</span></span>
  
    <span data-ttu-id="d461a-136">For instance, in this example the sample dataset may have missing values, so a [Clean Missing Data][clean-missing-data] module was included to deal with them.</span><span class="sxs-lookup"><span data-stu-id="d461a-136">For instance, in this example the sample dataset may have missing values, so a [Clean Missing Data][clean-missing-data] module was included to deal with them.</span></span> <span data-ttu-id="d461a-137">Also, the sample dataset includes columns that are not needed to train the model.</span><span class="sxs-lookup"><span data-stu-id="d461a-137">Also, the sample dataset includes columns that are not needed to train the model.</span></span> <span data-ttu-id="d461a-138">So a [Select Columns in Dataset][select-columns] module was included to exclude those extra columns from the data flow.</span><span class="sxs-lookup"><span data-stu-id="d461a-138">So a [Select Columns in Dataset][select-columns] module was included to exclude those extra columns from the data flow.</span></span> <span data-ttu-id="d461a-139">If you know that the data that will be submitted for scoring through the web service will not have missing values, then you can remove the [Clean Missing Data][clean-missing-data] module.</span><span class="sxs-lookup"><span data-stu-id="d461a-139">If you know that the data that will be submitted for scoring through the web service will not have missing values, then you can remove the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="d461a-140">However, since the [Select Columns in Dataset][select-columns] module helps define the columns of data that the trained model expects, that module needs to remain.</span><span class="sxs-lookup"><span data-stu-id="d461a-140">However, since the [Select Columns in Dataset][select-columns] module helps define the columns of data that the trained model expects, that module needs to remain.</span></span>

* <span data-ttu-id="d461a-141">**Train** - These modules are used to train the model.</span><span class="sxs-lookup"><span data-stu-id="d461a-141">**Train** - These modules are used to train the model.</span></span> <span data-ttu-id="d461a-142">When you click **Set Up Web Service**, these modules are replaced with a single module that contains the model you trained.</span><span class="sxs-lookup"><span data-stu-id="d461a-142">When you click **Set Up Web Service**, these modules are replaced with a single module that contains the model you trained.</span></span> <span data-ttu-id="d461a-143">This new module is saved in the **Trained Models** section of the module palette.</span><span class="sxs-lookup"><span data-stu-id="d461a-143">This new module is saved in the **Trained Models** section of the module palette.</span></span>

* <span data-ttu-id="d461a-144">**Score** - In this example, the [Split Data][split] module is used to divide the data stream into test data and training data.</span><span class="sxs-lookup"><span data-stu-id="d461a-144">**Score** - In this example, the [Split Data][split] module is used to divide the data stream into test data and training data.</span></span> <span data-ttu-id="d461a-145">In the predictive experiment, we're not training anymore, so [Split Data][split] can be removed.</span><span class="sxs-lookup"><span data-stu-id="d461a-145">In the predictive experiment, we're not training anymore, so [Split Data][split] can be removed.</span></span> <span data-ttu-id="d461a-146">Similarly, the second [Score Model][score-model] module and the [Evaluate Model][evaluate-model] module are used to compare results from the test data, so these modules are not needed in the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="d461a-146">Similarly, the second [Score Model][score-model] module and the [Evaluate Model][evaluate-model] module are used to compare results from the test data, so these modules are not needed in the predictive experiment.</span></span> <span data-ttu-id="d461a-147">The remaining [Score Model][score-model] module, however, is needed to return a score result through the web service.</span><span class="sxs-lookup"><span data-stu-id="d461a-147">The remaining [Score Model][score-model] module, however, is needed to return a score result through the web service.</span></span>

<span data-ttu-id="d461a-148">Here is how our example looks after clicking **Set Up Web Service**:</span><span class="sxs-lookup"><span data-stu-id="d461a-148">Here is how our example looks after clicking **Set Up Web Service**:</span></span>

![Converted predictive experiment][figure3]

<span data-ttu-id="d461a-150">The work done by **Set Up Web Service** may be sufficient to prepare your experiment to be deployed as a web service.</span><span class="sxs-lookup"><span data-stu-id="d461a-150">The work done by **Set Up Web Service** may be sufficient to prepare your experiment to be deployed as a web service.</span></span> <span data-ttu-id="d461a-151">However, you may want to do some additional work specific to your experiment.</span><span class="sxs-lookup"><span data-stu-id="d461a-151">However, you may want to do some additional work specific to your experiment.</span></span>

### <a name="adjust-input-and-output-modules"></a><span data-ttu-id="d461a-152">Adjust input and output modules</span><span class="sxs-lookup"><span data-stu-id="d461a-152">Adjust input and output modules</span></span>
<span data-ttu-id="d461a-153">In your training experiment, you used a set of training data and then did some processing to get the data in a form that the machine learning algorithm needed.</span><span class="sxs-lookup"><span data-stu-id="d461a-153">In your training experiment, you used a set of training data and then did some processing to get the data in a form that the machine learning algorithm needed.</span></span> <span data-ttu-id="d461a-154">If the data you expect to receive through the web service will not need this processing, you can bypass it: connect the output of the **Web service input module** to a different module in your experiment.</span><span class="sxs-lookup"><span data-stu-id="d461a-154">If the data you expect to receive through the web service will not need this processing, you can bypass it: connect the output of the **Web service input module** to a different module in your experiment.</span></span> <span data-ttu-id="d461a-155">The user's data will now arrive in the model at this location.</span><span class="sxs-lookup"><span data-stu-id="d461a-155">The user's data will now arrive in the model at this location.</span></span>

<span data-ttu-id="d461a-156">For example, by default **Set Up Web Service** puts the **Web service input** module at the top of your data flow, as shown in the figure above.</span><span class="sxs-lookup"><span data-stu-id="d461a-156">For example, by default **Set Up Web Service** puts the **Web service input** module at the top of your data flow, as shown in the figure above.</span></span> <span data-ttu-id="d461a-157">But we can manually position the **Web service input** past the data processing modules:</span><span class="sxs-lookup"><span data-stu-id="d461a-157">But we can manually position the **Web service input** past the data processing modules:</span></span>

![Moving the web service input][figure4]

<span data-ttu-id="d461a-159">The input data provided through the web service will now pass directly into the Score Model module without any preprocessing.</span><span class="sxs-lookup"><span data-stu-id="d461a-159">The input data provided through the web service will now pass directly into the Score Model module without any preprocessing.</span></span>

<span data-ttu-id="d461a-160">Similarly, by default **Set Up Web Service** puts the Web service output module at the bottom of your data flow.</span><span class="sxs-lookup"><span data-stu-id="d461a-160">Similarly, by default **Set Up Web Service** puts the Web service output module at the bottom of your data flow.</span></span> <span data-ttu-id="d461a-161">In this example, the web service will return to the user the output of the [Score Model][score-model] module, which includes the complete input data vector plus the scoring results.</span><span class="sxs-lookup"><span data-stu-id="d461a-161">In this example, the web service will return to the user the output of the [Score Model][score-model] module, which includes the complete input data vector plus the scoring results.</span></span>
<span data-ttu-id="d461a-162">However, if you would prefer to return something different, then you can add additional modules before the **Web service output** module.</span><span class="sxs-lookup"><span data-stu-id="d461a-162">However, if you would prefer to return something different, then you can add additional modules before the **Web service output** module.</span></span> 

<span data-ttu-id="d461a-163">For example, to return only the scoring results and not the entire vector of input data, add a [Select Columns in Dataset][select-columns] module to exclude all columns except the scoring results.</span><span class="sxs-lookup"><span data-stu-id="d461a-163">For example, to return only the scoring results and not the entire vector of input data, add a [Select Columns in Dataset][select-columns] module to exclude all columns except the scoring results.</span></span> <span data-ttu-id="d461a-164">Then move the **Web service output** module to the output of the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="d461a-164">Then move the **Web service output** module to the output of the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="d461a-165">The experiment looks like this:</span><span class="sxs-lookup"><span data-stu-id="d461a-165">The experiment looks like this:</span></span>

![Moving the web service output][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a><span data-ttu-id="d461a-167">Add or remove additional data processing modules</span><span class="sxs-lookup"><span data-stu-id="d461a-167">Add or remove additional data processing modules</span></span>
<span data-ttu-id="d461a-168">If there are more modules in your experiment that you know will not be needed during scoring, these can be removed.</span><span class="sxs-lookup"><span data-stu-id="d461a-168">If there are more modules in your experiment that you know will not be needed during scoring, these can be removed.</span></span> <span data-ttu-id="d461a-169">For example, because we moved the **Web service input** module to a point after the data processing modules, we can remove the [Clean Missing Data][clean-missing-data] module from the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="d461a-169">For example, because we moved the **Web service input** module to a point after the data processing modules, we can remove the [Clean Missing Data][clean-missing-data] module from the predictive experiment.</span></span>

<span data-ttu-id="d461a-170">Our predictive experiment now looks like this:</span><span class="sxs-lookup"><span data-stu-id="d461a-170">Our predictive experiment now looks like this:</span></span>

![Removing additional module][figure6]


### <a name="add-optional-web-service-parameters"></a><span data-ttu-id="d461a-172">Add optional Web Service Parameters</span><span class="sxs-lookup"><span data-stu-id="d461a-172">Add optional Web Service Parameters</span></span>
<span data-ttu-id="d461a-173">In some cases, you may want to allow the user of your web service to change the behavior of modules when the service is accessed.</span><span class="sxs-lookup"><span data-stu-id="d461a-173">In some cases, you may want to allow the user of your web service to change the behavior of modules when the service is accessed.</span></span> <span data-ttu-id="d461a-174">*Web Service Parameters* allow you to do this.</span><span class="sxs-lookup"><span data-stu-id="d461a-174">*Web Service Parameters* allow you to do this.</span></span>

<span data-ttu-id="d461a-175">A common example is setting up an [Import Data][import-data] module so the user of the deployed web service can specify a different data source when the web service is accessed.</span><span class="sxs-lookup"><span data-stu-id="d461a-175">A common example is setting up an [Import Data][import-data] module so the user of the deployed web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="d461a-176">Or configuring an [Export Data][export-data] module so that a different destination can be specified.</span><span class="sxs-lookup"><span data-stu-id="d461a-176">Or configuring an [Export Data][export-data] module so that a different destination can be specified.</span></span>

<span data-ttu-id="d461a-177">You can define Web Service Parameters and associate them with one or more module parameters, and you can specify whether they are required or optional.</span><span class="sxs-lookup"><span data-stu-id="d461a-177">You can define Web Service Parameters and associate them with one or more module parameters, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="d461a-178">The user of the web service provides values for these parameters when the service is accessed, and the module actions are modified accordingly.</span><span class="sxs-lookup"><span data-stu-id="d461a-178">The user of the web service provides values for these parameters when the service is accessed, and the module actions are modified accordingly.</span></span>

<span data-ttu-id="d461a-179">For more information about what Web Service Parameters are and how to use them, see [Using Azure Machine Learning Web Service Parameters][webserviceparameters].</span><span class="sxs-lookup"><span data-stu-id="d461a-179">For more information about what Web Service Parameters are and how to use them, see [Using Azure Machine Learning Web Service Parameters][webserviceparameters].</span></span>

[webserviceparameters]: web-service-parameters.md


## <a name="deploy-the-predictive-experiment-as-a-web-service"></a><span data-ttu-id="d461a-180">Deploy the predictive experiment as a web service</span><span class="sxs-lookup"><span data-stu-id="d461a-180">Deploy the predictive experiment as a web service</span></span>
<span data-ttu-id="d461a-181">Now that the predictive experiment has been sufficiently prepared, you can deploy it as an Azure web service.</span><span class="sxs-lookup"><span data-stu-id="d461a-181">Now that the predictive experiment has been sufficiently prepared, you can deploy it as an Azure web service.</span></span> <span data-ttu-id="d461a-182">Using the web service, users can send data to your model and the model will return its predictions.</span><span class="sxs-lookup"><span data-stu-id="d461a-182">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="d461a-183">For more information on the complete deployment process, see [Deploy an Azure Machine Learning web service][deploy]</span><span class="sxs-lookup"><span data-stu-id="d461a-183">For more information on the complete deployment process, see [Deploy an Azure Machine Learning web service][deploy]</span></span>

[deploy]: publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
