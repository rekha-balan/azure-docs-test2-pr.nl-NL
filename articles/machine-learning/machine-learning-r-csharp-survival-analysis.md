---
title: (deprecated) Survival Analysis with Azure Machine Learning | Microsoft Docs
description: (deprecated) Survival Analysis event occurrence probability
services: machine-learning
documentationcenter: ''
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 2665d3fc1c5ef5404152d4dc8bb40384e8b2e264
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552026"
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="e3aa9-103">(deprecated) Survival Analysis</span><span class="sxs-lookup"><span data-stu-id="e3aa9-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="e3aa9-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="e3aa9-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="e3aa9-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="e3aa9-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="e3aa9-108">In other words, the question “when this event will occur?”</span><span class="sxs-lookup"><span data-stu-id="e3aa9-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="e3aa9-109">is asked.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-109">is asked.</span></span> <span data-ttu-id="e3aa9-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="e3aa9-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e3aa9-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span><span class="sxs-lookup"><span data-stu-id="e3aa9-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="e3aa9-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="e3aa9-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="e3aa9-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="e3aa9-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="e3aa9-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="e3aa9-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="e3aa9-119">Consumption of web service</span><span class="sxs-lookup"><span data-stu-id="e3aa9-119">Consumption of web service</span></span>
<span data-ttu-id="e3aa9-120">The input data schema of the web service is shown in the following table.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="e3aa9-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="e3aa9-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="e3aa9-123">The number of features of the data is flexible.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="e3aa9-124">All the elements in the input string must be numeric.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="e3aa9-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="e3aa9-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="e3aa9-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="e3aa9-128">trainingdata - A character string.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-128">trainingdata - A character string.</span></span> <span data-ttu-id="e3aa9-129">Rows are separated by comma, and columns are separated by semicolon.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="e3aa9-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="e3aa9-131">testingdata - One row of data that contains predictor variables for a particular object.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="e3aa9-132">time_of_interest - The elapsed time of interest n.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="e3aa9-133">index_time - The column index of the “time” dimension (starting from 1).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="e3aa9-134">index_event - The column index of the “event” dimension (starting from 1).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="e3aa9-135">variable_types - A character string with semicolons as separators in it.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="e3aa9-136">0 represents continuous variables and 1 represents factor variables.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="e3aa9-137">The output is the probability of an event occurring by a specific time.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="e3aa9-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="e3aa9-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="e3aa9-140">Starting C# code for web service consumption:</span><span class="sxs-lookup"><span data-stu-id="e3aa9-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="e3aa9-141">The interpretation of this test is as follows.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="e3aa9-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="e3aa9-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="e3aa9-144">Creation of web service</span><span class="sxs-lookup"><span data-stu-id="e3aa9-144">Creation of web service</span></span>
> <span data-ttu-id="e3aa9-145">This web service was created using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="e3aa9-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="e3aa9-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="e3aa9-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="e3aa9-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="e3aa9-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="e3aa9-151">This module does data preprocessing, model building, and predictions.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="e3aa9-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="e3aa9-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="e3aa9-154">Then the “coxph” function is executed after a series data processing tasks.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="e3aa9-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="e3aa9-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="e3aa9-157">Finally, the probability of the time of interest is obtained.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="e3aa9-158">Experiment flow:</span><span class="sxs-lookup"><span data-stu-id="e3aa9-158">Experiment flow:</span></span>
![experiment flow][1]

#### <a name="module-1"></a><span data-ttu-id="e3aa9-160">Module 1:</span><span class="sxs-lookup"><span data-stu-id="e3aa9-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="e3aa9-161">Module 2:</span><span class="sxs-lookup"><span data-stu-id="e3aa9-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="e3aa9-162">Limitations</span><span class="sxs-lookup"><span data-stu-id="e3aa9-162">Limitations</span></span>
<span data-ttu-id="e3aa9-163">This web service can take only numerical values as feature variables (columns).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="e3aa9-164">The “event” column can take only value 0 or 1.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="e3aa9-165">The “time” column needs to be a positive integer.</span><span class="sxs-lookup"><span data-stu-id="e3aa9-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="e3aa9-166">FAQ</span><span class="sxs-lookup"><span data-stu-id="e3aa9-166">FAQ</span></span>
<span data-ttu-id="e3aa9-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e3aa9-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


