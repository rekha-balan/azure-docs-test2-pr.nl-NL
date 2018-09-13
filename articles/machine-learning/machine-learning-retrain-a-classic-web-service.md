---
title: Retrain a Classic web service | Microsoft Docs
description: Learn how to programmatically retrain a model and update the web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondlaghaeian
editor: ''
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555062"
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="b57cc-103">Retrain a Classic web service</span><span class="sxs-lookup"><span data-stu-id="b57cc-103">Retrain a Classic web service</span></span>
<span data-ttu-id="b57cc-104">The Predictive Web Service you deployed is the default scoring endpoint.</span><span class="sxs-lookup"><span data-stu-id="b57cc-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="b57cc-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span><span class="sxs-lookup"><span data-stu-id="b57cc-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="b57cc-106">To retrain the web service, you must add a new endpoint to the web service.</span><span class="sxs-lookup"><span data-stu-id="b57cc-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b57cc-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b57cc-107">Prerequisites</span></span>
<span data-ttu-id="b57cc-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="b57cc-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b57cc-109">The predictive experiment must be deployed as a Classic machine learning web service.</span><span class="sxs-lookup"><span data-stu-id="b57cc-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="b57cc-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="b57cc-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="b57cc-111">Add a new Endpoint</span><span class="sxs-lookup"><span data-stu-id="b57cc-111">Add a new Endpoint</span></span>
<span data-ttu-id="b57cc-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span><span class="sxs-lookup"><span data-stu-id="b57cc-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="b57cc-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span><span class="sxs-lookup"><span data-stu-id="b57cc-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="b57cc-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span><span class="sxs-lookup"><span data-stu-id="b57cc-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="b57cc-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="b57cc-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="b57cc-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span><span class="sxs-lookup"><span data-stu-id="b57cc-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="b57cc-117">The Predictive Web Service should end with "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="b57cc-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="b57cc-118">There are three ways in which you can add a new end point to a web service:</span><span class="sxs-lookup"><span data-stu-id="b57cc-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="b57cc-119">Programmatically</span><span class="sxs-lookup"><span data-stu-id="b57cc-119">Programmatically</span></span>
2. <span data-ttu-id="b57cc-120">Use the Microsoft Azure Web Services portal</span><span class="sxs-lookup"><span data-stu-id="b57cc-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="b57cc-121">Use the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b57cc-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="b57cc-122">Programmatically add an endpoint</span><span class="sxs-lookup"><span data-stu-id="b57cc-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="b57cc-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b57cc-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="b57cc-124">Use the Microsoft Azure Web Services portal to add an endpoint</span><span class="sxs-lookup"><span data-stu-id="b57cc-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="b57cc-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span><span class="sxs-lookup"><span data-stu-id="b57cc-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="b57cc-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="b57cc-127">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-127">Click **Add**.</span></span>
4. <span data-ttu-id="b57cc-128">Type a name and description for the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="b57cc-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="b57cc-129">Select the logging level and whether sample data is enabled.</span><span class="sxs-lookup"><span data-stu-id="b57cc-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="b57cc-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="b57cc-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="b57cc-131">Use the Azure classic portal to add an endpoint</span><span class="sxs-lookup"><span data-stu-id="b57cc-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="b57cc-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b57cc-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b57cc-133">In the left menu, click **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="b57cc-134">Under Name, click your workspace and then click **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="b57cc-135">Under Name, click **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="b57cc-136">At the bottom of the page, click **Add Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="b57cc-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b57cc-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="b57cc-138">Update the added endpoint’s Trained Model</span><span class="sxs-lookup"><span data-stu-id="b57cc-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="b57cc-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span><span class="sxs-lookup"><span data-stu-id="b57cc-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="b57cc-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span><span class="sxs-lookup"><span data-stu-id="b57cc-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="b57cc-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span><span class="sxs-lookup"><span data-stu-id="b57cc-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="b57cc-142">To retrieve the path URL:</span><span class="sxs-lookup"><span data-stu-id="b57cc-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="b57cc-143">Copy and paste the URL into your browser.</span><span class="sxs-lookup"><span data-stu-id="b57cc-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="b57cc-144">Click the Update Resource link.</span><span class="sxs-lookup"><span data-stu-id="b57cc-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="b57cc-145">Copy the POST URL of the PATCH request.</span><span class="sxs-lookup"><span data-stu-id="b57cc-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="b57cc-146">For example:</span><span class="sxs-lookup"><span data-stu-id="b57cc-146">For example:</span></span>
   
     <span data-ttu-id="b57cc-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="b57cc-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="b57cc-148">You can now use the trained model to update the scoring endpoint that you created previously.</span><span class="sxs-lookup"><span data-stu-id="b57cc-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="b57cc-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b57cc-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

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

<span data-ttu-id="b57cc-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span><span class="sxs-lookup"><span data-stu-id="b57cc-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="b57cc-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="b57cc-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="b57cc-152">To get the Resource Name:</span><span class="sxs-lookup"><span data-stu-id="b57cc-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="b57cc-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b57cc-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b57cc-154">In the left menu, click **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="b57cc-155">Under Name, click your workspace and then click **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="b57cc-156">Under Name, click **Census Model [predictive exp.]**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="b57cc-157">Click the new endpoint you added.</span><span class="sxs-lookup"><span data-stu-id="b57cc-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="b57cc-158">On the endpoint dashboard, click **Update Resource**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="b57cc-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span><span class="sxs-lookup"><span data-stu-id="b57cc-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="b57cc-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span><span class="sxs-lookup"><span data-stu-id="b57cc-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="b57cc-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="b57cc-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="b57cc-162">Summary</span><span class="sxs-lookup"><span data-stu-id="b57cc-162">Summary</span></span>
<span data-ttu-id="b57cc-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span><span class="sxs-lookup"><span data-stu-id="b57cc-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="b57cc-164">Periodic model retraining with new data.</span><span class="sxs-lookup"><span data-stu-id="b57cc-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="b57cc-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span><span class="sxs-lookup"><span data-stu-id="b57cc-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b57cc-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="b57cc-166">Next steps</span></span>
[<span data-ttu-id="b57cc-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span><span class="sxs-lookup"><span data-stu-id="b57cc-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

