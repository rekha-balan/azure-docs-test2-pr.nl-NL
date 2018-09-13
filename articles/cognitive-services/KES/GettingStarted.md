---
title: Get started with the Knowledge Exploration Service | Microsoft Docs
description: Use Knowledge Exploration Service (KES) to create an engine for an interactive search experience across academic publications in Microsoft Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 98105091624ba3864fd18d42d1640792e622f2a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552487"
---
<a name="getting-started"></a>
# <a name="getting-started"></a><span data-ttu-id="43508-103">Getting Started</span><span class="sxs-lookup"><span data-stu-id="43508-103">Getting Started</span></span>
<span data-ttu-id="43508-104">In this walkthrough, we will use the Knowledge Exploration Service (KES) to create the backend engine for an interactive search experience over academic publications.</span><span class="sxs-lookup"><span data-stu-id="43508-104">In this walkthrough, we will use the Knowledge Exploration Service (KES) to create the backend engine for an interactive search experience over academic publications.</span></span>  <span data-ttu-id="43508-105">The command line tool [`kes.exe`](CommandLine.md) and all example files can be installed from the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488).</span><span class="sxs-lookup"><span data-stu-id="43508-105">The command line tool [`kes.exe`](CommandLine.md) and all example files can be installed from the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488).</span></span>

<span data-ttu-id="43508-106">The academic publications example contains a sample of 1000 academic papers published by researchers at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43508-106">The academic publications example contains a sample of 1000 academic papers published by researchers at Microsoft.</span></span>  <span data-ttu-id="43508-107">Each paper is associated with a title, publication year, authors, and keywords.</span><span class="sxs-lookup"><span data-stu-id="43508-107">Each paper is associated with a title, publication year, authors, and keywords.</span></span>  <span data-ttu-id="43508-108">Each author is represented by an ID, name, and affiliation at the time of publication.</span><span class="sxs-lookup"><span data-stu-id="43508-108">Each author is represented by an ID, name, and affiliation at the time of publication.</span></span>  <span data-ttu-id="43508-109">Each keyword may be associated with a set of synonyms (ex.</span><span class="sxs-lookup"><span data-stu-id="43508-109">Each keyword may be associated with a set of synonyms (ex.</span></span> <span data-ttu-id="43508-110">*support vector machine* &rarr; *svm*).</span><span class="sxs-lookup"><span data-stu-id="43508-110">*support vector machine* &rarr; *svm*).</span></span>

<a name="defining-schema"></a>
## <a name="defining-schema"></a><span data-ttu-id="43508-111">Defining schema</span><span class="sxs-lookup"><span data-stu-id="43508-111">Defining schema</span></span>
<span data-ttu-id="43508-112">The schema describes the attribute structure of the objects in our domain.</span><span class="sxs-lookup"><span data-stu-id="43508-112">The schema describes the attribute structure of the objects in our domain.</span></span>  <span data-ttu-id="43508-113">It specifies the name and data type for each attribute in a JSON file format.</span><span class="sxs-lookup"><span data-stu-id="43508-113">It specifies the name and data type for each attribute in a JSON file format.</span></span>  <span data-ttu-id="43508-114">Below is the content of the file *Academic.schema* that we use in this example:</span><span class="sxs-lookup"><span data-stu-id="43508-114">Below is the content of the file *Academic.schema* that we use in this example:</span></span>

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

<span data-ttu-id="43508-115">Here, we define *Title*, *Year*, and *Keyword* as a string, integer, and string attribute, respectively.</span><span class="sxs-lookup"><span data-stu-id="43508-115">Here, we define *Title*, *Year*, and *Keyword* as a string, integer, and string attribute, respectively.</span></span>  <span data-ttu-id="43508-116">Since authors are represented by their ID, name, and affiliation, we define *Author* as a Composite attribute with 3 sub-attributes: *Author.Id*, *Author.Name*, and *Author.Affiliation*.</span><span class="sxs-lookup"><span data-stu-id="43508-116">Since authors are represented by their ID, name, and affiliation, we define *Author* as a Composite attribute with 3 sub-attributes: *Author.Id*, *Author.Name*, and *Author.Affiliation*.</span></span>

<span data-ttu-id="43508-117">By default, attributes support all operations available for their data type, including *equals*, *starts_with*, *is_between*, etc.  Since author ID is only used internally as an identifier, we override the default and specify *equals* as the only indexed operation.</span><span class="sxs-lookup"><span data-stu-id="43508-117">By default, attributes support all operations available for their data type, including *equals*, *starts_with*, *is_between*, etc.  Since author ID is only used internally as an identifier, we override the default and specify *equals* as the only indexed operation.</span></span>

<span data-ttu-id="43508-118">For the *Keyword* attribute, we allow synonyms to match the canonical keyword values by specifying the synonym file *Keyword.syn* in the attribute definition.</span><span class="sxs-lookup"><span data-stu-id="43508-118">For the *Keyword* attribute, we allow synonyms to match the canonical keyword values by specifying the synonym file *Keyword.syn* in the attribute definition.</span></span>  <span data-ttu-id="43508-119">This file contains a list of canonical and synonym value pairs:</span><span class="sxs-lookup"><span data-stu-id="43508-119">This file contains a list of canonical and synonym value pairs:</span></span>

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

<span data-ttu-id="43508-120">See [Schema Format](SchemaFormat.md) for additional information about the schema definition.</span><span class="sxs-lookup"><span data-stu-id="43508-120">See [Schema Format](SchemaFormat.md) for additional information about the schema definition.</span></span>

<a name="generating-data"></a>
## <a name="generating-data"></a><span data-ttu-id="43508-121">Generating data</span><span class="sxs-lookup"><span data-stu-id="43508-121">Generating data</span></span>
<span data-ttu-id="43508-122">The data file describes the list of the publications to index, with each line specifying the attribute values of a paper in [JSON format](http://json.org/).</span><span class="sxs-lookup"><span data-stu-id="43508-122">The data file describes the list of the publications to index, with each line specifying the attribute values of a paper in [JSON format](http://json.org/).</span></span>  <span data-ttu-id="43508-123">Below is a single line from the data file *Academic.data*, formatted for readability:</span><span class="sxs-lookup"><span data-stu-id="43508-123">Below is a single line from the data file *Academic.data*, formatted for readability:</span></span>

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

<span data-ttu-id="43508-124">In this snippet, we specify the *Title* and *Year* attribute of the paper as a JSON string and number, respectively.</span><span class="sxs-lookup"><span data-stu-id="43508-124">In this snippet, we specify the *Title* and *Year* attribute of the paper as a JSON string and number, respectively.</span></span>  <span data-ttu-id="43508-125">Multiple values are represented using JSON arrays.</span><span class="sxs-lookup"><span data-stu-id="43508-125">Multiple values are represented using JSON arrays.</span></span>  <span data-ttu-id="43508-126">Since "Author" is a composite attribute, each value is represented using a JSON object consisting of its sub-attributes.</span><span class="sxs-lookup"><span data-stu-id="43508-126">Since "Author" is a composite attribute, each value is represented using a JSON object consisting of its sub-attributes.</span></span>  <span data-ttu-id="43508-127">Attributes with missing values, such as "Keyword" in this case, can be excluded from the JSON representation.</span><span class="sxs-lookup"><span data-stu-id="43508-127">Attributes with missing values, such as "Keyword" in this case, can be excluded from the JSON representation.</span></span>

<span data-ttu-id="43508-128">To differentiate the likelihood of different papers, we specify the relative log probability using the built-in "logprob" attribute.</span><span class="sxs-lookup"><span data-stu-id="43508-128">To differentiate the likelihood of different papers, we specify the relative log probability using the built-in "logprob" attribute.</span></span>  <span data-ttu-id="43508-129">Given a probability *p* between 0 and 1, we compute the log probability as log(*p*), where log() is the natural log function.</span><span class="sxs-lookup"><span data-stu-id="43508-129">Given a probability *p* between 0 and 1, we compute the log probability as log(*p*), where log() is the natural log function.</span></span>

<span data-ttu-id="43508-130">See [Data Format](DataFormat.md) for additional information about the data format.</span><span class="sxs-lookup"><span data-stu-id="43508-130">See [Data Format](DataFormat.md) for additional information about the data format.</span></span>

<a name="building-index"></a>
## <a name="building-index"></a><span data-ttu-id="43508-131">Building index</span><span class="sxs-lookup"><span data-stu-id="43508-131">Building index</span></span>
<span data-ttu-id="43508-132">Once we have a schema file and data file, we can build a compressed binary index of the data objects using [`kes.exe build_index`](CommandLine.md#build_index-command).</span><span class="sxs-lookup"><span data-stu-id="43508-132">Once we have a schema file and data file, we can build a compressed binary index of the data objects using [`kes.exe build_index`](CommandLine.md#build_index-command).</span></span>  <span data-ttu-id="43508-133">In this example, we build the index file *Academic.index* from the input schema file *Academic.schema* and data file *Academic.data* using the following command:</span><span class="sxs-lookup"><span data-stu-id="43508-133">In this example, we build the index file *Academic.index* from the input schema file *Academic.schema* and data file *Academic.data* using the following command:</span></span>

`kes.exe build_index Academic.schema Academic.data Academic.index`

<span data-ttu-id="43508-134">For rapid prototyping outside of Azure, [`kes.exe build_index`](CommandLine.md#build_index-command) can build small indices locally from data files containing up to 10,000 objects.</span><span class="sxs-lookup"><span data-stu-id="43508-134">For rapid prototyping outside of Azure, [`kes.exe build_index`](CommandLine.md#build_index-command) can build small indices locally from data files containing up to 10,000 objects.</span></span>  <span data-ttu-id="43508-135">For larger data files, we can either run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or perform a remote build in Azure.</span><span class="sxs-lookup"><span data-stu-id="43508-135">For larger data files, we can either run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or perform a remote build in Azure.</span></span>  <span data-ttu-id="43508-136">See [Scaling up](#scaling-up) for details.</span><span class="sxs-lookup"><span data-stu-id="43508-136">See [Scaling up](#scaling-up) for details.</span></span>

<a name="authoring-grammar"></a>
## <a name="authoring-grammar"></a><span data-ttu-id="43508-137">Authoring grammar</span><span class="sxs-lookup"><span data-stu-id="43508-137">Authoring grammar</span></span>
<span data-ttu-id="43508-138">The grammar specifies the set of natural language queries that the service can interpret, as well as how these natural language queries are translated into semantic query expressions.</span><span class="sxs-lookup"><span data-stu-id="43508-138">The grammar specifies the set of natural language queries that the service can interpret, as well as how these natural language queries are translated into semantic query expressions.</span></span>  <span data-ttu-id="43508-139">In this example, we use the grammar specified in *academic.xml*:</span><span class="sxs-lookup"><span data-stu-id="43508-139">In this example, we use the grammar specified in *academic.xml*:</span></span>

```xml
<grammar root="GetPapers">

  <!-- Import academic data schema-->
  <import schema="academic.schema" name="academic"/>

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

<span data-ttu-id="43508-140">For more information about the grammar specification syntax, see [Grammar Format](GrammarFormat.md).</span><span class="sxs-lookup"><span data-stu-id="43508-140">For more information about the grammar specification syntax, see [Grammar Format](GrammarFormat.md).</span></span>

<a name="compiling-grammar"></a>
## <a name="compiling-grammar"></a><span data-ttu-id="43508-141">Compiling grammar</span><span class="sxs-lookup"><span data-stu-id="43508-141">Compiling grammar</span></span>
<span data-ttu-id="43508-142">Once we have an XML grammar specification, we can compile it into a binary grammar using [`kes.exe build_grammar`](CommandLine.md#build_grammar-command).</span><span class="sxs-lookup"><span data-stu-id="43508-142">Once we have an XML grammar specification, we can compile it into a binary grammar using [`kes.exe build_grammar`](CommandLine.md#build_grammar-command).</span></span>  <span data-ttu-id="43508-143">Note that if the grammar imports a schema, the schema file needs to be located in the same path as the grammar XML.</span><span class="sxs-lookup"><span data-stu-id="43508-143">Note that if the grammar imports a schema, the schema file needs to be located in the same path as the grammar XML.</span></span>  <span data-ttu-id="43508-144">In this example, we build the binary grammar file *Academic.grammar* from the input XML grammar file *Academic.xml* using the following command:</span><span class="sxs-lookup"><span data-stu-id="43508-144">In this example, we build the binary grammar file *Academic.grammar* from the input XML grammar file *Academic.xml* using the following command:</span></span>

`kes.exe build_grammar Academic.xml Academic.grammar`

<a name="hosting-index"></a>
## <a name="hosting-service"></a><span data-ttu-id="43508-145">Hosting service</span><span class="sxs-lookup"><span data-stu-id="43508-145">Hosting service</span></span>
<span data-ttu-id="43508-146">For rapid prototyping, we can host the grammar and index in a web service on the local machine using [`kes.exe host_service`](CommandLine.md#host_service-command).</span><span class="sxs-lookup"><span data-stu-id="43508-146">For rapid prototyping, we can host the grammar and index in a web service on the local machine using [`kes.exe host_service`](CommandLine.md#host_service-command).</span></span>  <span data-ttu-id="43508-147">Once hosted, we can access the service via [web APIs](WebAPI.md) to validate the data correctness and grammar design.</span><span class="sxs-lookup"><span data-stu-id="43508-147">Once hosted, we can access the service via [web APIs](WebAPI.md) to validate the data correctness and grammar design.</span></span>  <span data-ttu-id="43508-148">In this example, we host the grammar file *Academic.grammar* and index file *Academic.index* at http://localhost:8000/ using the following command:</span><span class="sxs-lookup"><span data-stu-id="43508-148">In this example, we host the grammar file *Academic.grammar* and index file *Academic.index* at http://localhost:8000/ using the following command:</span></span>

`kes.exe host_service Academic.grammar Academic.index --port 8000`

<span data-ttu-id="43508-149">This initiates a local instance of the web service.</span><span class="sxs-lookup"><span data-stu-id="43508-149">This initiates a local instance of the web service.</span></span>  <span data-ttu-id="43508-150">We can interactively test the service by visiting `http::localhost:<port>` from a browser.</span><span class="sxs-lookup"><span data-stu-id="43508-150">We can interactively test the service by visiting `http::localhost:<port>` from a browser.</span></span>  <span data-ttu-id="43508-151">For more information, see [Testing service](#testing-service).</span><span class="sxs-lookup"><span data-stu-id="43508-151">For more information, see [Testing service](#testing-service).</span></span>  <span data-ttu-id="43508-152">We can also directly call various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span><span class="sxs-lookup"><span data-stu-id="43508-152">We can also directly call various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span></span>  <span data-ttu-id="43508-153">To stop the service, enter 'quit' into the `kes.exe host_service` command prompt or press 'Ctrl+C'.</span><span class="sxs-lookup"><span data-stu-id="43508-153">To stop the service, enter 'quit' into the `kes.exe host_service` command prompt or press 'Ctrl+C'.</span></span>

* [<span data-ttu-id="43508-154">http://localhost:8000/interpret?query=papers by susan t dumais</span><span class="sxs-lookup"><span data-stu-id="43508-154">http://localhost:8000/interpret?query=papers by susan t dumais</span></span>](http://localhost:8000/interpret?query=papers%20by%20susan%20t%20dumais)
* [<span data-ttu-id="43508-155">http://localhost:8000/interpret?query=papers by susan t d&complete=1</span><span class="sxs-lookup"><span data-stu-id="43508-155">http://localhost:8000/interpret?query=papers by susan t d&complete=1</span></span>](http://localhost:8000/interpret?query=papers%20by%20susan%20t%20d&complete=1)
* [<span data-ttu-id="43508-156">http://localhost:8000/evaluate?expr=Composite(Author.Name=='susan t dumais')&attributes=Title,Year,Author.Name,Author.Id&count=2</span><span class="sxs-lookup"><span data-stu-id="43508-156">http://localhost:8000/evaluate?expr=Composite(Author.Name=='susan t dumais')&attributes=Title,Year,Author.Name,Author.Id&count=2</span></span>](http://localhost:8000/evaluate?expr=Composite%28Author.Name==%27susan%20t%20dumais%27%29&attributes=Title,Year,Author.Name,Author.Id&count=2)
* [<span data-ttu-id="43508-157">http://localhost:8000/calchistogram?expr=And(Composite(Author.Name=='susan t dumais'),Year>=2013)&attributes=Year,Keyword&count=4</span><span class="sxs-lookup"><span data-stu-id="43508-157">http://localhost:8000/calchistogram?expr=And(Composite(Author.Name=='susan t dumais'),Year>=2013)&attributes=Year,Keyword&count=4</span></span>](http://localhost:8000/calchistogram?expr=And%28Composite%28Author.Name=='susan%20t%20dumais'%29,Year>=2013%29&attributes=Year,Keyword&count=4)

<span data-ttu-id="43508-158">Outside of Azure, [`kes.exe host_service`](CommandLine.md#host_service-command) is limited to indices of up to 10,000 objects, an API rate of 10 requests per second, and a total of 1000 requests before the process automatically terminates.</span><span class="sxs-lookup"><span data-stu-id="43508-158">Outside of Azure, [`kes.exe host_service`](CommandLine.md#host_service-command) is limited to indices of up to 10,000 objects, an API rate of 10 requests per second, and a total of 1000 requests before the process automatically terminates.</span></span>  <span data-ttu-id="43508-159">To bypass these restrictions, we can run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or deploy to an Azure cloud service using the [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) command.</span><span class="sxs-lookup"><span data-stu-id="43508-159">To bypass these restrictions, we can run the command from within a [Windows VM in Azure](../../../articles/virtual-machines/windows/quick-create-portal.md), or deploy to an Azure cloud service using the [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) command.</span></span>  <span data-ttu-id="43508-160">See [Deploying service](#deploying-service) for details.</span><span class="sxs-lookup"><span data-stu-id="43508-160">See [Deploying service](#deploying-service) for details.</span></span>

<a name="scaling-up"></a>
## <a name="scaling-up"></a><span data-ttu-id="43508-161">Scaling up</span><span class="sxs-lookup"><span data-stu-id="43508-161">Scaling up</span></span>
<span data-ttu-id="43508-162">When running `kes.exe` outside of Azure, the index is limited to 10,000 objects.</span><span class="sxs-lookup"><span data-stu-id="43508-162">When running `kes.exe` outside of Azure, the index is limited to 10,000 objects.</span></span>  <span data-ttu-id="43508-163">Once we are ready to scale up, we can build and host larger indices using Azure.</span><span class="sxs-lookup"><span data-stu-id="43508-163">Once we are ready to scale up, we can build and host larger indices using Azure.</span></span>  <span data-ttu-id="43508-164">We can sign up for a [free trial](https://azure.microsoft.com/en-us/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43508-164">We can sign up for a [free trial](https://azure.microsoft.com/en-us/pricing/free-trial/).</span></span>  <span data-ttu-id="43508-165">Alternatively, for Visual Studio/MSDN subscriber, we can [activate subscriber benefits](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/) which offer some Azure credits each month.</span><span class="sxs-lookup"><span data-stu-id="43508-165">Alternatively, for Visual Studio/MSDN subscriber, we can [activate subscriber benefits](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/) which offer some Azure credits each month.</span></span>

<span data-ttu-id="43508-166">To allow `kes.exe` access to an Azure account, visit https://manage.windowsazure.com/publishsettings/ to download the Azure Publish Settings file.</span><span class="sxs-lookup"><span data-stu-id="43508-166">To allow `kes.exe` access to an Azure account, visit https://manage.windowsazure.com/publishsettings/ to download the Azure Publish Settings file.</span></span>  <span data-ttu-id="43508-167">If prompted, sign into the desired Azure account.</span><span class="sxs-lookup"><span data-stu-id="43508-167">If prompted, sign into the desired Azure account.</span></span>  <span data-ttu-id="43508-168">Once signed in, the browser will automatically download the Publish Settings file.</span><span class="sxs-lookup"><span data-stu-id="43508-168">Once signed in, the browser will automatically download the Publish Settings file.</span></span>  <span data-ttu-id="43508-169">Save it as *AzurePublishSettings.xml* in the working directory from where `kes.exe` runs.</span><span class="sxs-lookup"><span data-stu-id="43508-169">Save it as *AzurePublishSettings.xml* in the working directory from where `kes.exe` runs.</span></span>

<span data-ttu-id="43508-170">There are two ways to build and host large indices.</span><span class="sxs-lookup"><span data-stu-id="43508-170">There are two ways to build and host large indices.</span></span>  <span data-ttu-id="43508-171">The first is to prepare the schema and data files in a Windows VM in Azure and run [`kes.exe build_index`](#building-index) to build the index locally on the VM without any size restrictions.</span><span class="sxs-lookup"><span data-stu-id="43508-171">The first is to prepare the schema and data files in a Windows VM in Azure and run [`kes.exe build_index`](#building-index) to build the index locally on the VM without any size restrictions.</span></span>  <span data-ttu-id="43508-172">The resulting index can be hosted locally on the VM using [`kes.exe host_service`](#hosting-service) for rapid prototyping, again without any restrictions.</span><span class="sxs-lookup"><span data-stu-id="43508-172">The resulting index can be hosted locally on the VM using [`kes.exe host_service`](#hosting-service) for rapid prototyping, again without any restrictions.</span></span>  <span data-ttu-id="43508-173">See the [Azure VM tutorial](../../../articles/virtual-machines/windows/quick-create-portal.md) for detailed steps to create an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="43508-173">See the [Azure VM tutorial](../../../articles/virtual-machines/windows/quick-create-portal.md) for detailed steps to create an Azure VM.</span></span>

<span data-ttu-id="43508-174">The second method is to perform a remote Azure build using [`kes.exe build_index`](CommandLine.md#build_index-command) with the `--remote` parameter, which specifies an Azure VM size.</span><span class="sxs-lookup"><span data-stu-id="43508-174">The second method is to perform a remote Azure build using [`kes.exe build_index`](CommandLine.md#build_index-command) with the `--remote` parameter, which specifies an Azure VM size.</span></span>  <span data-ttu-id="43508-175">When the `--remote` parameter is specified, the command creates a temporary Azure VM of that size, builds the index on the VM, uploads the index to the target blob storage, and deletes the VM upon completion.</span><span class="sxs-lookup"><span data-stu-id="43508-175">When the `--remote` parameter is specified, the command creates a temporary Azure VM of that size, builds the index on the VM, uploads the index to the target blob storage, and deletes the VM upon completion.</span></span>  <span data-ttu-id="43508-176">Your Azure subscription is charged for the cost of the VM while the index is being built.</span><span class="sxs-lookup"><span data-stu-id="43508-176">Your Azure subscription is charged for the cost of the VM while the index is being built.</span></span>  <span data-ttu-id="43508-177">This remote Azure build capability allows [`kes.exe build_index`](CommandLine.md#build_index-command) to be executed in any environment.</span><span class="sxs-lookup"><span data-stu-id="43508-177">This remote Azure build capability allows [`kes.exe build_index`](CommandLine.md#build_index-command) to be executed in any environment.</span></span>  <span data-ttu-id="43508-178">When performing a remote build, the input schema and data arguments may be local file paths or [Azure blob storage](../../../articles/storage/storage-dotnet-how-to-use-blobs.md) URLs.</span><span class="sxs-lookup"><span data-stu-id="43508-178">When performing a remote build, the input schema and data arguments may be local file paths or [Azure blob storage](../../../articles/storage/storage-dotnet-how-to-use-blobs.md) URLs.</span></span>  <span data-ttu-id="43508-179">The output index argument must be a blob storage URL.</span><span class="sxs-lookup"><span data-stu-id="43508-179">The output index argument must be a blob storage URL.</span></span>  <span data-ttu-id="43508-180">To create an Azure storage account, see [Create Storage Account](../../../articles/storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="43508-180">To create an Azure storage account, see [Create Storage Account](../../../articles/storage/storage-create-storage-account.md).</span></span>  <span data-ttu-id="43508-181">Note that only classic storage accounts are supported at this time.</span><span class="sxs-lookup"><span data-stu-id="43508-181">Note that only classic storage accounts are supported at this time.</span></span>  <span data-ttu-id="43508-182">We can use the utility [AzCopy](../../../articles/storage/storage-use-azcopy.md) to efficiently copy files to and from blob storage.</span><span class="sxs-lookup"><span data-stu-id="43508-182">We can use the utility [AzCopy](../../../articles/storage/storage-use-azcopy.md) to efficiently copy files to and from blob storage.</span></span>

<span data-ttu-id="43508-183">In this example, we assume that the blob storage container http://&lt;*account*&gt;.blob.core.windows.net/&lt;*container*&gt;/ has already been created, containing the schema *Academic.schema*, referenced synonym file *Keywords.syn*, and full-scale data file *Academic.full.data*.</span><span class="sxs-lookup"><span data-stu-id="43508-183">In this example, we assume that the blob storage container http://&lt;*account*&gt;.blob.core.windows.net/&lt;*container*&gt;/ has already been created, containing the schema *Academic.schema*, referenced synonym file *Keywords.syn*, and full-scale data file *Academic.full.data*.</span></span>  <span data-ttu-id="43508-184">We can build the full index remotely using the following command:</span><span class="sxs-lookup"><span data-stu-id="43508-184">We can build the full index remotely using the following command:</span></span>

`kes.exe build_index http://<account>.blob.core.windows.net/<container>/Academic.schema http://<account>.blob.core.windows.net/<container>/Academic.full.data http://<account>.blob.core.windows.net/<container>/Academic.full.index --remote Large`

<span data-ttu-id="43508-185">Note that it may take 5-10 minutes to provision a temporay VM to build the index.</span><span class="sxs-lookup"><span data-stu-id="43508-185">Note that it may take 5-10 minutes to provision a temporay VM to build the index.</span></span>  <span data-ttu-id="43508-186">Thus, for rapid prototyping, we recommend one of two options:</span><span class="sxs-lookup"><span data-stu-id="43508-186">Thus, for rapid prototyping, we recommend one of two options:</span></span>
  1. <span data-ttu-id="43508-187">Develop with a smaller data set locally on any machine.</span><span class="sxs-lookup"><span data-stu-id="43508-187">Develop with a smaller data set locally on any machine.</span></span>
  2. <span data-ttu-id="43508-188">Manually [create an Azure VM](../../../articles/virtual-machines/windows/quick-create-portal.md), [connect to it](../../../articles/virtual-machines/windows/quick-create-portal.md#connect-to-virtual-machine) via Remote Desktop, install the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488), and run [`kes.exe`](CommandLine.md) from within the VM.</span><span class="sxs-lookup"><span data-stu-id="43508-188">Manually [create an Azure VM](../../../articles/virtual-machines/windows/quick-create-portal.md), [connect to it](../../../articles/virtual-machines/windows/quick-create-portal.md#connect-to-virtual-machine) via Remote Desktop, install the [Knowledge Exploration Service SDK](https://www.microsoft.com/en-us/download/details.aspx?id=51488), and run [`kes.exe`](CommandLine.md) from within the VM.</span></span>

<span data-ttu-id="43508-189">To avoid paging which slows down the build process, we recommend using a VM with 3 times the amount of RAM as the input data file size for index building, and a VM with 1 GB more RAM than the index size for hosting.</span><span class="sxs-lookup"><span data-stu-id="43508-189">To avoid paging which slows down the build process, we recommend using a VM with 3 times the amount of RAM as the input data file size for index building, and a VM with 1 GB more RAM than the index size for hosting.</span></span>  <span data-ttu-id="43508-190">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="43508-190">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span></span>

<a name="deploying-service"></a>
## <a name="deploying-service"></a><span data-ttu-id="43508-191">Deploying service</span><span class="sxs-lookup"><span data-stu-id="43508-191">Deploying service</span></span>
<span data-ttu-id="43508-192">Once we have a grammar and index, we are ready to deploy the service to an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="43508-192">Once we have a grammar and index, we are ready to deploy the service to an Azure cloud service.</span></span>  <span data-ttu-id="43508-193">To create a new Azure cloud service, see [How to Create and Deploy a Cloud Service](../../../articles/cloud-services/cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43508-193">To create a new Azure cloud service, see [How to Create and Deploy a Cloud Service](../../../articles/cloud-services/cloud-services-how-to-create-deploy-portal.md).</span></span>  <span data-ttu-id="43508-194">Do not specify a deployment package at this point.</span><span class="sxs-lookup"><span data-stu-id="43508-194">Do not specify a deployment package at this point.</span></span>  

<span data-ttu-id="43508-195">Once the cloud service has been created, we can use [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) to deploy the service.</span><span class="sxs-lookup"><span data-stu-id="43508-195">Once the cloud service has been created, we can use [`kes.exe deploy_service`](CommandLine.md#deploy_service-command) to deploy the service.</span></span>  <span data-ttu-id="43508-196">An Azure cloud service has two deployment slots: Production and Staging.</span><span class="sxs-lookup"><span data-stu-id="43508-196">An Azure cloud service has two deployment slots: Production and Staging.</span></span>  <span data-ttu-id="43508-197">For a service that receives live user traffic, we should initially deploy to the Staging slot and wait for the service to start up and initialize itself.</span><span class="sxs-lookup"><span data-stu-id="43508-197">For a service that receives live user traffic, we should initially deploy to the Staging slot and wait for the service to start up and initialize itself.</span></span>  <span data-ttu-id="43508-198">Once the service is running, we can send a few requests to validate the deployment and verify that it passes basic tests.</span><span class="sxs-lookup"><span data-stu-id="43508-198">Once the service is running, we can send a few requests to validate the deployment and verify that it passes basic tests.</span></span>  <span data-ttu-id="43508-199">Then, we [swap](../../../articles/cloud-services/cloud-services-nodejs-stage-application.md) the contents of the Staging slot with the Production slot so that live traffic will now be directed to the newly deployed service.</span><span class="sxs-lookup"><span data-stu-id="43508-199">Then, we [swap](../../../articles/cloud-services/cloud-services-nodejs-stage-application.md) the contents of the Staging slot with the Production slot so that live traffic will now be directed to the newly deployed service.</span></span>  <span data-ttu-id="43508-200">We can repeat this process when deploying an updated version of the service with new data.</span><span class="sxs-lookup"><span data-stu-id="43508-200">We can repeat this process when deploying an updated version of the service with new data.</span></span>  <span data-ttu-id="43508-201">Like all other Azure cloud services, we can optionally use the Azure portal to configure [auto-scaling](../../../articles/cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="43508-201">Like all other Azure cloud services, we can optionally use the Azure portal to configure [auto-scaling](../../../articles/cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="43508-202">In this example, we will deploy the Academic index to the staging slot of an existing cloud service with *large* VMs using the following command:</span><span class="sxs-lookup"><span data-stu-id="43508-202">In this example, we will deploy the Academic index to the staging slot of an existing cloud service with *large* VMs using the following command:</span></span>

`kes.exe deploy_service http://<account>.blob.core.windows.net/<container>/Academic.grammar http://<account>.blob.core.windows.net/<container>/Academic.index <serviceName> large --slot Staging`

<span data-ttu-id="43508-203">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="43508-203">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span></span>  <span data-ttu-id="43508-204">Once the service has been deployed, we can call the various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span><span class="sxs-lookup"><span data-stu-id="43508-204">Once the service has been deployed, we can call the various [web APIs](WebAPI.md) to test natural language interpretation, query completion, structured query evaluation, and histogram computation.</span></span>  

<a name="testing-service"></a>
## <a name="testing-service"></a><span data-ttu-id="43508-205">Testing service</span><span class="sxs-lookup"><span data-stu-id="43508-205">Testing service</span></span>
<span data-ttu-id="43508-206">To debug a live service, we can simply navigate to the host machine from a web browser.</span><span class="sxs-lookup"><span data-stu-id="43508-206">To debug a live service, we can simply navigate to the host machine from a web browser.</span></span>  <span data-ttu-id="43508-207">For a local service deployed via [host_service](#hosting-service), visit `http://localhost:<port>/`.</span><span class="sxs-lookup"><span data-stu-id="43508-207">For a local service deployed via [host_service](#hosting-service), visit `http://localhost:<port>/`.</span></span>  <span data-ttu-id="43508-208">For an Azure cloud service deployed via [deploy_service](#deploying-service), visit `http://<serviceName>.cloudapp.net/`.</span><span class="sxs-lookup"><span data-stu-id="43508-208">For an Azure cloud service deployed via [deploy_service](#deploying-service), visit `http://<serviceName>.cloudapp.net/`.</span></span>  <span data-ttu-id="43508-209">This page contains a link to information about basic API call statistics as well as the grammar and index hosted at this service.</span><span class="sxs-lookup"><span data-stu-id="43508-209">This page contains a link to information about basic API call statistics as well as the grammar and index hosted at this service.</span></span> <span data-ttu-id="43508-210">This page also contains an interactive search interface that demonstrates the use of the web APIs.</span><span class="sxs-lookup"><span data-stu-id="43508-210">This page also contains an interactive search interface that demonstrates the use of the web APIs.</span></span>  <span data-ttu-id="43508-211">We can enter queries interactively into the search box to see the results of the [interpret](interpretMethod.md), [evaluate](evaluateMethod.md), and [calchistogram](calchistogramMethod.md) API calls.</span><span class="sxs-lookup"><span data-stu-id="43508-211">We can enter queries interactively into the search box to see the results of the [interpret](interpretMethod.md), [evaluate](evaluateMethod.md), and [calchistogram](calchistogramMethod.md) API calls.</span></span>  <span data-ttu-id="43508-212">The underlying HTML source of this page also serves as an example of how to integrate the web APIs into an app to create a rich interactive search experience.</span><span class="sxs-lookup"><span data-stu-id="43508-212">The underlying HTML source of this page also serves as an example of how to integrate the web APIs into an app to create a rich interactive search experience.</span></span>


