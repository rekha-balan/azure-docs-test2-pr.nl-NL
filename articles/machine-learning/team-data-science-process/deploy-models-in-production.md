---
title: Deploy models in production - Azure Machine Learning | Microsoft Docs
description: How to deploy models to production enabling them to play an active role in making business decisions.
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/30/2017
ms.author: deguhath
ms.openlocfilehash: 0505d58261ec32015f8847b710791249f87f049b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966328"
---
# <a name="deploy-models-in-production"></a>Deploy models in production

Production deployment enables a model to play an active role in a business. Predictions from a deployed model can be used for business decisions.

## <a name="production-platforms"></a>Production platforms
There are various approaches and platforms to put models into production. Here are a few options:


- [Model deployment in Azure Machine Learning](../desktop-workbench/model-management-overview.md)
- [Deployment of a model in SQL-server](https://docs.microsoft.com/sql/advanced-analytics/tutorials/sqldev-py6-operationalize-the-model)
- [Microsoft Machine Learning Server](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone)


>[!NOTE]
>Prior to deployment, one has to insure the latency of model scoring is low enough to use in production.
>


>[!NOTE]
>For deployment using Azure Machine Learning Studio, see [Deploy an Azure Machine Learning web service](../studio/publish-a-machine-learning-web-service.md).
>

## <a name="ab-testing"></a>A/B testing
When multiple models are in production, it can be useful to perform [A/B testing](https://en.wikipedia.org/wiki/A/B_testing) to compare performance of the models. 

 
## <a name="next-steps"></a>Next steps

Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided. They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article. They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application. 
 


