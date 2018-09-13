---
title: Creating Web service endpoints in Machine Learning | Microsoft Docs
description: Creating Web service endpoints in Azure Machine Learning
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.component: studio
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.openlocfilehash: 8cdf8c5ac3676d8abc9084fc842484aca5b6d1c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871741"
---
# <a name="creating-endpoints"></a><span data-ttu-id="32116-103">Creating endpoints</span><span class="sxs-lookup"><span data-stu-id="32116-103">Creating endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="32116-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span><span class="sxs-lookup"><span data-stu-id="32116-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="32116-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span><span class="sxs-lookup"><span data-stu-id="32116-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="32116-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span><span class="sxs-lookup"><span data-stu-id="32116-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="32116-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span><span class="sxs-lookup"><span data-stu-id="32116-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="32116-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span><span class="sxs-lookup"><span data-stu-id="32116-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="32116-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span><span class="sxs-lookup"><span data-stu-id="32116-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="32116-110">Adding endpoints to a Web service</span><span class="sxs-lookup"><span data-stu-id="32116-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="32116-111">There are two ways to add an endpoint to a Web service.</span><span class="sxs-lookup"><span data-stu-id="32116-111">There are two ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="32116-112">Programmatically</span><span class="sxs-lookup"><span data-stu-id="32116-112">Programmatically</span></span>
* <span data-ttu-id="32116-113">Through the Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="32116-113">Through the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="32116-114">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span><span class="sxs-lookup"><span data-stu-id="32116-114">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="32116-115">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span><span class="sxs-lookup"><span data-stu-id="32116-115">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="32116-116">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span><span class="sxs-lookup"><span data-stu-id="32116-116">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="32116-117">Adding an endpoint programmatically</span><span class="sxs-lookup"><span data-stu-id="32116-117">Adding an endpoint programmatically</span></span>
<span data-ttu-id="32116-118">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span><span class="sxs-lookup"><span data-stu-id="32116-118">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="32116-119">Adding an endpoint using the Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="32116-119">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="32116-120">In Machine Learning Studio, on the left navigation column, click Web Services.</span><span class="sxs-lookup"><span data-stu-id="32116-120">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="32116-121">At the bottom of the Web service dashboard, click **Manage endpoints**.</span><span class="sxs-lookup"><span data-stu-id="32116-121">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="32116-122">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span><span class="sxs-lookup"><span data-stu-id="32116-122">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="32116-123">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="32116-123">Click **New**.</span></span>
4. <span data-ttu-id="32116-124">Type a name and description for the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="32116-124">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="32116-125">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span><span class="sxs-lookup"><span data-stu-id="32116-125">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="32116-126">Select the logging level and whether sample data is enabled.</span><span class="sxs-lookup"><span data-stu-id="32116-126">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="32116-127">For more information on logging, see [Enable logging for Machine Learning Web services](web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="32116-127">For more information on logging, see [Enable logging for Machine Learning Web services](web-services-logging.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32116-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="32116-128">Next steps</span></span>
<span data-ttu-id="32116-129">[How to consume an Azure Machine Learning Web service](consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="32116-129">[How to consume an Azure Machine Learning Web service](consume-web-services.md).</span></span>

