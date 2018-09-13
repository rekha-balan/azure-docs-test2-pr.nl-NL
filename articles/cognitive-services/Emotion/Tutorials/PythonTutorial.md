---
title: Emotion API Python tutorial | Microsoft Docs
description: Use a Jupyter notebook to learn how to use the Cognitive Services Emotion API with Python. Visualize your results by using popular libraries.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 01/30/2017
ms.author: anroth
ms.openlocfilehash: c81d6fcbf2fe3790e654a1be0de1ed5c93154448
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564106"
---
# <a name="emotion-api-using-python-tutorial"></a><span data-ttu-id="41bef-104">Emotion API using Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="41bef-104">Emotion API using Python Tutorial</span></span>

<span data-ttu-id="41bef-105">To make it easy to get started with Emotion API, the Jupyter notebook linked below shows you how to use the API in Python and how to visualize your results using some popular libraries.</span><span class="sxs-lookup"><span data-stu-id="41bef-105">To make it easy to get started with Emotion API, the Jupyter notebook linked below shows you how to use the API in Python and how to visualize your results using some popular libraries.</span></span> 

[<span data-ttu-id="41bef-106">Link to notebook in GitHub</span><span class="sxs-lookup"><span data-stu-id="41bef-106">Link to notebook in GitHub</span></span>](https://github.com/Microsoft/Cognitive-Emotion-Python/blob/master/Jupyter%20Notebook/Emotion%20Analysis%20Example.ipynb)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="41bef-107">Using the Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="41bef-107">Using the Jupyter Notebook</span></span>

<span data-ttu-id="41bef-108">To use the notebook interactively, you will need to clone it and run it in Jupyter.</span><span class="sxs-lookup"><span data-stu-id="41bef-108">To use the notebook interactively, you will need to clone it and run it in Jupyter.</span></span> <span data-ttu-id="41bef-109">To learn how to get started with interactive Jupyter notebooks, follow the instructions at http://jupyter.readthedocs.org/en/latest/install.html.</span><span class="sxs-lookup"><span data-stu-id="41bef-109">To learn how to get started with interactive Jupyter notebooks, follow the instructions at http://jupyter.readthedocs.org/en/latest/install.html.</span></span> 

<span data-ttu-id="41bef-110">To use this notebook, you will need a subscription key for the Emotion API.</span><span class="sxs-lookup"><span data-stu-id="41bef-110">To use this notebook, you will need a subscription key for the Emotion API.</span></span> <span data-ttu-id="41bef-111">Visit the [Subscription page](https://www.microsoft.com/cognitive-services/en-us/sign-up) to sign up.</span><span class="sxs-lookup"><span data-stu-id="41bef-111">Visit the [Subscription page](https://www.microsoft.com/cognitive-services/en-us/sign-up) to sign up.</span></span> <span data-ttu-id="41bef-112">On the “Sign in” page, use your Microsoft account to sign in and you will be able to subscribe and get free keys.</span><span class="sxs-lookup"><span data-stu-id="41bef-112">On the “Sign in” page, use your Microsoft account to sign in and you will be able to subscribe and get free keys.</span></span> <span data-ttu-id="41bef-113">After completing the sign-up process, paste your key into the variables section shown below.</span><span class="sxs-lookup"><span data-stu-id="41bef-113">After completing the sign-up process, paste your key into the variables section shown below.</span></span> <span data-ttu-id="41bef-114">Either the primary or the secondary key works.</span><span class="sxs-lookup"><span data-stu-id="41bef-114">Either the primary or the secondary key works.</span></span>

```
Python Example 

#Variables

_url = 'https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize'
_key = None #Here you have to paste your primary key
_maxNumRetries = 10

```
