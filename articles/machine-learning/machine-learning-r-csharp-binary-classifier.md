---
title: (deprecated) Binary Classifier - Azure | Microsoft Docs
description: (deprecated) Binary Classifier
services: machine-learning
documentationcenter: ''
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 2371eab12d01cc8f7e970d739a4c428d2a7d5581
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554009"
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="0be11-103">(deprecated) Binary Classifier</span><span class="sxs-lookup"><span data-stu-id="0be11-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="0be11-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="0be11-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0be11-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0be11-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0be11-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0be11-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0be11-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span><span class="sxs-lookup"><span data-stu-id="0be11-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="0be11-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span><span class="sxs-lookup"><span data-stu-id="0be11-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="0be11-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span><span class="sxs-lookup"><span data-stu-id="0be11-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0be11-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span><span class="sxs-lookup"><span data-stu-id="0be11-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="0be11-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span><span class="sxs-lookup"><span data-stu-id="0be11-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="0be11-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span><span class="sxs-lookup"><span data-stu-id="0be11-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="0be11-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span><span class="sxs-lookup"><span data-stu-id="0be11-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0be11-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span><span class="sxs-lookup"><span data-stu-id="0be11-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="0be11-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span><span class="sxs-lookup"><span data-stu-id="0be11-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0be11-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span><span class="sxs-lookup"><span data-stu-id="0be11-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0be11-117">Consumption of web service</span><span class="sxs-lookup"><span data-stu-id="0be11-117">Consumption of web service</span></span>
<span data-ttu-id="0be11-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span><span class="sxs-lookup"><span data-stu-id="0be11-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="0be11-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span><span class="sxs-lookup"><span data-stu-id="0be11-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="0be11-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span><span class="sxs-lookup"><span data-stu-id="0be11-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="0be11-121">An example dataset could look like this:</span><span class="sxs-lookup"><span data-stu-id="0be11-121">An example dataset could look like this:</span></span>

![Sample data][1]

<span data-ttu-id="0be11-123">Observations without a dependent variable should be input as “NA” for y.</span><span class="sxs-lookup"><span data-stu-id="0be11-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="0be11-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span><span class="sxs-lookup"><span data-stu-id="0be11-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="0be11-125">The output is the predicted value for each of the rows based on the independent variables.</span><span class="sxs-lookup"><span data-stu-id="0be11-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="0be11-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span><span class="sxs-lookup"><span data-stu-id="0be11-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0be11-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0be11-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0be11-128">Starting C# code for web service consumption:</span><span class="sxs-lookup"><span data-stu-id="0be11-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
        var httpClient = new HttpClient();

        httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
        httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var response = httpClient.PostAsync(acitionUri, new StringContent(json));
        var result = response.Result.Content;
        var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="0be11-129">Creation of web service</span><span class="sxs-lookup"><span data-stu-id="0be11-129">Creation of web service</span></span>
> <span data-ttu-id="0be11-130">This web service was created using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0be11-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0be11-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0be11-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0be11-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span><span class="sxs-lookup"><span data-stu-id="0be11-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="0be11-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span><span class="sxs-lookup"><span data-stu-id="0be11-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="0be11-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span><span class="sxs-lookup"><span data-stu-id="0be11-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="0be11-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span><span class="sxs-lookup"><span data-stu-id="0be11-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="0be11-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span><span class="sxs-lookup"><span data-stu-id="0be11-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="0be11-137">The second module fits a generic logistic regression model for the input data.</span><span class="sxs-lookup"><span data-stu-id="0be11-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Experiment flow][2]

#### <a name="module-1"></a><span data-ttu-id="0be11-139">Module 1:</span><span class="sxs-lookup"><span data-stu-id="0be11-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="0be11-140">Module 2:</span><span class="sxs-lookup"><span data-stu-id="0be11-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="0be11-141">Limitations</span><span class="sxs-lookup"><span data-stu-id="0be11-141">Limitations</span></span>
<span data-ttu-id="0be11-142">This is a very simple example of a binary classification web service.</span><span class="sxs-lookup"><span data-stu-id="0be11-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="0be11-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span><span class="sxs-lookup"><span data-stu-id="0be11-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="0be11-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span><span class="sxs-lookup"><span data-stu-id="0be11-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0be11-145">FAQ</span><span class="sxs-lookup"><span data-stu-id="0be11-145">FAQ</span></span>
<span data-ttu-id="0be11-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0be11-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


