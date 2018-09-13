---
title: Trigger Azure Functions using webhooks in Azure IoT Central
description: Create a function app that runs each time a rule is triggered in Azure IoT Central.
author: viv-liu
ms.author: viviali
ms.date: 09/06/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 7b14dc4eeec1ab543c407b1bb1cf8a5ce46f3ecb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864791"
---
# <a name="trigger-azure-functions-using-webhooks-in-azure-iot-central"></a><span data-ttu-id="9c803-103">Trigger Azure Functions using webhooks in Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="9c803-103">Trigger Azure Functions using webhooks in Azure IoT Central</span></span>

<span data-ttu-id="9c803-104">Use Azure Functions to run serverless code on the webhook output from IoT Central rules.</span><span class="sxs-lookup"><span data-stu-id="9c803-104">Use Azure Functions to run serverless code on the webhook output from IoT Central rules.</span></span> <span data-ttu-id="9c803-105">You don't have to provision a VM or publish a web app to use Azure Functions, but instead you can run this code serverlessly.</span><span class="sxs-lookup"><span data-stu-id="9c803-105">You don't have to provision a VM or publish a web app to use Azure Functions, but instead you can run this code serverlessly.</span></span> <span data-ttu-id="9c803-106">Use Azure Functions to transform the webhook payload before sending it to its final destination such as a SQL database or Event Grid.</span><span class="sxs-lookup"><span data-stu-id="9c803-106">Use Azure Functions to transform the webhook payload before sending it to its final destination such as a SQL database or Event Grid.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9c803-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c803-107">Prerequisites</span></span>
+ <span data-ttu-id="9c803-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9c803-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="how-to-connect-azure-functions"></a><span data-ttu-id="9c803-109">How to connect Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9c803-109">How to connect Azure Functions</span></span>

1. <span data-ttu-id="9c803-110">[Create a new function app in the Azure Portal.](https://ms.portal.azure.com/#create/Microsoft.FunctionApp).</span><span class="sxs-lookup"><span data-stu-id="9c803-110">[Create a new function app in the Azure Portal.](https://ms.portal.azure.com/#create/Microsoft.FunctionApp).</span></span>
2. <span data-ttu-id="9c803-111">Expand your function app and click the + button next to Functions.</span><span class="sxs-lookup"><span data-stu-id="9c803-111">Expand your function app and click the + button next to Functions.</span></span> <span data-ttu-id="9c803-112">If this function is the first one in your function app, select Custom function.</span><span class="sxs-lookup"><span data-stu-id="9c803-112">If this function is the first one in your function app, select Custom function.</span></span> <span data-ttu-id="9c803-113">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="9c803-113">This displays the complete set of function templates.</span></span>
3. <span data-ttu-id="9c803-114">In the search field, type generic and then choose your desired language for the generic webhook trigger template.</span><span class="sxs-lookup"><span data-stu-id="9c803-114">In the search field, type generic and then choose your desired language for the generic webhook trigger template.</span></span> <span data-ttu-id="9c803-115">This topic uses a C# function.</span><span class="sxs-lookup"><span data-stu-id="9c803-115">This topic uses a C# function.</span></span> 
4. <span data-ttu-id="9c803-116">In your new function, click **</> Get function URL**, then copy and save the value.</span><span class="sxs-lookup"><span data-stu-id="9c803-116">In your new function, click **</> Get function URL**, then copy and save the value.</span></span> <span data-ttu-id="9c803-117">You use this value to configure the webhook.</span><span class="sxs-lookup"><span data-stu-id="9c803-117">You use this value to configure the webhook.</span></span> 
4. <span data-ttu-id="9c803-118">In IoT Central, find the rule that you want to connect to your function app.</span><span class="sxs-lookup"><span data-stu-id="9c803-118">In IoT Central, find the rule that you want to connect to your function app.</span></span> 
5. <span data-ttu-id="9c803-119">Add a webhook action.</span><span class="sxs-lookup"><span data-stu-id="9c803-119">Add a webhook action.</span></span> <span data-ttu-id="9c803-120">Enter a **Display name** and paste in the function URL you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="9c803-120">Enter a **Display name** and paste in the function URL you copied earlier.</span></span>
6. <span data-ttu-id="9c803-121">Save the rule.</span><span class="sxs-lookup"><span data-stu-id="9c803-121">Save the rule.</span></span> <span data-ttu-id="9c803-122">Now when the rule is triggered, the webhook will invoke the function app to run.</span><span class="sxs-lookup"><span data-stu-id="9c803-122">Now when the rule is triggered, the webhook will invoke the function app to run.</span></span> <span data-ttu-id="9c803-123">In your function app, you can observe the Logs and see each time the function is triggered.</span><span class="sxs-lookup"><span data-stu-id="9c803-123">In your function app, you can observe the Logs and see each time the function is triggered.</span></span>

<span data-ttu-id="9c803-124">For more information, visit the Azure Functions article about [creating a function triggered by a generic webhook](https://docs.microsoft.com/azure/azure-functions/functions-create-generic-webhook-triggered-function).</span><span class="sxs-lookup"><span data-stu-id="9c803-124">For more information, visit the Azure Functions article about [creating a function triggered by a generic webhook](https://docs.microsoft.com/azure/azure-functions/functions-create-generic-webhook-triggered-function).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c803-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c803-125">Next steps</span></span>
<span data-ttu-id="9c803-126">Now that you have learned how to set up and use webhooks, the suggested next step is to explore [building workflows in Microsoft Flow](howto-add-microsoft-flow.md).</span><span class="sxs-lookup"><span data-stu-id="9c803-126">Now that you have learned how to set up and use webhooks, the suggested next step is to explore [building workflows in Microsoft Flow](howto-add-microsoft-flow.md).</span></span>
