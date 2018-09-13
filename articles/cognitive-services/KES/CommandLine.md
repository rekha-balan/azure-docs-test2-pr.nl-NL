---
title: Knowledge Exploration Service command-line interface | Microsoft Docs
description: Use the KES command-line interface to build index and grammar files from structured data, and then deploy them as web services in Microsoft Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/24/2016
ms.author: paulhsu
ms.openlocfilehash: d6a892e6391805babcaa40a3ecb471c0e7e4342f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553992"
---
# <a name="command-line-interface"></a><span data-ttu-id="0b1d4-103">Command Line Interface</span><span class="sxs-lookup"><span data-stu-id="0b1d4-103">Command Line Interface</span></span>
<span data-ttu-id="0b1d4-104">The KES command line interface provides the ability to build index and grammar files from structured data and deploy them as web services.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-104">The KES command line interface provides the ability to build index and grammar files from structured data and deploy them as web services.</span></span>  <span data-ttu-id="0b1d4-105">It uses the general syntax: `kes.exe <command> <required_args> [<optional_args>]`.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-105">It uses the general syntax: `kes.exe <command> <required_args> [<optional_args>]`.</span></span>  <span data-ttu-id="0b1d4-106">You can run `kes.exe` without arguments to display a list of commands, or `kes.exe <command>` to display a list of arguments available for the specified command.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-106">You can run `kes.exe` without arguments to display a list of commands, or `kes.exe <command>` to display a list of arguments available for the specified command.</span></span>  <span data-ttu-id="0b1d4-107">Below is a list of available commands:</span><span class="sxs-lookup"><span data-stu-id="0b1d4-107">Below is a list of available commands:</span></span>
* <span data-ttu-id="0b1d4-108">build_index</span><span class="sxs-lookup"><span data-stu-id="0b1d4-108">build_index</span></span>
* <span data-ttu-id="0b1d4-109">build_grammar</span><span class="sxs-lookup"><span data-stu-id="0b1d4-109">build_grammar</span></span>
* <span data-ttu-id="0b1d4-110">host_service</span><span class="sxs-lookup"><span data-stu-id="0b1d4-110">host_service</span></span>
* <span data-ttu-id="0b1d4-111">deploy_service</span><span class="sxs-lookup"><span data-stu-id="0b1d4-111">deploy_service</span></span>
* <span data-ttu-id="0b1d4-112">describe_index</span><span class="sxs-lookup"><span data-stu-id="0b1d4-112">describe_index</span></span>
* <span data-ttu-id="0b1d4-113">describe_grammar</span><span class="sxs-lookup"><span data-stu-id="0b1d4-113">describe_grammar</span></span>

<a name="build_index-command"></a>
## <a name="buildindex-command"></a><span data-ttu-id="0b1d4-114">build_index Command</span><span class="sxs-lookup"><span data-stu-id="0b1d4-114">build_index Command</span></span>
<span data-ttu-id="0b1d4-115">The **build_index** command builds a binary index file from a schema definition file and a data file of objects to be indexed.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-115">The **build_index** command builds a binary index file from a schema definition file and a data file of objects to be indexed.</span></span>  <span data-ttu-id="0b1d4-116">The resulting index file can be used to evaluate structured query expressions, or to generate interpretations of natural language queries in conjunction with a compiled grammar file.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-116">The resulting index file can be used to evaluate structured query expressions, or to generate interpretations of natural language queries in conjunction with a compiled grammar file.</span></span>

`kes.exe build_index <schemaFile> <dataFile> <indexFile> [options]`

| <span data-ttu-id="0b1d4-117">Parameter</span><span class="sxs-lookup"><span data-stu-id="0b1d4-117">Parameter</span></span>      | <span data-ttu-id="0b1d4-118">Description</span><span class="sxs-lookup"><span data-stu-id="0b1d4-118">Description</span></span>               |
|----------------|---------------------------|
| `<schemaFile>` | <span data-ttu-id="0b1d4-119">Input schema path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-119">Input schema path</span></span> |
| `<dataFile>`   | <span data-ttu-id="0b1d4-120">Input data path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-120">Input data path</span></span>   |
| `<indexFile>`  | <span data-ttu-id="0b1d4-121">Output index path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-121">Output index path</span></span> |
| `--description <description>` | <span data-ttu-id="0b1d4-122">Description string</span><span class="sxs-lookup"><span data-stu-id="0b1d4-122">Description string</span></span> |
| `--remote <vmSize>`           | <span data-ttu-id="0b1d4-123">Size of VM for remote build</span><span class="sxs-lookup"><span data-stu-id="0b1d4-123">Size of VM for remote build</span></span> |

<span data-ttu-id="0b1d4-124">These files may be specified by local file paths or URL paths to Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-124">These files may be specified by local file paths or URL paths to Azure blobs.</span></span>  <span data-ttu-id="0b1d4-125">The schema file describes the structure of the objects being indexed as well as the operations to be supported (see [Schema Format](SchemaFormat.md)).</span><span class="sxs-lookup"><span data-stu-id="0b1d4-125">The schema file describes the structure of the objects being indexed as well as the operations to be supported (see [Schema Format](SchemaFormat.md)).</span></span>  <span data-ttu-id="0b1d4-126">The data file enumerates the objects and attribute values to be indexed (see [Data Format](DataFormat.md)).</span><span class="sxs-lookup"><span data-stu-id="0b1d4-126">The data file enumerates the objects and attribute values to be indexed (see [Data Format](DataFormat.md)).</span></span>  <span data-ttu-id="0b1d4-127">When the build succeeds, the output index file contains a compressed representation of the input data that supports the desired operations.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-127">When the build succeeds, the output index file contains a compressed representation of the input data that supports the desired operations.</span></span>  

<span data-ttu-id="0b1d4-128">A description string may be optionally specified to subsequently identify a binary index using the **describe_index** command.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-128">A description string may be optionally specified to subsequently identify a binary index using the **describe_index** command.</span></span>  

<span data-ttu-id="0b1d4-129">By default, the index is built on the local machine.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-129">By default, the index is built on the local machine.</span></span>  <span data-ttu-id="0b1d4-130">Outside of the Azure environment, local builds are limited to data files containing up to 10,000 objects.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-130">Outside of the Azure environment, local builds are limited to data files containing up to 10,000 objects.</span></span>  <span data-ttu-id="0b1d4-131">When the --remote flag is specified, the index will be built on a temporarily created Azure VM of the specified size.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-131">When the --remote flag is specified, the index will be built on a temporarily created Azure VM of the specified size.</span></span>  <span data-ttu-id="0b1d4-132">This allows large indices to be built efficiently using Azure VMs with more memory.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-132">This allows large indices to be built efficiently using Azure VMs with more memory.</span></span>  <span data-ttu-id="0b1d4-133">To avoid paging which slows down the build process, we recommend using a VM with 3 times the amount of RAM as the input data file size.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-133">To avoid paging which slows down the build process, we recommend using a VM with 3 times the amount of RAM as the input data file size.</span></span>  <span data-ttu-id="0b1d4-134">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d4-134">For a list of available VM sizes, see [Sizes for virtual machines](../../../articles/virtual-machines/virtual-machines-windows-sizes.md).</span></span>

> [!TIP] 
> <span data-ttu-id="0b1d4-135">For faster builds, presort the objects in the data file by decreasing probability.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-135">For faster builds, presort the objects in the data file by decreasing probability.</span></span>

<a name="build_grammar-command"></a>
## <a name="buildgrammar-command"></a><span data-ttu-id="0b1d4-136">build_grammar Command</span><span class="sxs-lookup"><span data-stu-id="0b1d4-136">build_grammar Command</span></span>
<span data-ttu-id="0b1d4-137">The **build_grammar** command compiles a grammar specified in XML to a binary grammar file.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-137">The **build_grammar** command compiles a grammar specified in XML to a binary grammar file.</span></span>  <span data-ttu-id="0b1d4-138">The resulting grammar file can be used in conjunction with an index file to generate interpretations of natural language queries.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-138">The resulting grammar file can be used in conjunction with an index file to generate interpretations of natural language queries.</span></span>

`kes.exe build_grammar <xmlFile> <grammarFile>`

| <span data-ttu-id="0b1d4-139">Parameter</span><span class="sxs-lookup"><span data-stu-id="0b1d4-139">Parameter</span></span>       | <span data-ttu-id="0b1d4-140">Description</span><span class="sxs-lookup"><span data-stu-id="0b1d4-140">Description</span></span>               |
|-----------------|---------------------------|
| `<xmlFile>`     | <span data-ttu-id="0b1d4-141">Input XML grammar specification path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-141">Input XML grammar specification path</span></span> |
| `<grammarFile>` | <span data-ttu-id="0b1d4-142">Output compiled grammar path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-142">Output compiled grammar path</span></span>         |

<span data-ttu-id="0b1d4-143">These files may be specified by local file paths or URL paths to Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-143">These files may be specified by local file paths or URL paths to Azure blobs.</span></span>  <span data-ttu-id="0b1d4-144">The grammar specification describes the set of weighted natural language expressions and their semantic interpretations (see [Grammar Format](GrammarFormat.md)).</span><span class="sxs-lookup"><span data-stu-id="0b1d4-144">The grammar specification describes the set of weighted natural language expressions and their semantic interpretations (see [Grammar Format](GrammarFormat.md)).</span></span>  <span data-ttu-id="0b1d4-145">When the build succeeds, the output grammar file contains a binary representation of the grammar specification to enable fast decoding.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-145">When the build succeeds, the output grammar file contains a binary representation of the grammar specification to enable fast decoding.</span></span>

<a name="host_service-command"/>
## <a name="hostservice-command"></a><span data-ttu-id="0b1d4-146">host_service Command</span><span class="sxs-lookup"><span data-stu-id="0b1d4-146">host_service Command</span></span>
<span data-ttu-id="0b1d4-147">The **host_service** command hosts an instance of the KES service on the local machine.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-147">The **host_service** command hosts an instance of the KES service on the local machine.</span></span>

`kes.exe host_service <grammarFile> <indexFile> [options]`

| <span data-ttu-id="0b1d4-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="0b1d4-148">Parameter</span></span>       | <span data-ttu-id="0b1d4-149">Description</span><span class="sxs-lookup"><span data-stu-id="0b1d4-149">Description</span></span>                |
|-----------------|----------------------------|
| `<grammarFile>` | <span data-ttu-id="0b1d4-150">Input binary grammar path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-150">Input binary grammar path</span></span>         |
| `<indexFile>`   | <span data-ttu-id="0b1d4-151">Input binary index path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-151">Input binary index path</span></span>           |
| `--port <port>` | <span data-ttu-id="0b1d4-152">Local port number.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-152">Local port number.</span></span>  <span data-ttu-id="0b1d4-153">Default: 8000</span><span class="sxs-lookup"><span data-stu-id="0b1d4-153">Default: 8000</span></span> |

<span data-ttu-id="0b1d4-154">These files may be specified by local file paths or URL paths to Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-154">These files may be specified by local file paths or URL paths to Azure blobs.</span></span>  <span data-ttu-id="0b1d4-155">A web service will be hosted at http://localhost:&lt;port&gt;/.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-155">A web service will be hosted at http://localhost:&lt;port&gt;/.</span></span>  <span data-ttu-id="0b1d4-156">See [Web APIs](WebAPI.md) for a list of supported operations.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-156">See [Web APIs](WebAPI.md) for a list of supported operations.</span></span>

<span data-ttu-id="0b1d4-157">Outside of the Azure environment, locally hosted services are limited to index files up to 1 MB in size, 10 requests per second, and 1000 total calls.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-157">Outside of the Azure environment, locally hosted services are limited to index files up to 1 MB in size, 10 requests per second, and 1000 total calls.</span></span>  <span data-ttu-id="0b1d4-158">To overcome these limitations, run **host_service** inside an Azure VM, or deploy to an Azure cloud service using **deploy_service**.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-158">To overcome these limitations, run **host_service** inside an Azure VM, or deploy to an Azure cloud service using **deploy_service**.</span></span>

<a name="deploy_service-command"/>
## <a name="deployservice-command"></a><span data-ttu-id="0b1d4-159">deploy_service Command</span><span class="sxs-lookup"><span data-stu-id="0b1d4-159">deploy_service Command</span></span>
<span data-ttu-id="0b1d4-160">The **deploy_service** command deploys an instance of the KES service to an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-160">The **deploy_service** command deploys an instance of the KES service to an Azure cloud service.</span></span>

`kes.exe deploy_service <grammarFile> <indexFile> <serviceName> <vmSize>[options]`

| <span data-ttu-id="0b1d4-161">Parameter</span><span class="sxs-lookup"><span data-stu-id="0b1d4-161">Parameter</span></span>       | <span data-ttu-id="0b1d4-162">Description</span><span class="sxs-lookup"><span data-stu-id="0b1d4-162">Description</span></span>                  |
|-----------------|------------------------------|
| `<grammarFile>` | <span data-ttu-id="0b1d4-163">Input binary grammar path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-163">Input binary grammar path</span></span>           |
| `<indexFile>`   | <span data-ttu-id="0b1d4-164">Input binary index path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-164">Input binary index path</span></span>             |
| `<serviceName>` | <span data-ttu-id="0b1d4-165">Name of target cloud service</span><span class="sxs-lookup"><span data-stu-id="0b1d4-165">Name of target cloud service</span></span> |
| `<vmSize>`      | <span data-ttu-id="0b1d4-166">Size of cloud service VM</span><span class="sxs-lookup"><span data-stu-id="0b1d4-166">Size of cloud service VM</span></span>     |
| `--slot <slot>` | <span data-ttu-id="0b1d4-167">Cloud service slot: "staging" (default), "production"</span><span class="sxs-lookup"><span data-stu-id="0b1d4-167">Cloud service slot: "staging" (default), "production"</span></span> |

<span data-ttu-id="0b1d4-168">These files may be specified by local file paths or URL paths to Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-168">These files may be specified by local file paths or URL paths to Azure blobs.</span></span>  <span data-ttu-id="0b1d4-169">Service name specifies a preconfigured Azure cloud service (see [How to Create and Deploy a Cloud Service](../../../articles/cloud-services/cloud-services-how-to-create-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="0b1d4-169">Service name specifies a preconfigured Azure cloud service (see [How to Create and Deploy a Cloud Service](../../../articles/cloud-services/cloud-services-how-to-create-deploy-portal.md)).</span></span>  <span data-ttu-id="0b1d4-170">The command will automatically deploy the KES service to the specified Azure cloud service, using VMs of the specified size.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-170">The command will automatically deploy the KES service to the specified Azure cloud service, using VMs of the specified size.</span></span>  <span data-ttu-id="0b1d4-171">To avoid paging which significantly decreases performance, we recommend using a VM with 1 GB more RAM than the input index file size.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-171">To avoid paging which significantly decreases performance, we recommend using a VM with 1 GB more RAM than the input index file size.</span></span>  <span data-ttu-id="0b1d4-172">For a list of available VM sizes, see [Sizes for Cloud Services](../../../articles/cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d4-172">For a list of available VM sizes, see [Sizes for Cloud Services](../../../articles/cloud-services/cloud-services-sizes-specs.md).</span></span>

<span data-ttu-id="0b1d4-173">By default, the service is deployed to the staging environment, optionally overridden via the --slot parameter.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-173">By default, the service is deployed to the staging environment, optionally overridden via the --slot parameter.</span></span>  <span data-ttu-id="0b1d4-174">See [Web APIs](WebAPI.md) for a list of supported operations.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-174">See [Web APIs](WebAPI.md) for a list of supported operations.</span></span>

<a name="describe_index-command"/>
## <a name="describeindex-command"></a><span data-ttu-id="0b1d4-175">describe_index command</span><span class="sxs-lookup"><span data-stu-id="0b1d4-175">describe_index command</span></span>
<span data-ttu-id="0b1d4-176">The **describe_index** command outputs information about an index file, including the schema and description.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-176">The **describe_index** command outputs information about an index file, including the schema and description.</span></span>

`kes.exe describe_index <indexFile>`

| <span data-ttu-id="0b1d4-177">Parameter</span><span class="sxs-lookup"><span data-stu-id="0b1d4-177">Parameter</span></span>     | <span data-ttu-id="0b1d4-178">Description</span><span class="sxs-lookup"><span data-stu-id="0b1d4-178">Description</span></span>      |
|---------------|------------------|
| `<indexFile>` | <span data-ttu-id="0b1d4-179">Input index path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-179">Input index path</span></span> |

<span data-ttu-id="0b1d4-180">This file may be specified by a local file path or a URL path to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-180">This file may be specified by a local file path or a URL path to an Azure blob.</span></span>  <span data-ttu-id="0b1d4-181">The output description string can be specified using the --description parameter of the **build_index** command.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-181">The output description string can be specified using the --description parameter of the **build_index** command.</span></span>

<a name="describe_grammar-command"/>
## <a name="describegrammar-command"></a><span data-ttu-id="0b1d4-182">describe_grammar command</span><span class="sxs-lookup"><span data-stu-id="0b1d4-182">describe_grammar command</span></span>
<span data-ttu-id="0b1d4-183">The **describe_grammar** command outputs the original grammar specification used to build the binary grammar.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-183">The **describe_grammar** command outputs the original grammar specification used to build the binary grammar.</span></span>

`kes.exe describe_grammar <grammarFile>`

| <span data-ttu-id="0b1d4-184">Parameter</span><span class="sxs-lookup"><span data-stu-id="0b1d4-184">Parameter</span></span>       | <span data-ttu-id="0b1d4-185">Description</span><span class="sxs-lookup"><span data-stu-id="0b1d4-185">Description</span></span>      |
|-----------------|------------------|
| `<grammarFile>` | <span data-ttu-id="0b1d4-186">Input grammar path</span><span class="sxs-lookup"><span data-stu-id="0b1d4-186">Input grammar path</span></span> |

<span data-ttu-id="0b1d4-187">This file may be specified by a local file path or a URL path to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="0b1d4-187">This file may be specified by a local file path or a URL path to an Azure blob.</span></span>

