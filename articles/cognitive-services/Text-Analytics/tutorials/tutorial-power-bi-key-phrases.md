---
title: Text Analytics With Power BI - Azure Cognitive Services | Microsoft Docs
description: Learn how to use Text Analytics to extract key phrases from text stored in Power BI.
services: cognitive-services
author: luiscabrer
manager: cgronlun
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: tutorial
ms.date: 3/07/2018
ms.author: luisca
ms.openlocfilehash: 2cdb93d44218627efdcb0360d8cf4a4eeeca177a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870635"
---
# <a name="text-analytics-with-power-bi"></a><span data-ttu-id="f889a-103">Text Analytics with Power BI</span><span class="sxs-lookup"><span data-stu-id="f889a-103">Text Analytics with Power BI</span></span>

<span data-ttu-id="f889a-104">Microsoft Power BI distills organizational data into beautiful reports, which you can distribute across your organization for faster, deeper insight.</span><span class="sxs-lookup"><span data-stu-id="f889a-104">Microsoft Power BI distills organizational data into beautiful reports, which you can distribute across your organization for faster, deeper insight.</span></span> <span data-ttu-id="f889a-105">The Text Analytics service, part of Cognitive Services in Microsoft Azure, can extract the most important phrases from text via its Key Phrases API.</span><span class="sxs-lookup"><span data-stu-id="f889a-105">The Text Analytics service, part of Cognitive Services in Microsoft Azure, can extract the most important phrases from text via its Key Phrases API.</span></span> <span data-ttu-id="f889a-106">Together, these tools can help you quickly see what your customers are talking about and how they feel about it.</span><span class="sxs-lookup"><span data-stu-id="f889a-106">Together, these tools can help you quickly see what your customers are talking about and how they feel about it.</span></span>

<span data-ttu-id="f889a-107">In this tutorial, you can see how to integrate Power BI Desktop and the Key Phrases API to extract the most important phrases from customer feedback using a custom Power Query function.</span><span class="sxs-lookup"><span data-stu-id="f889a-107">In this tutorial, you can see how to integrate Power BI Desktop and the Key Phrases API to extract the most important phrases from customer feedback using a custom Power Query function.</span></span> <span data-ttu-id="f889a-108">We also create a Word Cloud from these phrases.</span><span class="sxs-lookup"><span data-stu-id="f889a-108">We also create a Word Cloud from these phrases.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f889a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f889a-109">Prerequisites</span></span>

<span data-ttu-id="f889a-110">To do this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="f889a-110">To do this tutorial, you need:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f889a-111">Microsoft Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f889a-111">Microsoft Power BI Desktop.</span></span> <span data-ttu-id="f889a-112">[Download at no charge](https://powerbi.microsoft.com/get-started/).</span><span class="sxs-lookup"><span data-stu-id="f889a-112">[Download at no charge](https://powerbi.microsoft.com/get-started/).</span></span>
> * <span data-ttu-id="f889a-113">A Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="f889a-113">A Microsoft Azure account.</span></span> <span data-ttu-id="f889a-114">[Start a free trial](https://azure.microsoft.com/free/) or [sign in](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f889a-114">[Start a free trial](https://azure.microsoft.com/free/) or [sign in](https://portal.azure.com/).</span></span>
> * <span data-ttu-id="f889a-115">An access key for Text Analytics.</span><span class="sxs-lookup"><span data-stu-id="f889a-115">An access key for Text Analytics.</span></span> <span data-ttu-id="f889a-116">[Sign up](../../cognitive-services-apis-create-account.md), then [get your key](../how-tos/text-analytics-how-to-access-key.md).</span><span class="sxs-lookup"><span data-stu-id="f889a-116">[Sign up](../../cognitive-services-apis-create-account.md), then [get your key](../how-tos/text-analytics-how-to-access-key.md).</span></span>
> * <span data-ttu-id="f889a-117">Customer comments.</span><span class="sxs-lookup"><span data-stu-id="f889a-117">Customer comments.</span></span> <span data-ttu-id="f889a-118">[Get our example data](https://aka.ms/cogsvc/ta) or use your own.</span><span class="sxs-lookup"><span data-stu-id="f889a-118">[Get our example data](https://aka.ms/cogsvc/ta) or use your own.</span></span>

## <a name="loading-customer-data"></a><span data-ttu-id="f889a-119">Loading customer data</span><span class="sxs-lookup"><span data-stu-id="f889a-119">Loading customer data</span></span>

<span data-ttu-id="f889a-120">To get started, open Power BI Desktop and load the Comma-Separated Value (CSV) file **FabrikamComments.csv**.</span><span class="sxs-lookup"><span data-stu-id="f889a-120">To get started, open Power BI Desktop and load the Comma-Separated Value (CSV) file **FabrikamComments.csv**.</span></span> <span data-ttu-id="f889a-121">This file represents a day's worth of hypothetical activity in a fictional small company's support forum.</span><span class="sxs-lookup"><span data-stu-id="f889a-121">This file represents a day's worth of hypothetical activity in a fictional small company's support forum.</span></span>

> [!NOTE]
> <span data-ttu-id="f889a-122">Power BI can use data from a wide variety of sources, such as Facebook or a SQL database.</span><span class="sxs-lookup"><span data-stu-id="f889a-122">Power BI can use data from a wide variety of sources, such as Facebook or a SQL database.</span></span> <span data-ttu-id="f889a-123">Learn more at [Facebook integration with Power BI](https://powerbi.microsoft.com/integrations/facebook/) and [SQL Server integration with Power BI](https://powerbi.microsoft.com/integrations/sql-server/).</span><span class="sxs-lookup"><span data-stu-id="f889a-123">Learn more at [Facebook integration with Power BI](https://powerbi.microsoft.com/integrations/facebook/) and [SQL Server integration with Power BI](https://powerbi.microsoft.com/integrations/sql-server/).</span></span>

<span data-ttu-id="f889a-124">In the main Power BI Desktop window, find the External Data group of the Home ribbon.</span><span class="sxs-lookup"><span data-stu-id="f889a-124">In the main Power BI Desktop window, find the External Data group of the Home ribbon.</span></span> <span data-ttu-id="f889a-125">Choose **Text/CSV** in the **Get Data** drop-down menu in this group.</span><span class="sxs-lookup"><span data-stu-id="f889a-125">Choose **Text/CSV** in the **Get Data** drop-down menu in this group.</span></span>

![[The Get Data button]](../media/tutorials/power-bi/get-data-button.png)

<span data-ttu-id="f889a-127">The Open dialog appears.</span><span class="sxs-lookup"><span data-stu-id="f889a-127">The Open dialog appears.</span></span> <span data-ttu-id="f889a-128">Navigate to your Downloads folder, or whatever folder contains the sample data file.</span><span class="sxs-lookup"><span data-stu-id="f889a-128">Navigate to your Downloads folder, or whatever folder contains the sample data file.</span></span> <span data-ttu-id="f889a-129">Click `FabrikamComments.csv`, then the **Open** button.</span><span class="sxs-lookup"><span data-stu-id="f889a-129">Click `FabrikamComments.csv`, then the **Open** button.</span></span> <span data-ttu-id="f889a-130">The CSV import dialog appears.</span><span class="sxs-lookup"><span data-stu-id="f889a-130">The CSV import dialog appears.</span></span>

![[The CSV Import dialog]](../media/tutorials/power-bi/csv-import.png)

<span data-ttu-id="f889a-132">The CSV import dialog lets you verify that Power BI Desktop has correctly detected the character set, delimiter, header rows, and column types.</span><span class="sxs-lookup"><span data-stu-id="f889a-132">The CSV import dialog lets you verify that Power BI Desktop has correctly detected the character set, delimiter, header rows, and column types.</span></span> <span data-ttu-id="f889a-133">This information is all correct, so we click **Load**.</span><span class="sxs-lookup"><span data-stu-id="f889a-133">This information is all correct, so we click **Load**.</span></span>

<span data-ttu-id="f889a-134">To see the loaded data, switch to the Data view using the Data View button along the left edge of the Power BI workspace.</span><span class="sxs-lookup"><span data-stu-id="f889a-134">To see the loaded data, switch to the Data view using the Data View button along the left edge of the Power BI workspace.</span></span> <span data-ttu-id="f889a-135">A table opens containing our data, like in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="f889a-135">A table opens containing our data, like in Microsoft Excel.</span></span>

![[The initial view of the imported data]](../media/tutorials/power-bi/initial-data-view.png)

## <a name="preparing-the-data"></a><span data-ttu-id="f889a-137">Preparing the data</span><span class="sxs-lookup"><span data-stu-id="f889a-137">Preparing the data</span></span>

<span data-ttu-id="f889a-138">You may need to transform your data in Power BI Desktop before it's ready to be processed by the Key Phrases service.</span><span class="sxs-lookup"><span data-stu-id="f889a-138">You may need to transform your data in Power BI Desktop before it's ready to be processed by the Key Phrases service.</span></span>

<span data-ttu-id="f889a-139">Our data, for example, contains both a `subject` field and a `comment` field.</span><span class="sxs-lookup"><span data-stu-id="f889a-139">Our data, for example, contains both a `subject` field and a `comment` field.</span></span> <span data-ttu-id="f889a-140">We should consider text in both of these fields, not just `comment`, when we extract key phrases.</span><span class="sxs-lookup"><span data-stu-id="f889a-140">We should consider text in both of these fields, not just `comment`, when we extract key phrases.</span></span> <span data-ttu-id="f889a-141">The Merge Columns function in Power BI Desktop makes this task easy.</span><span class="sxs-lookup"><span data-stu-id="f889a-141">The Merge Columns function in Power BI Desktop makes this task easy.</span></span>

<span data-ttu-id="f889a-142">Open the Query Editor from the main Power BI Desktop window by clicking **Edit Queries** in the External Data group in the Home ribbon.</span><span class="sxs-lookup"><span data-stu-id="f889a-142">Open the Query Editor from the main Power BI Desktop window by clicking **Edit Queries** in the External Data group in the Home ribbon.</span></span> 

![[The External Data group in Home ribbon]](../media/tutorials/power-bi/edit-queries.png)

<span data-ttu-id="f889a-144">Select "FabrikamComments" in the Queries list at the left side of the window if it is not already selected.</span><span class="sxs-lookup"><span data-stu-id="f889a-144">Select "FabrikamComments" in the Queries list at the left side of the window if it is not already selected.</span></span>

<span data-ttu-id="f889a-145">Now select both the `subject` and `comment` columns in the table.</span><span class="sxs-lookup"><span data-stu-id="f889a-145">Now select both the `subject` and `comment` columns in the table.</span></span> <span data-ttu-id="f889a-146">You may need to scroll horizontally to see these columns.</span><span class="sxs-lookup"><span data-stu-id="f889a-146">You may need to scroll horizontally to see these columns.</span></span> <span data-ttu-id="f889a-147">First click the `subject` column header, then hold down the Control key and click the `comment` column header.</span><span class="sxs-lookup"><span data-stu-id="f889a-147">First click the `subject` column header, then hold down the Control key and click the `comment` column header.</span></span>

![[Selecting fields to be merged]](../media/tutorials/power-bi/select-columns.png)

<span data-ttu-id="f889a-149">In the Text Columns group of the Transform ribbon, click **Merge Columns**.</span><span class="sxs-lookup"><span data-stu-id="f889a-149">In the Text Columns group of the Transform ribbon, click **Merge Columns**.</span></span> <span data-ttu-id="f889a-150">The Merge Columns dialog appears.</span><span class="sxs-lookup"><span data-stu-id="f889a-150">The Merge Columns dialog appears.</span></span>

![[Merging fields using the Merge Columns dialog]](../media/tutorials/power-bi/merge-columns.png)

<span data-ttu-id="f889a-152">In the Merge Columns dialog, choose Tab as the separator, then click **OK.**</span><span class="sxs-lookup"><span data-stu-id="f889a-152">In the Merge Columns dialog, choose Tab as the separator, then click **OK.**</span></span> <span data-ttu-id="f889a-153">Done!</span><span class="sxs-lookup"><span data-stu-id="f889a-153">Done!</span></span>

<span data-ttu-id="f889a-154">You might also consider filtering out blank messages using the Remove Empty filter or removing unprintable characters using the Clean transformation.</span><span class="sxs-lookup"><span data-stu-id="f889a-154">You might also consider filtering out blank messages using the Remove Empty filter or removing unprintable characters using the Clean transformation.</span></span> <span data-ttu-id="f889a-155">If your data contains a column like the `spamscore` column in our sample file, you can skip "spam" comments using a Number Filter.</span><span class="sxs-lookup"><span data-stu-id="f889a-155">If your data contains a column like the `spamscore` column in our sample file, you can skip "spam" comments using a Number Filter.</span></span>

## <a name="understanding-the-api"></a><span data-ttu-id="f889a-156">Understanding the API</span><span class="sxs-lookup"><span data-stu-id="f889a-156">Understanding the API</span></span>

<span data-ttu-id="f889a-157">The Key Phrases API can process up to a thousand text documents per HTTP request.</span><span class="sxs-lookup"><span data-stu-id="f889a-157">The Key Phrases API can process up to a thousand text documents per HTTP request.</span></span> <span data-ttu-id="f889a-158">Power BI prefers to deal with records one at a time, though, so our calls to the API will contain only a single document.</span><span class="sxs-lookup"><span data-stu-id="f889a-158">Power BI prefers to deal with records one at a time, though, so our calls to the API will contain only a single document.</span></span> <span data-ttu-id="f889a-159">[The API](//westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) requires the following fields for each document being processed.</span><span class="sxs-lookup"><span data-stu-id="f889a-159">[The API](//westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) requires the following fields for each document being processed.</span></span>

| | |
| - | - |
| `id`  | <span data-ttu-id="f889a-160">A unique identifier for this document within the request.</span><span class="sxs-lookup"><span data-stu-id="f889a-160">A unique identifier for this document within the request.</span></span> <span data-ttu-id="f889a-161">The response also contains this field.</span><span class="sxs-lookup"><span data-stu-id="f889a-161">The response also contains this field.</span></span> <span data-ttu-id="f889a-162">That way, if you process multiple documents, you can easily associate the extracted key phrases with the document they came from.</span><span class="sxs-lookup"><span data-stu-id="f889a-162">That way, if you process multiple documents, you can easily associate the extracted key phrases with the document they came from.</span></span> <span data-ttu-id="f889a-163">We are processing one document per request, so we already know which document the response is associated with, and `id` can be the same in each request.</span><span class="sxs-lookup"><span data-stu-id="f889a-163">We are processing one document per request, so we already know which document the response is associated with, and `id` can be the same in each request.</span></span>|
| `text`  | <span data-ttu-id="f889a-164">The text to be processed.</span><span class="sxs-lookup"><span data-stu-id="f889a-164">The text to be processed.</span></span> <span data-ttu-id="f889a-165">We get it from the `Merged` column we created, which contains the combined subject line and comment text.</span><span class="sxs-lookup"><span data-stu-id="f889a-165">We get it from the `Merged` column we created, which contains the combined subject line and comment text.</span></span> <span data-ttu-id="f889a-166">The Key Phrases API requires this data be no longer than about 5,000 characters.</span><span class="sxs-lookup"><span data-stu-id="f889a-166">The Key Phrases API requires this data be no longer than about 5,000 characters.</span></span>|
| `language` | <span data-ttu-id="f889a-167">The code representing the language the document is written in.</span><span class="sxs-lookup"><span data-stu-id="f889a-167">The code representing the language the document is written in.</span></span> <span data-ttu-id="f889a-168">All our messages are in English, so we can hard-code language `en` in our query.</span><span class="sxs-lookup"><span data-stu-id="f889a-168">All our messages are in English, so we can hard-code language `en` in our query.</span></span>|

<span data-ttu-id="f889a-169">We need to combine these fields into a JSON (JavaScript Object Notation) document for submission to the Key Phrases API.</span><span class="sxs-lookup"><span data-stu-id="f889a-169">We need to combine these fields into a JSON (JavaScript Object Notation) document for submission to the Key Phrases API.</span></span> <span data-ttu-id="f889a-170">The response from this request is also a JSON document, and we must parse it and fish out the key phrases.</span><span class="sxs-lookup"><span data-stu-id="f889a-170">The response from this request is also a JSON document, and we must parse it and fish out the key phrases.</span></span>

## <a name="creating-a-custom-function"></a><span data-ttu-id="f889a-171">Creating a custom function</span><span class="sxs-lookup"><span data-stu-id="f889a-171">Creating a custom function</span></span>

<span data-ttu-id="f889a-172">Now we're ready to create the custom function that will integrate Power BI and Text Analytics.</span><span class="sxs-lookup"><span data-stu-id="f889a-172">Now we're ready to create the custom function that will integrate Power BI and Text Analytics.</span></span> <span data-ttu-id="f889a-173">Power BI Desktop invokes the function for each row of the table and creates a new column with the results.</span><span class="sxs-lookup"><span data-stu-id="f889a-173">Power BI Desktop invokes the function for each row of the table and creates a new column with the results.</span></span>

<span data-ttu-id="f889a-174">The function receives the text to be processed as a parameter.</span><span class="sxs-lookup"><span data-stu-id="f889a-174">The function receives the text to be processed as a parameter.</span></span> <span data-ttu-id="f889a-175">It converts data to and from the required JavaScript Object Notation (JSON) and makes the HTTP request to the Key Phrases API endpoint.</span><span class="sxs-lookup"><span data-stu-id="f889a-175">It converts data to and from the required JavaScript Object Notation (JSON) and makes the HTTP request to the Key Phrases API endpoint.</span></span> <span data-ttu-id="f889a-176">After parsing the response, the function returns a string containing a comma-separated list of the extracted key phrases.</span><span class="sxs-lookup"><span data-stu-id="f889a-176">After parsing the response, the function returns a string containing a comma-separated list of the extracted key phrases.</span></span>

> [!NOTE]
> <span data-ttu-id="f889a-177">Power BI Desktop custom functions are written in the [Power Query M formula language](https://msdn.microsoft.com/library/mt211003.aspx), or just "M" for short.</span><span class="sxs-lookup"><span data-stu-id="f889a-177">Power BI Desktop custom functions are written in the [Power Query M formula language](https://msdn.microsoft.com/library/mt211003.aspx), or just "M" for short.</span></span> <span data-ttu-id="f889a-178">M is a functional programming language based on [F#](https://docs.microsoft.com/dotnet/fsharp/).</span><span class="sxs-lookup"><span data-stu-id="f889a-178">M is a functional programming language based on [F#](https://docs.microsoft.com/dotnet/fsharp/).</span></span> <span data-ttu-id="f889a-179">You don't need to be a programmer to finish this tutorial, though; the required code is included below.</span><span class="sxs-lookup"><span data-stu-id="f889a-179">You don't need to be a programmer to finish this tutorial, though; the required code is included below.</span></span>

<span data-ttu-id="f889a-180">You should still be in the Query Editor window.</span><span class="sxs-lookup"><span data-stu-id="f889a-180">You should still be in the Query Editor window.</span></span> <span data-ttu-id="f889a-181">From the Home ribbon, click **New Source** (in the New Query group) and choose **Blank Query** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f889a-181">From the Home ribbon, click **New Source** (in the New Query group) and choose **Blank Query** from the drop-down menu.</span></span> 

<span data-ttu-id="f889a-182">A new query, initially named Query1, appears in the Queries list.</span><span class="sxs-lookup"><span data-stu-id="f889a-182">A new query, initially named Query1, appears in the Queries list.</span></span> <span data-ttu-id="f889a-183">Double-click this entry and name it `KeyPhrases`.</span><span class="sxs-lookup"><span data-stu-id="f889a-183">Double-click this entry and name it `KeyPhrases`.</span></span>

<span data-ttu-id="f889a-184">Now open the Advanced Editor window by clicking **Advanced Editor** in the Query group of the Home ribbon.</span><span class="sxs-lookup"><span data-stu-id="f889a-184">Now open the Advanced Editor window by clicking **Advanced Editor** in the Query group of the Home ribbon.</span></span> <span data-ttu-id="f889a-185">Delete the code that's already in that window and paste in the following code.</span><span class="sxs-lookup"><span data-stu-id="f889a-185">Delete the code that's already in that window and paste in the following code.</span></span> 

> [!NOTE]
> <span data-ttu-id="f889a-186">In the examples below we assume the endpoint is at https://westus.api.cognitive.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f889a-186">In the examples below we assume the endpoint is at https://westus.api.cognitive.microsoft.com.</span></span>  <span data-ttu-id="f889a-187">Text Analytics supports creation of a subscription in 13 different regions.</span><span class="sxs-lookup"><span data-stu-id="f889a-187">Text Analytics supports creation of a subscription in 13 different regions.</span></span> <span data-ttu-id="f889a-188">If you signed up for the service in a different region, please make sure to use the endpoint for the region you selected.</span><span class="sxs-lookup"><span data-stu-id="f889a-188">If you signed up for the service in a different region, please make sure to use the endpoint for the region you selected.</span></span> <span data-ttu-id="f889a-189">It should be shown in the Overview page in the Azure portal when you select your Text Analytics subscription.</span><span class="sxs-lookup"><span data-stu-id="f889a-189">It should be shown in the Overview page in the Azure portal when you select your Text Analytics subscription.</span></span>

```fsharp
// Returns key phrases from the text in a comma-separated list
(text) => let
    apikey      = "YOUR_API_KEY_HERE",
    endpoint    = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases",
    jsontext    = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
    jsonbody    = "{ documents: [ { language: ""en"", id: ""0"", text: " & jsontext & " } ] }",
    bytesbody   = Text.ToBinary(jsonbody),
    headers     = [#"Ocp-Apim-Subscription-Key" = apikey],
    bytesresp   = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
    jsonresp    = Json.Document(bytesresp),
    keyphrases  = Text.Lower(Text.Combine(jsonresp[documents]{0}[keyPhrases], ", "))
in  keyphrases
```

<span data-ttu-id="f889a-190">Also paste in your Text Analytics API key, obtained from the Microsoft Azure dashboard, in the line starting with `apikey`.</span><span class="sxs-lookup"><span data-stu-id="f889a-190">Also paste in your Text Analytics API key, obtained from the Microsoft Azure dashboard, in the line starting with `apikey`.</span></span> <span data-ttu-id="f889a-191">(Be sure to leave the quotation marks before and after the key.) Then click **Done.**</span><span class="sxs-lookup"><span data-stu-id="f889a-191">(Be sure to leave the quotation marks before and after the key.) Then click **Done.**</span></span>

## <a name="using-the-function"></a><span data-ttu-id="f889a-192">Using the function</span><span class="sxs-lookup"><span data-stu-id="f889a-192">Using the function</span></span>

<span data-ttu-id="f889a-193">Now we can use the custom function to obtain the key phrases contained in each of our customer comments and store them in a new column in the table.</span><span class="sxs-lookup"><span data-stu-id="f889a-193">Now we can use the custom function to obtain the key phrases contained in each of our customer comments and store them in a new column in the table.</span></span> 

<span data-ttu-id="f889a-194">Still in the Query Editor, switch back to the FabrikamComments query, change to the Add Column ribbon, and click the **Invoke Custom Function** button in the General group.</span><span class="sxs-lookup"><span data-stu-id="f889a-194">Still in the Query Editor, switch back to the FabrikamComments query, change to the Add Column ribbon, and click the **Invoke Custom Function** button in the General group.</span></span>

![[Invoke Custom Function button]](../media/tutorials/power-bi/invoke-custom-function-button.png)<br><br>

<span data-ttu-id="f889a-196">In the Invoke Custom Function dialog, enter `keyphrases` as the name of the new column.</span><span class="sxs-lookup"><span data-stu-id="f889a-196">In the Invoke Custom Function dialog, enter `keyphrases` as the name of the new column.</span></span> <span data-ttu-id="f889a-197">Choose our custom function, `KeyPhrases`, as the Function Query.</span><span class="sxs-lookup"><span data-stu-id="f889a-197">Choose our custom function, `KeyPhrases`, as the Function Query.</span></span> 

<span data-ttu-id="f889a-198">A new field appears in the dialog, asking which field we want to pass to our function as the `text` parameter.</span><span class="sxs-lookup"><span data-stu-id="f889a-198">A new field appears in the dialog, asking which field we want to pass to our function as the `text` parameter.</span></span> <span data-ttu-id="f889a-199">Choose `Merged` (the column we created earlier by merging the subject and message fields) from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f889a-199">Choose `Merged` (the column we created earlier by merging the subject and message fields) from the drop-down menu.</span></span>

![[Invoking a custom function]](../media/tutorials/power-bi/invoke-custom-function.png)

<span data-ttu-id="f889a-201">Finally, click **OK.**</span><span class="sxs-lookup"><span data-stu-id="f889a-201">Finally, click **OK.**</span></span>

<span data-ttu-id="f889a-202">If everything's ready, Power BI calls our function once for each row in our table, performing the Key Phrases queries and adding the new column to the table.</span><span class="sxs-lookup"><span data-stu-id="f889a-202">If everything's ready, Power BI calls our function once for each row in our table, performing the Key Phrases queries and adding the new column to the table.</span></span> <span data-ttu-id="f889a-203">But before that happens, you may need to specify authentication and privacy settings.</span><span class="sxs-lookup"><span data-stu-id="f889a-203">But before that happens, you may need to specify authentication and privacy settings.</span></span>

## <a name="authentication-and-privacy"></a><span data-ttu-id="f889a-204">Authentication and privacy</span><span class="sxs-lookup"><span data-stu-id="f889a-204">Authentication and privacy</span></span>

<span data-ttu-id="f889a-205">After you close the Invoke Custom Function dialog, a banner may appear asking you to specify how to connect to the Key Phrases endpoint.</span><span class="sxs-lookup"><span data-stu-id="f889a-205">After you close the Invoke Custom Function dialog, a banner may appear asking you to specify how to connect to the Key Phrases endpoint.</span></span>

![[credentials banner]](../media/tutorials/power-bi/credentials-banner.png)

<span data-ttu-id="f889a-207">Click **Edit Credentials,** make sure Anonymous is selected in the dialog, then click **Connect.**</span><span class="sxs-lookup"><span data-stu-id="f889a-207">Click **Edit Credentials,** make sure Anonymous is selected in the dialog, then click **Connect.**</span></span> 

> [!NOTE]
> <span data-ttu-id="f889a-208">Why anonymous?</span><span class="sxs-lookup"><span data-stu-id="f889a-208">Why anonymous?</span></span> <span data-ttu-id="f889a-209">The Text Analytics service authenticates you using the API key, so Power BI does not need to provide credentials for the HTTP request itself.</span><span class="sxs-lookup"><span data-stu-id="f889a-209">The Text Analytics service authenticates you using the API key, so Power BI does not need to provide credentials for the HTTP request itself.</span></span>

![[setting authentication to anonymous]](../media/tutorials/power-bi/access-web-content.png)

<span data-ttu-id="f889a-211">If you see the Edit Credentials banner even after choosing anonymous access, you may have forgotten to paste in your API key.</span><span class="sxs-lookup"><span data-stu-id="f889a-211">If you see the Edit Credentials banner even after choosing anonymous access, you may have forgotten to paste in your API key.</span></span> <span data-ttu-id="f889a-212">Check the `KeyPhrases` custom function in the Advanced Editor to make sure it's there.</span><span class="sxs-lookup"><span data-stu-id="f889a-212">Check the `KeyPhrases` custom function in the Advanced Editor to make sure it's there.</span></span>

<span data-ttu-id="f889a-213">Next, a banner may appear asking you to provide information about your data sources' privacy.</span><span class="sxs-lookup"><span data-stu-id="f889a-213">Next, a banner may appear asking you to provide information about your data sources' privacy.</span></span> 

![[privacy banner]](../media/tutorials/power-bi/privacy-banner.png)

<span data-ttu-id="f889a-215">Click **Continue** and choose Public for each of the data sources in the dialog.</span><span class="sxs-lookup"><span data-stu-id="f889a-215">Click **Continue** and choose Public for each of the data sources in the dialog.</span></span> <span data-ttu-id="f889a-216">Then click **Save.**</span><span class="sxs-lookup"><span data-stu-id="f889a-216">Then click **Save.**</span></span>

![[setting data source privacy]](../media/tutorials/power-bi/privacy-dialog.png)

## <a name="creating-the-word-cloud"></a><span data-ttu-id="f889a-218">Creating the word cloud</span><span class="sxs-lookup"><span data-stu-id="f889a-218">Creating the word cloud</span></span>

<span data-ttu-id="f889a-219">Once you have dealt with any banners that appear, click **Close & Apply** in the Home ribbon to close the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="f889a-219">Once you have dealt with any banners that appear, click **Close & Apply** in the Home ribbon to close the Query Editor.</span></span>

<span data-ttu-id="f889a-220">Power BI Desktop takes a moment to make the necessary HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="f889a-220">Power BI Desktop takes a moment to make the necessary HTTP requests.</span></span> <span data-ttu-id="f889a-221">For each row in the table, the new `keyphrases` column contains the key phrases detected in the text by the Key Phrases API.</span><span class="sxs-lookup"><span data-stu-id="f889a-221">For each row in the table, the new `keyphrases` column contains the key phrases detected in the text by the Key Phrases API.</span></span> 

<span data-ttu-id="f889a-222">Let's use this column to generate a word cloud.</span><span class="sxs-lookup"><span data-stu-id="f889a-222">Let's use this column to generate a word cloud.</span></span> <span data-ttu-id="f889a-223">To get started, click the Report button in the main Power BI Desktop window, to the left of the workspace.</span><span class="sxs-lookup"><span data-stu-id="f889a-223">To get started, click the Report button in the main Power BI Desktop window, to the left of the workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="f889a-224">Why use extracted key phrases to generate a word cloud, rather than the full text of every comment?</span><span class="sxs-lookup"><span data-stu-id="f889a-224">Why use extracted key phrases to generate a word cloud, rather than the full text of every comment?</span></span> <span data-ttu-id="f889a-225">The key phrases provide us with the *important* words from our customer comments, not just the *most common* words.</span><span class="sxs-lookup"><span data-stu-id="f889a-225">The key phrases provide us with the *important* words from our customer comments, not just the *most common* words.</span></span> <span data-ttu-id="f889a-226">Also, word sizing in the resulting cloud isn't skewed by the frequent use of a word in a relatively small number of comments.</span><span class="sxs-lookup"><span data-stu-id="f889a-226">Also, word sizing in the resulting cloud isn't skewed by the frequent use of a word in a relatively small number of comments.</span></span>

<span data-ttu-id="f889a-227">If you don't already have the Word Cloud custom visual installed, install it.</span><span class="sxs-lookup"><span data-stu-id="f889a-227">If you don't already have the Word Cloud custom visual installed, install it.</span></span> <span data-ttu-id="f889a-228">In the Visualizations panel to the right of the workspace, click the three dots (**...**) and choose **Import From Store**.</span><span class="sxs-lookup"><span data-stu-id="f889a-228">In the Visualizations panel to the right of the workspace, click the three dots (**...**) and choose **Import From Store**.</span></span> <span data-ttu-id="f889a-229">Then search for "cloud" and click the **Add** button next the Word Cloud visual.</span><span class="sxs-lookup"><span data-stu-id="f889a-229">Then search for "cloud" and click the **Add** button next the Word Cloud visual.</span></span> <span data-ttu-id="f889a-230">Power BI installs the Word Cloud visual and lets you know it installed successfully.</span><span class="sxs-lookup"><span data-stu-id="f889a-230">Power BI installs the Word Cloud visual and lets you know it installed successfully.</span></span>

![[adding a custom visual]](../media/tutorials/power-bi/add-custom-visuals.png)<br><br>

<span data-ttu-id="f889a-232">Now, let's make our word cloud!</span><span class="sxs-lookup"><span data-stu-id="f889a-232">Now, let's make our word cloud!</span></span>

![[Word Cloud icon in visualizations panel]](../media/tutorials/power-bi/visualizations-panel.png)

<span data-ttu-id="f889a-234">First, click the Word Cloud icon in the Visualizations panel.</span><span class="sxs-lookup"><span data-stu-id="f889a-234">First, click the Word Cloud icon in the Visualizations panel.</span></span> <span data-ttu-id="f889a-235">A new report appears in the workspace.</span><span class="sxs-lookup"><span data-stu-id="f889a-235">A new report appears in the workspace.</span></span> <span data-ttu-id="f889a-236">Drag the `keyphrases` field from the Fields panel to the Category field in the Visualizations panel.</span><span class="sxs-lookup"><span data-stu-id="f889a-236">Drag the `keyphrases` field from the Fields panel to the Category field in the Visualizations panel.</span></span> <span data-ttu-id="f889a-237">The word cloud appears inside the report.</span><span class="sxs-lookup"><span data-stu-id="f889a-237">The word cloud appears inside the report.</span></span>

<span data-ttu-id="f889a-238">Now switch to the Format page of the Visualizations panel.</span><span class="sxs-lookup"><span data-stu-id="f889a-238">Now switch to the Format page of the Visualizations panel.</span></span> <span data-ttu-id="f889a-239">In the Stop Words category, turn on **Default Stop Words** to eliminate short, common words like "of" from the cloud.</span><span class="sxs-lookup"><span data-stu-id="f889a-239">In the Stop Words category, turn on **Default Stop Words** to eliminate short, common words like "of" from the cloud.</span></span> 

![[activating default stop words]](../media/tutorials/power-bi/default-stop-words.png)

<span data-ttu-id="f889a-241">Down a little further in this panel, turn off **Rotate Text** and **Title**.</span><span class="sxs-lookup"><span data-stu-id="f889a-241">Down a little further in this panel, turn off **Rotate Text** and **Title**.</span></span>

![[activate focus mode]](../media/tutorials/power-bi/word-cloud-focus-mode.png)

<span data-ttu-id="f889a-243">Click the Focus Mode tool in the report to get a better look at our word cloud.</span><span class="sxs-lookup"><span data-stu-id="f889a-243">Click the Focus Mode tool in the report to get a better look at our word cloud.</span></span> <span data-ttu-id="f889a-244">The tool expands the word cloud to fill the entire workspace, as shown below.</span><span class="sxs-lookup"><span data-stu-id="f889a-244">The tool expands the word cloud to fill the entire workspace, as shown below.</span></span>

![[A Word Cloud]](../media/tutorials/power-bi/word-cloud.png)

## <a name="more-text-analytics-services"></a><span data-ttu-id="f889a-246">More Text Analytics services</span><span class="sxs-lookup"><span data-stu-id="f889a-246">More Text Analytics services</span></span>

<span data-ttu-id="f889a-247">The Text Analytics service, one of the Cognitive Services offered by Microsoft Azure, also provides sentiment analysis and language detection.</span><span class="sxs-lookup"><span data-stu-id="f889a-247">The Text Analytics service, one of the Cognitive Services offered by Microsoft Azure, also provides sentiment analysis and language detection.</span></span> <span data-ttu-id="f889a-248">The language detection in particular is useful if your customer feedback is not all in English.</span><span class="sxs-lookup"><span data-stu-id="f889a-248">The language detection in particular is useful if your customer feedback is not all in English.</span></span>

<span data-ttu-id="f889a-249">Both of these other APIs are very similar to the Key Phrases API.</span><span class="sxs-lookup"><span data-stu-id="f889a-249">Both of these other APIs are very similar to the Key Phrases API.</span></span> <span data-ttu-id="f889a-250">Near-identical custom functions can thus be used to integrate them with Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f889a-250">Near-identical custom functions can thus be used to integrate them with Power BI Desktop.</span></span> <span data-ttu-id="f889a-251">Just create a blank query and paste the appropriate code below into the Advanced Editor, as you did earlier.</span><span class="sxs-lookup"><span data-stu-id="f889a-251">Just create a blank query and paste the appropriate code below into the Advanced Editor, as you did earlier.</span></span> <span data-ttu-id="f889a-252">(Don't forget your access key!) Then, as before, use the function to add a new column to the table.</span><span class="sxs-lookup"><span data-stu-id="f889a-252">(Don't forget your access key!) Then, as before, use the function to add a new column to the table.</span></span>

<span data-ttu-id="f889a-253">The Sentiment Analysis function below returns a score indicating how positive the sentiment expressed in the text is.</span><span class="sxs-lookup"><span data-stu-id="f889a-253">The Sentiment Analysis function below returns a score indicating how positive the sentiment expressed in the text is.</span></span>

```fsharp
// Returns the sentiment score of the text, from 0.0 (least favorable) to 1.0 (most favorable)
(text) => let
    apikey      = "YOUR_API_KEY_HERE",
    endpoint    = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment",
    jsontext    = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
    jsonbody    = "{ documents: [ { language: ""en"", id: ""0"", text: " & jsontext & " } ] }",
    bytesbody   = Text.ToBinary(jsonbody),
    headers     = [#"Ocp-Apim-Subscription-Key" = apikey],
    bytesresp   = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
    jsonresp    = Json.Document(bytesresp),
    sentiment   = jsonresp[documents]{0}[score]
in  sentiment
```

<span data-ttu-id="f889a-254">Here are two versions of a Language Detection function.</span><span class="sxs-lookup"><span data-stu-id="f889a-254">Here are two versions of a Language Detection function.</span></span> <span data-ttu-id="f889a-255">The first returns the ISO language code (e.g. `en` for English), while the second returns the "friendly" name (e.g. `English`).</span><span class="sxs-lookup"><span data-stu-id="f889a-255">The first returns the ISO language code (e.g. `en` for English), while the second returns the "friendly" name (e.g. `English`).</span></span> <span data-ttu-id="f889a-256">You may notice that only the last line of the body differs between the two versions.</span><span class="sxs-lookup"><span data-stu-id="f889a-256">You may notice that only the last line of the body differs between the two versions.</span></span>

```fsharp
// Returns the two-letter language code (e.g. en for English) of the text
(text) => let
    apikey      = "YOUR_API_KEY_HERE",
    endpoint    = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages",
    jsontext    = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
    jsonbody    = "{ documents: [ { id: ""0"", text: " & jsontext & " } ] }",
    bytesbody   = Text.ToBinary(jsonbody),
    headers     = [#"Ocp-Apim-Subscription-Key" = apikey],
    bytesresp   = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
    jsonresp    = Json.Document(bytesresp),
    language    = jsonresp[documents]{0}[detectedLanguages]{0}[iso6391Name]
in  language
```
```fsharp
// Returns the name (e.g. English) of the language in which the text is written
(text) => let
    apikey      = "YOUR_API_KEY_HERE",
    endpoint    = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages",
    jsontext    = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
    jsonbody    = "{ documents: [ { id: ""0"", text: " & jsontext & " } ] }",
    bytesbody   = Text.ToBinary(jsonbody),
    headers     = [#"Ocp-Apim-Subscription-Key" = apikey],
    bytesresp   = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
    jsonresp    = Json.Document(bytesresp),
    language    = jsonresp[documents]{0}[detectedLanguages]{0}[name]
in  language
```

<span data-ttu-id="f889a-257">Finally, here's a variant of the Key Phrases function already presented that returns the phrases as a list object, rather than as a single string of comma-separated phrases.</span><span class="sxs-lookup"><span data-stu-id="f889a-257">Finally, here's a variant of the Key Phrases function already presented that returns the phrases as a list object, rather than as a single string of comma-separated phrases.</span></span> 

> [!NOTE]
> <span data-ttu-id="f889a-258">Returning a single string simplified our word cloud example.</span><span class="sxs-lookup"><span data-stu-id="f889a-258">Returning a single string simplified our word cloud example.</span></span> <span data-ttu-id="f889a-259">A list, on the other hand, is a more flexible format for working with the returned phrases in Power BI.</span><span class="sxs-lookup"><span data-stu-id="f889a-259">A list, on the other hand, is a more flexible format for working with the returned phrases in Power BI.</span></span> <span data-ttu-id="f889a-260">You can manipulate list objects in Power BI Desktop using the Structured Column group in the Query Editor's Transform ribbon.</span><span class="sxs-lookup"><span data-stu-id="f889a-260">You can manipulate list objects in Power BI Desktop using the Structured Column group in the Query Editor's Transform ribbon.</span></span>

```fsharp
// Returns key phrases from the text as a list object
(text) => let
    apikey      = "YOUR_API_KEY_HERE",
    endpoint    = "https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases",
    jsontext    = Text.FromBinary(Json.FromValue(Text.Start(Text.Trim(text), 5000))),
    jsonbody    = "{ documents: [ { language: ""en"", id: ""0"", text: " & jsontext & " } ] }",
    bytesbody   = Text.ToBinary(jsonbody),
    headers     = [#"Ocp-Apim-Subscription-Key" = apikey],
    bytesresp   = Web.Contents(endpoint, [Headers=headers, Content=bytesbody]),
    jsonresp    = Json.Document(bytesresp),
    keyphrases  = jsonresp[documents]{0}[keyPhrases]
in  keyphrases
```

## <a name="next-steps"></a><span data-ttu-id="f889a-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="f889a-261">Next steps</span></span>

<span data-ttu-id="f889a-262">Learn more about the Text Analytics service, the Power Query M formula language, or Power BI.</span><span class="sxs-lookup"><span data-stu-id="f889a-262">Learn more about the Text Analytics service, the Power Query M formula language, or Power BI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f889a-263">Text Analytics API reference</span><span class="sxs-lookup"><span data-stu-id="f889a-263">Text Analytics API reference</span></span>](//westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f889a-264">Power Query M reference</span><span class="sxs-lookup"><span data-stu-id="f889a-264">Power Query M reference</span></span>](//msdn.microsoft.com/library/mt211003.aspx)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f889a-265">Power BI documentation</span><span class="sxs-lookup"><span data-stu-id="f889a-265">Power BI documentation</span></span>](//powerbi.microsoft.com/documentation/powerbi-landing-page/)
