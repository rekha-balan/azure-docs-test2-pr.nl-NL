---
title: Get started with the Knowledge Exploration Service | Microsoft Docs
description: Use Knowledge Exploration Service (KES) to create an engine for an interactive search experience across academic publications in Microsoft Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.component: knowledge-exploration
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 02dc9368eef02d6fa507335ef3171e923412acca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774143"
---
<a name="getting-started"></a>
# <a name="get-started-with-the-knowledge-exploration-service"></a><span data-ttu-id="14034-103">Get started with the Knowledge Exploration Service</span><span class="sxs-lookup"><span data-stu-id="14034-103">Get started with the Knowledge Exploration Service</span></span>
<span data-ttu-id="14034-104">In this walkthrough, you use the Knowledge Exploration Service (KES) to create the engine for an interactive search experience for academic publications.</span><span class="sxs-lookup"><span data-stu-id="14034-104">In this walkthrough, you use the Knowledge Exploration Service (KES) to create the engine for an interactive search experience for academic publications.</span></span> <span data-ttu-id="14034-105">You can install the command line tool, [`kes.exe`](CommandLine.md), and all example files from the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488).</span><span class="sxs-lookup"><span data-stu-id="14034-105">You can install the command line tool, [`kes.exe`](CommandLine.md), and all example files from the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488).</span></span>

<span data-ttu-id="14034-106">The academic publications example contains a sample of 1000 academic papers published by researchers at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="14034-106">The academic publications example contains a sample of 1000 academic papers published by researchers at Microsoft.</span></span>  <span data-ttu-id="14034-107">Each paper is associated with a title, publication year, authors, and keywords.</span><span class="sxs-lookup"><span data-stu-id="14034-107">Each paper is associated with a title, publication year, authors, and keywords.</span></span> <span data-ttu-id="14034-108">Each author is represented by an ID, name, and affiliation at the time of publication.</span><span class="sxs-lookup"><span data-stu-id="14034-108">Each author is represented by an ID, name, and affiliation at the time of publication.</span></span> <span data-ttu-id="14034-109">Each keyword can be associated with a set of synonyms (for example, the keyword "support vector machine" can be associated with the synonym "svm").</span><span class="sxs-lookup"><span data-stu-id="14034-109">Each keyword can be associated with a set of synonyms (for example, the keyword "support vector machine" can be associated with the synonym "svm").</span></span>

<a name="defining-schema"></a>
## <a name="define-the-schema"></a><span data-ttu-id="14034-110">Define the schema</span><span class="sxs-lookup"><span data-stu-id="14034-110">Define the schema</span></span>
<span data-ttu-id="14034-111">The schema describes the attribute structure of the objects in the domain.</span><span class="sxs-lookup"><span data-stu-id="14034-111">The schema describes the attribute structure of the objects in the domain.</span></span> <span data-ttu-id="14034-112">It specifies the name and data type for each attribute in a JSON file format.</span><span class="sxs-lookup"><span data-stu-id="14034-112">It specifies the name and data type for each attribute in a JSON file format.</span></span> <span data-ttu-id="14034-113">The following example is the content of the file *Academic.schema*.</span><span class="sxs-lookup"><span data-stu-id="14034-113">The following example is the content of the file *Academic.schema*.</span></span>

```json
{
  "attributes":[
    {"name":"Title", "type":"String"},
    {"name":"Year", "type":"Int32"},
    {"name":"Author", "type":"Composite"},
    {"name":"Author.Id", "type":"Int64", "operations":["equals"]},
    {"name":"Author.Name", "type":"String"},
    {"name":"Author.Affiliation", "type":"String"},
    {"name":"Keyword", "type":"String", "synonyms":"Keyword.syn"}
  ]
}
```

<span data-ttu-id="14034-114">Here, you define *Title*, *Year*, and *Keyword* as a string, integer, and string attribute, respectively.</span><span class="sxs-lookup"><span data-stu-id="14034-114">Here, you define *Title*, *Year*, and *Keyword* as a string, integer, and string attribute, respectively.</span></span> <span data-ttu-id="14034-115">Because authors are represented by ID, name, and affiliation, you define *Author* as a composite attribute with three sub-attributes: *Author.Id*, *Author.Name*, and *Author.Affiliation*.</span><span class="sxs-lookup"><span data-stu-id="14034-115">Because authors are represented by ID, name, and affiliation, you define *Author* as a composite attribute with three sub-attributes: *Author.Id*, *Author.Name*, and *Author.Affiliation*.</span></span>

<span data-ttu-id="14034-116">By default, attributes support all operations available for their data type, including *equals*, *starts_with*, and *is_between*.</span><span class="sxs-lookup"><span data-stu-id="14034-116">By default, attributes support all operations available for their data type, including *equals*, *starts_with*, and *is_between*.</span></span> <span data-ttu-id="14034-117">Because author ID is only used internally as an identifier, override the default, and specify *equals* as the only indexed operation.</span><span class="sxs-lookup"><span data-stu-id="14034-117">Because author ID is only used internally as an identifier, override the default, and specify *equals* as the only indexed operation.</span></span>

<span data-ttu-id="14034-118">For the *Keyword* attribute, allow synonyms to match the canonical keyword values by specifying the synonym file *Keyword.syn* in the attribute definition.</span><span class="sxs-lookup"><span data-stu-id="14034-118">For the *Keyword* attribute, allow synonyms to match the canonical keyword values by specifying the synonym file *Keyword.syn* in the attribute definition.</span></span> <span data-ttu-id="14034-119">This file contains a list of canonical and synonym value pairs:</span><span class="sxs-lookup"><span data-stu-id="14034-119">This file contains a list of canonical and synonym value pairs:</span></span>

```json
...
["support vector machine","support vector machines"]
["support vector machine","support vector networks"]
["support vector machine","support vector regression"]
["support vector machine","support vector"]
["support vector machine","svm machine learning"]
["support vector machine","svm"]
["support vector machine","svms"]
["support vector machine","vector machine"]
...
```

<span data-ttu-id="14034-120">For additional information about the schema definition, see [Schema Format](SchemaFormat.md).</span><span class="sxs-lookup"><span data-stu-id="14034-120">For additional information about the schema definition, see [Schema Format](SchemaFormat.md).</span></span>

<a name="generating-data"></a>
## <a name="generate-data"></a><span data-ttu-id="14034-121">Generate data</span><span class="sxs-lookup"><span data-stu-id="14034-121">Generate data</span></span>
<span data-ttu-id="14034-122">The data file describes the list of the publications to index, with each line specifying the attribute values of a paper in [JSON format](http://json.org/).</span><span class="sxs-lookup"><span data-stu-id="14034-122">The data file describes the list of the publications to index, with each line specifying the attribute values of a paper in [JSON format](http://json.org/).</span></span>  <span data-ttu-id="14034-123">The following example is a single line from the data file *Academic.data*, formatted for readability:</span><span class="sxs-lookup"><span data-stu-id="14034-123">The following example is a single line from the data file *Academic.data*, formatted for readability:</span></span>

```
...
{
    "logprob": -16.714,
    "Title": "the world wide telescope",
    "Year": 2001,
    "Author": [
        {
            "Id": 717694024,
            "Name": "alexander s szalay",
            "Affiliation": "microsoft"
        },
        {
            "Id": 2131537204,
            "Name": "jim gray",
            "Affiliation": "microsoft"
        }
    ]
}
...
```

<span data-ttu-id="14034-124">In this snippet, you specify the *Title* and *Year* attribute of the paper as a JSON string and number, respectively.</span><span class="sxs-lookup"><span data-stu-id="14034-124">In this snippet, you specify the *Title* and *Year* attribute of the paper as a JSON string and number, respectively.</span></span> <span data-ttu-id="14034-125">Multiple values are represented by using JSON arrays.</span><span class="sxs-lookup"><span data-stu-id="14034-125">Multiple values are represented by using JSON arrays.</span></span> <span data-ttu-id="14034-126">Because *Author* is a composite attribute, each value is represented by using a JSON object consisting of its sub-attributes.</span><span class="sxs-lookup"><span data-stu-id="14034-126">Because *Author* is a composite attribute, each value is represented by using a JSON object consisting of its sub-attributes.</span></span> <span data-ttu-id="14034-127">Attributes with missing values, such as *Keyword* in this case, can be excluded from the JSON representation.</span><span class="sxs-lookup"><span data-stu-id="14034-127">Attributes with missing values, such as *Keyword* in this case, can be excluded from the JSON representation.</span></span>

<span data-ttu-id="14034-128">To differentiate the likelihood of different papers, specify the relative log probability by using the built-in *logprob* attribute.</span><span class="sxs-lookup"><span data-stu-id="14034-128">To differentiate the likelihood of different papers, specify the relative log probability by using the built-in *logprob* attribute.</span></span> <span data-ttu-id="14034-129">Given a probability *p* between 0 and 1, you compute the log probability as log(*p*), where log() is the natural log function.</span><span class="sxs-lookup"><span data-stu-id="14034-129">Given a probability *p* between 0 and 1, you compute the log probability as log(*p*), where log() is the natural log function.</span></span>

<span data-ttu-id="14034-130">For more information, see [Data Format](DataFormat.md).</span><span class="sxs-lookup"><span data-stu-id="14034-130">For more information, see [Data Format](DataFormat.md).</span></span>

<a name="building-index"></a>
## <a name="build-a-compressed-binary-index"></a><span data-ttu-id="14034-131">Build a compressed binary index</span><span class="sxs-lookup"><span data-stu-id="14034-131">Build a compressed binary index</span></span>
<span data-ttu-id="14034-132">After you have a schema file and data file, you can build a compressed binary index of the data objects by using [`kes.exe build_index`](CommandLine.md#build_index-command).</span><span class="sxs-lookup"><span data-stu-id="14034-132">After you have a schema file and data file, you can build a compressed binary index of the data objects by using [`kes.exe build_index`](CommandLine.md#build_index-command).</span></span> <span data-ttu-id="14034-133">In this example, you build the index file *Academic.index* from the input schema file *Academic.schema* and data file *Academic.data*.</span><span class="sxs-lookup"><span data-stu-id="14034-133">In this example, you build the index file *Academic.index* from the input schema file *Academic.schema* and data file *Academic.data*.</span></span> <span data-ttu-id="14034-134">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="14034-134">Use the following command:</span></span>

`kes.exe build_index Academic.schema Academic.data Academic.index`

<span data-ttu-id="14034-135">For rapid prototyping outside of Azure, [`kes.exe build_index`](CommandLine.md#build_index-command) can build small indices locally, from data files containing up to 10,000 objects.</span><span class="sxs-lookup"><span data-stu-id="14034-135">For rapid prototyping outside of Azure, [`kes.exe build_index`](CommandLine.md#build_index-command) can build small indices locally, from data files containing up to 10,000 objects.</span></span> <span data-ttu-id="14034-136">For larger data files, you can either run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or perform a remote build in Azure.</span><span class="sxs-lookup"><span data-stu-id="14034-136">For larger data files, you can either run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or perform a remote build in Azure.</span></span> <span data-ttu-id="14034-137">For details, see [Scaling up](#scaling-up).</span><span class="sxs-lookup"><span data-stu-id="14034-137">For details, see [Scaling up](#scaling-up).</span></span>

<a name="authoring-grammar"></a>
## <a name="use-an-xml-grammar-specification"></a><span data-ttu-id="14034-138">Use an XML grammar specification</span><span class="sxs-lookup"><span data-stu-id="14034-138">Use an XML grammar specification</span></span>
<span data-ttu-id="14034-139">The grammar specifies the set of natural language queries that the service can interpret, as well as how these natural language queries are translated into semantic query expressions.</span><span class="sxs-lookup"><span data-stu-id="14034-139">The grammar specifies the set of natural language queries that the service can interpret, as well as how these natural language queries are translated into semantic query expressions.</span></span> <span data-ttu-id="14034-140">In this example, you use the grammar specified in *academic.xml*:</span><span class="sxs-lookup"><span data-stu-id="14034-140">In this example, you use the grammar specified in *academic.xml*:</span></span>

```xml
<grammar root="GetPapers">

  <!-- Import academic data schema-->
  <import schema="Academic.schema" name="academic"/>

  <!-- Define root rule-->
  <rule id="GetPapers">
    <example>papers about machine learning by michael jordan</example>

    papers
    <tag>
      yearOnce = false;
      isBeyondEndOfQuery = false;
      query = All();
    </tag>

    <item repeat="1-" repeat-logprob="-10">
      <!-- Do not complete additional attributes beyond end of query -->
      <tag>AssertEquals(isBeyondEndOfQuery, false);</tag>

      <one-of>
        <!-- about <keyword> -->
        <item logprob="-0.5">
          about <attrref uri="academic#Keyword" name="keyword"/>
          <tag>query = And(query, keyword);</tag>
        </item>

        <!-- by <authorName> [while at <authorAffiliation>] -->
        <item logprob="-1">
          by <attrref uri="academic#Author.Name" name="authorName"/>
          <tag>authorQuery = authorName;</tag>
          <item repeat="0-1" repeat-logprob="-1.5">
            while at <attrref uri="academic#Author.Affiliation" name="authorAffiliation"/>
            <tag>authorQuery = And(authorQuery, authorAffiliation);</tag>
          </item>
          <tag>
            authorQuery = Composite(authorQuery);
            query = And(query, authorQuery);
          </tag>
        </item>

        <!-- written (in|before|after) <year> -->
        <item logprob="-1.5">
          <!-- Allow this grammar path to be traversed only once -->
          <tag>
            AssertEquals(yearOnce, false);
            yearOnce = true;
          </tag>
          <ruleref uri="#GetPaperYear" name="year"/>
          <tag>query = And(query, year);</tag>
        </item>
      </one-of>

      <!-- Determine if current parse position is beyond end of query -->
      <tag>isBeyondEndOfQuery = GetVariable("IsBeyondEndOfQuery", "system");</tag>
    </item>
    <tag>out = query;</tag>
  </rule>

  <rule id="GetPaperYear">
    <tag>year = All();</tag>
    written
    <one-of>
      <item>
        in <attrref uri="academic#Year" name="year"/>
      </item>
      <item>
        before
        <one-of>
          <item>[year]</item>
          <item>
            <attrref uri="academic#Year" op="lt" name="year"/>
          </item>
        </one-of>
      </item>
      <item>
        after
        <one-of>
          <item>[year]</item>
          <item>
            <attrref uri="academic#Year" op="gt" name="year"/>
          </item>
        </one-of>
      </item>
    </one-of>
    <tag>out = year;</tag>
  </rule>
</grammar>
```

<span data-ttu-id="14034-141">For more information about the grammar specification syntax, see [Grammar Format](GrammarFormat.md).</span><span class="sxs-lookup"><span data-stu-id="14034-141">For more information about the grammar specification syntax, see [Grammar Format](GrammarFormat.md).</span></span>

<a name="compiling-grammar"></a>
## <a name="compile-the-grammar"></a><span data-ttu-id="14034-142">Compile the grammar</span><span class="sxs-lookup"><span data-stu-id="14034-142">Compile the grammar</span></span>
<span data-ttu-id="14034-143">After you have an XML grammar specification, you can compile it into a binary grammar by using [`kes.exe build_grammar`](CommandLine.md#build_grammar-command).</span><span class="sxs-lookup"><span data-stu-id="14034-143">After you have an XML grammar specification, you can compile it into a binary grammar by using [`kes.exe build_grammar`](CommandLine.md#build_grammar-command).</span></span> <span data-ttu-id="14034-144">Note that if the grammar imports a schema, the schema file needs to be located in the same path as the grammar XML.</span><span class="sxs-lookup"><span data-stu-id="14034-144">Note that if the grammar imports a schema, the schema file needs to be located in the same path as the grammar XML.</span></span> <span data-ttu-id="14034-145">In this example, you build the binary grammar file *Academic.grammar* from the input XML grammar file *Academic.xml*.</span><span class="sxs-lookup"><span data-stu-id="14034-145">In this example, you build the binary grammar file *Academic.grammar* from the input XML grammar file *Academic.xml*.</span></span> <span data-ttu-id="14034-146">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="14034-146">Use the following command:</span></span>

`kes.exe build_grammar Academic.xml Academic.grammar`

<a name="hosting-index"></a>
## <a name="host-the-grammar-and-index-in-a-web-service"></a><span data-ttu-id="14034-147">Host the grammar and index in a web service</span><span class="sxs-lookup"><span data-stu-id="14034-147">Host the grammar and index in a web service</span></span>
<span data-ttu-id="14034-148">For rapid prototyping, you can host the grammar and index in a web service on the local machine, by using [`kes.exe host_service`](CommandLine.md#host_service-command).</span><span class="sxs-lookup"><span data-stu-id="14034-148">For rapid prototyping, you can host the grammar and index in a web service on the local machine, by using [`kes.exe host_service`](CommandLine.md#host_service-command).</span></span> <span data-ttu-id="14034-149">You can then access the service via [web APIs](WebAPI.md) to validate the data correctness and grammar design.</span><span class="sxs-lookup"><span data-stu-id="14034-149">You can then access the service via [web APIs](WebAPI.md) to validate the data correctness and grammar design.</span></span> <span data-ttu-id="14034-150">In this example, you host the grammar file *Academic.grammar* and index file *Academic.index* at http://localhost:8000/.</span><span class="sxs-lookup"><span data-stu-id="14034-150">In this example, you host the grammar file *Academic.grammar* and index file *Academic.index* at http://localhost:8000/.</span></span> <span data-ttu-id="14034-151">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="14034-151">Use the following command:</span></span>

`kes.exe host_service Academic.grammar Academic.index --port 8000`

<span data-ttu-id="14034-152">This initiates a local instance of the web service.</span><span class="sxs-lookup"><span data-stu-id="14034-152">This initiates a local instance of the web service.</span></span> <span data-ttu-id="14034-153">You can interactively test the service by visiting `http::localhost:<port>` from a browser.</span><span class="sxs-lookup"><span data-stu-id="14034-153">You can interactively test the service by visiting `http::localhost:<port>` from a browser.</span></span> <span data-ttu-id="14034-154">For more information, see [Testing service](#testing-service).</span><span class="sxs-lookup"><span data-stu-id="14034-154">For more information, see [Testing service](#testing-service).</span></span>

<span data-ttu-id="14034-155">You can also directly call various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span><span class="sxs-lookup"><span data-stu-id="14034-155">You can also directly call various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span></span> <span data-ttu-id="14034-156">To stop the service, enter "quit" into the `kes.exe host_service` command prompt, or press Ctrl+C.</span><span class="sxs-lookup"><span data-stu-id="14034-156">To stop the service, enter "quit" into the `kes.exe host_service` command prompt, or press Ctrl+C.</span></span> <span data-ttu-id="14034-157">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="14034-157">Here are some examples:</span></span>

* [<span data-ttu-id="14034-158">http://localhost:8000/interpret?query=papers by susan t dumais</span><span class="sxs-lookup"><span data-stu-id="14034-158">http://localhost:8000/interpret?query=papers by susan t dumais</span></span>](http://localhost:8000/interpret?query=papers%20by%20susan%20t%20dumais)
* [<span data-ttu-id="14034-159">http://localhost:8000/interpret?query=papers by susan t d&complete=1</span><span class="sxs-lookup"><span data-stu-id="14034-159">http://localhost:8000/interpret?query=papers by susan t d&complete=1</span></span>](http://localhost:8000/interpret?query=papers%20by%20susan%20t%20d&complete=1)
* [<span data-ttu-id="14034-160">http://localhost:8000/evaluate?expr=Composite(Author.Name=='susan t dumais')&attributes=Title,Year,Author.Name,Author.Id&count=2</span><span class="sxs-lookup"><span data-stu-id="14034-160">http://localhost:8000/evaluate?expr=Composite(Author.Name=='susan t dumais')&attributes=Title,Year,Author.Name,Author.Id&count=2</span></span>](http://localhost:8000/evaluate?expr=Composite%28Author.Name==%27susan%20t%20dumais%27%29&attributes=Title,Year,Author.Name,Author.Id&count=2)
* [<span data-ttu-id="14034-161">http://localhost:8000/calchistogram?expr=And(Composite(Author.Name=='susan t dumais'),Year>=2013)&attributes=Year,Keyword&count=4</span><span class="sxs-lookup"><span data-stu-id="14034-161">http://localhost:8000/calchistogram?expr=And(Composite(Author.Name=='susan t dumais'),Year>=2013)&attributes=Year,Keyword&count=4</span></span>](http://localhost:8000/calchistogram?expr=And%28Composite%28Author.Name=='susan%20t%20dumais'%29,Year>=2013%29&attributes=Year,Keyword&count=4)

<span data-ttu-id="14034-162">Outside of Azure, [`kes.exe host_service`](CommandLine.md#host_service-command) is limited to indices of up to 10,000 objects.</span><span class="sxs-lookup"><span data-stu-id="14034-162">Outside of Azure, [`kes.exe host_service`](CommandLine.md#host_service-command) is limited to indices of up to 10,000 objects.</span></span> <span data-ttu-id="14034-163">Other limits include an API rate of 10 requests per second, and a total of 1000 requests before the process automatically terminates.</span><span class="sxs-lookup"><span data-stu-id="14034-163">Other limits include an API rate of 10 requests per second, and a total of 1000 requests before the process automatically terminates.</span></span> <span data-ttu-id="14034-164">To bypass these restrictions, run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or deploy to an Azure cloud service by using the [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) command.</span><span class="sxs-lookup"><span data-stu-id="14034-164">To bypass these restrictions, run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or deploy to an Azure cloud service by using the [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) command.</span></span> <span data-ttu-id="14034-165">For details, see [Deploying service](#deploying-service).</span><span class="sxs-lookup"><span data-stu-id="14034-165">For details, see [Deploying service](#deploying-service).</span></span>

<a name="scaling-up"></a>
## <a name="scale-up-to-host-larger-indices"></a><span data-ttu-id="14034-166">Scale up to host larger indices</span><span class="sxs-lookup"><span data-stu-id="14034-166">Scale up to host larger indices</span></span>
<span data-ttu-id="14034-167">When you are running `kes.exe` outside of Azure, the index is limited to 10,000 objects.</span><span class="sxs-lookup"><span data-stu-id="14034-167">When you are running `kes.exe` outside of Azure, the index is limited to 10,000 objects.</span></span> <span data-ttu-id="14034-168">You can build and host larger indices by using Azure.</span><span class="sxs-lookup"><span data-stu-id="14034-168">You can build and host larger indices by using Azure.</span></span> <span data-ttu-id="14034-169">Sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14034-169">Sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="14034-170">Alternatively, if you subscribe to Visual Studio or MSDN, you can [activate subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="14034-170">Alternatively, if you subscribe to Visual Studio or MSDN, you can [activate subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="14034-171">These offer some Azure credits each month.</span><span class="sxs-lookup"><span data-stu-id="14034-171">These offer some Azure credits each month.</span></span>

<span data-ttu-id="14034-172">To allow `kes.exe` access to an Azure account, [download the Azure Publish Settings file](https://portal.azure.com/#blade/Microsoft_Azure_ClassicResources/PublishingProfileBlade) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="14034-172">To allow `kes.exe` access to an Azure account, [download the Azure Publish Settings file](https://portal.azure.com/#blade/Microsoft_Azure_ClassicResources/PublishingProfileBlade) from the Azure portal.</span></span> <span data-ttu-id="14034-173">If prompted, sign into the desired Azure account.</span><span class="sxs-lookup"><span data-stu-id="14034-173">If prompted, sign into the desired Azure account.</span></span> <span data-ttu-id="14034-174">Save the file as *AzurePublishSettings.xml* in the working directory from where `kes.exe` runs.</span><span class="sxs-lookup"><span data-stu-id="14034-174">Save the file as *AzurePublishSettings.xml* in the working directory from where `kes.exe` runs.</span></span>

<span data-ttu-id="14034-175">There are two ways to build and host large indices.</span><span class="sxs-lookup"><span data-stu-id="14034-175">There are two ways to build and host large indices.</span></span> <span data-ttu-id="14034-176">The first is to prepare the schema and data files in a Windows VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="14034-176">The first is to prepare the schema and data files in a Windows VM in Azure.</span></span> <span data-ttu-id="14034-177">Then run [`kes.exe build_index`](#building-index) to build the index locally on the VM, without any size restrictions.</span><span class="sxs-lookup"><span data-stu-id="14034-177">Then run [`kes.exe build_index`](#building-index) to build the index locally on the VM, without any size restrictions.</span></span> <span data-ttu-id="14034-178">The resulting index can be hosted locally on the VM by using [`kes.exe host_service`](#hosting-service) for rapid prototyping, again without any restrictions.</span><span class="sxs-lookup"><span data-stu-id="14034-178">The resulting index can be hosted locally on the VM by using [`kes.exe host_service`](#hosting-service) for rapid prototyping, again without any restrictions.</span></span> <span data-ttu-id="14034-179">For detailed steps, see the [Azure VM tutorial](../../../articles/virtual-machines/windows/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14034-179">For detailed steps, see the [Azure VM tutorial](../../../articles/virtual-machines/windows/quick-create-portal.md).</span></span>

<span data-ttu-id="14034-180">The second method is to perform a remote Azure build, by using [`kes.exe build_index`](CommandLine.md#build_index-command) with the `--remote` parameter.</span><span class="sxs-lookup"><span data-stu-id="14034-180">The second method is to perform a remote Azure build, by using [`kes.exe build_index`](CommandLine.md#build_index-command) with the `--remote` parameter.</span></span> <span data-ttu-id="14034-181">This specifies an Azure VM size.</span><span class="sxs-lookup"><span data-stu-id="14034-181">This specifies an Azure VM size.</span></span> <span data-ttu-id="14034-182">When the `--remote` parameter is specified, the command creates a temporary Azure VM of that size.</span><span class="sxs-lookup"><span data-stu-id="14034-182">When the `--remote` parameter is specified, the command creates a temporary Azure VM of that size.</span></span> <span data-ttu-id="14034-183">It then builds the index on the VM, uploads the index to the target blob storage, and deletes the VM upon completion.</span><span class="sxs-lookup"><span data-stu-id="14034-183">It then builds the index on the VM, uploads the index to the target blob storage, and deletes the VM upon completion.</span></span> <span data-ttu-id="14034-184">Your Azure subscription is charged for the cost of the VM while the index is being built.</span><span class="sxs-lookup"><span data-stu-id="14034-184">Your Azure subscription is charged for the cost of the VM while the index is being built.</span></span>

<span data-ttu-id="14034-185">This remote Azure build capability allows [`kes.exe build_index`](CommandLine.md#build_index-command) to be run in any environment.</span><span class="sxs-lookup"><span data-stu-id="14034-185">This remote Azure build capability allows [`kes.exe build_index`](CommandLine.md#build_index-command) to be run in any environment.</span></span> <span data-ttu-id="14034-186">When you are performing a remote build, the input schema and data arguments can be local file paths or [Azure blob storage](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) URLs.</span><span class="sxs-lookup"><span data-stu-id="14034-186">When you are performing a remote build, the input schema and data arguments can be local file paths or [Azure blob storage](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) URLs.</span></span> <span data-ttu-id="14034-187">The output index argument must be a blob storage URL.</span><span class="sxs-lookup"><span data-stu-id="14034-187">The output index argument must be a blob storage URL.</span></span> <span data-ttu-id="14034-188">To create an Azure storage account, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="14034-188">To create an Azure storage account, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="14034-189">To copy files efficiently to and from blob storage, use the [AzCopy](../../storage/common/storage-use-azcopy.md) utility.</span><span class="sxs-lookup"><span data-stu-id="14034-189">To copy files efficiently to and from blob storage, use the [AzCopy](../../storage/common/storage-use-azcopy.md) utility.</span></span>

<span data-ttu-id="14034-190">In this example, you can assume that the following blob storage container has already been created: http://&lt;*account*&gt;.blob.core.windows.net/&lt;*container*&gt;/.</span><span class="sxs-lookup"><span data-stu-id="14034-190">In this example, you can assume that the following blob storage container has already been created: http://&lt;*account*&gt;.blob.core.windows.net/&lt;*container*&gt;/.</span></span> <span data-ttu-id="14034-191">It contains the schema *Academic.schema*, the referenced synonym file *Keywords.syn*, and the full-scale data file *Academic.full.data*.</span><span class="sxs-lookup"><span data-stu-id="14034-191">It contains the schema *Academic.schema*, the referenced synonym file *Keywords.syn*, and the full-scale data file *Academic.full.data*.</span></span> <span data-ttu-id="14034-192">You can build the full index remotely by using the following command:</span><span class="sxs-lookup"><span data-stu-id="14034-192">You can build the full index remotely by using the following command:</span></span>

`kes.exe build_index http://<account>.blob.core.windows.net/<container>/Academic.schema http://<account>.blob.core.windows.net/<container>/Academic.full.data http://<account>.blob.core.windows.net/<container>/Academic.full.index --remote <vm_size>`

<span data-ttu-id="14034-193">Note that it might take 5-10 minutes to provision a temporay VM to build the index.</span><span class="sxs-lookup"><span data-stu-id="14034-193">Note that it might take 5-10 minutes to provision a temporay VM to build the index.</span></span> <span data-ttu-id="14034-194">For rapid prototyping, you can:</span><span class="sxs-lookup"><span data-stu-id="14034-194">For rapid prototyping, you can:</span></span>
- <span data-ttu-id="14034-195">Develop with a smaller data set locally on any machine.</span><span class="sxs-lookup"><span data-stu-id="14034-195">Develop with a smaller data set locally on any machine.</span></span>
- <span data-ttu-id="14034-196">Manually [create an Azure VM](../../../articles/virtual-machines/windows/quick-create-portal.md), [connect to it](../../../articles/virtual-machines/windows/quick-create-portal.md#connect-to-virtual-machine) via Remote Desktop, install the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488), and run [`kes.exe`](CommandLine.md) from within the VM.</span><span class="sxs-lookup"><span data-stu-id="14034-196">Manually [create an Azure VM](../../../articles/virtual-machines/windows/quick-create-portal.md), [connect to it](../../../articles/virtual-machines/windows/quick-create-portal.md#connect-to-virtual-machine) via Remote Desktop, install the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488), and run [`kes.exe`](CommandLine.md) from within the VM.</span></span>

<span data-ttu-id="14034-197">Paging slows down the build process.</span><span class="sxs-lookup"><span data-stu-id="14034-197">Paging slows down the build process.</span></span> <span data-ttu-id="14034-198">To avoid paging, use a VM with three times the amount of RAM as the input data file size for index building.</span><span class="sxs-lookup"><span data-stu-id="14034-198">To avoid paging, use a VM with three times the amount of RAM as the input data file size for index building.</span></span> <span data-ttu-id="14034-199">Use a VM with 1 GB more RAM than the index size for hosting.</span><span class="sxs-lookup"><span data-stu-id="14034-199">Use a VM with 1 GB more RAM than the index size for hosting.</span></span> <span data-ttu-id="14034-200">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="14034-200">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span></span>

<a name="deploying-service"></a>
## <a name="deploy-the-service"></a><span data-ttu-id="14034-201">Deploy the service</span><span class="sxs-lookup"><span data-stu-id="14034-201">Deploy the service</span></span>
<span data-ttu-id="14034-202">After you have a grammar and index, you are ready to deploy the service to an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="14034-202">After you have a grammar and index, you are ready to deploy the service to an Azure cloud service.</span></span> <span data-ttu-id="14034-203">To create a new Azure cloud service, see [How to create and deploy a cloud service](../../../articles/cloud-services/cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14034-203">To create a new Azure cloud service, see [How to create and deploy a cloud service](../../../articles/cloud-services/cloud-services-how-to-create-deploy-portal.md).</span></span> <span data-ttu-id="14034-204">Do not specify a deployment package at this point.</span><span class="sxs-lookup"><span data-stu-id="14034-204">Do not specify a deployment package at this point.</span></span>  

<span data-ttu-id="14034-205">When you have created the cloud service, you can use [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) to deploy the service.</span><span class="sxs-lookup"><span data-stu-id="14034-205">When you have created the cloud service, you can use [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) to deploy the service.</span></span> <span data-ttu-id="14034-206">An Azure cloud service has two deployment slots: production and staging.</span><span class="sxs-lookup"><span data-stu-id="14034-206">An Azure cloud service has two deployment slots: production and staging.</span></span> <span data-ttu-id="14034-207">For a service that receives live user traffic, you should initially deploy to the staging slot.</span><span class="sxs-lookup"><span data-stu-id="14034-207">For a service that receives live user traffic, you should initially deploy to the staging slot.</span></span> <span data-ttu-id="14034-208">Wait for the service to start up and initialize itself.</span><span class="sxs-lookup"><span data-stu-id="14034-208">Wait for the service to start up and initialize itself.</span></span> <span data-ttu-id="14034-209">Then you can send a few requests to validate the deployment and verify that it passes basic tests.</span><span class="sxs-lookup"><span data-stu-id="14034-209">Then you can send a few requests to validate the deployment and verify that it passes basic tests.</span></span>

<span data-ttu-id="14034-210">[Swap](../../../articles/cloud-services/cloud-services-nodejs-stage-application.md) the contents of the staging slot with the production slot, so that live traffic is now directed to the newly deployed service.</span><span class="sxs-lookup"><span data-stu-id="14034-210">[Swap](../../../articles/cloud-services/cloud-services-nodejs-stage-application.md) the contents of the staging slot with the production slot, so that live traffic is now directed to the newly deployed service.</span></span> <span data-ttu-id="14034-211">You can repeat this process when deploying an updated version of the service with new data.</span><span class="sxs-lookup"><span data-stu-id="14034-211">You can repeat this process when deploying an updated version of the service with new data.</span></span> <span data-ttu-id="14034-212">As with all other Azure cloud services, you can optionally use the Azure portal to configure [auto-scaling](../../../articles/cloud-services/cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14034-212">As with all other Azure cloud services, you can optionally use the Azure portal to configure [auto-scaling](../../../articles/cloud-services/cloud-services-how-to-scale-portal.md).</span></span>

<span data-ttu-id="14034-213">In this example, you deploy the *Academic* index to the staging slot of an existing cloud service with *<vm_size>* VMs.</span><span class="sxs-lookup"><span data-stu-id="14034-213">In this example, you deploy the *Academic* index to the staging slot of an existing cloud service with *<vm_size>* VMs.</span></span> <span data-ttu-id="14034-214">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="14034-214">Use the following command:</span></span>

`kes.exe deploy_service http://<account>.blob.core.windows.net/<container>/Academic.grammar http://<account>.blob.core.windows.net/<container>/Academic.index <serviceName> <vm_size> --slot Staging`

<span data-ttu-id="14034-215">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="14034-215">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span></span>

<span data-ttu-id="14034-216">After you deploy the service, you can call the various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span><span class="sxs-lookup"><span data-stu-id="14034-216">After you deploy the service, you can call the various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span></span>  

<a name="testing-service"></a>
## <a name="test-the-service"></a><span data-ttu-id="14034-217">Test the service</span><span class="sxs-lookup"><span data-stu-id="14034-217">Test the service</span></span>
<span data-ttu-id="14034-218">To debug a live service, browse to the host machine from a web browser.</span><span class="sxs-lookup"><span data-stu-id="14034-218">To debug a live service, browse to the host machine from a web browser.</span></span> <span data-ttu-id="14034-219">For a local service deployed via [host_service](#hosting-service), visit `http://localhost:<port>/`.</span><span class="sxs-lookup"><span data-stu-id="14034-219">For a local service deployed via [host_service](#hosting-service), visit `http://localhost:<port>/`.</span></span>  <span data-ttu-id="14034-220">For an Azure cloud service deployed via [deploy_service](#deploying-service), visit `http://<serviceName>.cloudapp.net/`.</span><span class="sxs-lookup"><span data-stu-id="14034-220">For an Azure cloud service deployed via [deploy_service](#deploying-service), visit `http://<serviceName>.cloudapp.net/`.</span></span>

<span data-ttu-id="14034-221">This page contains a link to information about basic API call statistics, as well as the grammar and index hosted at this service.</span><span class="sxs-lookup"><span data-stu-id="14034-221">This page contains a link to information about basic API call statistics, as well as the grammar and index hosted at this service.</span></span> <span data-ttu-id="14034-222">This page also contains an interactive search interface that demonstrates the use of the web APIs.</span><span class="sxs-lookup"><span data-stu-id="14034-222">This page also contains an interactive search interface that demonstrates the use of the web APIs.</span></span> <span data-ttu-id="14034-223">Enter queries into the search box to see the results of the [interpret](interpretMethod.md), [evaluate](evaluateMethod.md), and [calchistogram](calchistogramMethod.md) API calls.</span><span class="sxs-lookup"><span data-stu-id="14034-223">Enter queries into the search box to see the results of the [interpret](interpretMethod.md), [evaluate](evaluateMethod.md), and [calchistogram](calchistogramMethod.md) API calls.</span></span> <span data-ttu-id="14034-224">The underlying HTML source of this page also serves as an example of how to integrate the web APIs into an app, to create a rich, interactive search experience.</span><span class="sxs-lookup"><span data-stu-id="14034-224">The underlying HTML source of this page also serves as an example of how to integrate the web APIs into an app, to create a rich, interactive search experience.</span></span>


