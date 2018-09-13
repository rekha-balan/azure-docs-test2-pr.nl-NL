---
title: Example additional source data connections possible with Azure Machine Learning data preparation  | Microsoft Docs
description: This document provides a set of examples of source data connections that are possible with Azure Machine Learning data preparation
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 89a30c070abe3b10414c7284bb33f2c8216ee0c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857328"
---
# <a name="sample-of-custom-source-connections-python"></a><span data-ttu-id="48b1c-103">Sample of custom source connections (Python)</span><span class="sxs-lookup"><span data-stu-id="48b1c-103">Sample of custom source connections (Python)</span></span> 
<span data-ttu-id="48b1c-104">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48b1c-104">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span></span>

## <a name="load-data-from-dataworld"></a><span data-ttu-id="48b1c-105">Load data from data.world</span><span class="sxs-lookup"><span data-stu-id="48b1c-105">Load data from data.world</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48b1c-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48b1c-106">Prerequisites</span></span>

#### <a name="register-yourself-at-dataworld"></a><span data-ttu-id="48b1c-107">Register yourself at data.world</span><span class="sxs-lookup"><span data-stu-id="48b1c-107">Register yourself at data.world</span></span>
<span data-ttu-id="48b1c-108">You need an API token from the data.world website.</span><span class="sxs-lookup"><span data-stu-id="48b1c-108">You need an API token from the data.world website.</span></span>

#### <a name="install-dataworld-library"></a><span data-ttu-id="48b1c-109">Install data.world library</span><span class="sxs-lookup"><span data-stu-id="48b1c-109">Install data.world library</span></span>

<span data-ttu-id="48b1c-110">Open the Azure Machine Learning Workbench command-line interface by selecting **File** > **Open command-line interface**.</span><span class="sxs-lookup"><span data-stu-id="48b1c-110">Open the Azure Machine Learning Workbench command-line interface by selecting **File** > **Open command-line interface**.</span></span>

```console
pip install git+git://github.com/datadotworld/data.world-py.git
```

<span data-ttu-id="48b1c-111">Next, run `dw configure` on the command line, which prompts you for your token.</span><span class="sxs-lookup"><span data-stu-id="48b1c-111">Next, run `dw configure` on the command line, which prompts you for your token.</span></span> <span data-ttu-id="48b1c-112">When you enter your token, a .dw/ directory is created in your home directory and your token is stored there.</span><span class="sxs-lookup"><span data-stu-id="48b1c-112">When you enter your token, a .dw/ directory is created in your home directory and your token is stored there.</span></span>

```
API token (obtained at: https://data.world/settings/advanced): <enter API token here>
```
<span data-ttu-id="48b1c-113">Now you should be able to import data.world libraries.</span><span class="sxs-lookup"><span data-stu-id="48b1c-113">Now you should be able to import data.world libraries.</span></span>

#### <a name="load-data-into-data-preparation"></a><span data-ttu-id="48b1c-114">Load data into data preparation</span><span class="sxs-lookup"><span data-stu-id="48b1c-114">Load data into data preparation</span></span>

<span data-ttu-id="48b1c-115">Create a Transform Data Flow (Script) transform.</span><span class="sxs-lookup"><span data-stu-id="48b1c-115">Create a Transform Data Flow (Script) transform.</span></span> <span data-ttu-id="48b1c-116">Then use the following script to load the data from data.world.</span><span class="sxs-lookup"><span data-stu-id="48b1c-116">Then use the following script to load the data from data.world.</span></span>

```python
#paths = df['Path'].tolist()

import datadotworld as dw

#Load the dataset.
lds = dw.load_dataset('data-society/the-simpsons-by-the-data')

#Load specific data frame from the dataset.
df = lds.dataframes['simpsons_episodes']

```
## <a name="azure-cosmos-db-as-a-data-source-connection"></a><span data-ttu-id="48b1c-117">Azure Cosmos DB as a data source connection</span><span class="sxs-lookup"><span data-stu-id="48b1c-117">Azure Cosmos DB as a data source connection</span></span>
<span data-ttu-id="48b1c-118">For an example of Azure Cosmos DB as a data connection, read [Load Azure Cosmos DB as a source data connection](data-prep-load-azure-cosmos-db.md)</span><span class="sxs-lookup"><span data-stu-id="48b1c-118">For an example of Azure Cosmos DB as a data connection, read [Load Azure Cosmos DB as a source data connection](data-prep-load-azure-cosmos-db.md)</span></span>
