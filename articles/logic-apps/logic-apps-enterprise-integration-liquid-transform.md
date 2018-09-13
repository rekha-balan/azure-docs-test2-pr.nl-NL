---
title: Convert JSON data with Liquid transforms - Azure Logic Apps | Microsoft Docs
description: Create transforms or maps for advanced JSON transformations using Logic Apps and Liquid template
services: logic-apps
ms.service: logic-apps
author: divyaswarnkar
ms.author: divswa
manager: jeconnoc
ms.reviewer: estfan, LADocs
ms.suite: integration
ms.topic: article
ms.date: 08/16/2018
ms.openlocfilehash: 140c92d260ac6423127e478e304cbebcf9c42124
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868142"
---
# <a name="perform-advanced-json-transformations-with-liquid-templates-in-azure-logic-apps"></a><span data-ttu-id="fb12b-103">Perform advanced JSON transformations with Liquid templates in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fb12b-103">Perform advanced JSON transformations with Liquid templates in Azure Logic Apps</span></span>

<span data-ttu-id="fb12b-104">You can perform basic JSON transformations in your logic apps with native data operation actions such as **Compose** or **Parse JSON**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-104">You can perform basic JSON transformations in your logic apps with native data operation actions such as **Compose** or **Parse JSON**.</span></span> <span data-ttu-id="fb12b-105">To perform advanced JSON transformations, you can create templates or maps with [Liquid](https://shopify.github.io/liquid/), which is an open-source template language for flexible web apps.</span><span class="sxs-lookup"><span data-stu-id="fb12b-105">To perform advanced JSON transformations, you can create templates or maps with [Liquid](https://shopify.github.io/liquid/), which is an open-source template language for flexible web apps.</span></span> <span data-ttu-id="fb12b-106">Liquid templates let you define how to transform JSON output and supports more complex JSON transformations, such as iterations, control flows, variables, and so on.</span><span class="sxs-lookup"><span data-stu-id="fb12b-106">Liquid templates let you define how to transform JSON output and supports more complex JSON transformations, such as iterations, control flows, variables, and so on.</span></span> 

<span data-ttu-id="fb12b-107">So, before you can perform a Liquid transformation in your logic app, you first define the JSON to JSON mapping with a Liquid template and store that map in your integration account.</span><span class="sxs-lookup"><span data-stu-id="fb12b-107">So, before you can perform a Liquid transformation in your logic app, you first define the JSON to JSON mapping with a Liquid template and store that map in your integration account.</span></span> <span data-ttu-id="fb12b-108">This article shows you how to create and use this Liquid template or map.</span><span class="sxs-lookup"><span data-stu-id="fb12b-108">This article shows you how to create and use this Liquid template or map.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fb12b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb12b-109">Prerequisites</span></span>

* <span data-ttu-id="fb12b-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fb12b-110">An Azure subscription.</span></span> <span data-ttu-id="fb12b-111">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fb12b-111">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="fb12b-112">Or, [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="fb12b-112">Or, [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="fb12b-113">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="fb12b-113">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="fb12b-114">A basic [Integration Account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)</span><span class="sxs-lookup"><span data-stu-id="fb12b-114">A basic [Integration Account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)</span></span>

## <a name="create-liquid-template-or-map-for-your-integration-account"></a><span data-ttu-id="fb12b-115">Create Liquid template or map for your integration account</span><span class="sxs-lookup"><span data-stu-id="fb12b-115">Create Liquid template or map for your integration account</span></span>

1. <span data-ttu-id="fb12b-116">For this example, create the sample Liquid template described in this step.</span><span class="sxs-lookup"><span data-stu-id="fb12b-116">For this example, create the sample Liquid template described in this step.</span></span>
<span data-ttu-id="fb12b-117">If you want to use any filters in your Liquid template, make sure those filters start with uppercase.</span><span class="sxs-lookup"><span data-stu-id="fb12b-117">If you want to use any filters in your Liquid template, make sure those filters start with uppercase.</span></span> <span data-ttu-id="fb12b-118">Learn more about [Liquid filters](https://shopify.github.io/liquid/basics/introduction/#filters).</span><span class="sxs-lookup"><span data-stu-id="fb12b-118">Learn more about [Liquid filters](https://shopify.github.io/liquid/basics/introduction/#filters).</span></span> 

   ```json
   {%- assign deviceList = content.devices | Split: ', ' -%}
   
   {
      "fullName": "{{content.firstName | Append: ' ' | Append: content.lastName}}",
      "firstNameUpperCase": "{{content.firstName | Upcase}}",
      "phoneAreaCode": "{{content.phone | Slice: 1, 3}}",
      "devices" : [
         {%- for device in deviceList -%}
            {%- if forloop.Last == true -%}
            "{{device}}"
            {%- else -%}
            "{{device}}",
            {%- endif -%}
        {%- endfor -%}
        ]
   }
   ```

2. <span data-ttu-id="fb12b-119">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb12b-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fb12b-120">On the main Azure menu, select **All resources**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-120">On the main Azure menu, select **All resources**.</span></span> <span data-ttu-id="fb12b-121">In the search box, find and select your integration account.</span><span class="sxs-lookup"><span data-stu-id="fb12b-121">In the search box, find and select your integration account.</span></span>

   ![Select integration account](./media/logic-apps-enterprise-integration-liquid-transform/select-integration-account.png)

3.  <span data-ttu-id="fb12b-123">Under **Components**, select **Maps**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-123">Under **Components**, select **Maps**.</span></span>

    ![Select maps](./media/logic-apps-enterprise-integration-liquid-transform/add-maps.png)

4. <span data-ttu-id="fb12b-125">Choose **Add** and provide these details for your map:</span><span class="sxs-lookup"><span data-stu-id="fb12b-125">Choose **Add** and provide these details for your map:</span></span>

   | <span data-ttu-id="fb12b-126">Property</span><span class="sxs-lookup"><span data-stu-id="fb12b-126">Property</span></span> | <span data-ttu-id="fb12b-127">Value</span><span class="sxs-lookup"><span data-stu-id="fb12b-127">Value</span></span> | <span data-ttu-id="fb12b-128">Description</span><span class="sxs-lookup"><span data-stu-id="fb12b-128">Description</span></span> | 
   |----------|-------|-------------|
   | <span data-ttu-id="fb12b-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="fb12b-129">**Name**</span></span> | <span data-ttu-id="fb12b-130">JsonToJsonTemplate</span><span class="sxs-lookup"><span data-stu-id="fb12b-130">JsonToJsonTemplate</span></span> | <span data-ttu-id="fb12b-131">The name for your map, which is "JsonToJsonTemplate" in this example</span><span class="sxs-lookup"><span data-stu-id="fb12b-131">The name for your map, which is "JsonToJsonTemplate" in this example</span></span> | 
   | <span data-ttu-id="fb12b-132">**Map type**</span><span class="sxs-lookup"><span data-stu-id="fb12b-132">**Map type**</span></span> | <span data-ttu-id="fb12b-133">**liquid**</span><span class="sxs-lookup"><span data-stu-id="fb12b-133">**liquid**</span></span> | <span data-ttu-id="fb12b-134">The type for your map.</span><span class="sxs-lookup"><span data-stu-id="fb12b-134">The type for your map.</span></span> <span data-ttu-id="fb12b-135">For JSON to JSON transformation, you must select **liquid**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-135">For JSON to JSON transformation, you must select **liquid**.</span></span> | 
   | <span data-ttu-id="fb12b-136">**Map**</span><span class="sxs-lookup"><span data-stu-id="fb12b-136">**Map**</span></span> | <span data-ttu-id="fb12b-137">"SimpleJsonToJsonTemplate.liquid"</span><span class="sxs-lookup"><span data-stu-id="fb12b-137">"SimpleJsonToJsonTemplate.liquid"</span></span> | <span data-ttu-id="fb12b-138">An existing Liquid template or map file to use for transformation, which is "SimpleJsonToJsonTemplate.liquid" in this example.</span><span class="sxs-lookup"><span data-stu-id="fb12b-138">An existing Liquid template or map file to use for transformation, which is "SimpleJsonToJsonTemplate.liquid" in this example.</span></span> <span data-ttu-id="fb12b-139">To find this file, you can use the file picker.</span><span class="sxs-lookup"><span data-stu-id="fb12b-139">To find this file, you can use the file picker.</span></span> |
   ||| 

   ![Add liquid template](./media/logic-apps-enterprise-integration-liquid-transform/add-liquid-template.png)
    
## <a name="add-the-liquid-action-for-json-transformation"></a><span data-ttu-id="fb12b-141">Add the Liquid action for JSON transformation</span><span class="sxs-lookup"><span data-stu-id="fb12b-141">Add the Liquid action for JSON transformation</span></span>

1. <span data-ttu-id="fb12b-142">In the Azure portal, follow these steps to [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="fb12b-142">In the Azure portal, follow these steps to [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

2. <span data-ttu-id="fb12b-143">In the Logic App Designer, add the [Request trigger](../connectors/connectors-native-reqres.md#use-the-http-request-trigger) to your logic app.</span><span class="sxs-lookup"><span data-stu-id="fb12b-143">In the Logic App Designer, add the [Request trigger](../connectors/connectors-native-reqres.md#use-the-http-request-trigger) to your logic app.</span></span>

3. <span data-ttu-id="fb12b-144">Under the trigger, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-144">Under the trigger, choose **New step**.</span></span> <span data-ttu-id="fb12b-145">In the search box, enter "liquid" as your filter, and select this action: **Transform JSON to JSON - Liquid**</span><span class="sxs-lookup"><span data-stu-id="fb12b-145">In the search box, enter "liquid" as your filter, and select this action: **Transform JSON to JSON - Liquid**</span></span>

   ![Find and select Liquid action](./media/logic-apps-enterprise-integration-liquid-transform/search-action-liquid.png)

4. <span data-ttu-id="fb12b-147">Click inside the **Content** box so that the dynamic content list appears, and select the **Body** token.</span><span class="sxs-lookup"><span data-stu-id="fb12b-147">Click inside the **Content** box so that the dynamic content list appears, and select the **Body** token.</span></span>
  
   ![Select body](./media/logic-apps-enterprise-integration-liquid-transform/select-body.png)
 
5. <span data-ttu-id="fb12b-149">From the **Map** list, select your Liquid template, which is "JsonToJsonTemplate" in this example.</span><span class="sxs-lookup"><span data-stu-id="fb12b-149">From the **Map** list, select your Liquid template, which is "JsonToJsonTemplate" in this example.</span></span>

   ![Select map](./media/logic-apps-enterprise-integration-liquid-transform/select-map.png)

   <span data-ttu-id="fb12b-151">If the maps list is empty, most likely your logic app is not linked to your integration account.</span><span class="sxs-lookup"><span data-stu-id="fb12b-151">If the maps list is empty, most likely your logic app is not linked to your integration account.</span></span> 
   <span data-ttu-id="fb12b-152">To link your logic app to the integration account that has the Liquid template or map, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="fb12b-152">To link your logic app to the integration account that has the Liquid template or map, follow these steps:</span></span>

   1. <span data-ttu-id="fb12b-153">On your logic app menu, select **Workflow settings**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-153">On your logic app menu, select **Workflow settings**.</span></span>

   2. <span data-ttu-id="fb12b-154">From the **Select an Integration account** list, select your integration account, and choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="fb12b-154">From the **Select an Integration account** list, select your integration account, and choose **Save**.</span></span>

     ![Link logic app to integration account](./media/logic-apps-enterprise-integration-liquid-transform/link-integration-account.png)

## <a name="test-your-logic-app"></a><span data-ttu-id="fb12b-156">Test your logic app</span><span class="sxs-lookup"><span data-stu-id="fb12b-156">Test your logic app</span></span>

<span data-ttu-id="fb12b-157">Post JSON input to your logic app from [Postman](https://www.getpostman.com/postman) or a similar tool.</span><span class="sxs-lookup"><span data-stu-id="fb12b-157">Post JSON input to your logic app from [Postman](https://www.getpostman.com/postman) or a similar tool.</span></span> <span data-ttu-id="fb12b-158">The transformed JSON output from your logic app looks like this example:</span><span class="sxs-lookup"><span data-stu-id="fb12b-158">The transformed JSON output from your logic app looks like this example:</span></span>
  
![Example output](./media/logic-apps-enterprise-integration-liquid-transform/example-output-jsontojson.png)

## <a name="more-liquid-action-examples"></a><span data-ttu-id="fb12b-160">More Liquid action examples</span><span class="sxs-lookup"><span data-stu-id="fb12b-160">More Liquid action examples</span></span>
<span data-ttu-id="fb12b-161">Liquid is not limited to only JSON transformations.</span><span class="sxs-lookup"><span data-stu-id="fb12b-161">Liquid is not limited to only JSON transformations.</span></span> <span data-ttu-id="fb12b-162">Here are other available transformation actions that use Liquid.</span><span class="sxs-lookup"><span data-stu-id="fb12b-162">Here are other available transformation actions that use Liquid.</span></span>

* <span data-ttu-id="fb12b-163">Transform JSON to text</span><span class="sxs-lookup"><span data-stu-id="fb12b-163">Transform JSON to text</span></span>
  
  <span data-ttu-id="fb12b-164">Here is the Liquid template used for this example:</span><span class="sxs-lookup"><span data-stu-id="fb12b-164">Here is the Liquid template used for this example:</span></span>
   
   ``` json
   {{content.firstName | Append: ' ' | Append: content.lastName}}
   ```
   <span data-ttu-id="fb12b-165">Here are sample input and output:</span><span class="sxs-lookup"><span data-stu-id="fb12b-165">Here are sample input and output:</span></span>
  
   ![Example output JSON to text](./media/logic-apps-enterprise-integration-liquid-transform/example-output-jsontotext.png)

* <span data-ttu-id="fb12b-167">Transform XML to JSON</span><span class="sxs-lookup"><span data-stu-id="fb12b-167">Transform XML to JSON</span></span>
  
  <span data-ttu-id="fb12b-168">Here is the Liquid template used for this example:</span><span class="sxs-lookup"><span data-stu-id="fb12b-168">Here is the Liquid template used for this example:</span></span>
   
   ``` json
   [{% JSONArrayFor item in content -%}
        {{item}}
    {% endJSONArrayFor -%}]
   ```
   <span data-ttu-id="fb12b-169">Here are sample input and output:</span><span class="sxs-lookup"><span data-stu-id="fb12b-169">Here are sample input and output:</span></span>

   ![Example output XML to JSON](./media/logic-apps-enterprise-integration-liquid-transform/example-output-xmltojson.png)

* <span data-ttu-id="fb12b-171">Transform XML to text</span><span class="sxs-lookup"><span data-stu-id="fb12b-171">Transform XML to text</span></span>
  
  <span data-ttu-id="fb12b-172">Here is the Liquid template used for this example:</span><span class="sxs-lookup"><span data-stu-id="fb12b-172">Here is the Liquid template used for this example:</span></span>

   ``` json
   {{content.firstName | Append: ' ' | Append: content.lastName}}
   ```

   <span data-ttu-id="fb12b-173">Here are sample input and output:</span><span class="sxs-lookup"><span data-stu-id="fb12b-173">Here are sample input and output:</span></span>

   ![Example output XML to text](./media/logic-apps-enterprise-integration-liquid-transform/example-output-xmltotext.png)

## <a name="next-steps"></a><span data-ttu-id="fb12b-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb12b-175">Next steps</span></span>

* [<span data-ttu-id="fb12b-176">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="fb12b-176">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")  
* [<span data-ttu-id="fb12b-177">Learn more about maps</span><span class="sxs-lookup"><span data-stu-id="fb12b-177">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Learn about enterprise integration maps")  

