---
title: (deprecated) Forecasting - ETS + STL - Azure  | Microsoft Docs
description: (deprecated) Forecasting - ETS + STL
services: machine-learning
documentationcenter: ''
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 5014c032f11cb0f78694f6b5cbcee6d935a4932a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553069"
---
# <a name="deprecated-forecasting---ets--stl"></a><span data-ttu-id="2bb8f-103">(deprecated) Forecasting - ETS + STL</span><span class="sxs-lookup"><span data-stu-id="2bb8f-103">(deprecated) Forecasting - ETS + STL</span></span>

> [!NOTE]
> <span data-ttu-id="2bb8f-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2bb8f-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="2bb8f-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2bb8f-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="2bb8f-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2bb8f-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implements Seasonal Trend Decomposition (STL) and Exponential Smoothing (ETS) models to produce predictions based on the historical data provided by the user.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implements Seasonal Trend Decomposition (STL) and Exponential Smoothing (ETS) models to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="2bb8f-108">Will the demand for a specific product increase this year?</span><span class="sxs-lookup"><span data-stu-id="2bb8f-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="2bb8f-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span><span class="sxs-lookup"><span data-stu-id="2bb8f-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="2bb8f-110">Forecasting models are apt to address such questions.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="2bb8f-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="2bb8f-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2bb8f-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="2bb8f-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2bb8f-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2bb8f-116">Consumption of web service</span><span class="sxs-lookup"><span data-stu-id="2bb8f-116">Consumption of web service</span></span>
<span data-ttu-id="2bb8f-117">This service accepts 4 arguments and calculates the forecasts.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-117">This service accepts 4 arguments and calculates the forecasts.</span></span>
<span data-ttu-id="2bb8f-118">The input arguments are:</span><span class="sxs-lookup"><span data-stu-id="2bb8f-118">The input arguments are:</span></span>

* <span data-ttu-id="2bb8f-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span><span class="sxs-lookup"><span data-stu-id="2bb8f-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="2bb8f-120">Horizon - Future forecast time-frame.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="2bb8f-121">Date - Add in the new time series data for time.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="2bb8f-122">Value - Add in the new time series data values.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="2bb8f-123">The output of the service is the calculated forecast values.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="2bb8f-124">Sample input could be:</span><span class="sxs-lookup"><span data-stu-id="2bb8f-124">Sample input could be:</span></span> 

* <span data-ttu-id="2bb8f-125">Frequency - 12</span><span class="sxs-lookup"><span data-stu-id="2bb8f-125">Frequency - 12</span></span>
* <span data-ttu-id="2bb8f-126">Horizon - 12</span><span class="sxs-lookup"><span data-stu-id="2bb8f-126">Horizon - 12</span></span>
* <span data-ttu-id="2bb8f-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="2bb8f-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="2bb8f-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="2bb8f-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="2bb8f-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2bb8f-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2bb8f-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2bb8f-131">Starting C# code for web service consumption:</span><span class="sxs-lookup"><span data-stu-id="2bb8f-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="2bb8f-132">Creation of web service</span><span class="sxs-lookup"><span data-stu-id="2bb8f-132">Creation of web service</span></span>
> <span data-ttu-id="2bb8f-133">This web service was created using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2bb8f-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="2bb8f-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2bb8f-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="2bb8f-136">From within Azure Machine Learning, a new blank experiment was created.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="2bb8f-137">Sample input data was uploaded with a predefined data schema.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="2bb8f-138">Linked to the data schema is an [Execute R Script][execute-r-script] module, which generates STL and ETS forecasting models by using ‘stl’, ‘ets’, and ‘forecast’ functions from R.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-138">Linked to the data schema is an [Execute R Script][execute-r-script] module, which generates STL and ETS forecasting models by using ‘stl’, ‘ets’, and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="2bb8f-139">Experiment flow:</span><span class="sxs-lookup"><span data-stu-id="2bb8f-139">Experiment flow:</span></span>
![Experiment flow][2]

#### <a name="module-1"></a><span data-ttu-id="2bb8f-141">Module 1:</span><span class="sxs-lookup"><span data-stu-id="2bb8f-141">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Sample data][3]    

#### <a name="module-2"></a><span data-ttu-id="2bb8f-143">Module 2:</span><span class="sxs-lookup"><span data-stu-id="2bb8f-143">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a><span data-ttu-id="2bb8f-144">Limitations</span><span class="sxs-lookup"><span data-stu-id="2bb8f-144">Limitations</span></span>
<span data-ttu-id="2bb8f-145">This is a very simple example for ETS + STL forecasting.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-145">This is a very simple example for ETS + STL forecasting.</span></span> <span data-ttu-id="2bb8f-146">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-146">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="2bb8f-147">The length of the date and value vectors should be the same, and the length of the time series should be greater than 2\*frequency.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-147">The length of the date and value vectors should be the same, and the length of the time series should be greater than 2\*frequency.</span></span> <span data-ttu-id="2bb8f-148">The date variable should adhere to the format ‘mm/dd/yyyy’.</span><span class="sxs-lookup"><span data-stu-id="2bb8f-148">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="2bb8f-149">FAQ</span><span class="sxs-lookup"><span data-stu-id="2bb8f-149">FAQ</span></span>
<span data-ttu-id="2bb8f-150">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2bb8f-150">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/



