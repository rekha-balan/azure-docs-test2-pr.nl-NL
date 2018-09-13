---
title: Create, edit, or extend JSON for logic app definitions - Azure Logic Apps | Microsoft Docs
description: Author and extend JSON for logic app definitions in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, jehollan, LADocs
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.topic: article
ms.date: 01/01/2018
ms.openlocfilehash: 1f2e136810194ad044255f9d129b5c03549221b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44794890"
---
# <a name="create-edit-or-extend-json-for-logic-app-definitions-in-azure-logic-apps"></a><span data-ttu-id="93bfc-103">Create, edit, or extend JSON for logic app definitions in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="93bfc-103">Create, edit, or extend JSON for logic app definitions in Azure Logic Apps</span></span>

<span data-ttu-id="93bfc-104">When you create enterprise integration solutions with automated workflows in [Azure Logic Apps](../logic-apps/logic-apps-overview.md), the underlying logic app definitions use simple and declarative JavaScript Object Notation (JSON) along with the [Workflow Definition Language (WDL) schema](../logic-apps/logic-apps-workflow-definition-language.md) for their description and validation.</span><span class="sxs-lookup"><span data-stu-id="93bfc-104">When you create enterprise integration solutions with automated workflows in [Azure Logic Apps](../logic-apps/logic-apps-overview.md), the underlying logic app definitions use simple and declarative JavaScript Object Notation (JSON) along with the [Workflow Definition Language (WDL) schema](../logic-apps/logic-apps-workflow-definition-language.md) for their description and validation.</span></span> <span data-ttu-id="93bfc-105">These formats make logic app definitions easier to read and understand without knowing much about code.</span><span class="sxs-lookup"><span data-stu-id="93bfc-105">These formats make logic app definitions easier to read and understand without knowing much about code.</span></span> <span data-ttu-id="93bfc-106">When you want to automate creating and deploying logic apps, you can include logic app definitions as [Azure resources](../azure-resource-manager/resource-group-overview.md) inside [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment).</span><span class="sxs-lookup"><span data-stu-id="93bfc-106">When you want to automate creating and deploying logic apps, you can include logic app definitions as [Azure resources](../azure-resource-manager/resource-group-overview.md) inside [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span> <span data-ttu-id="93bfc-107">To create, manage, and deploy logic apps, you can then use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.logicapp), [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md), or the [Azure Logic Apps REST APIs](https://docs.microsoft.com/rest/api/logic/).</span><span class="sxs-lookup"><span data-stu-id="93bfc-107">To create, manage, and deploy logic apps, you can then use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.logicapp), [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md), or the [Azure Logic Apps REST APIs](https://docs.microsoft.com/rest/api/logic/).</span></span>

<span data-ttu-id="93bfc-108">To work with logic app definitions in JSON, open the Code View editor when working in the Azure portal or in Visual Studio, or copy the definition into any editor that you want.</span><span class="sxs-lookup"><span data-stu-id="93bfc-108">To work with logic app definitions in JSON, open the Code View editor when working in the Azure portal or in Visual Studio, or copy the definition into any editor that you want.</span></span> <span data-ttu-id="93bfc-109">If you're new to logic apps, review [how to create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="93bfc-109">If you're new to logic apps, review [how to create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="93bfc-110">Some Azure Logic Apps capabilities, such as defining parameters and multiple triggers in logic app definitions, are available only in JSON, not the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="93bfc-110">Some Azure Logic Apps capabilities, such as defining parameters and multiple triggers in logic app definitions, are available only in JSON, not the Logic Apps Designer.</span></span> <span data-ttu-id="93bfc-111">So for these tasks, you must work in Code View or another editor.</span><span class="sxs-lookup"><span data-stu-id="93bfc-111">So for these tasks, you must work in Code View or another editor.</span></span>

## <a name="edit-json---azure-portal"></a><span data-ttu-id="93bfc-112">Edit JSON - Azure portal</span><span class="sxs-lookup"><span data-stu-id="93bfc-112">Edit JSON - Azure portal</span></span>

1. <span data-ttu-id="93bfc-113">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span><span class="sxs-lookup"><span data-stu-id="93bfc-113">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>

2. <span data-ttu-id="93bfc-114">From the left menu, choose **All services**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-114">From the left menu, choose **All services**.</span></span> <span data-ttu-id="93bfc-115">In the search box, find "logic apps", and then from the results, select your logic app.</span><span class="sxs-lookup"><span data-stu-id="93bfc-115">In the search box, find "logic apps", and then from the results, select your logic app.</span></span>

3. <span data-ttu-id="93bfc-116">On your logic app's menu, under **Development Tools**, select **Logic App Code View**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-116">On your logic app's menu, under **Development Tools**, select **Logic App Code View**.</span></span>

   <span data-ttu-id="93bfc-117">The Code View editor opens and shows your logic app definition in JSON format.</span><span class="sxs-lookup"><span data-stu-id="93bfc-117">The Code View editor opens and shows your logic app definition in JSON format.</span></span>

## <a name="edit-json---visual-studio"></a><span data-ttu-id="93bfc-118">Edit JSON - Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93bfc-118">Edit JSON - Visual Studio</span></span>

<span data-ttu-id="93bfc-119">Before you can work on your logic app definition in Visual Studio, make sure that you've [installed the required tools](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="93bfc-119">Before you can work on your logic app definition in Visual Studio, make sure that you've [installed the required tools](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md#prerequisites).</span></span> <span data-ttu-id="93bfc-120">To create a logic app with Visual Studio, review [Quickstart: Automate tasks and processes with Azure Logic Apps - Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="93bfc-120">To create a logic app with Visual Studio, review [Quickstart: Automate tasks and processes with Azure Logic Apps - Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span></span>

<span data-ttu-id="93bfc-121">In Visual Studio, you can open logic apps that were created and deployed either directly from the Azure portal or as Azure Resource Manager projects from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93bfc-121">In Visual Studio, you can open logic apps that were created and deployed either directly from the Azure portal or as Azure Resource Manager projects from Visual Studio.</span></span>

1. <span data-ttu-id="93bfc-122">Open the Visual Studio solution, or [Azure Resource Group](../azure-resource-manager/resource-group-overview.md) project, that contains your logic app.</span><span class="sxs-lookup"><span data-stu-id="93bfc-122">Open the Visual Studio solution, or [Azure Resource Group](../azure-resource-manager/resource-group-overview.md) project, that contains your logic app.</span></span>

2. <span data-ttu-id="93bfc-123">Find and open your logic app's definition, which by default, appears in an [Resource Manager template](../azure-resource-manager/resource-group-overview.md#template-deployment), named **LogicApp.json**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-123">Find and open your logic app's definition, which by default, appears in an [Resource Manager template](../azure-resource-manager/resource-group-overview.md#template-deployment), named **LogicApp.json**.</span></span> <span data-ttu-id="93bfc-124">You can use and customize this template for deployment to different environments.</span><span class="sxs-lookup"><span data-stu-id="93bfc-124">You can use and customize this template for deployment to different environments.</span></span>

3. <span data-ttu-id="93bfc-125">Open the shortcut menu for your logic app definition and template.</span><span class="sxs-lookup"><span data-stu-id="93bfc-125">Open the shortcut menu for your logic app definition and template.</span></span> <span data-ttu-id="93bfc-126">Select **Open With Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-126">Select **Open With Logic App Designer**.</span></span>

   ![Open logic app in a Visual Studio solution](./media/logic-apps-author-definitions/open-logic-app-designer.png)

4. <span data-ttu-id="93bfc-128">At the bottom of the designer, choose **Code View**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-128">At the bottom of the designer, choose **Code View**.</span></span> 

   <span data-ttu-id="93bfc-129">The Code View editor opens and shows your logic app definition in JSON format.</span><span class="sxs-lookup"><span data-stu-id="93bfc-129">The Code View editor opens and shows your logic app definition in JSON format.</span></span>

5. <span data-ttu-id="93bfc-130">To return to designer view, at the bottom of the Code View editor, choose **Design**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-130">To return to designer view, at the bottom of the Code View editor, choose **Design**.</span></span>

## <a name="parameters"></a><span data-ttu-id="93bfc-131">Parameters</span><span class="sxs-lookup"><span data-stu-id="93bfc-131">Parameters</span></span>

<span data-ttu-id="93bfc-132">Parameters let you reuse values throughout your logic app and are good for replacing values that you might change often.</span><span class="sxs-lookup"><span data-stu-id="93bfc-132">Parameters let you reuse values throughout your logic app and are good for replacing values that you might change often.</span></span> <span data-ttu-id="93bfc-133">For example, if you have an email address that you want use in multiple places, you should define that email address as a parameter.</span><span class="sxs-lookup"><span data-stu-id="93bfc-133">For example, if you have an email address that you want use in multiple places, you should define that email address as a parameter.</span></span> 

<span data-ttu-id="93bfc-134">Parameters are also useful when you need to override parameters in different environments, Learn more about [parameters for deployment](#deployment-parameters) and the [REST API for Azure Logic Apps documentation](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="93bfc-134">Parameters are also useful when you need to override parameters in different environments, Learn more about [parameters for deployment](#deployment-parameters) and the [REST API for Azure Logic Apps documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

> [!NOTE]
> <span data-ttu-id="93bfc-135">Parameters are only available in code view.</span><span class="sxs-lookup"><span data-stu-id="93bfc-135">Parameters are only available in code view.</span></span>

<span data-ttu-id="93bfc-136">In the [first example logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md), you created a workflow that sends emails when new posts appear in a website's RSS feed.</span><span class="sxs-lookup"><span data-stu-id="93bfc-136">In the [first example logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md), you created a workflow that sends emails when new posts appear in a website's RSS feed.</span></span> <span data-ttu-id="93bfc-137">The feed's URL is hardcoded, so this example shows how to replace the query value with a parameter so that you can change feed's URL more easily.</span><span class="sxs-lookup"><span data-stu-id="93bfc-137">The feed's URL is hardcoded, so this example shows how to replace the query value with a parameter so that you can change feed's URL more easily.</span></span>

1. <span data-ttu-id="93bfc-138">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span><span class="sxs-lookup"><span data-stu-id="93bfc-138">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

   ``` json
     "currentFeedUrl" : {
      "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
   }
   ```

2. <span data-ttu-id="93bfc-139">In the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with `"feedUrl": "#@{parameters('currentFeedUrl')}"`.</span><span class="sxs-lookup"><span data-stu-id="93bfc-139">In the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with `"feedUrl": "#@{parameters('currentFeedUrl')}"`.</span></span> 

   <span data-ttu-id="93bfc-140">**Before**</span><span class="sxs-lookup"><span data-stu-id="93bfc-140">**Before**</span></span>
   ``` json
   }
      "queries": {
          "feedUrl": "https://s.ch9.ms/Feeds/RSS"
       }
   },   
   ```

   <span data-ttu-id="93bfc-141">**After**</span><span class="sxs-lookup"><span data-stu-id="93bfc-141">**After**</span></span>
   ``` json
   }
      "queries": {
          "feedUrl": "#@{parameters('currentFeedUrl')}"
       }
   },   
   ```

   <span data-ttu-id="93bfc-142">To join two or more strings, you can also use the `concat` function.</span><span class="sxs-lookup"><span data-stu-id="93bfc-142">To join two or more strings, you can also use the `concat` function.</span></span> 
   <span data-ttu-id="93bfc-143">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the previous example.</span><span class="sxs-lookup"><span data-stu-id="93bfc-143">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the previous example.</span></span>

3.  <span data-ttu-id="93bfc-144">When you're done, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="93bfc-144">When you're done, choose **Save**.</span></span> 

<span data-ttu-id="93bfc-145">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span><span class="sxs-lookup"><span data-stu-id="93bfc-145">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<a name="deployment-parameters"></a>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="93bfc-146">Deployment parameters for different environments</span><span class="sxs-lookup"><span data-stu-id="93bfc-146">Deployment parameters for different environments</span></span>

<span data-ttu-id="93bfc-147">Usually, deployment lifecycles have environments for development, staging, and production.</span><span class="sxs-lookup"><span data-stu-id="93bfc-147">Usually, deployment lifecycles have environments for development, staging, and production.</span></span> <span data-ttu-id="93bfc-148">For example, you might use the same logic app definition in all these environments but use different databases.</span><span class="sxs-lookup"><span data-stu-id="93bfc-148">For example, you might use the same logic app definition in all these environments but use different databases.</span></span> <span data-ttu-id="93bfc-149">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to use that region's database.</span><span class="sxs-lookup"><span data-stu-id="93bfc-149">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to use that region's database.</span></span> 

> [!NOTE] 
> <span data-ttu-id="93bfc-150">This scenario differs from taking parameters at *runtime* where you should use the `trigger()` function instead.</span><span class="sxs-lookup"><span data-stu-id="93bfc-150">This scenario differs from taking parameters at *runtime* where you should use the `trigger()` function instead.</span></span>

<span data-ttu-id="93bfc-151">Here's a basic definition:</span><span class="sxs-lookup"><span data-stu-id="93bfc-151">Here's a basic definition:</span></span>

``` json
{
    "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```
<span data-ttu-id="93bfc-152">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span><span class="sxs-lookup"><span data-stu-id="93bfc-152">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="93bfc-153">In each environment, you can provide a different value for the `connection` parameter.</span><span class="sxs-lookup"><span data-stu-id="93bfc-153">In each environment, you can provide a different value for the `connection` parameter.</span></span> <span data-ttu-id="93bfc-154">Because a default value no longer exists, the logic app payload requires this parameter:</span><span class="sxs-lookup"><span data-stu-id="93bfc-154">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

``` json
{
    "properties": {},
        "definition": {
          /// Use the definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

<span data-ttu-id="93bfc-155">To learn more, see the [REST API for Azure Logic Apps documentation](https://docs.microsoft.com/rest/api/logic/).</span><span class="sxs-lookup"><span data-stu-id="93bfc-155">To learn more, see the [REST API for Azure Logic Apps documentation](https://docs.microsoft.com/rest/api/logic/).</span></span>

## <a name="process-strings-with-functions"></a><span data-ttu-id="93bfc-156">Process strings with functions</span><span class="sxs-lookup"><span data-stu-id="93bfc-156">Process strings with functions</span></span>

<span data-ttu-id="93bfc-157">Logic Apps has various functions for working with strings.</span><span class="sxs-lookup"><span data-stu-id="93bfc-157">Logic Apps has various functions for working with strings.</span></span> <span data-ttu-id="93bfc-158">For example, suppose you want to pass a company name from an order to another system.</span><span class="sxs-lookup"><span data-stu-id="93bfc-158">For example, suppose you want to pass a company name from an order to another system.</span></span> <span data-ttu-id="93bfc-159">However, you're not sure about proper handling for character encoding.</span><span class="sxs-lookup"><span data-stu-id="93bfc-159">However, you're not sure about proper handling for character encoding.</span></span> <span data-ttu-id="93bfc-160">You could perform base64 encoding on this string, but to avoid escapes in the URL, you can replace several characters instead.</span><span class="sxs-lookup"><span data-stu-id="93bfc-160">You could perform base64 encoding on this string, but to avoid escapes in the URL, you can replace several characters instead.</span></span> <span data-ttu-id="93bfc-161">Also, you only need a substring for the company name because the first five characters are not used.</span><span class="sxs-lookup"><span data-stu-id="93bfc-161">Also, you only need a substring for the company name because the first five characters are not used.</span></span> 

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "companyName": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "Request",
      "kind": "Http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').companyName,5,sub(length(parameters('order').companyName), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="93bfc-162">These steps describe how this example processes this string, working from the inside to the outside:</span><span class="sxs-lookup"><span data-stu-id="93bfc-162">These steps describe how this example processes this string, working from the inside to the outside:</span></span>

``` 
"uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').companyName,5,sub(length(parameters('order').companyName), 5) )),'+','-') ,'/' ,'_' )}"
```

1. <span data-ttu-id="93bfc-163">Get the [`length()`](../logic-apps/logic-apps-workflow-definition-language.md) for the company name, so you get the total number of characters.</span><span class="sxs-lookup"><span data-stu-id="93bfc-163">Get the [`length()`](../logic-apps/logic-apps-workflow-definition-language.md) for the company name, so you get the total number of characters.</span></span>

2. <span data-ttu-id="93bfc-164">To get a shorter string, subtract `5`.</span><span class="sxs-lookup"><span data-stu-id="93bfc-164">To get a shorter string, subtract `5`.</span></span>

3. <span data-ttu-id="93bfc-165">Now get a [`substring()`](../logic-apps/logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="93bfc-165">Now get a [`substring()`](../logic-apps/logic-apps-workflow-definition-language.md).</span></span> <span data-ttu-id="93bfc-166">Start at index `5`, and go to the remainder of the string.</span><span class="sxs-lookup"><span data-stu-id="93bfc-166">Start at index `5`, and go to the remainder of the string.</span></span>

4. <span data-ttu-id="93bfc-167">Convert this substring to a [`base64()`](../logic-apps/logic-apps-workflow-definition-language.md) string.</span><span class="sxs-lookup"><span data-stu-id="93bfc-167">Convert this substring to a [`base64()`](../logic-apps/logic-apps-workflow-definition-language.md) string.</span></span>

5. <span data-ttu-id="93bfc-168">Now [`replace()`](../logic-apps/logic-apps-workflow-definition-language.md) all the `+` characters with `-` characters.</span><span class="sxs-lookup"><span data-stu-id="93bfc-168">Now [`replace()`](../logic-apps/logic-apps-workflow-definition-language.md) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="93bfc-169">Finally, [`replace()`](../logic-apps/logic-apps-workflow-definition-language.md) all the `/` characters with `_` characters.</span><span class="sxs-lookup"><span data-stu-id="93bfc-169">Finally, [`replace()`](../logic-apps/logic-apps-workflow-definition-language.md) all the `/` characters with `_` characters.</span></span>

## <a name="map-list-items-to-property-values-then-use-maps-as-parameters"></a><span data-ttu-id="93bfc-170">Map list items to property values, then use maps as parameters</span><span class="sxs-lookup"><span data-stu-id="93bfc-170">Map list items to property values, then use maps as parameters</span></span>

<span data-ttu-id="93bfc-171">To get different results based a property's value, you can create a map that matches each property value to a result, then use that map as a parameter.</span><span class="sxs-lookup"><span data-stu-id="93bfc-171">To get different results based a property's value, you can create a map that matches each property value to a result, then use that map as a parameter.</span></span> 

<span data-ttu-id="93bfc-172">For example, this workflow defines some categories as parameters and a map that matches those categories with a specific URL.</span><span class="sxs-lookup"><span data-stu-id="93bfc-172">For example, this workflow defines some categories as parameters and a map that matches those categories with a specific URL.</span></span> <span data-ttu-id="93bfc-173">First, the workflow gets a list of articles.</span><span class="sxs-lookup"><span data-stu-id="93bfc-173">First, the workflow gets a list of articles.</span></span> <span data-ttu-id="93bfc-174">Then, the workflow uses the map to find the URL matching the category for each article.</span><span class="sxs-lookup"><span data-stu-id="93bfc-174">Then, the workflow uses the map to find the URL matching the category for each article.</span></span>

*   <span data-ttu-id="93bfc-175">The [`intersection()`](../logic-apps/logic-apps-workflow-definition-language.md) function checks whether the category matches a known defined category.</span><span class="sxs-lookup"><span data-stu-id="93bfc-175">The [`intersection()`](../logic-apps/logic-apps-workflow-definition-language.md) function checks whether the category matches a known defined category.</span></span>

*   <span data-ttu-id="93bfc-176">After getting a matching category, the example pulls the item from the map using square brackets: `parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="93bfc-176">After getting a matching category, the example pulls the item from the map using square brackets: `parameters[...]`</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

## <a name="get-data-with-date-functions"></a><span data-ttu-id="93bfc-177">Get data with Date functions</span><span class="sxs-lookup"><span data-stu-id="93bfc-177">Get data with Date functions</span></span>

<span data-ttu-id="93bfc-178">To get data from a data source that doesn't natively support *triggers*, you can use Date functions for working with times and dates instead.</span><span class="sxs-lookup"><span data-stu-id="93bfc-178">To get data from a data source that doesn't natively support *triggers*, you can use Date functions for working with times and dates instead.</span></span> <span data-ttu-id="93bfc-179">For example, this expression finds how long this workflow's steps are taking, working from the inside to the outside:</span><span class="sxs-lookup"><span data-stu-id="93bfc-179">For example, this expression finds how long this workflow's steps are taking, working from the inside to the outside:</span></span>

``` json
"expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
```

1. <span data-ttu-id="93bfc-180">From the `order` action, extract the `startTime`.</span><span class="sxs-lookup"><span data-stu-id="93bfc-180">From the `order` action, extract the `startTime`.</span></span> 
2. <span data-ttu-id="93bfc-181">Get the current time with `utcNow()`.</span><span class="sxs-lookup"><span data-stu-id="93bfc-181">Get the current time with `utcNow()`.</span></span>
3. <span data-ttu-id="93bfc-182">Subtract one second:</span><span class="sxs-lookup"><span data-stu-id="93bfc-182">Subtract one second:</span></span>

   [`addseconds(..., -1)`](../logic-apps/logic-apps-workflow-definition-language.md) 

   <span data-ttu-id="93bfc-183">You can use other units of time, like `minutes` or `hours`.</span><span class="sxs-lookup"><span data-stu-id="93bfc-183">You can use other units of time, like `minutes` or `hours`.</span></span> 

3. <span data-ttu-id="93bfc-184">Now, you can compare these two values.</span><span class="sxs-lookup"><span data-stu-id="93bfc-184">Now, you can compare these two values.</span></span> 

   <span data-ttu-id="93bfc-185">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span><span class="sxs-lookup"><span data-stu-id="93bfc-185">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="93bfc-186">To format dates, you can use string formatters.</span><span class="sxs-lookup"><span data-stu-id="93bfc-186">To format dates, you can use string formatters.</span></span> <span data-ttu-id="93bfc-187">For example, to get the RFC1123, use [`utcnow('r')`](../logic-apps/logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="93bfc-187">For example, to get the RFC1123, use [`utcnow('r')`](../logic-apps/logic-apps-workflow-definition-language.md).</span></span> <span data-ttu-id="93bfc-188">Learn more about [date formatting](../logic-apps/logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="93bfc-188">Learn more about [date formatting](../logic-apps/logic-apps-workflow-definition-language.md).</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder-id"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```


## <a name="next-steps"></a><span data-ttu-id="93bfc-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="93bfc-189">Next steps</span></span>

* [<span data-ttu-id="93bfc-190">Run steps based on a condition (conditional statements)</span><span class="sxs-lookup"><span data-stu-id="93bfc-190">Run steps based on a condition (conditional statements)</span></span>](../logic-apps/logic-apps-control-flow-conditional-statement.md)
* [<span data-ttu-id="93bfc-191">Run steps based on different values (switch statements)</span><span class="sxs-lookup"><span data-stu-id="93bfc-191">Run steps based on different values (switch statements)</span></span>](../logic-apps/logic-apps-control-flow-switch-statement.md)
* [<span data-ttu-id="93bfc-192">Run and repeat steps (loops)</span><span class="sxs-lookup"><span data-stu-id="93bfc-192">Run and repeat steps (loops)</span></span>](../logic-apps/logic-apps-control-flow-loops.md)
* [<span data-ttu-id="93bfc-193">Run or merge parallel steps (branches)</span><span class="sxs-lookup"><span data-stu-id="93bfc-193">Run or merge parallel steps (branches)</span></span>](../logic-apps/logic-apps-control-flow-branches.md)
* [<span data-ttu-id="93bfc-194">Run steps based on grouped action status (scopes)</span><span class="sxs-lookup"><span data-stu-id="93bfc-194">Run steps based on grouped action status (scopes)</span></span>](../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md)
* <span data-ttu-id="93bfc-195">Learn more about the [Workflow Definition Language schema for Azure Logic Apps](../logic-apps/logic-apps-workflow-definition-language.md)</span><span class="sxs-lookup"><span data-stu-id="93bfc-195">Learn more about the [Workflow Definition Language schema for Azure Logic Apps](../logic-apps/logic-apps-workflow-definition-language.md)</span></span>
* <span data-ttu-id="93bfc-196">Learn more about [workflow actions and triggers for Azure Logic Apps](../logic-apps/logic-apps-workflow-actions-triggers.md)</span><span class="sxs-lookup"><span data-stu-id="93bfc-196">Learn more about [workflow actions and triggers for Azure Logic Apps](../logic-apps/logic-apps-workflow-actions-triggers.md)</span></span>