---
title: Consume a Machine Learning web service by using a web app template | Microsoft Docs
description: Use a web app template in Azure Marketplace to consume a predictive web service in Azure Machine Learning.
keywords: web service,operationalization,REST API,machine learning
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.openlocfilehash: 3fee99426a459ac42242cef34fc7d4bd9c134bc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966513"
---
# <a name="consume-an-azure-machine-learning-web-service-by-using-a-web-app-template"></a><span data-ttu-id="bedb5-104">Consume an Azure Machine Learning web service by using a web app template</span><span class="sxs-lookup"><span data-stu-id="bedb5-104">Consume an Azure Machine Learning web service by using a web app template</span></span>

<span data-ttu-id="bedb5-105">You can develop a predictive model and deploy it as an Azure web service by using:</span><span class="sxs-lookup"><span data-stu-id="bedb5-105">You can develop a predictive model and deploy it as an Azure web service by using:</span></span>
- <span data-ttu-id="bedb5-106">Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="bedb5-106">Azure Machine Learning Studio.</span></span>
- <span data-ttu-id="bedb5-107">Tools such as R or Python.</span><span class="sxs-lookup"><span data-stu-id="bedb5-107">Tools such as R or Python.</span></span> 

<span data-ttu-id="bedb5-108">After that, you can access the operationalized model by using a REST API.</span><span class="sxs-lookup"><span data-stu-id="bedb5-108">After that, you can access the operationalized model by using a REST API.</span></span>

<span data-ttu-id="bedb5-109">There are a number of ways to consume the REST API and access the web service.</span><span class="sxs-lookup"><span data-stu-id="bedb5-109">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="bedb5-110">For example, you can write an application in C#, R, or Python by using the sample code generated for you when you deployed the web service.</span><span class="sxs-lookup"><span data-stu-id="bedb5-110">For example, you can write an application in C#, R, or Python by using the sample code generated for you when you deployed the web service.</span></span> <span data-ttu-id="bedb5-111">(The sample code is available in the [Machine Learning Web Services portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio.) Or you can use the sample Microsoft Excel workbook created for you at the same time.</span><span class="sxs-lookup"><span data-stu-id="bedb5-111">(The sample code is available in the [Machine Learning Web Services portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio.) Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="bedb5-112">But the quickest and easiest way to access your web service is through the web app templates available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="bedb5-112">But the quickest and easiest way to access your web service is through the web app templates available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="azure-machine-learning-web-app-templates"></a><span data-ttu-id="bedb5-113">Azure Machine Learning web app templates</span><span class="sxs-lookup"><span data-stu-id="bedb5-113">Azure Machine Learning web app templates</span></span>
<span data-ttu-id="bedb5-114">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span><span class="sxs-lookup"><span data-stu-id="bedb5-114">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="bedb5-115">All you need to do is give the web app access to your web service and data, and the template does the rest.</span><span class="sxs-lookup"><span data-stu-id="bedb5-115">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="bedb5-116">Two templates are available:</span><span class="sxs-lookup"><span data-stu-id="bedb5-116">Two templates are available:</span></span>

* [<span data-ttu-id="bedb5-117">Azure ML Request-Response Service Web App Template</span><span class="sxs-lookup"><span data-stu-id="bedb5-117">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="bedb5-118">Azure ML Batch Execution Service Web App Template</span><span class="sxs-lookup"><span data-stu-id="bedb5-118">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="bedb5-119">Each template creates a sample ASP.NET application by using the API URI and key for your web service.</span><span class="sxs-lookup"><span data-stu-id="bedb5-119">Each template creates a sample ASP.NET application by using the API URI and key for your web service.</span></span> <span data-ttu-id="bedb5-120">The template then deploys the application as a website to Azure.</span><span class="sxs-lookup"><span data-stu-id="bedb5-120">The template then deploys the application as a website to Azure.</span></span> 

<span data-ttu-id="bedb5-121">The Request-Response Service (RRS) template creates a web app that you can use to send a single row of data to the web service to get a single result.</span><span class="sxs-lookup"><span data-stu-id="bedb5-121">The Request-Response Service (RRS) template creates a web app that you can use to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="bedb5-122">The Batch Execution Service (BES) template creates a web app that you can use to send many rows of data to get multiple results.</span><span class="sxs-lookup"><span data-stu-id="bedb5-122">The Batch Execution Service (BES) template creates a web app that you can use to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="bedb5-123">No coding is required to use these templates.</span><span class="sxs-lookup"><span data-stu-id="bedb5-123">No coding is required to use these templates.</span></span> <span data-ttu-id="bedb5-124">You just supply the API key and URI, and the template builds the application for you.</span><span class="sxs-lookup"><span data-stu-id="bedb5-124">You just supply the API key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="bedb5-125">To get the API key and request URI for a web service:</span><span class="sxs-lookup"><span data-stu-id="bedb5-125">To get the API key and request URI for a web service:</span></span>

1. <span data-ttu-id="bedb5-126">In the [Web Services portal](https://services.azureml.net/quickstart), select **Web Services** at the top.</span><span class="sxs-lookup"><span data-stu-id="bedb5-126">In the [Web Services portal](https://services.azureml.net/quickstart), select **Web Services** at the top.</span></span> <span data-ttu-id="bedb5-127">Or for a classic web service, select **Classic Web Services**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-127">Or for a classic web service, select **Classic Web Services**.</span></span>
2. <span data-ttu-id="bedb5-128">Select the web service that you want to access.</span><span class="sxs-lookup"><span data-stu-id="bedb5-128">Select the web service that you want to access.</span></span>
3. <span data-ttu-id="bedb5-129">For a classic web service, select the endpoint that you want to access.</span><span class="sxs-lookup"><span data-stu-id="bedb5-129">For a classic web service, select the endpoint that you want to access.</span></span>
4. <span data-ttu-id="bedb5-130">Select **Consume** at the top.</span><span class="sxs-lookup"><span data-stu-id="bedb5-130">Select **Consume** at the top.</span></span>
5. <span data-ttu-id="bedb5-131">Copy the primary or secondary key and save it.</span><span class="sxs-lookup"><span data-stu-id="bedb5-131">Copy the primary or secondary key and save it.</span></span>
6. <span data-ttu-id="bedb5-132">If you're creating an RRS template, copy the **Request-Response** URI and save it.</span><span class="sxs-lookup"><span data-stu-id="bedb5-132">If you're creating an RRS template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="bedb5-133">If you're creating a BES template, copy the **Batch Requests** URI and save it.</span><span class="sxs-lookup"><span data-stu-id="bedb5-133">If you're creating a BES template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-template"></a><span data-ttu-id="bedb5-134">How to use the Request-Response Service template</span><span class="sxs-lookup"><span data-stu-id="bedb5-134">How to use the Request-Response Service template</span></span>
<span data-ttu-id="bedb5-135">Follow these steps to use the RRS web app template, as shown in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="bedb5-135">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Process to use RRS web template][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="bedb5-137">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bedb5-137">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bedb5-138">Select **New**, search for and select **Azure ML Request-Response Service Web App**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-138">Select **New**, search for and select **Azure ML Request-Response Service Web App**, and then select **Create**.</span></span> 
3. <span data-ttu-id="bedb5-139">In the **Create** pane:</span><span class="sxs-lookup"><span data-stu-id="bedb5-139">In the **Create** pane:</span></span>
   
   * <span data-ttu-id="bedb5-140">Give your web app a unique name.</span><span class="sxs-lookup"><span data-stu-id="bedb5-140">Give your web app a unique name.</span></span> <span data-ttu-id="bedb5-141">The URL of the web app will be this name followed by **.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-141">The URL of the web app will be this name followed by **.azurewebsites.net**.</span></span> <span data-ttu-id="bedb5-142">An example is **http://carprediction.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-142">An example is **http://carprediction.azurewebsites.net**.</span></span>
   * <span data-ttu-id="bedb5-143">Select the Azure subscription and services under which your web service is running.</span><span class="sxs-lookup"><span data-stu-id="bedb5-143">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="bedb5-144">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-144">Select **Create**.</span></span>
     
   ![Create web app][image5]

4. <span data-ttu-id="bedb5-146">When Azure has finished deploying the web app, select the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span><span class="sxs-lookup"><span data-stu-id="bedb5-146">When Azure has finished deploying the web app, select the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="bedb5-147">For example, enter **http://carprediction.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-147">For example, enter **http://carprediction.azurewebsites.net**.</span></span>
5. <span data-ttu-id="bedb5-148">When the web app first runs, it asks you for the **API Post URL** and **API Key**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-148">When the web app first runs, it asks you for the **API Post URL** and **API Key**.</span></span> <span data-ttu-id="bedb5-149">Enter the values that you saved earlier (request URI and API key, respectively).</span><span class="sxs-lookup"><span data-stu-id="bedb5-149">Enter the values that you saved earlier (request URI and API key, respectively).</span></span> <span data-ttu-id="bedb5-150">Select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-150">Select **Submit**.</span></span>
     
   ![Enter post URI and API key][image6]

6. <span data-ttu-id="bedb5-152">The web app displays its **Web App Configuration** page with the current web service settings.</span><span class="sxs-lookup"><span data-stu-id="bedb5-152">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="bedb5-153">Here you can make changes to the settings that the web app uses.</span><span class="sxs-lookup"><span data-stu-id="bedb5-153">Here you can make changes to the settings that the web app uses.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bedb5-154">Changing the settings here only changes them for this web app.</span><span class="sxs-lookup"><span data-stu-id="bedb5-154">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="bedb5-155">It doesn't change the default settings of your web service.</span><span class="sxs-lookup"><span data-stu-id="bedb5-155">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="bedb5-156">For example, if you change the text in **Description** here, it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="bedb5-156">For example, if you change the text in **Description** here, it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="bedb5-157">When you're done, select **Save changes**, and then select **Go to Home Page**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-157">When you're done, select **Save changes**, and then select **Go to Home Page**.</span></span>

7. <span data-ttu-id="bedb5-158">From the home page, you can enter values to send to your web service.</span><span class="sxs-lookup"><span data-stu-id="bedb5-158">From the home page, you can enter values to send to your web service.</span></span> <span data-ttu-id="bedb5-159">Select **Submit** when you're done, and the result will be returned.</span><span class="sxs-lookup"><span data-stu-id="bedb5-159">Select **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="bedb5-160">If you want to return to the **Configuration** page, go to the **setting.aspx** page of the web app.</span><span class="sxs-lookup"><span data-stu-id="bedb5-160">If you want to return to the **Configuration** page, go to the **setting.aspx** page of the web app.</span></span> <span data-ttu-id="bedb5-161">For example, go to **http://carprediction.azurewebsites.net/setting.aspx**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-161">For example, go to **http://carprediction.azurewebsites.net/setting.aspx**.</span></span> <span data-ttu-id="bedb5-162">You're prompted to enter the API key again.</span><span class="sxs-lookup"><span data-stu-id="bedb5-162">You're prompted to enter the API key again.</span></span> <span data-ttu-id="bedb5-163">You need that to access the page and update the settings.</span><span class="sxs-lookup"><span data-stu-id="bedb5-163">You need that to access the page and update the settings.</span></span>

<span data-ttu-id="bedb5-164">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span><span class="sxs-lookup"><span data-stu-id="bedb5-164">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="bedb5-165">As long as it's running, you can browse to the home web address and enter new values.</span><span class="sxs-lookup"><span data-stu-id="bedb5-165">As long as it's running, you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-template"></a><span data-ttu-id="bedb5-166">How to use the Batch Execution Service template</span><span class="sxs-lookup"><span data-stu-id="bedb5-166">How to use the Batch Execution Service template</span></span>
<span data-ttu-id="bedb5-167">You can use the BES web app template in the same way as the RRS template.</span><span class="sxs-lookup"><span data-stu-id="bedb5-167">You can use the BES web app template in the same way as the RRS template.</span></span> <span data-ttu-id="bedb5-168">The difference is that you can use the created web app to submit multiple rows of data and receive multiple results.</span><span class="sxs-lookup"><span data-stu-id="bedb5-168">The difference is that you can use the created web app to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="bedb5-169">The input values for a batch execution web service can come from Azure Storage or a local file.</span><span class="sxs-lookup"><span data-stu-id="bedb5-169">The input values for a batch execution web service can come from Azure Storage or a local file.</span></span> <span data-ttu-id="bedb5-170">The results are stored in an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="bedb5-170">The results are stored in an Azure storage container.</span></span> <span data-ttu-id="bedb5-171">So, you need an Azure storage container to hold the results that the web app returns.</span><span class="sxs-lookup"><span data-stu-id="bedb5-171">So, you need an Azure storage container to hold the results that the web app returns.</span></span> <span data-ttu-id="bedb5-172">You also need to get your input data ready.</span><span class="sxs-lookup"><span data-stu-id="bedb5-172">You also need to get your input data ready.</span></span>

![Process to use BES web template][image2]

1. <span data-ttu-id="bedb5-174">Follow the same procedure to create the BES web app as for the RRS template.</span><span class="sxs-lookup"><span data-stu-id="bedb5-174">Follow the same procedure to create the BES web app as for the RRS template.</span></span> <span data-ttu-id="bedb5-175">But in this case, go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bedb5-175">But in this case, go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template in the Azure Marketplace.</span></span> <span data-ttu-id="bedb5-176">Select **Create Web App**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-176">Select **Create Web App**.</span></span>

2. <span data-ttu-id="bedb5-177">To specify where you want the results stored, enter the destination container information on the web app's home page.</span><span class="sxs-lookup"><span data-stu-id="bedb5-177">To specify where you want the results stored, enter the destination container information on the web app's home page.</span></span> <span data-ttu-id="bedb5-178">Also specify where the web app can get the input values: either in a local file or in an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="bedb5-178">Also specify where the web app can get the input values: either in a local file or in an Azure storage container.</span></span>
   <span data-ttu-id="bedb5-179">Select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="bedb5-179">Select **Submit**.</span></span>
   
   ![Storage information][image7]

<span data-ttu-id="bedb5-181">The web app displays a page with job status.</span><span class="sxs-lookup"><span data-stu-id="bedb5-181">The web app displays a page with job status.</span></span> <span data-ttu-id="bedb5-182">When the job is completed, you get the location of the results in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="bedb5-182">When the job is completed, you get the location of the results in Azure Blob storage.</span></span> <span data-ttu-id="bedb5-183">You also have the option of downloading the results to a local file.</span><span class="sxs-lookup"><span data-stu-id="bedb5-183">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="bedb5-184">For more information</span><span class="sxs-lookup"><span data-stu-id="bedb5-184">For more information</span></span>
<span data-ttu-id="bedb5-185">To learn more about:</span><span class="sxs-lookup"><span data-stu-id="bedb5-185">To learn more about:</span></span>

* <span data-ttu-id="bedb5-186">Creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="bedb5-186">Creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](create-experiment.md).</span></span>
* <span data-ttu-id="bedb5-187">How to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bedb5-187">How to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="bedb5-188">Other ways to access your web service, see [How to consume an Azure Machine Learning web service](consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="bedb5-188">Other ways to access your web service, see [How to consume an Azure Machine Learning web service](consume-web-services.md).</span></span>

[image1]: media/consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/consume-web-service-with-web-app-template/api-key.png
[image4]: media/consume-web-service-with-web-app-template/post-uri.png
[image5]: media/consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/consume-web-service-with-web-app-template/storage.png
