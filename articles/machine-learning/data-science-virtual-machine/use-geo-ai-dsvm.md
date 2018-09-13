---
title: Using the Geo Artificial Intelligence Data Science Virtual Machine  - Azure | Microsoft Docs
description: How to use a Geo AI Virtual Machine on Azure.
keywords: deep learning, AI, data science tools, data science virtual machine, Geospatial analytics
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/05/2018
ms.author: gokuma
ms.openlocfilehash: f346b086a0269f247d64edf9346b01849ba3d0ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869795"
---
# <a name="using-the-geo-artificial-intelligence-data-science-virtual-machine"></a><span data-ttu-id="7db34-104">Using the Geo Artificial Intelligence Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="7db34-104">Using the Geo Artificial Intelligence Data Science Virtual Machine</span></span>

<span data-ttu-id="7db34-105">Use the Geo AI Data Science VM to fetch data for analysis, perform data wrangling, and build models for AI applications that consume geospatial information.</span><span class="sxs-lookup"><span data-stu-id="7db34-105">Use the Geo AI Data Science VM to fetch data for analysis, perform data wrangling, and build models for AI applications that consume geospatial information.</span></span> <span data-ttu-id="7db34-106">Once you have provisioned your Geo AI Data Science VM and signed into ArcGIS Pro with your ArcGIS account, you can start interacting with ArcGIS desktop and ArcGis online.</span><span class="sxs-lookup"><span data-stu-id="7db34-106">Once you have provisioned your Geo AI Data Science VM and signed into ArcGIS Pro with your ArcGIS account, you can start interacting with ArcGIS desktop and ArcGis online.</span></span> <span data-ttu-id="7db34-107">You can also access ArcGIS from Python interfaces and an R language bridge pre-configured on the Geo-Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="7db34-107">You can also access ArcGIS from Python interfaces and an R language bridge pre-configured on the Geo-Data Science VM.</span></span> <span data-ttu-id="7db34-108">To build rich AI applications, combine it with the machine learning and deep learning frameworks and other data science software available on the Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="7db34-108">To build rich AI applications, combine it with the machine learning and deep learning frameworks and other data science software available on the Data Science VM.</span></span>  


## <a name="configuration-details"></a><span data-ttu-id="7db34-109">Configuration details</span><span class="sxs-lookup"><span data-stu-id="7db34-109">Configuration details</span></span>

<span data-ttu-id="7db34-110">The Python library, [arcpy](http://pro.arcgis.com/en/pro-app/arcpy/main/arcgis-pro-arcpy-reference.htm), which is used to interface with ArcGIS is installed in the global root conda environment of the Data Science VM that is found at ```c:\anaconda```.</span><span class="sxs-lookup"><span data-stu-id="7db34-110">The Python library, [arcpy](http://pro.arcgis.com/en/pro-app/arcpy/main/arcgis-pro-arcpy-reference.htm), which is used to interface with ArcGIS is installed in the global root conda environment of the Data Science VM that is found at ```c:\anaconda```.</span></span> 

- <span data-ttu-id="7db34-111">If you are running Python in a command prompt, run ```activate``` to activate into the conda root Python environment.</span><span class="sxs-lookup"><span data-stu-id="7db34-111">If you are running Python in a command prompt, run ```activate``` to activate into the conda root Python environment.</span></span> 
- <span data-ttu-id="7db34-112">If you are using an IDE or Jupyter notebook, you can select the environment or kernel to ensure you are in the correct conda environment.</span><span class="sxs-lookup"><span data-stu-id="7db34-112">If you are using an IDE or Jupyter notebook, you can select the environment or kernel to ensure you are in the correct conda environment.</span></span> 

<span data-ttu-id="7db34-113">The R-bridge to ArcGIS is installed as an R library named [arcgisbinding](https://github.com/R-ArcGIS/r-bridge) in the main Microsoft R server standalone instance located at ```C:\Program Files\Microsoft\ML Server\R_SERVER```.</span><span class="sxs-lookup"><span data-stu-id="7db34-113">The R-bridge to ArcGIS is installed as an R library named [arcgisbinding](https://github.com/R-ArcGIS/r-bridge) in the main Microsoft R server standalone instance located at ```C:\Program Files\Microsoft\ML Server\R_SERVER```.</span></span> <span data-ttu-id="7db34-114">Visual Studio, RStudio, and Jupyter are already pre-configured to use this R environment and will have access to the ```arcgisbinding``` R library.</span><span class="sxs-lookup"><span data-stu-id="7db34-114">Visual Studio, RStudio, and Jupyter are already pre-configured to use this R environment and will have access to the ```arcgisbinding``` R library.</span></span> 


## <a name="geo-ai-data-science-vm-samples"></a><span data-ttu-id="7db34-115">Geo AI Data Science VM samples</span><span class="sxs-lookup"><span data-stu-id="7db34-115">Geo AI Data Science VM samples</span></span>

<span data-ttu-id="7db34-116">In addition to the ML and deep learning framework-based samples from the base Data Science VM, a set of geospatial samples is also provided as part of the Geo AI Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="7db34-116">In addition to the ML and deep learning framework-based samples from the base Data Science VM, a set of geospatial samples is also provided as part of the Geo AI Data Science VM.</span></span> <span data-ttu-id="7db34-117">These samples can help you jump-start your development of AI applications using Geospatial data and the ArcGIS software.</span><span class="sxs-lookup"><span data-stu-id="7db34-117">These samples can help you jump-start your development of AI applications using Geospatial data and the ArcGIS software.</span></span> 


1. <span data-ttu-id="7db34-118">[Getting stated with Geospatial analytics with Python](https://github.com/Azure/DataScienceVM/blob/master/Notebooks/ArcGIS/Python%20walkthrough%20ArcGIS%20Data%20analysis%20and%20ML.ipynb): An introductory sample showing how to work with Geospatial data using the Python interface to ArcGIS provided by the [arcpy](http://pro.arcgis.com/en/pro-app/arcpy/main/arcgis-pro-arcpy-reference.htm) library.</span><span class="sxs-lookup"><span data-stu-id="7db34-118">[Getting stated with Geospatial analytics with Python](https://github.com/Azure/DataScienceVM/blob/master/Notebooks/ArcGIS/Python%20walkthrough%20ArcGIS%20Data%20analysis%20and%20ML.ipynb): An introductory sample showing how to work with Geospatial data using the Python interface to ArcGIS provided by the [arcpy](http://pro.arcgis.com/en/pro-app/arcpy/main/arcgis-pro-arcpy-reference.htm) library.</span></span> <span data-ttu-id="7db34-119">It also shows how you can combine traditional machine learning with geospatial data and visualize the result on a map in ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="7db34-119">It also shows how you can combine traditional machine learning with geospatial data and visualize the result on a map in ArcGIS.</span></span> 

2. <span data-ttu-id="7db34-120">[Getting stated with Geospatial analytics with R](https://github.com/Azure/DataScienceVM/blob/master/Notebooks/ArcGIS/R%20walkthrough%20ArcGIS%20Data%20analysis%20and%20ML.ipynb): An introductory sample that shows how to work with Geospatial data using the R interface to ArcGIS provided by the [arcgisbinding](https://github.com/R-ArcGIS/r-bridge) library.</span><span class="sxs-lookup"><span data-stu-id="7db34-120">[Getting stated with Geospatial analytics with R](https://github.com/Azure/DataScienceVM/blob/master/Notebooks/ArcGIS/R%20walkthrough%20ArcGIS%20Data%20analysis%20and%20ML.ipynb): An introductory sample that shows how to work with Geospatial data using the R interface to ArcGIS provided by the [arcgisbinding](https://github.com/R-ArcGIS/r-bridge) library.</span></span> 

3. <span data-ttu-id="7db34-121">[Pixel-level land use classification](https://github.com/Azure/pixel_level_land_classification): A tutorial that illustrates how to create a deep neural network model that accepts an aerial image as input and returns a land-cover label.</span><span class="sxs-lookup"><span data-stu-id="7db34-121">[Pixel-level land use classification](https://github.com/Azure/pixel_level_land_classification): A tutorial that illustrates how to create a deep neural network model that accepts an aerial image as input and returns a land-cover label.</span></span> <span data-ttu-id="7db34-122">Examples of land-cover labels are "forested" or "water."</span><span class="sxs-lookup"><span data-stu-id="7db34-122">Examples of land-cover labels are "forested" or "water."</span></span> <span data-ttu-id="7db34-123">The model returns such a label for every pixel in the image.</span><span class="sxs-lookup"><span data-stu-id="7db34-123">The model returns such a label for every pixel in the image.</span></span> <span data-ttu-id="7db34-124">The model is built using Microsoft's open-source [Cognitive Toolkit (CNTK)](https://www.microsoft.com/en-us/cognitive-toolkit/) deep learning framework.</span><span class="sxs-lookup"><span data-stu-id="7db34-124">The model is built using Microsoft's open-source [Cognitive Toolkit (CNTK)](https://www.microsoft.com/en-us/cognitive-toolkit/) deep learning framework.</span></span> <span data-ttu-id="7db34-125">The example also shows how to scale out the training on [Azure Batch AI](https://docs.microsoft.com/azure/batch-ai/) and consume the model predictions in ArcGIS Pro software.</span><span class="sxs-lookup"><span data-stu-id="7db34-125">The example also shows how to scale out the training on [Azure Batch AI](https://docs.microsoft.com/azure/batch-ai/) and consume the model predictions in ArcGIS Pro software.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="7db34-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="7db34-126">Next steps</span></span>

<span data-ttu-id="7db34-127">Additional samples that use the Data Science VM are available here:</span><span class="sxs-lookup"><span data-stu-id="7db34-127">Additional samples that use the Data Science VM are available here:</span></span>

* [<span data-ttu-id="7db34-128">Samples</span><span class="sxs-lookup"><span data-stu-id="7db34-128">Samples</span></span>](dsvm-samples-and-walkthroughs.md)

