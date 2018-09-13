---
title: Visualize and troubleshoot Stream Analytics jobs | Microsoft Docs
description: Learn how to visualize a Stream Analytics job pipeline for self-service troubleshooting using the diagnostics diagram feature.
keywords: ''
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 1b18f3d971a222e8efe4d1536f611cbe9bb84676
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554764"
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="c9b5f-103">Visualize and troubleshoot Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="c9b5f-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="c9b5f-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span><span class="sxs-lookup"><span data-stu-id="c9b5f-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="c9b5f-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="c9b5f-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="c9b5f-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="c9b5f-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="c9b5f-109">Using the diagnosis diagram tool</span><span class="sxs-lookup"><span data-stu-id="c9b5f-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="c9b5f-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="c9b5f-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="c9b5f-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="c9b5f-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="c9b5f-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9b5f-117">Next steps</span></span>
* [<span data-ttu-id="c9b5f-118">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b5f-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c9b5f-119">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b5f-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="c9b5f-120">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="c9b5f-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c9b5f-121">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="c9b5f-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c9b5f-122">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="c9b5f-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)




