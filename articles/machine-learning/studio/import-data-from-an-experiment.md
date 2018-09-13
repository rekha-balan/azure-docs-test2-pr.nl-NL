---
title: Import data into Machine Learning Studio from another experiment | Microsoft Docs
description: How to save training data in Azure Machine Learning Studio and use it in another experiment.
keywords: import data,data,data sources,training data
services: machine-learning
documentationcenter: ''
author: deguhath
ms.author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.openlocfilehash: 5007657da11cb45c6511780398c5425d14dca900
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865253"
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="25aae-104">Import your data into Azure Machine Learning Studio from another experiment</span><span class="sxs-lookup"><span data-stu-id="25aae-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="25aae-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span><span class="sxs-lookup"><span data-stu-id="25aae-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="25aae-106">To do this, you save the module as a dataset:</span><span class="sxs-lookup"><span data-stu-id="25aae-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="25aae-107">Click the output of the module that you want to save as a dataset.</span><span class="sxs-lookup"><span data-stu-id="25aae-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="25aae-108">Click **Save as Dataset**.</span><span class="sxs-lookup"><span data-stu-id="25aae-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="25aae-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span><span class="sxs-lookup"><span data-stu-id="25aae-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="25aae-110">Click the **OK** checkmark.</span><span class="sxs-lookup"><span data-stu-id="25aae-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="25aae-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span><span class="sxs-lookup"><span data-stu-id="25aae-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="25aae-112">You can find it in the **Saved Datasets** list in the module palette.</span><span class="sxs-lookup"><span data-stu-id="25aae-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

