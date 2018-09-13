---
title: Computer Vision API Python tutorial | Microsoft Docs
description: Learn how to use the Computer Vision API with Python by using Jupyter notebooks in Microsoft Cognitive Services. Visualize your results using popular libraries.
services: cognitive-services
author: KellyDF
manager: corncar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: article
ms.date: 02/25/2017
ms.author: kefre
ms.openlocfilehash: a093c2d066e70a8daf1fe1cd33ccf794ecb196af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784035"
---
# <a name="computer-vision-api-python-tutorial"></a><span data-ttu-id="0ab03-104">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="0ab03-104">Computer Vision API Python Tutorial</span></span>

<span data-ttu-id="0ab03-105">This tutorial shows you how to use the Computer Vision API in Python and how to visualize your results using some popular libraries.</span><span class="sxs-lookup"><span data-stu-id="0ab03-105">This tutorial shows you how to use the Computer Vision API in Python and how to visualize your results using some popular libraries.</span></span> <span data-ttu-id="0ab03-106">Use Jupyter to run the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ab03-106">Use Jupyter to run the tutorial.</span></span> <span data-ttu-id="0ab03-107">To learn how to get started with interactive Jupyter notebooks, refer to: [Jupyter Documementation](http://jupyter.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="0ab03-107">To learn how to get started with interactive Jupyter notebooks, refer to: [Jupyter Documementation](http://jupyter.readthedocs.io/en/latest/index.html).</span></span> 

### <a name="opening-the-tutorial-notebook-in-jupyter"></a><span data-ttu-id="0ab03-108">Opening the Tutorial Notebook in Jupyter</span><span class="sxs-lookup"><span data-stu-id="0ab03-108">Opening the Tutorial Notebook in Jupyter</span></span> 

1. <span data-ttu-id="0ab03-109">Navigate to the [tutorial notebook in GitHub](https://github.com/Microsoft/Cognitive-Vision-Python).</span><span class="sxs-lookup"><span data-stu-id="0ab03-109">Navigate to the [tutorial notebook in GitHub](https://github.com/Microsoft/Cognitive-Vision-Python).</span></span> 
2. <span data-ttu-id="0ab03-110">Click on the green button to clone or download the tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ab03-110">Click on the green button to clone or download the tutorial.</span></span> 
3. <span data-ttu-id="0ab03-111">Open a command prompt and go to the folder _Cognitive-Vision-Python-master\Jupyter Notebook_.</span><span class="sxs-lookup"><span data-stu-id="0ab03-111">Open a command prompt and go to the folder _Cognitive-Vision-Python-master\Jupyter Notebook_.</span></span> 
4. <span data-ttu-id="0ab03-112">Run the command **jupyter notebook** from the command prompt.</span><span class="sxs-lookup"><span data-stu-id="0ab03-112">Run the command **jupyter notebook** from the command prompt.</span></span> <span data-ttu-id="0ab03-113">This will start Jupyter.</span><span class="sxs-lookup"><span data-stu-id="0ab03-113">This will start Jupyter.</span></span>
5. <span data-ttu-id="0ab03-114">In the Jupyter window, click on _Computer Vision API Example.ipynb_ to open the tutorial notebook</span><span class="sxs-lookup"><span data-stu-id="0ab03-114">In the Jupyter window, click on _Computer Vision API Example.ipynb_ to open the tutorial notebook</span></span> 

### <a name="running-the-tutorial"></a><span data-ttu-id="0ab03-115">Running the Tutorial</span><span class="sxs-lookup"><span data-stu-id="0ab03-115">Running the Tutorial</span></span>

<span data-ttu-id="0ab03-116">To use this notebook, you will need a subscription key for the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="0ab03-116">To use this notebook, you will need a subscription key for the Computer Vision API.</span></span> <span data-ttu-id="0ab03-117">Visit the [Subscription page](https://azure.microsoft.com/try/cognitive-services/) to sign up.</span><span class="sxs-lookup"><span data-stu-id="0ab03-117">Visit the [Subscription page](https://azure.microsoft.com/try/cognitive-services/) to sign up.</span></span> <span data-ttu-id="0ab03-118">On the “Sign in” page, use your Microsoft account to sign in and you will be able to subscribe and get free keys.</span><span class="sxs-lookup"><span data-stu-id="0ab03-118">On the “Sign in” page, use your Microsoft account to sign in and you will be able to subscribe and get free keys.</span></span> <span data-ttu-id="0ab03-119">After completing the sign-up process, paste your key into the variables section of the notebook (reproduced below).</span><span class="sxs-lookup"><span data-stu-id="0ab03-119">After completing the sign-up process, paste your key into the variables section of the notebook (reproduced below).</span></span> <span data-ttu-id="0ab03-120">Either the primary or the secondary key works.</span><span class="sxs-lookup"><span data-stu-id="0ab03-120">Either the primary or the secondary key works.</span></span> <span data-ttu-id="0ab03-121">Make sure to enclose the key in quotes to make it a string.</span><span class="sxs-lookup"><span data-stu-id="0ab03-121">Make sure to enclose the key in quotes to make it a string.</span></span>

```python
# Variables

_url = 'https://westcentralus.api.cognitive.microsoft.com/vision/v1/analyses'
_key = None #Here you have to paste your primary key
_maxNumRetries = 10
```
