---
title: How to increase concurrency of an Azure Machine Learning web service | Microsoft Docs
description: Learn how to increase concurrency of an Azure Machine Learning web service by adding additional endpoints.
services: machine-learning
documentationcenter: ''
author: neerajkh
manager: srikants
editor: cgronlun
keywords: azure machine learning, web services, operationalization, scaling, endpoint, concurrency
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: c1570d9343b31d0e4b1cf4a4f3d8162d4db42d0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563783"
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="79ea4-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span><span class="sxs-lookup"><span data-stu-id="79ea4-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="79ea4-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span><span class="sxs-lookup"><span data-stu-id="79ea4-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="79ea4-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="79ea4-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="79ea4-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span><span class="sxs-lookup"><span data-stu-id="79ea4-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="79ea4-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span><span class="sxs-lookup"><span data-stu-id="79ea4-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="79ea4-109">You can then randomly distribute your load across all of them.</span><span class="sxs-lookup"><span data-stu-id="79ea4-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="79ea4-110">The scaling of a Web service is a common task.</span><span class="sxs-lookup"><span data-stu-id="79ea4-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="79ea4-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span><span class="sxs-lookup"><span data-stu-id="79ea4-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="79ea4-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="79ea4-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="79ea4-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="79ea4-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="79ea4-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span><span class="sxs-lookup"><span data-stu-id="79ea4-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="79ea4-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span><span class="sxs-lookup"><span data-stu-id="79ea4-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="79ea4-116">The synchronous APIs are typically used in situations where a low latency is desired.</span><span class="sxs-lookup"><span data-stu-id="79ea4-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="79ea4-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span><span class="sxs-lookup"><span data-stu-id="79ea4-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="79ea4-118">Let's say you have an API with a 50-ms latency.</span><span class="sxs-lookup"><span data-stu-id="79ea4-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="79ea4-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 \* 1000 / 50 = 400 times per second.</span><span class="sxs-lookup"><span data-stu-id="79ea4-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 \* 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="79ea4-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span><span class="sxs-lookup"><span data-stu-id="79ea4-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-scaling-webservice/machlearn-1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-scaling-webservice/machlearn-2.png


