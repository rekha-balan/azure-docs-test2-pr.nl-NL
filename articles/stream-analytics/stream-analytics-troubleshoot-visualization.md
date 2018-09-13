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
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Visualize and troubleshoot Stream Analytics jobs
In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter). With this in mind, Stream Analytics provides the capability for visualizing a streaming job. This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.

In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured. Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.

## <a name="using-the-diagnosis-diagram-tool"></a>Using the diagnosis diagram tool
To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Every input and output is color coded to indicate the current state of that component, as shown below.

![stream-analytics-troubleshoot-visualization-input-map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence. Clicking on each query step will show the corresponding section in a query editing pane as illustrated. 

![stream-analytics-troubleshoot-visualization-intermediate-steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Next steps
* [Introduction to Azure Stream Analytics](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics](stream-analytics-get-started.md)
* [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)




