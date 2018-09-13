---
title: Sample data in Azure blob containers, SQL Server, and Hive tables | Microsoft Docs
description: How to explore data stored in various Azure enviromnents.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670615"
---
# <a name="heading"></a><span data-ttu-id="22cc9-103">Sample data in Azure blob containers, SQL Server, and Hive tables</span><span class="sxs-lookup"><span data-stu-id="22cc9-103">Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="22cc9-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span><span class="sxs-lookup"><span data-stu-id="22cc9-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="22cc9-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span><span class="sxs-lookup"><span data-stu-id="22cc9-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="22cc9-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span><span class="sxs-lookup"><span data-stu-id="22cc9-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="22cc9-107">**Hive table data** is sampled using Hive queries.</span><span class="sxs-lookup"><span data-stu-id="22cc9-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="22cc9-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span><span class="sxs-lookup"><span data-stu-id="22cc9-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="22cc9-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="22cc9-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="22cc9-110">**Why sample data?**</span><span class="sxs-lookup"><span data-stu-id="22cc9-110">**Why sample data?**</span></span>

<span data-ttu-id="22cc9-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span><span class="sxs-lookup"><span data-stu-id="22cc9-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="22cc9-112">This facilitates data understanding, exploration, and feature engineering.</span><span class="sxs-lookup"><span data-stu-id="22cc9-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="22cc9-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="22cc9-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

