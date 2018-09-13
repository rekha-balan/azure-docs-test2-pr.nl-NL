---
title: Extend your experiment with R | Microsoft Docs
description: How to extend the functionality of Azure Machine Learning Studio through the R language by using the Execute R Script module.
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.openlocfilehash: 1f05119d94611df2e75afc3a56d9682d1149326c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869711"
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="3d881-103">Extend your experiment with R</span><span class="sxs-lookup"><span data-stu-id="3d881-103">Extend your experiment with R</span></span>
<span data-ttu-id="3d881-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="3d881-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="3d881-105">This module accepts multiple input datasets and yields a single dataset as output.</span><span class="sxs-lookup"><span data-stu-id="3d881-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="3d881-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="3d881-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="3d881-107">You access each input port of the module by using code similar to the following:</span><span class="sxs-lookup"><span data-stu-id="3d881-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="3d881-108">Listing all currently-installed packages</span><span class="sxs-lookup"><span data-stu-id="3d881-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="3d881-109">The list of installed packages can change.</span><span class="sxs-lookup"><span data-stu-id="3d881-109">The list of installed packages can change.</span></span> <span data-ttu-id="3d881-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d881-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="3d881-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="3d881-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="3d881-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="3d881-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="3d881-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span><span class="sxs-lookup"><span data-stu-id="3d881-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

![Download output of "Convert to CSV" module](./media/extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="3d881-115">Importing packages</span><span class="sxs-lookup"><span data-stu-id="3d881-115">Importing packages</span></span>
<span data-ttu-id="3d881-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="3d881-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="3d881-117">where the `my_favorite_package.zip` file contains your package.</span><span class="sxs-lookup"><span data-stu-id="3d881-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
