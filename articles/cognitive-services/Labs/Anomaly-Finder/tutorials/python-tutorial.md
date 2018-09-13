---
title: Anomaly Detection Python app - Microsoft Cognitive Services | Microsoft Docs
description: Explore a Python notebook that uses the Anomaly Detection API in Microsoft Cognitive Services. Send original data points to API and get the expected value and anomaly points.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: d35f41ddab21aa155376ad52ff4084298dab8fc5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866920"
---
# <a name="anomaly-detection-python-application"></a><span data-ttu-id="c4604-104">Anomaly Detection Python application</span><span class="sxs-lookup"><span data-stu-id="c4604-104">Anomaly Detection Python application</span></span>

<span data-ttu-id="c4604-105">The tutorial shows how to use the Anomaly Detection API in Python and how to visualize your results using popular libraries.</span><span class="sxs-lookup"><span data-stu-id="c4604-105">The tutorial shows how to use the Anomaly Detection API in Python and how to visualize your results using popular libraries.</span></span> <span data-ttu-id="c4604-106">Using Jupyter to run the tutorial and trying your own data with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="c4604-106">Using Jupyter to run the tutorial and trying your own data with your subscription key.</span></span> <span data-ttu-id="c4604-107">To learn how to get started with interactive Jupyter notebooks, refer to [Jupyter Documentation](http://jupyter.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="c4604-107">To learn how to get started with interactive Jupyter notebooks, refer to [Jupyter Documentation](http://jupyter.readthedocs.io/en/latest/index.html).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c4604-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4604-108">Prerequisites</span></span>

### <a name="subscribe-to-anomaly-detection-and-get-a-subscription-key"></a><span data-ttu-id="c4604-109">Subscribe to Anomaly Detection and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="c4604-109">Subscribe to Anomaly Detection and get a subscription key</span></span> 

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="download-the-example-code"></a><span data-ttu-id="c4604-110">Download the example code</span><span class="sxs-lookup"><span data-stu-id="c4604-110">Download the example code</span></span>

1. <span data-ttu-id="c4604-111">Navigate to the [tutorial notebook in Github](https://github.com/MicrosoftAnomalyDetection/python-sample).</span><span class="sxs-lookup"><span data-stu-id="c4604-111">Navigate to the [tutorial notebook in Github](https://github.com/MicrosoftAnomalyDetection/python-sample).</span></span>
2. <span data-ttu-id="c4604-112">Click on the green button to clone or download the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c4604-112">Click on the green button to clone or download the tutorial.</span></span> 

## <a name="opening-the-tutorial-notebook-in-jupyter"></a><span data-ttu-id="c4604-113">Opening the tutorial notebook in Jupyter</span><span class="sxs-lookup"><span data-stu-id="c4604-113">Opening the tutorial notebook in Jupyter</span></span>

1. <span data-ttu-id="c4604-114">Open a command prompt and go to the folder python-sample.</span><span class="sxs-lookup"><span data-stu-id="c4604-114">Open a command prompt and go to the folder python-sample.</span></span>
2. <span data-ttu-id="c4604-115">Run the command Jupyter notebook from the command prompt, which will start Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c4604-115">Run the command Jupyter notebook from the command prompt, which will start Jupyter.</span></span>
3. <span data-ttu-id="c4604-116">In the Jupyter window, click on <em>Anomaly Detection API Example.ipynb</em> to open the tutorial notebook.</span><span class="sxs-lookup"><span data-stu-id="c4604-116">In the Jupyter window, click on <em>Anomaly Detection API Example.ipynb</em> to open the tutorial notebook.</span></span>   

## <a name="running-the-tutorial"></a><span data-ttu-id="c4604-117">Running the tutorial</span><span class="sxs-lookup"><span data-stu-id="c4604-117">Running the tutorial</span></span>

<span data-ttu-id="c4604-118">To use this notebook, you will need a subscription key for the Anomaly Detection API.</span><span class="sxs-lookup"><span data-stu-id="c4604-118">To use this notebook, you will need a subscription key for the Anomaly Detection API.</span></span> <span data-ttu-id="c4604-119">Visit the Subscription page to sign up.</span><span class="sxs-lookup"><span data-stu-id="c4604-119">Visit the Subscription page to sign up.</span></span> <span data-ttu-id="c4604-120">On the “Sign in” page, use your Microsoft account to sign in and you will be able to subscribe and get your keys.</span><span class="sxs-lookup"><span data-stu-id="c4604-120">On the “Sign in” page, use your Microsoft account to sign in and you will be able to subscribe and get your keys.</span></span> <span data-ttu-id="c4604-121">After completing the sign-up process, paste your key into the variables section of the notebook (reproduced below).</span><span class="sxs-lookup"><span data-stu-id="c4604-121">After completing the sign-up process, paste your key into the variables section of the notebook (reproduced below).</span></span> <span data-ttu-id="c4604-122">Either the primary or the secondary key works.</span><span class="sxs-lookup"><span data-stu-id="c4604-122">Either the primary or the secondary key works.</span></span> <span data-ttu-id="c4604-123">Make sure to enclose the key in quotes to make it a string.</span><span class="sxs-lookup"><span data-stu-id="c4604-123">Make sure to enclose the key in quotes to make it a string.</span></span>

```Python

            # Variables
            endpoint = 'https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection'
            subscription_key = None #Here you have to paste your primary key

```

## <a name="next-steps"></a><span data-ttu-id="c4604-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4604-124">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4604-125">REST API reference</span><span class="sxs-lookup"><span data-stu-id="c4604-125">REST API reference</span></span>](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
