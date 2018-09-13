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
# <a name="sample-of-custom-source-connections-python"></a>Sample of custom source connections (Python) 
Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).

## <a name="load-data-from-dataworld"></a>Load data from data.world

### <a name="prerequisites"></a>Prerequisites

#### <a name="register-yourself-at-dataworld"></a>Register yourself at data.world
You need an API token from the data.world website.

#### <a name="install-dataworld-library"></a>Install data.world library

Open the Azure Machine Learning Workbench command-line interface by selecting **File** > **Open command-line interface**.

```console
pip install git+git://github.com/datadotworld/data.world-py.git
```

Next, run `dw configure` on the command line, which prompts you for your token. When you enter your token, a .dw/ directory is created in your home directory and your token is stored there.

```
API token (obtained at: https://data.world/settings/advanced): <enter API token here>
```
Now you should be able to import data.world libraries.

#### <a name="load-data-into-data-preparation"></a>Load data into data preparation

Create a Transform Data Flow (Script) transform. Then use the following script to load the data from data.world.

```python
#paths = df['Path'].tolist()

import datadotworld as dw

#Load the dataset.
lds = dw.load_dataset('data-society/the-simpsons-by-the-data')

#Load specific data frame from the dataset.
df = lds.dataframes['simpsons_episodes']

```
## <a name="azure-cosmos-db-as-a-data-source-connection"></a>Azure Cosmos DB as a data source connection
For an example of Azure Cosmos DB as a data connection, read [Load Azure Cosmos DB as a source data connection](data-prep-load-azure-cosmos-db.md)
