---
title: Azure Government Intelligence + Analytics | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: MeganYount
manager: zakramer
ms.assetid: 4b7720c1-699e-432b-9246-6e49fb77f497
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 12/06/2016
ms.author: MeganYount
ms.openlocfilehash: 0233aa66bc4f4f135456ec15bd09756e63192b14
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553611"
---
# <a name="azure-government-intelligence--analytics"></a>Azure Government Intelligence + Analytics
This article outlines the intelligence and analytics services, variations, and considerations for the Azure Government environment.

## <a name="hdinsight"></a>HDInsight
HDInsight on Linux Standard is generally available in Azure Government. You can see a demo on how to build data-centric solutions on Azure Government using HDInsight <a href=https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/>here</a>.

HDInsight on Linux Premium is coming soon.

### <a name="variations"></a>Variations
The following HDInsight features are not currently available in Azure Government.

* HDInsight is not available on Windows.
* Azure Data Lake Store is not currently available in Azure Government. Azure Blob Storage is the only available storage option currently.

The URLs for Log Analytics are different in Azure Government:

| Service Type | Azure Public | Azure Government |
| --- | --- | --- |
| HDInsight Cluster | \*.azurehdinsight.net | \*.azurehdinsight.us |

For more information, see [HDInsight public documentation](../hdinsight/hdinsight-hadoop-introduction.md).

## <a name="power-bi"></a>Power BI
Power BI US Government is generally available as part of the Office 365 US Government Community subscriptions. You can learn about Power BI US Government <a href=https://powerbi.microsoft.com/en-us/documentation/powerbi-service-govus-overview/>here</a>. You can see a demo on how to build data-centric solutions on Azure Government using Power BI <a href=https://channel9.msdn.com/Blogs/Azure/Cognitive-Services-HDInsight-and-Power-BI-on-Azure-Government/>here</a>.

Power BI Embedded is coming soon.

### <a name="variations"></a>Variations

The URLs for Power BI are different in US Government:

| Service Type | Power BI Commercial | Power BI US Government |
| --- | --- | --- |
| Power BI URL | app.powerbi.com | app.powerbigov.us |

## <a name="next-steps"></a>Next Steps
For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a>
