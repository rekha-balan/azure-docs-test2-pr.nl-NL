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
# <a name="creating-endpoints"></a>Creating Endpoints
> [!NOTE]
>  This topic describes techniques applicable to a **Classic** Machine Learning Web service.
> 
> 

When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created. In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.

To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service. Each endpoint in the Web service is independently addressed, throttled, and managed. Each endpoint is a unique URL and authorization key that you can distribute to your customers.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a>Adding endpoints to a Web service
There are three ways to add an endpoint to a Web service.

* Programmatically
* Through the Azure Machine Learning Web Services portal
* Though the Azure classic portal

Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets. In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.

> [!NOTE]
> If you have added additional endpoints to the Web service, you cannot delete the default endpoint.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Adding an endpoint programmatically
You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a>Adding an endpoint using the Azure Machine Learning Web Services portal
1. In Machine Learning Studio, on the left navigation column, click Web Services.
2. At the bottom of the Web service dashboard, click **Manage endpoints**. The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.
3. Click **New**.
4. Type a name and description for the new endpoint. Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers. Select the logging level and whether sample data is enabled. For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a>Adding an endpoint using the Azure classic portal
1. Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column. Click the workspace which contains the Web service in which you are interested.
   
    ![Navigate to workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-1.png)
2. Click **Web Services**.
   
    ![Navigate to Web services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-2.png)
3. Click the Web service you're interested in to see the list of available endpoints.
   
    ![Navigate to endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-3.png)
4. At the bottom of the page, click **Add Endpoint**. Type a name and description, ensure there are no other endpoints with the same name in this Web service. Leave the throttle level with its default value unless you have special requirements. To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).
   
    ![Create endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Next Steps
[How to consume a published Azure Machine Learning Web service](machine-learning-consume-web-services.md).





