---
title: Deployment stage of the Team Data Science Process lifecycle - Azure | Microsoft Docs
description: The goals, tasks, and deliverables for the deployment stage of your data-science projects
services: machine-learning
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
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: 9c54e93eca181331117f2f7faad3e7d07274412d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966561"
---
# <a name="deployment"></a>Deployment

This article outlines the goals, tasks, and deliverables associated with the deployment of the Team Data Science Process (TDSP). This process provides a recommended lifecycle that you can use to structure your data-science projects. The lifecycle outlines the major stages that projects typically execute, often iteratively:

   1. **Business understanding**
   2. **Data acquisition and understanding**
   3. **Modeling**
   4. **Deployment**
   5. **Customer acceptance**

Here is a visual representation of the TDSP lifecycle: 

![TDSP lifecycle](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goal"></a>Goal
Deploy models with a data pipeline to a production or production-like environment for final user acceptance. 

## <a name="how-to-do-it"></a>How to do it
The main task addressed in this stage:

**Operationalize the model**: Deploy the model and pipeline to a production or production-like environment for application consumption.

### <a name="operationalize-a-model"></a>Operationalize a model
After you have a set of models that perform well, you can operationalize them for other applications to consume. Depending on the business requirements, predictions are made either in real time or on a batch basis. To deploy models, you expose them with an open API interface. The interface enables the model to be easily consumed from various applications, such as:

   * Online websites
   * Spreadsheets 
   * Dashboards
   * Line-of-business applications 
   * Back-end applications 

For examples of model operationalization with an Azure Machine Learning web service, see [Deploy an Azure Machine Learning web service](../studio/publish-a-machine-learning-web-service.md). It is a best practice to build telemetry and monitoring into the production model and the data pipeline that you deploy. This practice helps with subsequent system status reporting and troubleshooting.  

## <a name="artifacts"></a>Artifacts

* A status dashboard that displays the system health and key metrics
* A final modeling report with deployment details
* A final solution architecture document


## <a name="next-steps"></a>Next steps

Here are links to each step in the lifecycle of the TDSP:

   1. [Business understanding](lifecycle-business-understanding.md)
   2. [Data Acquisition and understanding](lifecycle-data.md)
   3. [Modeling](lifecycle-modeling.md)
   4. [Deployment](lifecycle-deployment.md)
   5. [Customer acceptance](lifecycle-acceptance.md)

We provide full end-to-end walkthroughs that demonstrate all the steps in the process for specific scenarios. The [Example walkthroughs](walkthroughs.md) article provides a list of the scenarios with links and thumbnail descriptions. The walkthroughs illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application. 

For examples of how to execute steps in TDSPs that use Azure Machine Learning Studio, see [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess).
