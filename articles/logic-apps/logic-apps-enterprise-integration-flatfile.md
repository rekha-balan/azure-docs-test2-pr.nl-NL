---
title: Encode or decode flat files in Azure logic apps | Microsoft Docs
description: How to use the file file encoder or decoder in the Enterprise Integration Pack in your logic apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: mandia
ms.openlocfilehash: 9270ed300e2971440ca89fc2550b722318edc255
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550328"
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a><span data-ttu-id="e5b75-103">Overview of enterprise integration with flat files</span><span class="sxs-lookup"><span data-stu-id="e5b75-103">Overview of enterprise integration with flat files</span></span>

<span data-ttu-id="e5b75-104">You may want to encode XML content before you send it to a business partner in a business-to-business (B2B) scenario.</span><span class="sxs-lookup"><span data-stu-id="e5b75-104">You may want to encode XML content before you send it to a business partner in a business-to-business (B2B) scenario.</span></span> <span data-ttu-id="e5b75-105">In a logic app, you can use the flat file encoding connector to do this.</span><span class="sxs-lookup"><span data-stu-id="e5b75-105">In a logic app, you can use the flat file encoding connector to do this.</span></span> <span data-ttu-id="e5b75-106">The logic app that you create can get its XML content from a variety of sources, including from an HTTP request trigger, from another application, or even from one of the many [connectors](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e5b75-106">The logic app that you create can get its XML content from a variety of sources, including from an HTTP request trigger, from another application, or even from one of the many [connectors](../connectors/apis-list.md).</span></span> <span data-ttu-id="e5b75-107">For more information about logic apps, see the [logic apps documentation](logic-apps-what-are-logic-apps.md "Learn more about Logic apps").</span><span class="sxs-lookup"><span data-stu-id="e5b75-107">For more information about logic apps, see the [logic apps documentation](logic-apps-what-are-logic-apps.md "Learn more about Logic apps").</span></span>  

## <a name="create-the-flat-file-encoding-connector"></a><span data-ttu-id="e5b75-108">Create the flat file encoding connector</span><span class="sxs-lookup"><span data-stu-id="e5b75-108">Create the flat file encoding connector</span></span>
<span data-ttu-id="e5b75-109">Follow these steps to add a flat file encoding connector to your logic app.</span><span class="sxs-lookup"><span data-stu-id="e5b75-109">Follow these steps to add a flat file encoding connector to your logic app.</span></span>

1. <span data-ttu-id="e5b75-110">Create a logic app and [link it to your integration account](logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app").</span><span class="sxs-lookup"><span data-stu-id="e5b75-110">Create a logic app and [link it to your integration account](logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app").</span></span> <span data-ttu-id="e5b75-111">This account contains the schema you will use to encode the XML data.</span><span class="sxs-lookup"><span data-stu-id="e5b75-111">This account contains the schema you will use to encode the XML data.</span></span>  
2. <span data-ttu-id="e5b75-112">Add a **Request - When an HTTP request is received** trigger to your logic app.</span><span class="sxs-lookup"><span data-stu-id="e5b75-112">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>  
   <span data-ttu-id="e5b75-113">![Screenshot of trigger to select](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="e5b75-113">![Screenshot of trigger to select](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
3. <span data-ttu-id="e5b75-114">Add the flat file encoding action, as follows:</span><span class="sxs-lookup"><span data-stu-id="e5b75-114">Add the flat file encoding action, as follows:</span></span>
   
    <span data-ttu-id="e5b75-115">a.</span><span class="sxs-lookup"><span data-stu-id="e5b75-115">a.</span></span> <span data-ttu-id="e5b75-116">Select the **plus** sign.</span><span class="sxs-lookup"><span data-stu-id="e5b75-116">Select the **plus** sign.</span></span>
   
    <span data-ttu-id="e5b75-117">b.</span><span class="sxs-lookup"><span data-stu-id="e5b75-117">b.</span></span> <span data-ttu-id="e5b75-118">Select the **Add an action** link (appears after you have selected the plus sign).</span><span class="sxs-lookup"><span data-stu-id="e5b75-118">Select the **Add an action** link (appears after you have selected the plus sign).</span></span>
   
    <span data-ttu-id="e5b75-119">c.</span><span class="sxs-lookup"><span data-stu-id="e5b75-119">c.</span></span> <span data-ttu-id="e5b75-120">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span><span class="sxs-lookup"><span data-stu-id="e5b75-120">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span></span>
   
    <span data-ttu-id="e5b75-121">d.</span><span class="sxs-lookup"><span data-stu-id="e5b75-121">d.</span></span> <span data-ttu-id="e5b75-122">Select the **Flat File Encoding** option from the list.</span><span class="sxs-lookup"><span data-stu-id="e5b75-122">Select the **Flat File Encoding** option from the list.</span></span>   
   <span data-ttu-id="e5b75-123">![Screenshot of Flat File Encoding option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="e5b75-123">![Screenshot of Flat File Encoding option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
4. <span data-ttu-id="e5b75-124">On the **Flat File Encoding** dialog box, select the **Content** text box.</span><span class="sxs-lookup"><span data-stu-id="e5b75-124">On the **Flat File Encoding** dialog box, select the **Content** text box.</span></span>  
   <span data-ttu-id="e5b75-125">![Screenshot of Content text box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span><span class="sxs-lookup"><span data-stu-id="e5b75-125">![Screenshot of Content text box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)</span></span>  
5. <span data-ttu-id="e5b75-126">Select the body tag as the content that you want to encode.</span><span class="sxs-lookup"><span data-stu-id="e5b75-126">Select the body tag as the content that you want to encode.</span></span> <span data-ttu-id="e5b75-127">The body tag will populate the content field.</span><span class="sxs-lookup"><span data-stu-id="e5b75-127">The body tag will populate the content field.</span></span>     
   ![Screenshot of body tag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. <span data-ttu-id="e5b75-129">Select the **Schema Name** list box, and choose the schema you want to use to encode the input content.</span><span class="sxs-lookup"><span data-stu-id="e5b75-129">Select the **Schema Name** list box, and choose the schema you want to use to encode the input content.</span></span>    
   <span data-ttu-id="e5b75-130">![Screenshot of Schema Name list box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span><span class="sxs-lookup"><span data-stu-id="e5b75-130">![Screenshot of Schema Name list box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)</span></span>  
7. <span data-ttu-id="e5b75-131">Save your work.</span><span class="sxs-lookup"><span data-stu-id="e5b75-131">Save your work.</span></span>   
   ![Screenshot of Save icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

<span data-ttu-id="e5b75-133">At this point, you are finished setting up your flat file encoding connector.</span><span class="sxs-lookup"><span data-stu-id="e5b75-133">At this point, you are finished setting up your flat file encoding connector.</span></span> <span data-ttu-id="e5b75-134">In a real world application, you may want to store the encoded data in a line-of-business application, such as Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e5b75-134">In a real world application, you may want to store the encoded data in a line-of-business application, such as Salesforce.</span></span> <span data-ttu-id="e5b75-135">Or you can send that encoded data to a trading partner.</span><span class="sxs-lookup"><span data-stu-id="e5b75-135">Or you can send that encoded data to a trading partner.</span></span> <span data-ttu-id="e5b75-136">You can easily add an action to send the output of the encoding action to Salesforce, or to your trading partner, by using any one of the other connectors provided.</span><span class="sxs-lookup"><span data-stu-id="e5b75-136">You can easily add an action to send the output of the encoding action to Salesforce, or to your trading partner, by using any one of the other connectors provided.</span></span>

<span data-ttu-id="e5b75-137">You can now test your connector by making a request to the HTTP endpoint, and including the XML content in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="e5b75-137">You can now test your connector by making a request to the HTTP endpoint, and including the XML content in the body of the request.</span></span>  

## <a name="create-the-flat-file-decoding-connector"></a><span data-ttu-id="e5b75-138">Create the flat file decoding connector</span><span class="sxs-lookup"><span data-stu-id="e5b75-138">Create the flat file decoding connector</span></span>

> [!NOTE]
> <span data-ttu-id="e5b75-139">To complete these steps, you need to have a schema file already uploaded into you integration account.</span><span class="sxs-lookup"><span data-stu-id="e5b75-139">To complete these steps, you need to have a schema file already uploaded into you integration account.</span></span>

1. <span data-ttu-id="e5b75-140">Add a **Request - When an HTTP request is received** trigger to your logic app.</span><span class="sxs-lookup"><span data-stu-id="e5b75-140">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>  
   <span data-ttu-id="e5b75-141">![Screenshot of trigger to select](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span><span class="sxs-lookup"><span data-stu-id="e5b75-141">![Screenshot of trigger to select](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b/flatfile-1.png)</span></span>    
2. <span data-ttu-id="e5b75-142">Add the flat file decoding action, as follows:</span><span class="sxs-lookup"><span data-stu-id="e5b75-142">Add the flat file decoding action, as follows:</span></span>
   
    <span data-ttu-id="e5b75-143">a.</span><span class="sxs-lookup"><span data-stu-id="e5b75-143">a.</span></span> <span data-ttu-id="e5b75-144">Select the **plus** sign.</span><span class="sxs-lookup"><span data-stu-id="e5b75-144">Select the **plus** sign.</span></span>
   
    <span data-ttu-id="e5b75-145">b.</span><span class="sxs-lookup"><span data-stu-id="e5b75-145">b.</span></span> <span data-ttu-id="e5b75-146">Select the **Add an action** link (appears after you have selected the plus sign).</span><span class="sxs-lookup"><span data-stu-id="e5b75-146">Select the **Add an action** link (appears after you have selected the plus sign).</span></span>
   
    <span data-ttu-id="e5b75-147">c.</span><span class="sxs-lookup"><span data-stu-id="e5b75-147">c.</span></span> <span data-ttu-id="e5b75-148">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span><span class="sxs-lookup"><span data-stu-id="e5b75-148">In the search box, enter *Flat* to filter all the actions to the one that you want to use.</span></span>
   
    <span data-ttu-id="e5b75-149">d.</span><span class="sxs-lookup"><span data-stu-id="e5b75-149">d.</span></span> <span data-ttu-id="e5b75-150">Select the **Flat File Decoding** option from the list.</span><span class="sxs-lookup"><span data-stu-id="e5b75-150">Select the **Flat File Decoding** option from the list.</span></span>   
   <span data-ttu-id="e5b75-151">![Screenshot of Flat File Decoding option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span><span class="sxs-lookup"><span data-stu-id="e5b75-151">![Screenshot of Flat File Decoding option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)</span></span>   
3. <span data-ttu-id="e5b75-152">Select the **Content** control.</span><span class="sxs-lookup"><span data-stu-id="e5b75-152">Select the **Content** control.</span></span> <span data-ttu-id="e5b75-153">This produces a list of the content from earlier steps that you can use as the content to decode.</span><span class="sxs-lookup"><span data-stu-id="e5b75-153">This produces a list of the content from earlier steps that you can use as the content to decode.</span></span> <span data-ttu-id="e5b75-154">Notice that the *Body* from the incoming HTTP request is available to be used as the content to decode.</span><span class="sxs-lookup"><span data-stu-id="e5b75-154">Notice that the *Body* from the incoming HTTP request is available to be used as the content to decode.</span></span> <span data-ttu-id="e5b75-155">You can also enter the content to decode directly into the **Content** control.</span><span class="sxs-lookup"><span data-stu-id="e5b75-155">You can also enter the content to decode directly into the **Content** control.</span></span>     
4. <span data-ttu-id="e5b75-156">Select the *Body* tag.</span><span class="sxs-lookup"><span data-stu-id="e5b75-156">Select the *Body* tag.</span></span> <span data-ttu-id="e5b75-157">Notice the body tag is now in the **Content** control.</span><span class="sxs-lookup"><span data-stu-id="e5b75-157">Notice the body tag is now in the **Content** control.</span></span>
5. <span data-ttu-id="e5b75-158">Select the name of the schema that you want to use to decode the content.</span><span class="sxs-lookup"><span data-stu-id="e5b75-158">Select the name of the schema that you want to use to decode the content.</span></span> <span data-ttu-id="e5b75-159">The following screenshot shows that *OrderFile* is the selected schema name.</span><span class="sxs-lookup"><span data-stu-id="e5b75-159">The following screenshot shows that *OrderFile* is the selected schema name.</span></span> <span data-ttu-id="e5b75-160">This schema name had been uploaded into the integration account previously.</span><span class="sxs-lookup"><span data-stu-id="e5b75-160">This schema name had been uploaded into the integration account previously.</span></span>
   
   ![Screenshot of Flat File Decoding dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. <span data-ttu-id="e5b75-162">Save your work.</span><span class="sxs-lookup"><span data-stu-id="e5b75-162">Save your work.</span></span>  
   ![Screenshot of Save icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

<span data-ttu-id="e5b75-164">At this point, you are finished setting up your flat file decoding connector.</span><span class="sxs-lookup"><span data-stu-id="e5b75-164">At this point, you are finished setting up your flat file decoding connector.</span></span> <span data-ttu-id="e5b75-165">In a real world application, you may want to store the decoded data in a line-of-business application such as Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e5b75-165">In a real world application, you may want to store the decoded data in a line-of-business application such as Salesforce.</span></span> <span data-ttu-id="e5b75-166">You can easily add an action to send the output of the decoding action to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e5b75-166">You can easily add an action to send the output of the decoding action to Salesforce.</span></span>

<span data-ttu-id="e5b75-167">You can now test your connector by making a request to the HTTP endpoint and including the XML content you want to decode in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="e5b75-167">You can now test your connector by making a request to the HTTP endpoint and including the XML content you want to decode in the body of the request.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e5b75-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5b75-168">Next steps</span></span>
* <span data-ttu-id="e5b75-169">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack").</span><span class="sxs-lookup"><span data-stu-id="e5b75-169">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack").</span></span>  











