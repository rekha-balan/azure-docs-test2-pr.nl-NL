---
title: Retrain a Classic web service | Microsoft Docs
description: Learn how to programmatically retrain a model and update the web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.openlocfilehash: 6fc03865185b97fb1f34028239f647f97d5bd315
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869630"
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="ca953-103">Retrain a Classic web service</span><span class="sxs-lookup"><span data-stu-id="ca953-103">Retrain a Classic web service</span></span>
<span data-ttu-id="ca953-104">The Predictive Web Service you deployed is the default scoring endpoint.</span><span class="sxs-lookup"><span data-stu-id="ca953-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="ca953-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span><span class="sxs-lookup"><span data-stu-id="ca953-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="ca953-106">To retrain the web service, you must add a new endpoint to the web service.</span><span class="sxs-lookup"><span data-stu-id="ca953-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ca953-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ca953-107">Prerequisites</span></span>
<span data-ttu-id="ca953-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="ca953-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ca953-109">The predictive experiment must be deployed as a Classic machine learning web service.</span><span class="sxs-lookup"><span data-stu-id="ca953-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="ca953-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="ca953-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="ca953-111">Add a new endpoint</span><span class="sxs-lookup"><span data-stu-id="ca953-111">Add a new endpoint</span></span>
<span data-ttu-id="ca953-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span><span class="sxs-lookup"><span data-stu-id="ca953-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="ca953-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span><span class="sxs-lookup"><span data-stu-id="ca953-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="ca953-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span><span class="sxs-lookup"><span data-stu-id="ca953-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="ca953-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="ca953-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="ca953-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span><span class="sxs-lookup"><span data-stu-id="ca953-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="ca953-117">The Predictive Web Service should end with "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="ca953-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="ca953-118">There are two ways in which you can add a new end point to a web service:</span><span class="sxs-lookup"><span data-stu-id="ca953-118">There are two ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="ca953-119">Programmatically</span><span class="sxs-lookup"><span data-stu-id="ca953-119">Programmatically</span></span>
2. <span data-ttu-id="ca953-120">Use the Microsoft Azure Web Services portal</span><span class="sxs-lookup"><span data-stu-id="ca953-120">Use the Microsoft Azure Web Services portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="ca953-121">Programmatically add an endpoint</span><span class="sxs-lookup"><span data-stu-id="ca953-121">Programmatically add an endpoint</span></span>
<span data-ttu-id="ca953-122">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="ca953-122">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="ca953-123">Use the Microsoft Azure Web Services portal to add an endpoint</span><span class="sxs-lookup"><span data-stu-id="ca953-123">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="ca953-124">In Machine Learning Studio, on the left navigation column, click Web Services.</span><span class="sxs-lookup"><span data-stu-id="ca953-124">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="ca953-125">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span><span class="sxs-lookup"><span data-stu-id="ca953-125">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="ca953-126">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ca953-126">Click **Add**.</span></span>
4. <span data-ttu-id="ca953-127">Type a name and description for the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="ca953-127">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="ca953-128">Select the logging level and whether sample data is enabled.</span><span class="sxs-lookup"><span data-stu-id="ca953-128">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="ca953-129">For more information on logging, see [Enable logging for Machine Learning web services](web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="ca953-129">For more information on logging, see [Enable logging for Machine Learning web services](web-services-logging.md).</span></span>

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="ca953-130">Update the added endpoint’s trained model</span><span class="sxs-lookup"><span data-stu-id="ca953-130">Update the added endpoint’s trained model</span></span>
<span data-ttu-id="ca953-131">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span><span class="sxs-lookup"><span data-stu-id="ca953-131">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

<span data-ttu-id="ca953-132">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span><span class="sxs-lookup"><span data-stu-id="ca953-132">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="ca953-133">To retrieve the path URL:</span><span class="sxs-lookup"><span data-stu-id="ca953-133">To retrieve the path URL:</span></span>

1. <span data-ttu-id="ca953-134">Copy and paste the URL into your browser.</span><span class="sxs-lookup"><span data-stu-id="ca953-134">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="ca953-135">Click the Update Resource link.</span><span class="sxs-lookup"><span data-stu-id="ca953-135">Click the Update Resource link.</span></span>
3. <span data-ttu-id="ca953-136">Copy the POST URL of the PATCH request.</span><span class="sxs-lookup"><span data-stu-id="ca953-136">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="ca953-137">For example:</span><span class="sxs-lookup"><span data-stu-id="ca953-137">For example:</span></span>
   
     <span data-ttu-id="ca953-138">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="ca953-138">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="ca953-139">You can now use the trained model to update the scoring endpoint that you created previously.</span><span class="sxs-lookup"><span data-stu-id="ca953-139">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="ca953-140">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span><span class="sxs-lookup"><span data-stu-id="ca953-140">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="ca953-141">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span><span class="sxs-lookup"><span data-stu-id="ca953-141">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="ca953-142">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="ca953-142">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="ca953-143">To get the Resource Name:</span><span class="sxs-lookup"><span data-stu-id="ca953-143">To get the Resource Name:</span></span>

1. <span data-ttu-id="ca953-144">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ca953-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ca953-145">In the left menu, click **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="ca953-145">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="ca953-146">Under Name, click your workspace and then click **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="ca953-146">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="ca953-147">Under Name, click **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="ca953-147">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="ca953-148">Click the new endpoint you added.</span><span class="sxs-lookup"><span data-stu-id="ca953-148">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="ca953-149">On the endpoint dashboard, click **Update Resource**.</span><span class="sxs-lookup"><span data-stu-id="ca953-149">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="ca953-150">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span><span class="sxs-lookup"><span data-stu-id="ca953-150">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="ca953-151">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span><span class="sxs-lookup"><span data-stu-id="ca953-151">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="ca953-152">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="ca953-152">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="ca953-153">Summary</span><span class="sxs-lookup"><span data-stu-id="ca953-153">Summary</span></span>
<span data-ttu-id="ca953-154">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span><span class="sxs-lookup"><span data-stu-id="ca953-154">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="ca953-155">Periodic model retraining with new data.</span><span class="sxs-lookup"><span data-stu-id="ca953-155">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="ca953-156">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span><span class="sxs-lookup"><span data-stu-id="ca953-156">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca953-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="ca953-157">Next steps</span></span>
[<span data-ttu-id="ca953-158">Troubleshooting the retraining of an Azure Machine Learning classic web service</span><span class="sxs-lookup"><span data-stu-id="ca953-158">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](troubleshooting-retraining-models.md)

