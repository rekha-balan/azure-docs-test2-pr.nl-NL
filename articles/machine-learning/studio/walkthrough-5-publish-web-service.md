---
title: 'Step 5: Deploy the Machine Learning web service | Microsoft Docs'
description: 'Step 5 of the Develop a predictive solution walkthrough: Deploy a predictive experiment in Machine Learning Studio as a web service.'
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.openlocfilehash: 436656195e00311dd350a5526b01fffa56ac02ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864341"
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="a8f07-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="a8f07-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a8f07-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a8f07-105">Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="a8f07-105">Create a Machine Learning workspace</span></span>](walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="a8f07-106">Upload existing data</span><span class="sxs-lookup"><span data-stu-id="a8f07-106">Upload existing data</span></span>](walkthrough-2-upload-data.md)
3. [<span data-ttu-id="a8f07-107">Create a new experiment</span><span class="sxs-lookup"><span data-stu-id="a8f07-107">Create a new experiment</span></span>](walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a8f07-108">Train and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="a8f07-108">Train and evaluate the models</span></span>](walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="a8f07-109">**Deploy the web service**</span><span class="sxs-lookup"><span data-stu-id="a8f07-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="a8f07-110">Access the web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-110">Access the web service</span></span>](walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a8f07-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span><span class="sxs-lookup"><span data-stu-id="a8f07-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="a8f07-112">Up to this point we've been experimenting with training our model.</span><span class="sxs-lookup"><span data-stu-id="a8f07-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="a8f07-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span><span class="sxs-lookup"><span data-stu-id="a8f07-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="a8f07-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span><span class="sxs-lookup"><span data-stu-id="a8f07-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="a8f07-115">This is a three-step process:</span><span class="sxs-lookup"><span data-stu-id="a8f07-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="a8f07-116">Remove one of the models</span><span class="sxs-lookup"><span data-stu-id="a8f07-116">Remove one of the models</span></span>
2. <span data-ttu-id="a8f07-117">Convert the *training experiment* we've created into a *predictive experiment*</span><span class="sxs-lookup"><span data-stu-id="a8f07-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="a8f07-118">Deploy the predictive experiment as a web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="a8f07-119">Remove one of the models</span><span class="sxs-lookup"><span data-stu-id="a8f07-119">Remove one of the models</span></span>

<span data-ttu-id="a8f07-120">First, we need to trim this experiment down a little.</span><span class="sxs-lookup"><span data-stu-id="a8f07-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="a8f07-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="a8f07-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span><span class="sxs-lookup"><span data-stu-id="a8f07-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="a8f07-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span><span class="sxs-lookup"><span data-stu-id="a8f07-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="a8f07-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="a8f07-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="a8f07-125">We need to delete the following modules:</span><span class="sxs-lookup"><span data-stu-id="a8f07-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="a8f07-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="a8f07-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="a8f07-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span><span class="sxs-lookup"><span data-stu-id="a8f07-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="a8f07-128">[Normalize Data][normalize-data] (both of them)</span><span class="sxs-lookup"><span data-stu-id="a8f07-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="a8f07-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span><span class="sxs-lookup"><span data-stu-id="a8f07-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="a8f07-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![Removed the SVM model][3a]

<span data-ttu-id="a8f07-132">Our model should now look something like this:</span><span class="sxs-lookup"><span data-stu-id="a8f07-132">Our model should now look something like this:</span></span>

![Removed the SVM model][3]

<span data-ttu-id="a8f07-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="a8f07-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="a8f07-135">Convert the training experiment to a predictive experiment</span><span class="sxs-lookup"><span data-stu-id="a8f07-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="a8f07-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="a8f07-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="a8f07-137">This involves three steps:</span><span class="sxs-lookup"><span data-stu-id="a8f07-137">This involves three steps:</span></span>

1. <span data-ttu-id="a8f07-138">Save the model we've trained and then replace our training modules</span><span class="sxs-lookup"><span data-stu-id="a8f07-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="a8f07-139">Trim the experiment to remove modules that were only needed for training</span><span class="sxs-lookup"><span data-stu-id="a8f07-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="a8f07-140">Define where the web service will accept input and where it generates the output</span><span class="sxs-lookup"><span data-stu-id="a8f07-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="a8f07-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span><span class="sxs-lookup"><span data-stu-id="a8f07-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="a8f07-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="a8f07-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="a8f07-143">When you click **Set Up Web Service**, several things happen:</span><span class="sxs-lookup"><span data-stu-id="a8f07-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="a8f07-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span><span class="sxs-lookup"><span data-stu-id="a8f07-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="a8f07-145">Modules that were used for training are removed; specifically:</span><span class="sxs-lookup"><span data-stu-id="a8f07-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="a8f07-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="a8f07-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="a8f07-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="a8f07-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="a8f07-148">[Split Data][split]</span><span class="sxs-lookup"><span data-stu-id="a8f07-148">[Split Data][split]</span></span>
  * <span data-ttu-id="a8f07-149">the second [Execute R Script][execute-r-script] module that was used for test data</span><span class="sxs-lookup"><span data-stu-id="a8f07-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="a8f07-150">The saved trained model is added back into the experiment</span><span class="sxs-lookup"><span data-stu-id="a8f07-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="a8f07-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span><span class="sxs-lookup"><span data-stu-id="a8f07-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="a8f07-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="a8f07-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="a8f07-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="a8f07-154">The predictive experiment is the one we'll deploy as a web service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="a8f07-155">We need to take one additional step with this particular experiment.</span><span class="sxs-lookup"><span data-stu-id="a8f07-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="a8f07-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span><span class="sxs-lookup"><span data-stu-id="a8f07-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="a8f07-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span><span class="sxs-lookup"><span data-stu-id="a8f07-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="a8f07-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span><span class="sxs-lookup"><span data-stu-id="a8f07-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="a8f07-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="a8f07-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="a8f07-160">Our experiment should now look like this:</span><span class="sxs-lookup"><span data-stu-id="a8f07-160">Our experiment should now look like this:</span></span>  

![Scoring the trained model][4]  

> [!NOTE]
> <span data-ttu-id="a8f07-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="a8f07-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="a8f07-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span><span class="sxs-lookup"><span data-stu-id="a8f07-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="a8f07-164">It's true that the service doesn't need the original credit card data.</span><span class="sxs-lookup"><span data-stu-id="a8f07-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="a8f07-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span><span class="sxs-lookup"><span data-stu-id="a8f07-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="a8f07-166">This schema information is necessary to interpret the user's data.</span><span class="sxs-lookup"><span data-stu-id="a8f07-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="a8f07-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span><span class="sxs-lookup"><span data-stu-id="a8f07-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="a8f07-168">The data isn't used, just the schema.</span><span class="sxs-lookup"><span data-stu-id="a8f07-168">The data isn't used, just the schema.</span></span>  
> 
><span data-ttu-id="a8f07-169">One important thing to note is that if your original dataset contained the label, then the expected schema from the web input will also expect a column with the label!</span><span class="sxs-lookup"><span data-stu-id="a8f07-169">One important thing to note is that if your original dataset contained the label, then the expected schema from the web input will also expect a column with the label!</span></span> <span data-ttu-id="a8f07-170">A way around this is to remove the label, and any other data that was in the training dataset, but will not be in the web inputs, before connecting the web input and training dataset into a common module.</span><span class="sxs-lookup"><span data-stu-id="a8f07-170">A way around this is to remove the label, and any other data that was in the training dataset, but will not be in the web inputs, before connecting the web input and training dataset into a common module.</span></span> 
> 

<span data-ttu-id="a8f07-171">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-171">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="a8f07-172">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span><span class="sxs-lookup"><span data-stu-id="a8f07-172">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="a8f07-173">Deploy the web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-173">Deploy the web service</span></span>
<span data-ttu-id="a8f07-174">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8f07-174">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="a8f07-175">Deploy as a Classic web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-175">Deploy as a Classic web service</span></span>
<span data-ttu-id="a8f07-176">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-176">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="a8f07-177">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-177">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="a8f07-178">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span><span class="sxs-lookup"><span data-stu-id="a8f07-178">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="a8f07-179">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a8f07-179">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Web service dashboard][6]

<span data-ttu-id="a8f07-181">You can configure the service by clicking the **CONFIGURATION** tab. Here you can modify the service name (it's given the experiment name by default) and give it a description.</span><span class="sxs-lookup"><span data-stu-id="a8f07-181">You can configure the service by clicking the **CONFIGURATION** tab. Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="a8f07-182">You can also give more friendly labels for the input and output data.</span><span class="sxs-lookup"><span data-stu-id="a8f07-182">You can also give more friendly labels for the input and output data.</span></span>  

![Configure the web service][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="a8f07-184">Deploy as a New web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-184">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="a8f07-185">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-185">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="a8f07-186">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="a8f07-186">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span></span> 

<span data-ttu-id="a8f07-187">To deploy a New web service derived from our experiment:</span><span class="sxs-lookup"><span data-stu-id="a8f07-187">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="a8f07-188">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-188">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a8f07-189">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span><span class="sxs-lookup"><span data-stu-id="a8f07-189">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="a8f07-190">Enter a name for the web service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-190">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="a8f07-191">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span><span class="sxs-lookup"><span data-stu-id="a8f07-191">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="a8f07-192">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span><span class="sxs-lookup"><span data-stu-id="a8f07-192">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="a8f07-193">Click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-193">Click **Deploy**.</span></span>

<span data-ttu-id="a8f07-194">After a few minutes, the **Quickstart** page for your web service opens.</span><span class="sxs-lookup"><span data-stu-id="a8f07-194">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="a8f07-195">You can configure the service by clicking the **Configure** tab. Here you can modify the service title and give it a description.</span><span class="sxs-lookup"><span data-stu-id="a8f07-195">You can configure the service by clicking the **Configure** tab. Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="a8f07-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span><span class="sxs-lookup"><span data-stu-id="a8f07-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="a8f07-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span><span class="sxs-lookup"><span data-stu-id="a8f07-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="a8f07-198">You can update the web service after you've deployed it.</span><span class="sxs-lookup"><span data-stu-id="a8f07-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="a8f07-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a8f07-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span><span class="sxs-lookup"><span data-stu-id="a8f07-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="a8f07-201">Test the web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-201">Test the web service</span></span>

<span data-ttu-id="a8f07-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span><span class="sxs-lookup"><span data-stu-id="a8f07-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="a8f07-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span><span class="sxs-lookup"><span data-stu-id="a8f07-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="a8f07-204">The results are returned to the user from the web service through the **Web service output** module.</span><span class="sxs-lookup"><span data-stu-id="a8f07-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="a8f07-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span><span class="sxs-lookup"><span data-stu-id="a8f07-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="a8f07-206">This includes all the input data plus the credit risk value and the scoring probability.</span><span class="sxs-lookup"><span data-stu-id="a8f07-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="a8f07-207">But you can return something different if you want - for example, you could return just the credit risk value.</span><span class="sxs-lookup"><span data-stu-id="a8f07-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="a8f07-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span><span class="sxs-lookup"><span data-stu-id="a8f07-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="a8f07-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span><span class="sxs-lookup"><span data-stu-id="a8f07-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="a8f07-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span><span class="sxs-lookup"><span data-stu-id="a8f07-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="a8f07-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="a8f07-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="a8f07-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span><span class="sxs-lookup"><span data-stu-id="a8f07-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="a8f07-214">Test a Classic web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-214">Test a Classic web service</span></span>

<span data-ttu-id="a8f07-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="a8f07-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="a8f07-216">Test in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="a8f07-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="a8f07-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="a8f07-218">A dialog pops up and asks you for the input data for the service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="a8f07-219">These are the same columns that appeared in the original credit risk dataset.</span><span class="sxs-lookup"><span data-stu-id="a8f07-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="a8f07-220">Enter a set of data and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="a8f07-221">Test in the Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="a8f07-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="a8f07-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="a8f07-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="a8f07-224">These are the same columns that appeared in the original credit risk dataset.</span><span class="sxs-lookup"><span data-stu-id="a8f07-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="a8f07-225">Click **Test Request-Response**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="a8f07-226">Test a New web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-226">Test a New web service</span></span>

<span data-ttu-id="a8f07-227">You can test a New web service only in the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="a8f07-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="a8f07-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="a8f07-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="a8f07-229">The **Test** page opens and you can input data for the service.</span><span class="sxs-lookup"><span data-stu-id="a8f07-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="a8f07-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span><span class="sxs-lookup"><span data-stu-id="a8f07-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="a8f07-231">Enter a set of data and then click **Test Request-Response**.</span><span class="sxs-lookup"><span data-stu-id="a8f07-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="a8f07-232">The results of the test are displayed on the right-hand side of the page in the output column.</span><span class="sxs-lookup"><span data-stu-id="a8f07-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="a8f07-233">Manage the web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-233">Manage the web service</span></span>

<span data-ttu-id="a8f07-234">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="a8f07-234">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="a8f07-235">To monitor the performance of your web service:</span><span class="sxs-lookup"><span data-stu-id="a8f07-235">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="a8f07-236">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span><span class="sxs-lookup"><span data-stu-id="a8f07-236">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="a8f07-237">Click **Web services**</span><span class="sxs-lookup"><span data-stu-id="a8f07-237">Click **Web services**</span></span>
3. <span data-ttu-id="a8f07-238">Click your web service</span><span class="sxs-lookup"><span data-stu-id="a8f07-238">Click your web service</span></span>
4. <span data-ttu-id="a8f07-239">Click the **Dashboard**</span><span class="sxs-lookup"><span data-stu-id="a8f07-239">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="a8f07-240">**Next: [Access the web service](walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="a8f07-240">**Next: [Access the web service](walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/walkthrough-5-publish-web-service/publish4.png
[5]: ./media/walkthrough-5-publish-web-service/publish5.png
[6]: ./media/walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
