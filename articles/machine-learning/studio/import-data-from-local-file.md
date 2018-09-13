---
title: Import data from a file into Azure Machine Learning Studio | Microsoft Docs
description: Learn how to upload a training data file from your hard drive to Azure Machine Learning Studio. This creates a dataset module in the workspace.
keywords: import data,data format,data types,data sources,training data
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.openlocfilehash: 0365492b2814d686dd0bfa099e94717137b51725
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965501"
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="56dce-105">Import training data from a file on your hard drive into Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="56dce-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="56dce-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="56dce-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="56dce-107">By importing the data file, you have a dataset module ready for use in your workspace.</span><span class="sxs-lookup"><span data-stu-id="56dce-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="56dce-108">Steps to import data from a local file</span><span class="sxs-lookup"><span data-stu-id="56dce-108">Steps to import data from a local file</span></span>
<span data-ttu-id="56dce-109">To import data from a local hard drive, do the following:</span><span class="sxs-lookup"><span data-stu-id="56dce-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="56dce-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span><span class="sxs-lookup"><span data-stu-id="56dce-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="56dce-111">Select **DATASET** and **FROM LOCAL FILE**.</span><span class="sxs-lookup"><span data-stu-id="56dce-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="56dce-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span><span class="sxs-lookup"><span data-stu-id="56dce-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="56dce-113">Enter a name, identify the data type, and optionally enter a description.</span><span class="sxs-lookup"><span data-stu-id="56dce-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="56dce-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span><span class="sxs-lookup"><span data-stu-id="56dce-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="56dce-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span><span class="sxs-lookup"><span data-stu-id="56dce-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="56dce-116">Click this checkbox and then enter the name of an existing dataset.</span><span class="sxs-lookup"><span data-stu-id="56dce-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Upload a new dataset](./media/import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="56dce-118">During upload, you'll see a message that your file is being uploaded.</span><span class="sxs-lookup"><span data-stu-id="56dce-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="56dce-119">Upload time depends on the size of your data and the speed of your connection to the service.</span><span class="sxs-lookup"><span data-stu-id="56dce-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="56dce-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span><span class="sxs-lookup"><span data-stu-id="56dce-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="56dce-121">However, closing the browser causes the data upload to fail.</span><span class="sxs-lookup"><span data-stu-id="56dce-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="56dce-122">Dataset module is ready for use</span><span class="sxs-lookup"><span data-stu-id="56dce-122">Dataset module is ready for use</span></span>
<span data-ttu-id="56dce-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span><span class="sxs-lookup"><span data-stu-id="56dce-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="56dce-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span><span class="sxs-lookup"><span data-stu-id="56dce-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="56dce-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span><span class="sxs-lookup"><span data-stu-id="56dce-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
