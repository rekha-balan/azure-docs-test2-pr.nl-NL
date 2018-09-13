---
title: Sample data in Azure blob containers, SQL Server, and Hive tables | Microsoft Docs
description: How to explore data stored in various Azure enviromnents.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: 0efd754936b67611a747c6c5756de92443a937e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865876"
---
# <a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables
This document links to articles that cover how to sample data that is stored in one of three different Azure locations:

* **Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.
* **SQL Server data** is sampled using both SQL and the Python Programming Language. 
* **Hive table data** is sampled using Hive queries.

The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments. 

[!INCLUDE [cap-sample-data-selector](../../../includes/cap-sample-data-selector.md)]

This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

**Why sample data?**

If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size. This facilitates data understanding, exploration, and feature engineering. Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.

