---
title: Get started with Azure Stack storage development tools  | Microsoft Docs
description: Guidance to get started with using Azure Stack storage development tools
services: azure-stack
author: mabriggs
ms.author: mabrigg
ms.date: 07/03/2018
ms.topic: get-started-article
ms.service: azure-stack
manager: femila
ms.reviewer: xiaofmao
ms.openlocfilehash: 40f256b7a2be5a5a1d642983fa6ce018ee602ac2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857154"
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="ef522-103">Get started with Azure Stack storage development tools</span><span class="sxs-lookup"><span data-stu-id="ef522-103">Get started with Azure Stack storage development tools</span></span>

<span data-ttu-id="ef522-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="ef522-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="ef522-105">Microsoft Azure Stack provides a set of storage services that includes blob, table, and queue storage.</span><span class="sxs-lookup"><span data-stu-id="ef522-105">Microsoft Azure Stack provides a set of storage services that includes blob, table, and queue storage.</span></span>

<span data-ttu-id="ef522-106">Use this article as a guide to get started using Azure Stack storage development tools.</span><span class="sxs-lookup"><span data-stu-id="ef522-106">Use this article as a guide to get started using Azure Stack storage development tools.</span></span> <span data-ttu-id="ef522-107">You can find more detailed information and sample code in corresponding Azure storage tutorials.</span><span class="sxs-lookup"><span data-stu-id="ef522-107">You can find more detailed information and sample code in corresponding Azure storage tutorials.</span></span>

> [!NOTE]  
> <span data-ttu-id="ef522-108">There are known differences between Azure Stack storage and Azure storage, including specific requirements for each platform.</span><span class="sxs-lookup"><span data-stu-id="ef522-108">There are known differences between Azure Stack storage and Azure storage, including specific requirements for each platform.</span></span> <span data-ttu-id="ef522-109">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ef522-109">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="ef522-110">For more information, see [Azure Stack storage: Differences and considerations](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="ef522-110">For more information, see [Azure Stack storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="ef522-111">Azure client libraries</span><span class="sxs-lookup"><span data-stu-id="ef522-111">Azure client libraries</span></span>

<span data-ttu-id="ef522-112">The supported REST API versions for Azure Stack storage are 2017-04-17, 2016-05-31, 2015-12-11, 2015-07-08, 2015-04-05 for the 1802 update or newer versions, and 2015-04-05 for previous versions.</span><span class="sxs-lookup"><span data-stu-id="ef522-112">The supported REST API versions for Azure Stack storage are 2017-04-17, 2016-05-31, 2015-12-11, 2015-07-08, 2015-04-05 for the 1802 update or newer versions, and 2015-04-05 for previous versions.</span></span> <span data-ttu-id="ef522-113">The Azure Stack endpoints do not have full parity with the latest version of the Azure storage REST API.</span><span class="sxs-lookup"><span data-stu-id="ef522-113">The Azure Stack endpoints do not have full parity with the latest version of the Azure storage REST API.</span></span> <span data-ttu-id="ef522-114">For the storage client libraries, you need to be aware of the version that is compatible with the REST API.</span><span class="sxs-lookup"><span data-stu-id="ef522-114">For the storage client libraries, you need to be aware of the version that is compatible with the REST API.</span></span>

### <a name="1802-update-or-newer-versions"></a><span data-ttu-id="ef522-115">1802 update or newer versions</span><span class="sxs-lookup"><span data-stu-id="ef522-115">1802 update or newer versions</span></span>

| <span data-ttu-id="ef522-116">Client library</span><span class="sxs-lookup"><span data-stu-id="ef522-116">Client library</span></span> | <span data-ttu-id="ef522-117">Azure Stack supported version</span><span class="sxs-lookup"><span data-stu-id="ef522-117">Azure Stack supported version</span></span> | <span data-ttu-id="ef522-118">Link</span><span class="sxs-lookup"><span data-stu-id="ef522-118">Link</span></span> | <span data-ttu-id="ef522-119">Endpoint specification</span><span class="sxs-lookup"><span data-stu-id="ef522-119">Endpoint specification</span></span> |
|----------------|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| <span data-ttu-id="ef522-120">.NET</span><span class="sxs-lookup"><span data-stu-id="ef522-120">.NET</span></span> | <span data-ttu-id="ef522-121">8.7.0</span><span class="sxs-lookup"><span data-stu-id="ef522-121">8.7.0</span></span> | <span data-ttu-id="ef522-122">Nuget package:</span><span class="sxs-lookup"><span data-stu-id="ef522-122">Nuget package:</span></span><br>https://www.nuget.org/packages/WindowsAzure.Storage/8.7.0<br> <br><span data-ttu-id="ef522-123">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-123">GitHub release:</span></span><br>https://github.com/Azure/azure-storage-net/releases/tag/v8.7.0 | <span data-ttu-id="ef522-124">app.config file</span><span class="sxs-lookup"><span data-stu-id="ef522-124">app.config file</span></span> |
| <span data-ttu-id="ef522-125">Java</span><span class="sxs-lookup"><span data-stu-id="ef522-125">Java</span></span> | <span data-ttu-id="ef522-126">6.1.0</span><span class="sxs-lookup"><span data-stu-id="ef522-126">6.1.0</span></span> | <span data-ttu-id="ef522-127">Maven package:</span><span class="sxs-lookup"><span data-stu-id="ef522-127">Maven package:</span></span><br>http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/6.1.0<br> <br><span data-ttu-id="ef522-128">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-128">GitHub release:</span></span><br>https://github.com/Azure/azure-storage-java/releases/tag/v6.1.0 | <span data-ttu-id="ef522-129">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-129">Connection string setup</span></span> |
| <span data-ttu-id="ef522-130">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef522-130">Node.js</span></span> | <span data-ttu-id="ef522-131">2.7.0</span><span class="sxs-lookup"><span data-stu-id="ef522-131">2.7.0</span></span> | <span data-ttu-id="ef522-132">NPM link:</span><span class="sxs-lookup"><span data-stu-id="ef522-132">NPM link:</span></span><br>https://www.npmjs.com/package/azure-storage<br><span data-ttu-id="ef522-133">(Run: `npm install azure-storage@2.7.0`)</span><span class="sxs-lookup"><span data-stu-id="ef522-133">(Run: `npm install azure-storage@2.7.0`)</span></span><br> <br><span data-ttu-id="ef522-134">Github release:</span><span class="sxs-lookup"><span data-stu-id="ef522-134">Github release:</span></span><br>https://github.com/Azure/azure-storage-node/releases/tag/v2.7.0 | <span data-ttu-id="ef522-135">Service instance declaration</span><span class="sxs-lookup"><span data-stu-id="ef522-135">Service instance declaration</span></span> |
| <span data-ttu-id="ef522-136">C++</span><span class="sxs-lookup"><span data-stu-id="ef522-136">C++</span></span> | <span data-ttu-id="ef522-137">3.1.0</span><span class="sxs-lookup"><span data-stu-id="ef522-137">3.1.0</span></span> | <span data-ttu-id="ef522-138">Nuget package:</span><span class="sxs-lookup"><span data-stu-id="ef522-138">Nuget package:</span></span><br>https://www.nuget.org/packages/wastorage.v140/3.1.0<br> <br><span data-ttu-id="ef522-139">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-139">GitHub release:</span></span><br>https://github.com/Azure/azure-storage-cpp/releases/tag/v3.1.0 | <span data-ttu-id="ef522-140">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-140">Connection string setup</span></span> |
| <span data-ttu-id="ef522-141">PHP</span><span class="sxs-lookup"><span data-stu-id="ef522-141">PHP</span></span> | <span data-ttu-id="ef522-142">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ef522-142">1.0.0</span></span> | <span data-ttu-id="ef522-143">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-143">GitHub release:</span></span><br><span data-ttu-id="ef522-144">Common: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-common</span><span class="sxs-lookup"><span data-stu-id="ef522-144">Common: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-common</span></span><br><span data-ttu-id="ef522-145">Blob: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-blob</span><span class="sxs-lookup"><span data-stu-id="ef522-145">Blob: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-blob</span></span><br><span data-ttu-id="ef522-146">Queue:</span><span class="sxs-lookup"><span data-stu-id="ef522-146">Queue:</span></span><br>https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-queue<br><span data-ttu-id="ef522-147">Table: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-table</span><span class="sxs-lookup"><span data-stu-id="ef522-147">Table: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-table</span></span><br> <br><span data-ttu-id="ef522-148">Install via Composer (To learn more, [See the details below](#install-php-client-via-composer---current).)</span><span class="sxs-lookup"><span data-stu-id="ef522-148">Install via Composer (To learn more, [See the details below](#install-php-client-via-composer---current).)</span></span> | <span data-ttu-id="ef522-149">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-149">Connection string setup</span></span> |
| <span data-ttu-id="ef522-150">Python</span><span class="sxs-lookup"><span data-stu-id="ef522-150">Python</span></span> | <span data-ttu-id="ef522-151">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ef522-151">1.0.0</span></span> | <span data-ttu-id="ef522-152">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-152">GitHub release:</span></span><br><span data-ttu-id="ef522-153">Common:</span><span class="sxs-lookup"><span data-stu-id="ef522-153">Common:</span></span><br>https://github.com/Azure/azure-storage-python/releases/tag/v1.0.0-common<br><span data-ttu-id="ef522-154">Blob:</span><span class="sxs-lookup"><span data-stu-id="ef522-154">Blob:</span></span><br>https://github.com/Azure/azure-storage-python/releases/tag/v1.0.0-blob<br><span data-ttu-id="ef522-155">Queue:</span><span class="sxs-lookup"><span data-stu-id="ef522-155">Queue:</span></span><br>https://github.com/Azure/azure-storage-python/releases/tag/v1.0.0-queue | <span data-ttu-id="ef522-156">Service instance declaration</span><span class="sxs-lookup"><span data-stu-id="ef522-156">Service instance declaration</span></span> |
| <span data-ttu-id="ef522-157">Ruby</span><span class="sxs-lookup"><span data-stu-id="ef522-157">Ruby</span></span> | <span data-ttu-id="ef522-158">1.0.1</span><span class="sxs-lookup"><span data-stu-id="ef522-158">1.0.1</span></span> | <span data-ttu-id="ef522-159">RubyGems package:</span><span class="sxs-lookup"><span data-stu-id="ef522-159">RubyGems package:</span></span><br><span data-ttu-id="ef522-160">Common:</span><span class="sxs-lookup"><span data-stu-id="ef522-160">Common:</span></span><br>https://rubygems.org/gems/azure-storage-common/versions/1.0.1<br><span data-ttu-id="ef522-161">Blob: https://rubygems.org/gems/azure-storage-blob/versions/1.0.1</span><span class="sxs-lookup"><span data-stu-id="ef522-161">Blob: https://rubygems.org/gems/azure-storage-blob/versions/1.0.1</span></span><br><span data-ttu-id="ef522-162">Queue: https://rubygems.org/gems/azure-storage-queue/versions/1.0.1</span><span class="sxs-lookup"><span data-stu-id="ef522-162">Queue: https://rubygems.org/gems/azure-storage-queue/versions/1.0.1</span></span><br><span data-ttu-id="ef522-163">Table: https://rubygems.org/gems/azure-storage-table/versions/1.0.1</span><span class="sxs-lookup"><span data-stu-id="ef522-163">Table: https://rubygems.org/gems/azure-storage-table/versions/1.0.1</span></span><br> <br><span data-ttu-id="ef522-164">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-164">GitHub release:</span></span><br><span data-ttu-id="ef522-165">Common: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-common</span><span class="sxs-lookup"><span data-stu-id="ef522-165">Common: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-common</span></span><br><span data-ttu-id="ef522-166">Blob: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-blob</span><span class="sxs-lookup"><span data-stu-id="ef522-166">Blob: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-blob</span></span><br><span data-ttu-id="ef522-167">Queue: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-queue</span><span class="sxs-lookup"><span data-stu-id="ef522-167">Queue: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-queue</span></span><br><span data-ttu-id="ef522-168">Table: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-table</span><span class="sxs-lookup"><span data-stu-id="ef522-168">Table: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-table</span></span> | <span data-ttu-id="ef522-169">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-169">Connection string setup</span></span> |

#### <a name="install-php-client-via-composer---current"></a><span data-ttu-id="ef522-170">Install PHP client via Composer - current</span><span class="sxs-lookup"><span data-stu-id="ef522-170">Install PHP client via Composer - current</span></span>

<span data-ttu-id="ef522-171">To install via Composer: (take blob as example).</span><span class="sxs-lookup"><span data-stu-id="ef522-171">To install via Composer: (take blob as example).</span></span>

1. <span data-ttu-id="ef522-172">Create a file named **composer.json** in the root of the project with following code:</span><span class="sxs-lookup"><span data-stu-id="ef522-172">Create a file named **composer.json** in the root of the project with following code:</span></span>

  ```php
    {
      "require": {
      "Microsoft/azure-storage-blob":"1.0.0"
      }
    }
  ```

2. <span data-ttu-id="ef522-173">Download [composer.phar](http://getcomposer.org/composer.phar) to the project root.</span><span class="sxs-lookup"><span data-stu-id="ef522-173">Download [composer.phar](http://getcomposer.org/composer.phar) to the project root.</span></span>
3. <span data-ttu-id="ef522-174">Run: `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="ef522-174">Run: `php composer.phar install`.</span></span>

### <a name="previous-versions"></a><span data-ttu-id="ef522-175">Previous versions</span><span class="sxs-lookup"><span data-stu-id="ef522-175">Previous versions</span></span>

|<span data-ttu-id="ef522-176">Client library</span><span class="sxs-lookup"><span data-stu-id="ef522-176">Client library</span></span>|<span data-ttu-id="ef522-177">Azure Stack supported version</span><span class="sxs-lookup"><span data-stu-id="ef522-177">Azure Stack supported version</span></span>|<span data-ttu-id="ef522-178">Link</span><span class="sxs-lookup"><span data-stu-id="ef522-178">Link</span></span>|<span data-ttu-id="ef522-179">Endpoint specification</span><span class="sxs-lookup"><span data-stu-id="ef522-179">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="ef522-180">.NET</span><span class="sxs-lookup"><span data-stu-id="ef522-180">.NET</span></span>     |<span data-ttu-id="ef522-181">6.2.0</span><span class="sxs-lookup"><span data-stu-id="ef522-181">6.2.0</span></span>|<span data-ttu-id="ef522-182">Nuget package:</span><span class="sxs-lookup"><span data-stu-id="ef522-182">Nuget package:</span></span><br>[https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="ef522-183">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-183">GitHub release:</span></span><br>[https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="ef522-184">app.config file</span><span class="sxs-lookup"><span data-stu-id="ef522-184">app.config file</span></span>|
|<span data-ttu-id="ef522-185">Java</span><span class="sxs-lookup"><span data-stu-id="ef522-185">Java</span></span>|<span data-ttu-id="ef522-186">4.1.0</span><span class="sxs-lookup"><span data-stu-id="ef522-186">4.1.0</span></span>|<span data-ttu-id="ef522-187">Maven package:</span><span class="sxs-lookup"><span data-stu-id="ef522-187">Maven package:</span></span><br>[http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="ef522-188">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-188">GitHub release:</span></span><br> [https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="ef522-189">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-189">Connection string setup</span></span>|
|<span data-ttu-id="ef522-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef522-190">Node.js</span></span>     |<span data-ttu-id="ef522-191">1.1.0</span><span class="sxs-lookup"><span data-stu-id="ef522-191">1.1.0</span></span>|<span data-ttu-id="ef522-192">NPM link:</span><span class="sxs-lookup"><span data-stu-id="ef522-192">NPM link:</span></span><br>[https://www.npmjs.com/package/azure-storage](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="ef522-193">(run: `npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="ef522-193">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="ef522-194">Github release:</span><span class="sxs-lookup"><span data-stu-id="ef522-194">Github release:</span></span><br>[https://github.com/Azure/azure-storage-node/releases/tag/1.1.0](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="ef522-195">Service instance declaration</span><span class="sxs-lookup"><span data-stu-id="ef522-195">Service instance declaration</span></span>||<span data-ttu-id="ef522-196">C++</span><span class="sxs-lookup"><span data-stu-id="ef522-196">C++</span></span>|<span data-ttu-id="ef522-197">2.4.0</span><span class="sxs-lookup"><span data-stu-id="ef522-197">2.4.0</span></span>|<span data-ttu-id="ef522-198">Nuget package:</span><span class="sxs-lookup"><span data-stu-id="ef522-198">Nuget package:</span></span><br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="ef522-199">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-199">GitHub release:</span></span><br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="ef522-200">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-200">Connection string setup</span></span>|
|<span data-ttu-id="ef522-201">C++</span><span class="sxs-lookup"><span data-stu-id="ef522-201">C++</span></span>|<span data-ttu-id="ef522-202">2.4.0</span><span class="sxs-lookup"><span data-stu-id="ef522-202">2.4.0</span></span>|<span data-ttu-id="ef522-203">Nuget package:</span><span class="sxs-lookup"><span data-stu-id="ef522-203">Nuget package:</span></span><br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="ef522-204">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-204">GitHub release:</span></span><br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="ef522-205">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-205">Connection string setup</span></span>|
|<span data-ttu-id="ef522-206">PHP</span><span class="sxs-lookup"><span data-stu-id="ef522-206">PHP</span></span>|<span data-ttu-id="ef522-207">0.15.0</span><span class="sxs-lookup"><span data-stu-id="ef522-207">0.15.0</span></span>|<span data-ttu-id="ef522-208">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-208">GitHub release:</span></span><br>[https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="ef522-209">Install via Composer (see details below)</span><span class="sxs-lookup"><span data-stu-id="ef522-209">Install via Composer (see details below)</span></span>|<span data-ttu-id="ef522-210">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-210">Connection string setup</span></span>|
|<span data-ttu-id="ef522-211">Python</span><span class="sxs-lookup"><span data-stu-id="ef522-211">Python</span></span>     |<span data-ttu-id="ef522-212">0.30.0</span><span class="sxs-lookup"><span data-stu-id="ef522-212">0.30.0</span></span>|<span data-ttu-id="ef522-213">PIP package:</span><span class="sxs-lookup"><span data-stu-id="ef522-213">PIP package:</span></span><br> [https://pypi.python.org/pypi/azure-storage/0.30.0](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="ef522-214">(Run: `pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="ef522-214">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="ef522-215">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-215">GitHub release:</span></span><br> [https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="ef522-216">Service instance declaration</span><span class="sxs-lookup"><span data-stu-id="ef522-216">Service instance declaration</span></span>|
|<span data-ttu-id="ef522-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="ef522-217">Ruby</span></span>|<span data-ttu-id="ef522-218">0.12.1</span><span class="sxs-lookup"><span data-stu-id="ef522-218">0.12.1</span></span><br><span data-ttu-id="ef522-219">Preview</span><span class="sxs-lookup"><span data-stu-id="ef522-219">Preview</span></span>|<span data-ttu-id="ef522-220">RubyGems package:</span><span class="sxs-lookup"><span data-stu-id="ef522-220">RubyGems package:</span></span><br> [https://rubygems.org/gems/azure-storage/versions/0.12.1.preview](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="ef522-221">GitHub release:</span><span class="sxs-lookup"><span data-stu-id="ef522-221">GitHub release:</span></span><br> [https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="ef522-222">Connection string setup</span><span class="sxs-lookup"><span data-stu-id="ef522-222">Connection string setup</span></span>|

#### <a name="install-php-client-via-composer---previous"></a><span data-ttu-id="ef522-223">Install PHP client via Composer - previous</span><span class="sxs-lookup"><span data-stu-id="ef522-223">Install PHP client via Composer - previous</span></span>

<span data-ttu-id="ef522-224">To install via Composer:</span><span class="sxs-lookup"><span data-stu-id="ef522-224">To install via Composer:</span></span>

1. <span data-ttu-id="ef522-225">Create a file named **composer.json** in the root of the project with following code:</span><span class="sxs-lookup"><span data-stu-id="ef522-225">Create a file named **composer.json** in the root of the project with following code:</span></span>

  ```php
    {
          "require":{
          "Microsoft/azure-storage":"0.15.0"
          }
    }
  ```

2. <span data-ttu-id="ef522-226">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span><span class="sxs-lookup"><span data-stu-id="ef522-226">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
3. <span data-ttu-id="ef522-227">Run: `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="ef522-227">Run: `php composer.phar install`.</span></span>

## <a name="endpoint-declaration"></a><span data-ttu-id="ef522-228">Endpoint declaration</span><span class="sxs-lookup"><span data-stu-id="ef522-228">Endpoint declaration</span></span>

<span data-ttu-id="ef522-229">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span><span class="sxs-lookup"><span data-stu-id="ef522-229">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="ef522-230">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="ef522-230">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="ef522-231">Contact your cloud administrator if you’re not sure about your endpoint.</span><span class="sxs-lookup"><span data-stu-id="ef522-231">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="ef522-232">Examples</span><span class="sxs-lookup"><span data-stu-id="ef522-232">Examples</span></span>

### <a name="net"></a><span data-ttu-id="ef522-233">.NET</span><span class="sxs-lookup"><span data-stu-id="ef522-233">.NET</span></span>

<span data-ttu-id="ef522-234">For Azure Stack, the endpoint suffix is specified in the app.config file:</span><span class="sxs-lookup"><span data-stu-id="ef522-234">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString"
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```

### <a name="java"></a><span data-ttu-id="ef522-235">Java</span><span class="sxs-lookup"><span data-stu-id="ef522-235">Java</span></span>

<span data-ttu-id="ef522-236">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span><span class="sxs-lookup"><span data-stu-id="ef522-236">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="ef522-237">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef522-237">Node.js</span></span>

<span data-ttu-id="ef522-238">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span><span class="sxs-lookup"><span data-stu-id="ef522-238">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```

### <a name="c"></a><span data-ttu-id="ef522-239">C++</span><span class="sxs-lookup"><span data-stu-id="ef522-239">C++</span></span>

<span data-ttu-id="ef522-240">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span><span class="sxs-lookup"><span data-stu-id="ef522-240">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="ef522-241">PHP</span><span class="sxs-lookup"><span data-stu-id="ef522-241">PHP</span></span>

<span data-ttu-id="ef522-242">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span><span class="sxs-lookup"><span data-stu-id="ef522-242">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="ef522-243">Python</span><span class="sxs-lookup"><span data-stu-id="ef522-243">Python</span></span>

<span data-ttu-id="ef522-244">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span><span class="sxs-lookup"><span data-stu-id="ef522-244">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```

### <a name="ruby"></a><span data-ttu-id="ef522-245">Ruby</span><span class="sxs-lookup"><span data-stu-id="ef522-245">Ruby</span></span>

<span data-ttu-id="ef522-246">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span><span class="sxs-lookup"><span data-stu-id="ef522-246">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="ef522-247">Blob storage</span><span class="sxs-lookup"><span data-stu-id="ef522-247">Blob storage</span></span>

<span data-ttu-id="ef522-248">The following Azure Blob storage tutorials are applicable to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ef522-248">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="ef522-249">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="ef522-249">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="ef522-250">Get started with Azure Blob storage using .NET</span><span class="sxs-lookup"><span data-stu-id="ef522-250">Get started with Azure Blob storage using .NET</span></span>](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ef522-251">How to use Blob storage from Java</span><span class="sxs-lookup"><span data-stu-id="ef522-251">How to use Blob storage from Java</span></span>](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="ef522-252">How to use Blob storage from Node.js</span><span class="sxs-lookup"><span data-stu-id="ef522-252">How to use Blob storage from Node.js</span></span>](../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="ef522-253">How to use Blob storage from C++</span><span class="sxs-lookup"><span data-stu-id="ef522-253">How to use Blob storage from C++</span></span>](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="ef522-254">How to use Blob storage from PHP</span><span class="sxs-lookup"><span data-stu-id="ef522-254">How to use Blob storage from PHP</span></span>](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="ef522-255">How to use Azure Blob storage from Python</span><span class="sxs-lookup"><span data-stu-id="ef522-255">How to use Azure Blob storage from Python</span></span>](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="ef522-256">How to use Blob storage from Ruby</span><span class="sxs-lookup"><span data-stu-id="ef522-256">How to use Blob storage from Ruby</span></span>](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="ef522-257">Queue storage</span><span class="sxs-lookup"><span data-stu-id="ef522-257">Queue storage</span></span>

<span data-ttu-id="ef522-258">The following Azure Queue storage tutorials are applicable to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ef522-258">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="ef522-259">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="ef522-259">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="ef522-260">Get started with Azure Queue storage using .NET</span><span class="sxs-lookup"><span data-stu-id="ef522-260">Get started with Azure Queue storage using .NET</span></span>](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ef522-261">How to use Queue storage from Java</span><span class="sxs-lookup"><span data-stu-id="ef522-261">How to use Queue storage from Java</span></span>](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="ef522-262">How to use Queue storage from Node.js</span><span class="sxs-lookup"><span data-stu-id="ef522-262">How to use Queue storage from Node.js</span></span>](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="ef522-263">How to use Queue storage from C++</span><span class="sxs-lookup"><span data-stu-id="ef522-263">How to use Queue storage from C++</span></span>](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="ef522-264">How to use Queue storage from PHP</span><span class="sxs-lookup"><span data-stu-id="ef522-264">How to use Queue storage from PHP</span></span>](../../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="ef522-265">How to use Queue storage from Python</span><span class="sxs-lookup"><span data-stu-id="ef522-265">How to use Queue storage from Python</span></span>](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="ef522-266">How to use Queue storage from Ruby</span><span class="sxs-lookup"><span data-stu-id="ef522-266">How to use Queue storage from Ruby</span></span>](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)

## <a name="table-storage"></a><span data-ttu-id="ef522-267">Table storage</span><span class="sxs-lookup"><span data-stu-id="ef522-267">Table storage</span></span>

<span data-ttu-id="ef522-268">The following Azure Table storage tutorials are applicable to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ef522-268">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="ef522-269">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="ef522-269">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="ef522-270">Get started with Azure Table storage using .NET</span><span class="sxs-lookup"><span data-stu-id="ef522-270">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="ef522-271">How to use Table storage from Java</span><span class="sxs-lookup"><span data-stu-id="ef522-271">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="ef522-272">How to use Azure Table storage from Node.js</span><span class="sxs-lookup"><span data-stu-id="ef522-272">How to use Azure Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="ef522-273">How to use Table storage from C++</span><span class="sxs-lookup"><span data-stu-id="ef522-273">How to use Table storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="ef522-274">How to use Table storage from PHP</span><span class="sxs-lookup"><span data-stu-id="ef522-274">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="ef522-275">How to use Table storage in Python</span><span class="sxs-lookup"><span data-stu-id="ef522-275">How to use Table storage in Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="ef522-276">How to use Table storage from Ruby</span><span class="sxs-lookup"><span data-stu-id="ef522-276">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="ef522-277">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef522-277">Next steps</span></span>

* [<span data-ttu-id="ef522-278">Introduction to Microsoft Azure storage</span><span class="sxs-lookup"><span data-stu-id="ef522-278">Introduction to Microsoft Azure storage</span></span>](../../storage/common/storage-introduction.md)