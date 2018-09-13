---
title: Consume a Machine Learning Web Service from Excel | Microsoft Docs
description: Consume an Azure Machine Learning Web Service from Excel
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/1/2018
ms.openlocfilehash: 14621e50a397bc1f1922a4c8fae638d6b42ab8ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866541"
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="cd4ac-103">Consuming an Azure Machine Learning Web Service from Excel</span><span class="sxs-lookup"><span data-stu-id="cd4ac-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="cd4ac-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="cd4ac-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="cd4ac-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="cd4ac-106">Steps</span><span class="sxs-lookup"><span data-stu-id="cd4ac-106">Steps</span></span>
<span data-ttu-id="cd4ac-107">Publish a web service.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-107">Publish a web service.</span></span> <span data-ttu-id="cd4ac-108">[This page](walkthrough-5-publish-web-service.md) explains how to do it.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-108">[This page](walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="cd4ac-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span><span class="sxs-lookup"><span data-stu-id="cd4ac-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="cd4ac-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="cd4ac-111">**Classic Web Service**</span><span class="sxs-lookup"><span data-stu-id="cd4ac-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="cd4ac-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="cd4ac-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="cd4ac-114">Click on **Download Excel Workbook**.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="cd4ac-115">**New Web Service**</span><span class="sxs-lookup"><span data-stu-id="cd4ac-115">**New Web Service**</span></span>

1. <span data-ttu-id="cd4ac-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="cd4ac-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="cd4ac-118">**Using the workbook**</span><span class="sxs-lookup"><span data-stu-id="cd4ac-118">**Using the workbook**</span></span>

1. <span data-ttu-id="cd4ac-119">Open the workbook.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-119">Open the workbook.</span></span>
2. <span data-ttu-id="cd4ac-120">A Security Warning appears; click on the **Enable Editing** button.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="cd4ac-121">A Security Warning appears.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-121">A Security Warning appears.</span></span> <span data-ttu-id="cd4ac-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="cd4ac-123">Once macros are enabled, a table is generated.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="cd4ac-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="cd4ac-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="cd4ac-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="cd4ac-127">To score more than one row, fill the second row with data and the predicted values are produced.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="cd4ac-128">You can even paste several rows at once.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="cd4ac-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="cd4ac-130">Sharing your workbook</span><span class="sxs-lookup"><span data-stu-id="cd4ac-130">Sharing your workbook</span></span>
<span data-ttu-id="cd4ac-131">For the macros to work, your API Key must be part of the spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="cd4ac-132">That means that you should share the workbook only with entities/individuals you trust.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="cd4ac-133">Automatic updates</span><span class="sxs-lookup"><span data-stu-id="cd4ac-133">Automatic updates</span></span>
<span data-ttu-id="cd4ac-134">An RRS call is made in these two situations:</span><span class="sxs-lookup"><span data-stu-id="cd4ac-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="cd4ac-135">The first time a row has content in all of its **PARAMETERS**</span><span class="sxs-lookup"><span data-stu-id="cd4ac-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="cd4ac-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span><span class="sxs-lookup"><span data-stu-id="cd4ac-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/consuming-from-excel/excellink.png
[2]: ./media/consuming-from-excel/enableeditting.png
[3]: ./media/consuming-from-excel/enablecontent.png
[4]: ./media/consuming-from-excel/sampletable.png
