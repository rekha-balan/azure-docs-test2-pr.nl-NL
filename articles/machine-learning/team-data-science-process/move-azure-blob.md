---
title: Move Data to and from Azure Blob Storage | Microsoft Docs
description: Move Data to and from Azure Blob Storage
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: 854c671d4db6cdca2b019ed9adb0475e588281b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869393"
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="a98d8-103">Move data to and from Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a98d8-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="a98d8-104">Which method is best for you depends on your scenario.</span><span class="sxs-lookup"><span data-stu-id="a98d8-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="a98d8-105">The [Scenarios for advanced analytics in Azure Machine Learning](plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span><span class="sxs-lookup"><span data-stu-id="a98d8-105">The [Scenarios for advanced analytics in Azure Machine Learning](plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="a98d8-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="a98d8-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="a98d8-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span><span class="sxs-lookup"><span data-stu-id="a98d8-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="a98d8-108">create and schedule a pipeline that downloads data from Azure blob storage,</span><span class="sxs-lookup"><span data-stu-id="a98d8-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="a98d8-109">pass it to a published Azure Machine Learning web service,</span><span class="sxs-lookup"><span data-stu-id="a98d8-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="a98d8-110">receive the predictive analytics results, and</span><span class="sxs-lookup"><span data-stu-id="a98d8-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="a98d8-111">upload the results to storage.</span><span class="sxs-lookup"><span data-stu-id="a98d8-111">upload the results to storage.</span></span> 

<span data-ttu-id="a98d8-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../../data-factory/transform-data-using-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="a98d8-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../../data-factory/transform-data-using-machine-learning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98d8-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a98d8-113">Prerequisites</span></span>
<span data-ttu-id="a98d8-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span><span class="sxs-lookup"><span data-stu-id="a98d8-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="a98d8-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="a98d8-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="a98d8-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a98d8-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a98d8-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a98d8-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

