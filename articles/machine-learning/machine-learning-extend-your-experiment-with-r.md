---
title: Extend your experiment with R | Microsoft Docs
description: How to extend the functionality of Azure Machine Learning Studio through the R language by using the Execute R Script module.
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: f4b3df9612136a135b8330c0f4e400c5528350ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555801"
---
# <a name="extend-your-experiment-with-r"></a>Extend your experiment with R
You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.

This module accepts multiple input datasets and yields a single dataset as output. You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.

You access each input port of the module by using code similar to the following:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Listing all currently-installed packages
The list of installed packages can change. A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).

You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.
To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**. 

![Download output of "Convert to CSV" module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importing packages
You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

where the `my_favorite_package.zip` file contains your package.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/

