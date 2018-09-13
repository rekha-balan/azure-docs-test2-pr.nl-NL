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
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a>Import your data into Azure Machine Learning Studio from another experiment
[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment. To do this, you save the module as a dataset:

1. Click the output of the module that you want to save as a dataset.
2. Click **Save as Dataset**.
3. When prompted, enter a name and a description that would allow you to identify the dataset easily.
4. Click the **OK** checkmark.

When the save finishes, the dataset will be available for use within any experiment in your workspace. You can find it in the **Saved Datasets** list in the module palette.

