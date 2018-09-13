---
title: Consume a Machine Learning Web Service from Excel | Microsoft Docs
description: Consume an Azure Machine Learning Web Service from Excel
services: machine-learning
documentationcenter: ''
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: d34ed2f2a839dad184fe814500cdc93dad0edeba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661927"
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="e3380-103">Consuming an Azure Machine Learning Web Service from Excel</span><span class="sxs-lookup"><span data-stu-id="e3380-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="e3380-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span><span class="sxs-lookup"><span data-stu-id="e3380-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="e3380-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e3380-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="e3380-106">Steps</span><span class="sxs-lookup"><span data-stu-id="e3380-106">Steps</span></span>
<span data-ttu-id="e3380-107">Publish a web service.</span><span class="sxs-lookup"><span data-stu-id="e3380-107">Publish a web service.</span></span> <span data-ttu-id="e3380-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span><span class="sxs-lookup"><span data-stu-id="e3380-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="e3380-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span><span class="sxs-lookup"><span data-stu-id="e3380-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="e3380-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span><span class="sxs-lookup"><span data-stu-id="e3380-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="e3380-111">**Classic Web Service**</span><span class="sxs-lookup"><span data-stu-id="e3380-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="e3380-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span><span class="sxs-lookup"><span data-stu-id="e3380-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="e3380-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span><span class="sxs-lookup"><span data-stu-id="e3380-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="e3380-114">Click on **Download Excel Workbook**.</span><span class="sxs-lookup"><span data-stu-id="e3380-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="e3380-115">**New Web Service**</span><span class="sxs-lookup"><span data-stu-id="e3380-115">**New Web Service**</span></span>

1. <span data-ttu-id="e3380-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span><span class="sxs-lookup"><span data-stu-id="e3380-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="e3380-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span><span class="sxs-lookup"><span data-stu-id="e3380-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="e3380-118">**Using the workbook**</span><span class="sxs-lookup"><span data-stu-id="e3380-118">**Using the workbook**</span></span>

1. <span data-ttu-id="e3380-119">Open the workbook.</span><span class="sxs-lookup"><span data-stu-id="e3380-119">Open the workbook.</span></span>
2. <span data-ttu-id="e3380-120">A Security Warning appears; click on the **Enable Editing** button.</span><span class="sxs-lookup"><span data-stu-id="e3380-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="e3380-121">A Security Warning appears.</span><span class="sxs-lookup"><span data-stu-id="e3380-121">A Security Warning appears.</span></span> <span data-ttu-id="e3380-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="e3380-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="e3380-123">Once macros are enabled, a table is generated.</span><span class="sxs-lookup"><span data-stu-id="e3380-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="e3380-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span><span class="sxs-lookup"><span data-stu-id="e3380-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="e3380-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span><span class="sxs-lookup"><span data-stu-id="e3380-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="e3380-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span><span class="sxs-lookup"><span data-stu-id="e3380-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="e3380-127">To score more than one row, fill the second row with data and the predicted values are produced.</span><span class="sxs-lookup"><span data-stu-id="e3380-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="e3380-128">You can even paste several rows at once.</span><span class="sxs-lookup"><span data-stu-id="e3380-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="e3380-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span><span class="sxs-lookup"><span data-stu-id="e3380-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="e3380-130">Sharing your workbook</span><span class="sxs-lookup"><span data-stu-id="e3380-130">Sharing your workbook</span></span>
<span data-ttu-id="e3380-131">For the macros to work, your API Key must be part of the spreadsheet.</span><span class="sxs-lookup"><span data-stu-id="e3380-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="e3380-132">That means that you should share the workbook only with entities/individuals you trust.</span><span class="sxs-lookup"><span data-stu-id="e3380-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="e3380-133">Automatic updates</span><span class="sxs-lookup"><span data-stu-id="e3380-133">Automatic updates</span></span>
<span data-ttu-id="e3380-134">An RRS call is made in these two situations:</span><span class="sxs-lookup"><span data-stu-id="e3380-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="e3380-135">The first time a row has content in all of its **PARAMETERS**</span><span class="sxs-lookup"><span data-stu-id="e3380-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="e3380-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span><span class="sxs-lookup"><span data-stu-id="e3380-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consuming-from-excel/excellink.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consuming-from-excel/enableeditting.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consuming-from-excel/enablecontent.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-consuming-from-excel/sampletable.png




