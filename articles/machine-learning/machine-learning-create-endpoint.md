---
title: Creating Web service endpoints in Machine Learning | Microsoft Docs
description: Creating Web service endpoints in Azure Machine Learning
services: machine-learning
documentationcenter: ''
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: be7cb22e15d3f501c96a35e5d4e2dcbd7a5c929c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556041"
---
# <a name="creating-endpoints"></a><span data-ttu-id="14d42-103">Creating Endpoints</span><span class="sxs-lookup"><span data-stu-id="14d42-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="14d42-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span><span class="sxs-lookup"><span data-stu-id="14d42-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="14d42-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span><span class="sxs-lookup"><span data-stu-id="14d42-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="14d42-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span><span class="sxs-lookup"><span data-stu-id="14d42-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="14d42-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span><span class="sxs-lookup"><span data-stu-id="14d42-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="14d42-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span><span class="sxs-lookup"><span data-stu-id="14d42-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="14d42-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span><span class="sxs-lookup"><span data-stu-id="14d42-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="14d42-110">Adding endpoints to a Web service</span><span class="sxs-lookup"><span data-stu-id="14d42-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="14d42-111">There are three ways to add an endpoint to a Web service.</span><span class="sxs-lookup"><span data-stu-id="14d42-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="14d42-112">Programmatically</span><span class="sxs-lookup"><span data-stu-id="14d42-112">Programmatically</span></span>
* <span data-ttu-id="14d42-113">Through the Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="14d42-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="14d42-114">Though the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="14d42-114">Though the Azure classic portal</span></span>

<span data-ttu-id="14d42-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span><span class="sxs-lookup"><span data-stu-id="14d42-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="14d42-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span><span class="sxs-lookup"><span data-stu-id="14d42-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="14d42-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span><span class="sxs-lookup"><span data-stu-id="14d42-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="14d42-118">Adding an endpoint programmatically</span><span class="sxs-lookup"><span data-stu-id="14d42-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="14d42-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span><span class="sxs-lookup"><span data-stu-id="14d42-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="14d42-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="14d42-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="14d42-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span><span class="sxs-lookup"><span data-stu-id="14d42-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="14d42-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span><span class="sxs-lookup"><span data-stu-id="14d42-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="14d42-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span><span class="sxs-lookup"><span data-stu-id="14d42-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="14d42-124">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="14d42-124">Click **New**.</span></span>
4. <span data-ttu-id="14d42-125">Type a name and description for the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="14d42-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="14d42-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span><span class="sxs-lookup"><span data-stu-id="14d42-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="14d42-127">Select the logging level and whether sample data is enabled.</span><span class="sxs-lookup"><span data-stu-id="14d42-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="14d42-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="14d42-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="14d42-129">Adding an endpoint using the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="14d42-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="14d42-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span><span class="sxs-lookup"><span data-stu-id="14d42-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="14d42-131">Click the workspace which contains the Web service in which you are interested.</span><span class="sxs-lookup"><span data-stu-id="14d42-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Navigate to workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="14d42-133">Click **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="14d42-133">Click **Web Services**.</span></span>
   
    ![Navigate to Web services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="14d42-135">Click the Web service you're interested in to see the list of available endpoints.</span><span class="sxs-lookup"><span data-stu-id="14d42-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Navigate to endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="14d42-137">At the bottom of the page, click **Add Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="14d42-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="14d42-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span><span class="sxs-lookup"><span data-stu-id="14d42-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="14d42-139">Leave the throttle level with its default value unless you have special requirements.</span><span class="sxs-lookup"><span data-stu-id="14d42-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="14d42-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="14d42-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Create endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="14d42-142">Next Steps</span><span class="sxs-lookup"><span data-stu-id="14d42-142">Next Steps</span></span>
<span data-ttu-id="14d42-143">[How to consume a published Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="14d42-143">[How to consume a published Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>





