---
title: Transform XML between formats - Azure Logic Apps | Microsoft Docs
description: Create transforms or maps that convert XML between formats in Azure Logic Apps with Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.date: 07/08/2016
ms.openlocfilehash: 9dd471f70407191734b4c5a3aa84d5365a7beab8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818238"
---
# <a name="create-maps-that-transform-xml-between-formats-in-azure-logic-apps-with-enterprise-integration-pack"></a><span data-ttu-id="48723-103">Create maps that transform XML between formats in Azure Logic Apps with Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="48723-103">Create maps that transform XML between formats in Azure Logic Apps with Enterprise Integration Pack</span></span>

<span data-ttu-id="48723-104">The Enterprise integration Transform connector converts data from one format to another format.</span><span class="sxs-lookup"><span data-stu-id="48723-104">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="48723-105">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span><span class="sxs-lookup"><span data-stu-id="48723-105">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="48723-106">You can use a transform to reformat the date to be in the MonthDayYear format.</span><span class="sxs-lookup"><span data-stu-id="48723-106">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="48723-107">What does a transform do?</span><span class="sxs-lookup"><span data-stu-id="48723-107">What does a transform do?</span></span>
<span data-ttu-id="48723-108">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span><span class="sxs-lookup"><span data-stu-id="48723-108">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="48723-109">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span><span class="sxs-lookup"><span data-stu-id="48723-109">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="48723-110">How to create a transform?</span><span class="sxs-lookup"><span data-stu-id="48723-110">How to create a transform?</span></span>
<span data-ttu-id="48723-111">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="48723-111">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="48723-112">When you are finished creating and testing the transform, you upload the transform into your integration account.</span><span class="sxs-lookup"><span data-stu-id="48723-112">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="48723-113">How to use a transform</span><span class="sxs-lookup"><span data-stu-id="48723-113">How to use a transform</span></span>
<span data-ttu-id="48723-114">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span><span class="sxs-lookup"><span data-stu-id="48723-114">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="48723-115">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span><span class="sxs-lookup"><span data-stu-id="48723-115">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="48723-116">**Here are the steps to use a transform**:</span><span class="sxs-lookup"><span data-stu-id="48723-116">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="48723-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48723-117">Prerequisites</span></span>

* <span data-ttu-id="48723-118">Create an integration account and add a map to it</span><span class="sxs-lookup"><span data-stu-id="48723-118">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="48723-119">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span><span class="sxs-lookup"><span data-stu-id="48723-119">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="48723-120">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span><span class="sxs-lookup"><span data-stu-id="48723-120">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="48723-121">Add a **Request** trigger to your Logic app</span><span class="sxs-lookup"><span data-stu-id="48723-121">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="48723-122">Add the **Transform XML** action by first selecting **Add an action** </span><span class="sxs-lookup"><span data-stu-id="48723-122">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="48723-123">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span><span class="sxs-lookup"><span data-stu-id="48723-123">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="48723-124">Select the **Transform XML** action</span><span class="sxs-lookup"><span data-stu-id="48723-124">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="48723-125">Add the XML **CONTENT** that you transform.</span><span class="sxs-lookup"><span data-stu-id="48723-125">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="48723-126">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span><span class="sxs-lookup"><span data-stu-id="48723-126">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="48723-127">In this example, select the body of the HTTP request that triggered the Logic app.</span><span class="sxs-lookup"><span data-stu-id="48723-127">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="48723-128">Make sure that the content for the **Transform XML** is XML.</span><span class="sxs-lookup"><span data-stu-id="48723-128">Make sure that the content for the **Transform XML** is XML.</span></span> <span data-ttu-id="48723-129">If the content is not in XML or is base64-encoded, you must specify an expression that processes the content.</span><span class="sxs-lookup"><span data-stu-id="48723-129">If the content is not in XML or is base64-encoded, you must specify an expression that processes the content.</span></span> <span data-ttu-id="48723-130">For example, you can use [functions](logic-apps-workflow-definition-language.md#functions), like ```@base64ToBinary``` for decoding content or ```@xml``` for processing the content as XML.</span><span class="sxs-lookup"><span data-stu-id="48723-130">For example, you can use [functions](logic-apps-workflow-definition-language.md#functions), like ```@base64ToBinary``` for decoding content or ```@xml``` for processing the content as XML.</span></span>
 

7. <span data-ttu-id="48723-131">Select the name of the **MAP** that you want to use to perform the transformation.</span><span class="sxs-lookup"><span data-stu-id="48723-131">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="48723-132">The map must already be in your integration account.</span><span class="sxs-lookup"><span data-stu-id="48723-132">The map must already be in your integration account.</span></span> <span data-ttu-id="48723-133">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span><span class="sxs-lookup"><span data-stu-id="48723-133">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="48723-134">Save your work</span><span class="sxs-lookup"><span data-stu-id="48723-134">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="48723-135">At this point, you are finished setting up your map.</span><span class="sxs-lookup"><span data-stu-id="48723-135">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="48723-136">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span><span class="sxs-lookup"><span data-stu-id="48723-136">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="48723-137">You can easily as an action to send the output of the transform to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="48723-137">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="48723-138">You can now test your transform by making a request to the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="48723-138">You can now test your transform by making a request to the HTTP endpoint.</span></span>  


## <a name="features-and-use-cases"></a><span data-ttu-id="48723-139">Features and use cases</span><span class="sxs-lookup"><span data-stu-id="48723-139">Features and use cases</span></span>
* <span data-ttu-id="48723-140">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span><span class="sxs-lookup"><span data-stu-id="48723-140">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="48723-141">Or, you can create more complex transformations using the out-of-the-box map operations.</span><span class="sxs-lookup"><span data-stu-id="48723-141">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="48723-142">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span><span class="sxs-lookup"><span data-stu-id="48723-142">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="48723-143">You can do a direct data copy between the schemas.</span><span class="sxs-lookup"><span data-stu-id="48723-143">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="48723-144">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span><span class="sxs-lookup"><span data-stu-id="48723-144">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="48723-145">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span><span class="sxs-lookup"><span data-stu-id="48723-145">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="48723-146">Use the Test Map feature to add a sample XML message.</span><span class="sxs-lookup"><span data-stu-id="48723-146">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="48723-147">With a simple click, you can test the map you created, and see the generated output.</span><span class="sxs-lookup"><span data-stu-id="48723-147">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="48723-148">Upload existing maps</span><span class="sxs-lookup"><span data-stu-id="48723-148">Upload existing maps</span></span>  
* <span data-ttu-id="48723-149">Includes support for the XML format.</span><span class="sxs-lookup"><span data-stu-id="48723-149">Includes support for the XML format.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="48723-150">Advanced features</span><span class="sxs-lookup"><span data-stu-id="48723-150">Advanced features</span></span>

### <a name="reference-assembly-or-custom-code-from-maps"></a><span data-ttu-id="48723-151">Reference assembly or custom code from maps</span><span class="sxs-lookup"><span data-stu-id="48723-151">Reference assembly or custom code from maps</span></span> 
<span data-ttu-id="48723-152">The transform action also supports maps or transforms with reference to external assembly.</span><span class="sxs-lookup"><span data-stu-id="48723-152">The transform action also supports maps or transforms with reference to external assembly.</span></span> <span data-ttu-id="48723-153">This capability enables calls to custom .NET code directly from XSLT maps.</span><span class="sxs-lookup"><span data-stu-id="48723-153">This capability enables calls to custom .NET code directly from XSLT maps.</span></span> <span data-ttu-id="48723-154">Here are the prerequisites to use assembly in maps.</span><span class="sxs-lookup"><span data-stu-id="48723-154">Here are the prerequisites to use assembly in maps.</span></span>

* <span data-ttu-id="48723-155">The map and the assembly referenced from the map needs to be [uploaded to integration account](./logic-apps-enterprise-integration-maps.md).</span><span class="sxs-lookup"><span data-stu-id="48723-155">The map and the assembly referenced from the map needs to be [uploaded to integration account](./logic-apps-enterprise-integration-maps.md).</span></span> 

  > [!NOTE]
  > <span data-ttu-id="48723-156">Map and assembly are required to be uploaded in a specific order.</span><span class="sxs-lookup"><span data-stu-id="48723-156">Map and assembly are required to be uploaded in a specific order.</span></span> <span data-ttu-id="48723-157">You must upload the assembly before you upload the map that references the assembly.</span><span class="sxs-lookup"><span data-stu-id="48723-157">You must upload the assembly before you upload the map that references the assembly.</span></span>

* <span data-ttu-id="48723-158">The map must also have these attributes and a CDATA section that contains the call to the assembly code:</span><span class="sxs-lookup"><span data-stu-id="48723-158">The map must also have these attributes and a CDATA section that contains the call to the assembly code:</span></span>

    * <span data-ttu-id="48723-159">**name** is the custom assembly name.</span><span class="sxs-lookup"><span data-stu-id="48723-159">**name** is the custom assembly name.</span></span>
    * <span data-ttu-id="48723-160">**namespace** is the namespace in your assembly that includes the custom code.</span><span class="sxs-lookup"><span data-stu-id="48723-160">**namespace** is the namespace in your assembly that includes the custom code.</span></span>

  <span data-ttu-id="48723-161">This example shows a map that references an assembly named "XslUtilitiesLib" and calls the `circumreference` method from the assembly.</span><span class="sxs-lookup"><span data-stu-id="48723-161">This example shows a map that references an assembly named "XslUtilitiesLib" and calls the `circumreference` method from the assembly.</span></span>

  ````xml
  <?xml version="1.0" encoding="UTF-8"?>
  <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="urn:my-scripts">
  <msxsl:script language="C#" implements-prefix="user">
    <msxsl:assembly name="XsltHelperLib"/>
    <msxsl:using namespace="XsltHelpers"/>
    <![CDATA[public double circumference(int radius){ XsltHelper helper = new XsltHelper(); return helper.circumference(radius); }]]>
  </msxsl:script>
  <xsl:template match="data">
     <circles>
        <xsl:for-each select="circle">
            <circle>
                <xsl:copy-of select="node()"/>
                    <circumference>
                        <xsl:value-of select="user:circumference(radius)"/>
                    </circumference>
            </circle>
        </xsl:for-each>
     </circles>
    </xsl:template>
    </xsl:stylesheet>
  ````


### <a name="byte-order-mark"></a><span data-ttu-id="48723-162">Byte Order Mark</span><span class="sxs-lookup"><span data-stu-id="48723-162">Byte Order Mark</span></span>
<span data-ttu-id="48723-163">By default, the response from the transformation starts with the Byte Order Mark (BOM).</span><span class="sxs-lookup"><span data-stu-id="48723-163">By default, the response from the transformation starts with the Byte Order Mark (BOM).</span></span> <span data-ttu-id="48723-164">You can access this functionality only while working in the Code View editor.</span><span class="sxs-lookup"><span data-stu-id="48723-164">You can access this functionality only while working in the Code View editor.</span></span> <span data-ttu-id="48723-165">To disable this functionality, specify `disableByteOrderMark` for the `transformOptions` property:</span><span class="sxs-lookup"><span data-stu-id="48723-165">To disable this functionality, specify `disableByteOrderMark` for the `transformOptions` property:</span></span>

````json
"Transform_XML": {
    "inputs": {
        "content": "@{triggerBody()}",
        "integrationAccount": {
            "map": {
                "name": "TestMap"
            }
        },
        "transformOptions": "disableByteOrderMark"
    },
    "runAfter": {},
    "type": "Xslt"
}
````





## <a name="learn-more"></a><span data-ttu-id="48723-166">Learn more</span><span class="sxs-lookup"><span data-stu-id="48723-166">Learn more</span></span>
* [<span data-ttu-id="48723-167">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="48723-167">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")  
* [<span data-ttu-id="48723-168">Learn more about maps</span><span class="sxs-lookup"><span data-stu-id="48723-168">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Learn about enterprise integration maps")  

