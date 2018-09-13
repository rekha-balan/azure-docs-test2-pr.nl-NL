---
title: Import data into Machine Learning Studio from another experiment | Microsoft Docs
description: How to save training data in Azure Machine Learning Studio and use it in another experiment.
keywords: import data,data,data sources,training data
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671607"
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="a982e-104">Import your data into Azure Machine Learning Studio from another experiment</span><span class="sxs-lookup"><span data-stu-id="a982e-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="a982e-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span><span class="sxs-lookup"><span data-stu-id="a982e-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="a982e-106">To do this, you save the module as a dataset:</span><span class="sxs-lookup"><span data-stu-id="a982e-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="a982e-107">Click the output of the module that you want to save as a dataset.</span><span class="sxs-lookup"><span data-stu-id="a982e-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="a982e-108">Click **Save as Dataset**.</span><span class="sxs-lookup"><span data-stu-id="a982e-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="a982e-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span><span class="sxs-lookup"><span data-stu-id="a982e-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="a982e-110">Click the **OK** checkmark.</span><span class="sxs-lookup"><span data-stu-id="a982e-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="a982e-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span><span class="sxs-lookup"><span data-stu-id="a982e-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="a982e-112">You can find it in the **Saved Datasets** list in the module palette.</span><span class="sxs-lookup"><span data-stu-id="a982e-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

