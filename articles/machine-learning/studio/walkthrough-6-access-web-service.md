---
title: 'Step 6: Access the Machine Learning Web service | Microsoft Docs'
description: 'Step 6 of the Develop a predictive solution walkthrough: Access an active Azure Machine Learning Web service.'
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.openlocfilehash: be63a04d0fe71039b19eb6bc0678a319f622a811
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855853"
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="bf5e4-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="bf5e4-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="bf5e4-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="bf5e4-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="bf5e4-105">Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="bf5e4-105">Create a Machine Learning workspace</span></span>](walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="bf5e4-106">Upload existing data</span><span class="sxs-lookup"><span data-stu-id="bf5e4-106">Upload existing data</span></span>](walkthrough-2-upload-data.md)
3. [<span data-ttu-id="bf5e4-107">Create a new experiment</span><span class="sxs-lookup"><span data-stu-id="bf5e4-107">Create a new experiment</span></span>](walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="bf5e4-108">Train and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="bf5e4-108">Train and evaluate the models</span></span>](walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="bf5e4-109">Deploy the Web service</span><span class="sxs-lookup"><span data-stu-id="bf5e4-109">Deploy the Web service</span></span>](walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="bf5e4-110">**Access the Web service**</span><span class="sxs-lookup"><span data-stu-id="bf5e4-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="bf5e4-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="bf5e4-112">Now users are able to send data to it and receive results.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="bf5e4-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="bf5e4-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="bf5e4-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="bf5e4-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="bf5e4-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="bf5e4-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="bf5e4-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="bf5e4-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="bf5e4-119">All you need to do is provide access to your web service and data, and the template does the rest.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="bf5e4-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="bf5e4-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="bf5e4-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span><span class="sxs-lookup"><span data-stu-id="bf5e4-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="bf5e4-122">You can find complete details in [How to consume an Azure Machine Learning Web service](consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="bf5e4-122">You can find complete details in [How to consume an Azure Machine Learning Web service](consume-web-services.md).</span></span>

