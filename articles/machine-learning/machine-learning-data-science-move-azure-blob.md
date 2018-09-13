---
title: Move Data to and from Azure Blob Storage | Microsoft Docs
description: Move Data to and from Azure Blob Storage
services: machine-learning,storage
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: bd4b671f49f3b61399d8dfa813f3bff32b20acdb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554848"
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="72590-103">Move data to and from Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="72590-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="72590-104">Which method is best for you depends on your scenario.</span><span class="sxs-lookup"><span data-stu-id="72590-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="72590-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span><span class="sxs-lookup"><span data-stu-id="72590-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="72590-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="72590-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="72590-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span><span class="sxs-lookup"><span data-stu-id="72590-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="72590-108">create and schedule a pipeline that downloads data from Azure blob storage,</span><span class="sxs-lookup"><span data-stu-id="72590-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="72590-109">pass it to a published Azure Machine Learning web service,</span><span class="sxs-lookup"><span data-stu-id="72590-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="72590-110">receive the predictive analytics results, and</span><span class="sxs-lookup"><span data-stu-id="72590-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="72590-111">upload the results to storage.</span><span class="sxs-lookup"><span data-stu-id="72590-111">upload the results to storage.</span></span> 

<span data-ttu-id="72590-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="72590-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72590-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72590-113">Prerequisites</span></span>
<span data-ttu-id="72590-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span><span class="sxs-lookup"><span data-stu-id="72590-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="72590-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="72590-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="72590-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72590-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="72590-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="72590-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

