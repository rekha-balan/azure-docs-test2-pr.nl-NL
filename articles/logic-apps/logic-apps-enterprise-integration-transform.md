---
title: Convert XML data with transforms - Azure Logic Apps | Microsoft Docs
description: Create transforms or mapps to convert XML data between formats in logic apps by using the Enterprise Integration SDK
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: estfan
ms.openlocfilehash: c4036e64cc90c2e979140ec9a8cd94fe2fb676a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550340"
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="bd6f6-103">Enterprise integration with XML transforms</span><span class="sxs-lookup"><span data-stu-id="bd6f6-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="bd6f6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bd6f6-104">Overview</span></span>
<span data-ttu-id="bd6f6-105">The Enterprise integration Transform connector converts data from one format to another format.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="bd6f6-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="bd6f6-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="bd6f6-108">What does a transform do?</span><span class="sxs-lookup"><span data-stu-id="bd6f6-108">What does a transform do?</span></span>
<span data-ttu-id="bd6f6-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span><span class="sxs-lookup"><span data-stu-id="bd6f6-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="bd6f6-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="bd6f6-111">How to create a transform?</span><span class="sxs-lookup"><span data-stu-id="bd6f6-111">How to create a transform?</span></span>
<span data-ttu-id="bd6f6-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="bd6f6-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="bd6f6-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="bd6f6-114">How to use a transform</span><span class="sxs-lookup"><span data-stu-id="bd6f6-114">How to use a transform</span></span>
<span data-ttu-id="bd6f6-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="bd6f6-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span><span class="sxs-lookup"><span data-stu-id="bd6f6-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="bd6f6-117">**Here are the steps to use a transform**:</span><span class="sxs-lookup"><span data-stu-id="bd6f6-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bd6f6-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bd6f6-118">Prerequisites</span></span>

* <span data-ttu-id="bd6f6-119">Create an integration account and add a map to it</span><span class="sxs-lookup"><span data-stu-id="bd6f6-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="bd6f6-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span><span class="sxs-lookup"><span data-stu-id="bd6f6-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="bd6f6-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="bd6f6-122">Add a **Request** trigger to your Logic app</span><span class="sxs-lookup"><span data-stu-id="bd6f6-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="bd6f6-123">Add the **Transform XML** action by first selecting **Add an action** </span><span class="sxs-lookup"><span data-stu-id="bd6f6-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="bd6f6-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span><span class="sxs-lookup"><span data-stu-id="bd6f6-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="bd6f6-125">Select the **Transform XML** action</span><span class="sxs-lookup"><span data-stu-id="bd6f6-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="bd6f6-126">Add the XML **CONTENT** that you transform.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="bd6f6-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="bd6f6-128">In this example, select the body of the HTTP request that triggered the Logic app.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="bd6f6-129">Select the name of the **MAP** that you want to use to perform the transformation.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="bd6f6-130">The map must already be in your integration account.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-130">The map must already be in your integration account.</span></span> <span data-ttu-id="bd6f6-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="bd6f6-132">Save your work</span><span class="sxs-lookup"><span data-stu-id="bd6f6-132">Save your work</span></span>  
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="bd6f6-133">At this point, you are finished setting up your map.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="bd6f6-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="bd6f6-135">You can easily as an action to send the output of the transform to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="bd6f6-136">You can now test your transform by making a request to the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="bd6f6-137">Features and use cases</span><span class="sxs-lookup"><span data-stu-id="bd6f6-137">Features and use cases</span></span>
* <span data-ttu-id="bd6f6-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="bd6f6-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="bd6f6-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="bd6f6-141">You can do a direct data copy between the schemas.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="bd6f6-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="bd6f6-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="bd6f6-144">Use the Test Map feature to add a sample XML message.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="bd6f6-145">With a simple click, you can test the map you created, and see the generated output.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="bd6f6-146">Upload existing maps</span><span class="sxs-lookup"><span data-stu-id="bd6f6-146">Upload existing maps</span></span>  
* <span data-ttu-id="bd6f6-147">Includes support for the XML format.</span><span class="sxs-lookup"><span data-stu-id="bd6f6-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="bd6f6-148">Learn more</span><span class="sxs-lookup"><span data-stu-id="bd6f6-148">Learn more</span></span>
* [<span data-ttu-id="bd6f6-149">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="bd6f6-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")  
* [<span data-ttu-id="bd6f6-150">Learn more about maps</span><span class="sxs-lookup"><span data-stu-id="bd6f6-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Learn about enterprise integration maps")  






