---
title: Consume a Machine Learning web service with a web app template | Microsoft Docs
description: Use a web app template in Azure Marketplace to consume a predictive web service in Azure Machine Learning.
keywords: web service,operationalization,REST API,machine learning
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 571b7c8e110d84c9b72f786e960058d31b463eb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556522"
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="5dfdc-104">Consume an Azure Machine Learning web service with a web app template</span><span class="sxs-lookup"><span data-stu-id="5dfdc-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="5dfdc-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="5dfdc-106">There are a number of ways to consume the REST API and access the web service.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="5dfdc-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="5dfdc-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="5dfdc-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="5dfdc-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="5dfdc-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="5dfdc-110">The Azure Machine Learning Web App Templates</span><span class="sxs-lookup"><span data-stu-id="5dfdc-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="5dfdc-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="5dfdc-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="5dfdc-113">Two templates are available:</span><span class="sxs-lookup"><span data-stu-id="5dfdc-113">Two templates are available:</span></span>

* [<span data-ttu-id="5dfdc-114">Azure ML Request-Response Service Web App Template</span><span class="sxs-lookup"><span data-stu-id="5dfdc-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="5dfdc-115">Azure ML Batch Execution Service Web App Template</span><span class="sxs-lookup"><span data-stu-id="5dfdc-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="5dfdc-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="5dfdc-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="5dfdc-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="5dfdc-119">No coding is required to use these templates.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-119">No coding is required to use these templates.</span></span> <span data-ttu-id="5dfdc-120">You just supply the API Key and URI, and the template builds the application for you.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="5dfdc-121">To get the API key and Request URI for a web service:</span><span class="sxs-lookup"><span data-stu-id="5dfdc-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="5dfdc-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="5dfdc-123">Or for a Classic web service click **Classic Web Services**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="5dfdc-124">Click the web service you want to access.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="5dfdc-125">For a Classic web service, click the endpoint you want to access.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="5dfdc-126">Click **Consume** at the top.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="5dfdc-127">Copy the **Primary** or **Secondary Key** and save it.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="5dfdc-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="5dfdc-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="5dfdc-130">How to use the Request-Response Service (RRS) template</span><span class="sxs-lookup"><span data-stu-id="5dfdc-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="5dfdc-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Process to use RRS web template][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="5dfdc-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="5dfdc-134">Give your web app a unique name.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-134">Give your web app a unique name.</span></span> <span data-ttu-id="5dfdc-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="5dfdc-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="5dfdc-136">Select the Azure subscription and services under which your web service is running.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="5dfdc-137">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-137">Click **Create**.</span></span>
     
     ![Create web app][image5]

4. <span data-ttu-id="5dfdc-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="5dfdc-140">For example, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="5dfdc-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="5dfdc-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="5dfdc-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span><span class="sxs-lookup"><span data-stu-id="5dfdc-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="5dfdc-143">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-143">Click **Submit**.</span></span>
     
     ![Enter Post URI and API Key][image6]

6. <span data-ttu-id="5dfdc-145">The web app displays its **Web App Configuration** page with the current web service settings.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="5dfdc-146">Here you can make changes to the settings used by the web app.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5dfdc-147">Changing the settings here only changes them for this web app.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="5dfdc-148">It doesn't change the default settings of your web service.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="5dfdc-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="5dfdc-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="5dfdc-151">From the home page you can enter values to send to your web service.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="5dfdc-152">Click **Submit** when you're done, and the result will be returned.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="5dfdc-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="5dfdc-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="5dfdc-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="5dfdc-156">As long as it is running you can browse to the home web address and enter new values.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="5dfdc-157">How to use the Batch Execution Service (BES) template</span><span class="sxs-lookup"><span data-stu-id="5dfdc-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="5dfdc-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="5dfdc-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="5dfdc-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![Process to use BES web template][image2]

1. <span data-ttu-id="5dfdc-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="5dfdc-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="5dfdc-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="5dfdc-165">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-165">Click **Submit**.</span></span>
   
    ![Storage information][image7]

<span data-ttu-id="5dfdc-167">The web app will display a page with job status.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="5dfdc-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="5dfdc-169">You also have the option of downloading the results to a local file.</span><span class="sxs-lookup"><span data-stu-id="5dfdc-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="5dfdc-170">For more information</span><span class="sxs-lookup"><span data-stu-id="5dfdc-170">For more information</span></span>
<span data-ttu-id="5dfdc-171">To learn more about...</span><span class="sxs-lookup"><span data-stu-id="5dfdc-171">To learn more about...</span></span>

* <span data-ttu-id="5dfdc-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="5dfdc-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="5dfdc-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="5dfdc-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="5dfdc-174">other ways to access your web service, see [How to consume an Azure Machine Learning web service](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="5dfdc-174">other ways to access your web service, see [How to consume an Azure Machine Learning web service](machine-learning-consume-web-services.md)</span></span>

[image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consume-web-service-with-web-app-template/storage.png







