---
title: (deprecated) Binomial Distribution Suite - Azure | Microsoft Docs
description: (deprecated) Binomial Distribution Suite
services: machine-learning
documentationcenter: ''
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: cf92391de4b9a32bbca68fcc7ae6be58b4c14e43
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554360"
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="23b95-103">(deprecated) Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="23b95-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="23b95-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span><span class="sxs-lookup"><span data-stu-id="23b95-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="23b95-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="23b95-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="23b95-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="23b95-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="23b95-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span><span class="sxs-lookup"><span data-stu-id="23b95-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="23b95-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span><span class="sxs-lookup"><span data-stu-id="23b95-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="23b95-109">Each of the services emits different outputs based on the selected service (see description below).</span><span class="sxs-lookup"><span data-stu-id="23b95-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="23b95-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span><span class="sxs-lookup"><span data-stu-id="23b95-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="23b95-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span><span class="sxs-lookup"><span data-stu-id="23b95-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="23b95-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span><span class="sxs-lookup"><span data-stu-id="23b95-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="23b95-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span><span class="sxs-lookup"><span data-stu-id="23b95-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="23b95-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span><span class="sxs-lookup"><span data-stu-id="23b95-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="23b95-115">Consumption of web service</span><span class="sxs-lookup"><span data-stu-id="23b95-115">Consumption of web service</span></span>
<span data-ttu-id="23b95-116">The Binomial Distribution Suite includes the following 3 services.</span><span class="sxs-lookup"><span data-stu-id="23b95-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="23b95-117">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="23b95-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="23b95-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span><span class="sxs-lookup"><span data-stu-id="23b95-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="23b95-119">The input arguments are:</span><span class="sxs-lookup"><span data-stu-id="23b95-119">The input arguments are:</span></span>

* <span data-ttu-id="23b95-120">p - A single aggregated probability of multiple trials.</span><span class="sxs-lookup"><span data-stu-id="23b95-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="23b95-121">size - The number of trials.</span><span class="sxs-lookup"><span data-stu-id="23b95-121">size - The number of trials.</span></span>
* <span data-ttu-id="23b95-122">prob - The probability of success in a trial.</span><span class="sxs-lookup"><span data-stu-id="23b95-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="23b95-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span><span class="sxs-lookup"><span data-stu-id="23b95-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="23b95-124">The output of the service is the calculated quantile that is associated with the given probability.</span><span class="sxs-lookup"><span data-stu-id="23b95-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="23b95-125">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="23b95-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="23b95-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span><span class="sxs-lookup"><span data-stu-id="23b95-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="23b95-127">The input arguments are:</span><span class="sxs-lookup"><span data-stu-id="23b95-127">The input arguments are:</span></span>

* <span data-ttu-id="23b95-128">q - A single quantile of an event with binomial distribution.</span><span class="sxs-lookup"><span data-stu-id="23b95-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="23b95-129">size - The number of trials.</span><span class="sxs-lookup"><span data-stu-id="23b95-129">size - The number of trials.</span></span>
* <span data-ttu-id="23b95-130">prob - The probability of success in a trial.</span><span class="sxs-lookup"><span data-stu-id="23b95-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="23b95-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span><span class="sxs-lookup"><span data-stu-id="23b95-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="23b95-132">The output of the service is the calculated probability that is associated with the given quantile.</span><span class="sxs-lookup"><span data-stu-id="23b95-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="23b95-133">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="23b95-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="23b95-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span><span class="sxs-lookup"><span data-stu-id="23b95-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="23b95-135">The following arguments should be provided to it within the request:</span><span class="sxs-lookup"><span data-stu-id="23b95-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="23b95-136">n - Number of observations.</span><span class="sxs-lookup"><span data-stu-id="23b95-136">n - Number of observations.</span></span> 
* <span data-ttu-id="23b95-137">size - Number of trials.</span><span class="sxs-lookup"><span data-stu-id="23b95-137">size - Number of trials.</span></span>
* <span data-ttu-id="23b95-138">prob - Probability of success.</span><span class="sxs-lookup"><span data-stu-id="23b95-138">prob - Probability of success.</span></span>

<span data-ttu-id="23b95-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span><span class="sxs-lookup"><span data-stu-id="23b95-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="23b95-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span><span class="sxs-lookup"><span data-stu-id="23b95-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="23b95-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="23b95-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="23b95-142">Starting C# code for web service consumption:</span><span class="sxs-lookup"><span data-stu-id="23b95-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="23b95-143">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="23b95-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="23b95-144">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="23b95-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="23b95-145">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="23b95-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="23b95-146">Creation of web service</span><span class="sxs-lookup"><span data-stu-id="23b95-146">Creation of web service</span></span>
> <span data-ttu-id="23b95-147">This web service was created using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="23b95-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="23b95-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="23b95-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="23b95-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span><span class="sxs-lookup"><span data-stu-id="23b95-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="23b95-150">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="23b95-150">Binomial Distribution Quantile Calculator</span></span>
![Create workspace][4]

#### <a name="module-1"></a><span data-ttu-id="23b95-152">Module 1:</span><span class="sxs-lookup"><span data-stu-id="23b95-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="23b95-153">Module 2:</span><span class="sxs-lookup"><span data-stu-id="23b95-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="23b95-154">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="23b95-154">Binomial Distribution Probability Calculator</span></span>
![Create workspace][5]

#### <a name="module-1"></a><span data-ttu-id="23b95-156">Module 1:</span><span class="sxs-lookup"><span data-stu-id="23b95-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="23b95-157">Module 2:</span><span class="sxs-lookup"><span data-stu-id="23b95-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="23b95-158">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="23b95-158">Binomial Distribution Generator</span></span>
![Create workspace][6]

#### <a name="module-1"></a><span data-ttu-id="23b95-160">Module 1:</span><span class="sxs-lookup"><span data-stu-id="23b95-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="23b95-161">Module 2:</span><span class="sxs-lookup"><span data-stu-id="23b95-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="23b95-162">Limitations</span><span class="sxs-lookup"><span data-stu-id="23b95-162">Limitations</span></span>
<span data-ttu-id="23b95-163">These are very simple examples surrounding the binomial distribution.</span><span class="sxs-lookup"><span data-stu-id="23b95-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="23b95-164">As can be seen from the example code above, little error catching is implemented.</span><span class="sxs-lookup"><span data-stu-id="23b95-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="23b95-165">FAQ</span><span class="sxs-lookup"><span data-stu-id="23b95-165">FAQ</span></span>
<span data-ttu-id="23b95-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="23b95-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-r-csharp-binomial-distribution/binomial_6.png




