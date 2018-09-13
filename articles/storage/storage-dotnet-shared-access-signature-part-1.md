---
title: Using shared access signatures (SAS) in Azure Storage | Microsoft Docs
description: Learn to use shared access signatures (SAS) to delegate access to Azure Storage resources, including blobs, queues, tables, and files.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 8ea771db11b15d3e618c72d7ca261d1a8a23203a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564573"
---
# <a name="using-shared-access-signatures-sas"></a><span data-ttu-id="258a6-103">Using shared access signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="258a6-103">Using shared access signatures (SAS)</span></span>

<span data-ttu-id="258a6-104">A shared access signature (SAS) provides you with a way to grant limited access to objects in your storage account to other clients, without exposing your account key.</span><span class="sxs-lookup"><span data-stu-id="258a6-104">A shared access signature (SAS) provides you with a way to grant limited access to objects in your storage account to other clients, without exposing your account key.</span></span> <span data-ttu-id="258a6-105">In this article, we provide an overview of the SAS model, review SAS best practices, and look at some examples.</span><span class="sxs-lookup"><span data-stu-id="258a6-105">In this article, we provide an overview of the SAS model, review SAS best practices, and look at some examples.</span></span>

<span data-ttu-id="258a6-106">For additional code examples using SAS beyond those presented here, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) and other samples available in the [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage) library.</span><span class="sxs-lookup"><span data-stu-id="258a6-106">For additional code examples using SAS beyond those presented here, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) and other samples available in the [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage) library.</span></span> <span data-ttu-id="258a6-107">You can download the sample applications and run them, or browse the code on GitHub.</span><span class="sxs-lookup"><span data-stu-id="258a6-107">You can download the sample applications and run them, or browse the code on GitHub.</span></span>

## <a name="what-is-a-shared-access-signature"></a><span data-ttu-id="258a6-108">What is a shared access signature?</span><span class="sxs-lookup"><span data-stu-id="258a6-108">What is a shared access signature?</span></span>
<span data-ttu-id="258a6-109">A shared access signature provides delegated access to resources in your storage account.</span><span class="sxs-lookup"><span data-stu-id="258a6-109">A shared access signature provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="258a6-110">With a SAS, you can grant clients access to resources in your storage account, without sharing your account keys.</span><span class="sxs-lookup"><span data-stu-id="258a6-110">With a SAS, you can grant clients access to resources in your storage account, without sharing your account keys.</span></span> <span data-ttu-id="258a6-111">This is the key point of using shared access signatures in your applications--a SAS is a secure way to share your storage resources without compromising your account keys.</span><span class="sxs-lookup"><span data-stu-id="258a6-111">This is the key point of using shared access signatures in your applications--a SAS is a secure way to share your storage resources without compromising your account keys.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

<span data-ttu-id="258a6-112">A SAS gives you granular control over the type of access you grant to clients who have the SAS, including:</span><span class="sxs-lookup"><span data-stu-id="258a6-112">A SAS gives you granular control over the type of access you grant to clients who have the SAS, including:</span></span>

* <span data-ttu-id="258a6-113">The interval over which the SAS is valid, including the start time and the expiry time.</span><span class="sxs-lookup"><span data-stu-id="258a6-113">The interval over which the SAS is valid, including the start time and the expiry time.</span></span>
* <span data-ttu-id="258a6-114">The permissions granted by the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-114">The permissions granted by the SAS.</span></span> <span data-ttu-id="258a6-115">For example, a SAS for a blob might grant read and write permissions to that blob, but not delete permissions.</span><span class="sxs-lookup"><span data-stu-id="258a6-115">For example, a SAS for a blob might grant read and write permissions to that blob, but not delete permissions.</span></span>
* <span data-ttu-id="258a6-116">An optional IP address or range of IP addresses from which Azure Storage will accept the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-116">An optional IP address or range of IP addresses from which Azure Storage will accept the SAS.</span></span> <span data-ttu-id="258a6-117">For example, you might specify a range of IP addresses belonging to your organization.</span><span class="sxs-lookup"><span data-stu-id="258a6-117">For example, you might specify a range of IP addresses belonging to your organization.</span></span>
* <span data-ttu-id="258a6-118">The protocol over which Azure Storage will accept the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-118">The protocol over which Azure Storage will accept the SAS.</span></span> <span data-ttu-id="258a6-119">You can use this optional parameter to restrict access to clients using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="258a6-119">You can use this optional parameter to restrict access to clients using HTTPS.</span></span>

## <a name="when-should-you-use-a-shared-access-signature"></a><span data-ttu-id="258a6-120">When should you use a shared access signature?</span><span class="sxs-lookup"><span data-stu-id="258a6-120">When should you use a shared access signature?</span></span>
<span data-ttu-id="258a6-121">You can use a SAS when you want to provide access to resources in your storage account to any client not possessing your storage account's access keys.</span><span class="sxs-lookup"><span data-stu-id="258a6-121">You can use a SAS when you want to provide access to resources in your storage account to any client not possessing your storage account's access keys.</span></span> <span data-ttu-id="258a6-122">Your storage account includes both a primary and secondary access key, both of which grant administrative access to your account, and all resources within it.</span><span class="sxs-lookup"><span data-stu-id="258a6-122">Your storage account includes both a primary and secondary access key, both of which grant administrative access to your account, and all resources within it.</span></span> <span data-ttu-id="258a6-123">Exposing either of these keys opens your account to the possibility of malicious or negligent use.</span><span class="sxs-lookup"><span data-stu-id="258a6-123">Exposing either of these keys opens your account to the possibility of malicious or negligent use.</span></span> <span data-ttu-id="258a6-124">Shared access signatures provide a safe alternative that allows clients to read, write, and delete data in your storage account according to the permissions you've explicitly granted, and without need for an account key.</span><span class="sxs-lookup"><span data-stu-id="258a6-124">Shared access signatures provide a safe alternative that allows clients to read, write, and delete data in your storage account according to the permissions you've explicitly granted, and without need for an account key.</span></span>

<span data-ttu-id="258a6-125">A common scenario where a SAS is useful is a service where users read and write their own data to your storage account.</span><span class="sxs-lookup"><span data-stu-id="258a6-125">A common scenario where a SAS is useful is a service where users read and write their own data to your storage account.</span></span> <span data-ttu-id="258a6-126">In a scenario where a storage account stores user data, there are two typical design patterns:</span><span class="sxs-lookup"><span data-stu-id="258a6-126">In a scenario where a storage account stores user data, there are two typical design patterns:</span></span>

1. <span data-ttu-id="258a6-127">Clients upload and download data via a front-end proxy service, which performs authentication.</span><span class="sxs-lookup"><span data-stu-id="258a6-127">Clients upload and download data via a front-end proxy service, which performs authentication.</span></span> <span data-ttu-id="258a6-128">This front-end proxy service has the advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale to match demand may be expensive or difficult.</span><span class="sxs-lookup"><span data-stu-id="258a6-128">This front-end proxy service has the advantage of allowing validation of business rules, but for large amounts of data or high-volume transactions, creating a service that can scale to match demand may be expensive or difficult.</span></span>

  ![Scenario diagram: Front-end proxy service][sas-storage-fe-proxy-service]

1. <span data-ttu-id="258a6-130">A lightweight service authenticates the client as needed and then generates a SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-130">A lightweight service authenticates the client as needed and then generates a SAS.</span></span> <span data-ttu-id="258a6-131">Once the client receives the SAS, they can access storage account resources directly with the permissions defined by the SAS and for the interval allowed by the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-131">Once the client receives the SAS, they can access storage account resources directly with the permissions defined by the SAS and for the interval allowed by the SAS.</span></span> <span data-ttu-id="258a6-132">The SAS mitigates the need for routing all data through the front-end proxy service.</span><span class="sxs-lookup"><span data-stu-id="258a6-132">The SAS mitigates the need for routing all data through the front-end proxy service.</span></span>

  ![Scenario diagram: SAS provider service][sas-storage-provider-service]

<span data-ttu-id="258a6-134">Many real-world services may use a hybrid of these two approaches.</span><span class="sxs-lookup"><span data-stu-id="258a6-134">Many real-world services may use a hybrid of these two approaches.</span></span> <span data-ttu-id="258a6-135">For example, some data might be processed and validated via the front-end proxy, while other data is saved and/or read directly using SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-135">For example, some data might be processed and validated via the front-end proxy, while other data is saved and/or read directly using SAS.</span></span>

<span data-ttu-id="258a6-136">Additionally, you will need to use a SAS to authenticate the source object in a copy operation in certain scenarios:</span><span class="sxs-lookup"><span data-stu-id="258a6-136">Additionally, you will need to use a SAS to authenticate the source object in a copy operation in certain scenarios:</span></span>

* <span data-ttu-id="258a6-137">When you copy a blob to another blob that resides in a different storage account, you must use a SAS to authenticate the source blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-137">When you copy a blob to another blob that resides in a different storage account, you must use a SAS to authenticate the source blob.</span></span> <span data-ttu-id="258a6-138">You can optionally use a SAS to authenticate the destination blob as well.</span><span class="sxs-lookup"><span data-stu-id="258a6-138">You can optionally use a SAS to authenticate the destination blob as well.</span></span>
* <span data-ttu-id="258a6-139">When you copy a file to another file that resides in a different storage account, you must use a SAS to authenticate the source file.</span><span class="sxs-lookup"><span data-stu-id="258a6-139">When you copy a file to another file that resides in a different storage account, you must use a SAS to authenticate the source file.</span></span> <span data-ttu-id="258a6-140">You can optionally use a SAS to authenticate the destination file as well.</span><span class="sxs-lookup"><span data-stu-id="258a6-140">You can optionally use a SAS to authenticate the destination file as well.</span></span>
* <span data-ttu-id="258a6-141">When you copy a blob to a file, or a file to a blob, you must use a SAS to authenticate the source object, even if the source and destination objects reside within the same storage account.</span><span class="sxs-lookup"><span data-stu-id="258a6-141">When you copy a blob to a file, or a file to a blob, you must use a SAS to authenticate the source object, even if the source and destination objects reside within the same storage account.</span></span>

## <a name="types-of-shared-access-signatures"></a><span data-ttu-id="258a6-142">Types of shared access signatures</span><span class="sxs-lookup"><span data-stu-id="258a6-142">Types of shared access signatures</span></span>
<span data-ttu-id="258a6-143">You can create two types of shared access signatures:</span><span class="sxs-lookup"><span data-stu-id="258a6-143">You can create two types of shared access signatures:</span></span>

* <span data-ttu-id="258a6-144">**Service SAS.**</span><span class="sxs-lookup"><span data-stu-id="258a6-144">**Service SAS.**</span></span> <span data-ttu-id="258a6-145">The service SAS delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service.</span><span class="sxs-lookup"><span data-stu-id="258a6-145">The service SAS delegates access to a resource in just one of the storage services: the Blob, Queue, Table, or File service.</span></span> <span data-ttu-id="258a6-146">See [Constructing a Service SAS](https://msdn.microsoft.com/library/dn140255.aspx) and [Service SAS Examples](https://msdn.microsoft.com/library/dn140256.aspx) for in-depth information about constructing the service SAS token.</span><span class="sxs-lookup"><span data-stu-id="258a6-146">See [Constructing a Service SAS](https://msdn.microsoft.com/library/dn140255.aspx) and [Service SAS Examples](https://msdn.microsoft.com/library/dn140256.aspx) for in-depth information about constructing the service SAS token.</span></span>
* <span data-ttu-id="258a6-147">**Account SAS.**</span><span class="sxs-lookup"><span data-stu-id="258a6-147">**Account SAS.**</span></span> <span data-ttu-id="258a6-148">The account SAS delegates access to resources in one or more of the storage services.</span><span class="sxs-lookup"><span data-stu-id="258a6-148">The account SAS delegates access to resources in one or more of the storage services.</span></span> <span data-ttu-id="258a6-149">All of the operations available via a service SAS are also available via an account SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-149">All of the operations available via a service SAS are also available via an account SAS.</span></span> <span data-ttu-id="258a6-150">Additionally, with the account SAS, you can delegate access to operations that apply to a given service, such as **Get/Set Service Properties** and **Get Service Stats**. You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-150">Additionally, with the account SAS, you can delegate access to operations that apply to a given service, such as **Get/Set Service Properties** and **Get Service Stats**. You can also delegate access to read, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="258a6-151">See [Constructing an Account SAS](https://msdn.microsoft.com/library/mt584140.aspx) for in-depth information about constructing the account SAS token.</span><span class="sxs-lookup"><span data-stu-id="258a6-151">See [Constructing an Account SAS](https://msdn.microsoft.com/library/mt584140.aspx) for in-depth information about constructing the account SAS token.</span></span>

## <a name="how-a-shared-access-signature-works"></a><span data-ttu-id="258a6-152">How a shared access signature works</span><span class="sxs-lookup"><span data-stu-id="258a6-152">How a shared access signature works</span></span>
<span data-ttu-id="258a6-153">A shared access signature is a signed URI that points to one or more storage resources and includes a token that contains a special set of query parameters.</span><span class="sxs-lookup"><span data-stu-id="258a6-153">A shared access signature is a signed URI that points to one or more storage resources and includes a token that contains a special set of query parameters.</span></span> <span data-ttu-id="258a6-154">The token indicates how the resources may be accessed by the client.</span><span class="sxs-lookup"><span data-stu-id="258a6-154">The token indicates how the resources may be accessed by the client.</span></span> <span data-ttu-id="258a6-155">One of the query parameters, the signature, is constructed from the SAS parameters and signed with the account key.</span><span class="sxs-lookup"><span data-stu-id="258a6-155">One of the query parameters, the signature, is constructed from the SAS parameters and signed with the account key.</span></span> <span data-ttu-id="258a6-156">This signature is used by Azure Storage to authenticate the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-156">This signature is used by Azure Storage to authenticate the SAS.</span></span>

<span data-ttu-id="258a6-157">Here's an example of a SAS URI, showing the resource URI and the SAS token:</span><span class="sxs-lookup"><span data-stu-id="258a6-157">Here's an example of a SAS URI, showing the resource URI and the SAS token:</span></span>

![Components of a SAS URI][sas-storage-uri]

<span data-ttu-id="258a6-159">The SAS token is a string you generate on the *client* side (see the [SAS examples](#sas-examples) section for code examples).</span><span class="sxs-lookup"><span data-stu-id="258a6-159">The SAS token is a string you generate on the *client* side (see the [SAS examples](#sas-examples) section for code examples).</span></span> <span data-ttu-id="258a6-160">A SAS token you generate with the storage client library, for example, is not tracked by Azure Storage in any way.</span><span class="sxs-lookup"><span data-stu-id="258a6-160">A SAS token you generate with the storage client library, for example, is not tracked by Azure Storage in any way.</span></span> <span data-ttu-id="258a6-161">You can create an unlimited number of SAS tokens on the client side.</span><span class="sxs-lookup"><span data-stu-id="258a6-161">You can create an unlimited number of SAS tokens on the client side.</span></span>

<span data-ttu-id="258a6-162">When a client provides a SAS URI to Azure Storage as part of a request, the service checks the SAS parameters and signature to verify that it is valid for authenticating the request.</span><span class="sxs-lookup"><span data-stu-id="258a6-162">When a client provides a SAS URI to Azure Storage as part of a request, the service checks the SAS parameters and signature to verify that it is valid for authenticating the request.</span></span> <span data-ttu-id="258a6-163">If the service verifies that the signature is valid, then the request is authenticated.</span><span class="sxs-lookup"><span data-stu-id="258a6-163">If the service verifies that the signature is valid, then the request is authenticated.</span></span> <span data-ttu-id="258a6-164">Otherwise, the request is declined with error code 403 (Forbidden).</span><span class="sxs-lookup"><span data-stu-id="258a6-164">Otherwise, the request is declined with error code 403 (Forbidden).</span></span>

## <a name="shared-access-signature-parameters"></a><span data-ttu-id="258a6-165">Shared access signature parameters</span><span class="sxs-lookup"><span data-stu-id="258a6-165">Shared access signature parameters</span></span>
<span data-ttu-id="258a6-166">The account SAS and service SAS tokens include some common parameters, and also take a few parameters that that are different.</span><span class="sxs-lookup"><span data-stu-id="258a6-166">The account SAS and service SAS tokens include some common parameters, and also take a few parameters that that are different.</span></span>

### <a name="parameters-common-to-account-sas-and-service-sas-tokens"></a><span data-ttu-id="258a6-167">Parameters common to account SAS and service SAS tokens</span><span class="sxs-lookup"><span data-stu-id="258a6-167">Parameters common to account SAS and service SAS tokens</span></span>
* <span data-ttu-id="258a6-168">**Api version** An optional parameter that specifies the storage service version to use to execute the request.</span><span class="sxs-lookup"><span data-stu-id="258a6-168">**Api version** An optional parameter that specifies the storage service version to use to execute the request.</span></span>
* <span data-ttu-id="258a6-169">**Service version** A required parameter that specifies the storage service version to use to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="258a6-169">**Service version** A required parameter that specifies the storage service version to use to authenticate the request.</span></span>
* <span data-ttu-id="258a6-170">**Start time.**</span><span class="sxs-lookup"><span data-stu-id="258a6-170">**Start time.**</span></span> <span data-ttu-id="258a6-171">This is the time at which the SAS becomes valid.</span><span class="sxs-lookup"><span data-stu-id="258a6-171">This is the time at which the SAS becomes valid.</span></span> <span data-ttu-id="258a6-172">The start time for a shared access signature is optional.</span><span class="sxs-lookup"><span data-stu-id="258a6-172">The start time for a shared access signature is optional.</span></span> <span data-ttu-id="258a6-173">If a start time is omitted, the SAS is effective immediately.</span><span class="sxs-lookup"><span data-stu-id="258a6-173">If a start time is omitted, the SAS is effective immediately.</span></span> <span data-ttu-id="258a6-174">The start time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z`.</span><span class="sxs-lookup"><span data-stu-id="258a6-174">The start time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z`.</span></span>
* <span data-ttu-id="258a6-175">**Expiry time.**</span><span class="sxs-lookup"><span data-stu-id="258a6-175">**Expiry time.**</span></span> <span data-ttu-id="258a6-176">This is the time after which the SAS is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="258a6-176">This is the time after which the SAS is no longer valid.</span></span> <span data-ttu-id="258a6-177">Best practices recommend that you either specify an expiry time for a SAS, or associate it with a stored access policy.</span><span class="sxs-lookup"><span data-stu-id="258a6-177">Best practices recommend that you either specify an expiry time for a SAS, or associate it with a stored access policy.</span></span> <span data-ttu-id="258a6-178">The expiry time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z` (see more below).</span><span class="sxs-lookup"><span data-stu-id="258a6-178">The expiry time must be expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"), for example `1994-11-05T13:15:30Z` (see more below).</span></span>
* <span data-ttu-id="258a6-179">**Permissions.**</span><span class="sxs-lookup"><span data-stu-id="258a6-179">**Permissions.**</span></span> <span data-ttu-id="258a6-180">The permissions specified on the SAS indicate what operations the client can perform against the storage resource using the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-180">The permissions specified on the SAS indicate what operations the client can perform against the storage resource using the SAS.</span></span> <span data-ttu-id="258a6-181">Available permissions differ for an account SAS and a service SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-181">Available permissions differ for an account SAS and a service SAS.</span></span>
* <span data-ttu-id="258a6-182">**IP.**</span><span class="sxs-lookup"><span data-stu-id="258a6-182">**IP.**</span></span> <span data-ttu-id="258a6-183">An optional parameter that specifies an IP address or a range of IP addresses outside of Azure (see the section [Routing session configuration state](../expressroute/expressroute-workflows.md#routing-session-configuration-state) for Express Route) from which to accept requests.</span><span class="sxs-lookup"><span data-stu-id="258a6-183">An optional parameter that specifies an IP address or a range of IP addresses outside of Azure (see the section [Routing session configuration state](../expressroute/expressroute-workflows.md#routing-session-configuration-state) for Express Route) from which to accept requests.</span></span>
* <span data-ttu-id="258a6-184">**Protocol.**</span><span class="sxs-lookup"><span data-stu-id="258a6-184">**Protocol.**</span></span> <span data-ttu-id="258a6-185">An optional parameter that specifies the protocol permitted for a request.</span><span class="sxs-lookup"><span data-stu-id="258a6-185">An optional parameter that specifies the protocol permitted for a request.</span></span> <span data-ttu-id="258a6-186">Possible values are both HTTPS and HTTP (`https,http`), which is the default value, or HTTPS only (`https`).</span><span class="sxs-lookup"><span data-stu-id="258a6-186">Possible values are both HTTPS and HTTP (`https,http`), which is the default value, or HTTPS only (`https`).</span></span> <span data-ttu-id="258a6-187">Note that HTTP only is not a permitted value.</span><span class="sxs-lookup"><span data-stu-id="258a6-187">Note that HTTP only is not a permitted value.</span></span>
* <span data-ttu-id="258a6-188">**Signature.**</span><span class="sxs-lookup"><span data-stu-id="258a6-188">**Signature.**</span></span> <span data-ttu-id="258a6-189">The signature is constructed from the other parameters specified as part token and then encrypted.</span><span class="sxs-lookup"><span data-stu-id="258a6-189">The signature is constructed from the other parameters specified as part token and then encrypted.</span></span> <span data-ttu-id="258a6-190">It's used to authenticate the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-190">It's used to authenticate the SAS.</span></span>

### <a name="parameters-for-a-service-sas-token"></a><span data-ttu-id="258a6-191">Parameters for a service SAS token</span><span class="sxs-lookup"><span data-stu-id="258a6-191">Parameters for a service SAS token</span></span>
* <span data-ttu-id="258a6-192">**Storage resource.**</span><span class="sxs-lookup"><span data-stu-id="258a6-192">**Storage resource.**</span></span> <span data-ttu-id="258a6-193">Storage resources for which you can delegate access with a service SAS include:</span><span class="sxs-lookup"><span data-stu-id="258a6-193">Storage resources for which you can delegate access with a service SAS include:</span></span>
  * <span data-ttu-id="258a6-194">Containers and blobs</span><span class="sxs-lookup"><span data-stu-id="258a6-194">Containers and blobs</span></span>
  * <span data-ttu-id="258a6-195">File shares and files</span><span class="sxs-lookup"><span data-stu-id="258a6-195">File shares and files</span></span>
  * <span data-ttu-id="258a6-196">Queues</span><span class="sxs-lookup"><span data-stu-id="258a6-196">Queues</span></span>
  * <span data-ttu-id="258a6-197">Tables and ranges of table entities.</span><span class="sxs-lookup"><span data-stu-id="258a6-197">Tables and ranges of table entities.</span></span>

### <a name="parameters-for-an-account-sas-token"></a><span data-ttu-id="258a6-198">Parameters for an account SAS token</span><span class="sxs-lookup"><span data-stu-id="258a6-198">Parameters for an account SAS token</span></span>
* <span data-ttu-id="258a6-199">**Service or services.**</span><span class="sxs-lookup"><span data-stu-id="258a6-199">**Service or services.**</span></span> <span data-ttu-id="258a6-200">An account SAS can delegate access to one or more of the storage services.</span><span class="sxs-lookup"><span data-stu-id="258a6-200">An account SAS can delegate access to one or more of the storage services.</span></span> <span data-ttu-id="258a6-201">For example, you can create an account SAS that delegates access to the Blob and File service.</span><span class="sxs-lookup"><span data-stu-id="258a6-201">For example, you can create an account SAS that delegates access to the Blob and File service.</span></span> <span data-ttu-id="258a6-202">Or you can create a SAS that delegates access to all four services (Blob, Queue, Table, and File).</span><span class="sxs-lookup"><span data-stu-id="258a6-202">Or you can create a SAS that delegates access to all four services (Blob, Queue, Table, and File).</span></span>
* <span data-ttu-id="258a6-203">**Storage resource types.**</span><span class="sxs-lookup"><span data-stu-id="258a6-203">**Storage resource types.**</span></span> <span data-ttu-id="258a6-204">An account SAS applies to one or more classes of storage resources, rather than a specific resource.</span><span class="sxs-lookup"><span data-stu-id="258a6-204">An account SAS applies to one or more classes of storage resources, rather than a specific resource.</span></span> <span data-ttu-id="258a6-205">You can create an account SAS to delegate access to:</span><span class="sxs-lookup"><span data-stu-id="258a6-205">You can create an account SAS to delegate access to:</span></span>
  * <span data-ttu-id="258a6-206">Service-level APIs, which are called against the storage account resource.</span><span class="sxs-lookup"><span data-stu-id="258a6-206">Service-level APIs, which are called against the storage account resource.</span></span> <span data-ttu-id="258a6-207">Examples include **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.</span><span class="sxs-lookup"><span data-stu-id="258a6-207">Examples include **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.</span></span>
  * <span data-ttu-id="258a6-208">Container-level APIs, which are called against the container objects for each service: blob containers, queues, tables, and file shares.</span><span class="sxs-lookup"><span data-stu-id="258a6-208">Container-level APIs, which are called against the container objects for each service: blob containers, queues, tables, and file shares.</span></span> <span data-ttu-id="258a6-209">Examples include **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share**, and **List Blobs/Files and Directories**.</span><span class="sxs-lookup"><span data-stu-id="258a6-209">Examples include **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share**, and **List Blobs/Files and Directories**.</span></span>
  * <span data-ttu-id="258a6-210">Object-level APIs, which are called against blobs, queue messages, table entities, and files.</span><span class="sxs-lookup"><span data-stu-id="258a6-210">Object-level APIs, which are called against blobs, queue messages, table entities, and files.</span></span> <span data-ttu-id="258a6-211">For example, **Put Blob**, **Query Entity**, **Get Messages**, and **Create File**.</span><span class="sxs-lookup"><span data-stu-id="258a6-211">For example, **Put Blob**, **Query Entity**, **Get Messages**, and **Create File**.</span></span>

## <a name="examples-of-sas-uris"></a><span data-ttu-id="258a6-212">Examples of SAS URIs</span><span class="sxs-lookup"><span data-stu-id="258a6-212">Examples of SAS URIs</span></span>

### <a name="service-sas-uri-example"></a><span data-ttu-id="258a6-213">Service SAS URI example</span><span class="sxs-lookup"><span data-stu-id="258a6-213">Service SAS URI example</span></span>

<span data-ttu-id="258a6-214">Here is an example of a service SAS URI that provides read and write permissions to a blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-214">Here is an example of a service SAS URI that provides read and write permissions to a blob.</span></span> <span data-ttu-id="258a6-215">The table breaks down each part of the URI to understand how it contributes to the SAS:</span><span class="sxs-lookup"><span data-stu-id="258a6-215">The table breaks down each part of the URI to understand how it contributes to the SAS:</span></span>

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| <span data-ttu-id="258a6-216">Name</span><span class="sxs-lookup"><span data-stu-id="258a6-216">Name</span></span> | <span data-ttu-id="258a6-217">SAS portion</span><span class="sxs-lookup"><span data-stu-id="258a6-217">SAS portion</span></span> | <span data-ttu-id="258a6-218">Description</span><span class="sxs-lookup"><span data-stu-id="258a6-218">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="258a6-219">Blob URI</span><span class="sxs-lookup"><span data-stu-id="258a6-219">Blob URI</span></span> |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |<span data-ttu-id="258a6-220">The address of the blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-220">The address of the blob.</span></span> <span data-ttu-id="258a6-221">Note that using HTTPS is highly recommended.</span><span class="sxs-lookup"><span data-stu-id="258a6-221">Note that using HTTPS is highly recommended.</span></span> |
| <span data-ttu-id="258a6-222">Storage services version</span><span class="sxs-lookup"><span data-stu-id="258a6-222">Storage services version</span></span> |`sv=2015-04-05` |<span data-ttu-id="258a6-223">For storage services version 2012-02-12 and later, this parameter indicates the version to use.</span><span class="sxs-lookup"><span data-stu-id="258a6-223">For storage services version 2012-02-12 and later, this parameter indicates the version to use.</span></span> |
| <span data-ttu-id="258a6-224">Start time</span><span class="sxs-lookup"><span data-stu-id="258a6-224">Start time</span></span> |`st=2015-04-29T22%3A18%3A26Z` |<span data-ttu-id="258a6-225">Specified in UTC time.</span><span class="sxs-lookup"><span data-stu-id="258a6-225">Specified in UTC time.</span></span> <span data-ttu-id="258a6-226">If you want the SAS to be valid immediately, omit the start time.</span><span class="sxs-lookup"><span data-stu-id="258a6-226">If you want the SAS to be valid immediately, omit the start time.</span></span> |
| <span data-ttu-id="258a6-227">Expiry time</span><span class="sxs-lookup"><span data-stu-id="258a6-227">Expiry time</span></span> |`se=2015-04-30T02%3A23%3A26Z` |<span data-ttu-id="258a6-228">Specified in UTC time.</span><span class="sxs-lookup"><span data-stu-id="258a6-228">Specified in UTC time.</span></span> |
| <span data-ttu-id="258a6-229">Resource</span><span class="sxs-lookup"><span data-stu-id="258a6-229">Resource</span></span> |`sr=b` |<span data-ttu-id="258a6-230">The resource is a blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-230">The resource is a blob.</span></span> |
| <span data-ttu-id="258a6-231">Permissions</span><span class="sxs-lookup"><span data-stu-id="258a6-231">Permissions</span></span> |`sp=rw` |<span data-ttu-id="258a6-232">The permissions granted by the SAS include Read (r) and Write (w).</span><span class="sxs-lookup"><span data-stu-id="258a6-232">The permissions granted by the SAS include Read (r) and Write (w).</span></span> |
| <span data-ttu-id="258a6-233">IP range</span><span class="sxs-lookup"><span data-stu-id="258a6-233">IP range</span></span> |`sip=168.1.5.60-168.1.5.70` |<span data-ttu-id="258a6-234">The range of IP addresses from which a request will be accepted.</span><span class="sxs-lookup"><span data-stu-id="258a6-234">The range of IP addresses from which a request will be accepted.</span></span> |
| <span data-ttu-id="258a6-235">Protocol</span><span class="sxs-lookup"><span data-stu-id="258a6-235">Protocol</span></span> |`spr=https` |<span data-ttu-id="258a6-236">Only requests using HTTPS are permitted.</span><span class="sxs-lookup"><span data-stu-id="258a6-236">Only requests using HTTPS are permitted.</span></span> |
| <span data-ttu-id="258a6-237">Signature</span><span class="sxs-lookup"><span data-stu-id="258a6-237">Signature</span></span> |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |<span data-ttu-id="258a6-238">Used to authenticate access to the blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-238">Used to authenticate access to the blob.</span></span> <span data-ttu-id="258a6-239">The signature is an HMAC computed over a string-to-sign and key using the SHA256 algorithm, and then encoded using Base64 encoding.</span><span class="sxs-lookup"><span data-stu-id="258a6-239">The signature is an HMAC computed over a string-to-sign and key using the SHA256 algorithm, and then encoded using Base64 encoding.</span></span> |

### <a name="account-sas-uri-example"></a><span data-ttu-id="258a6-240">Account SAS URI example</span><span class="sxs-lookup"><span data-stu-id="258a6-240">Account SAS URI example</span></span>

<span data-ttu-id="258a6-241">Here is an example of an account SAS that uses the same common parameters on the token.</span><span class="sxs-lookup"><span data-stu-id="258a6-241">Here is an example of an account SAS that uses the same common parameters on the token.</span></span> <span data-ttu-id="258a6-242">Since these parameters are described above, they are not described here.</span><span class="sxs-lookup"><span data-stu-id="258a6-242">Since these parameters are described above, they are not described here.</span></span> <span data-ttu-id="258a6-243">Only the parameters that are specific to account SAS are described in the table below.</span><span class="sxs-lookup"><span data-stu-id="258a6-243">Only the parameters that are specific to account SAS are described in the table below.</span></span>

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| <span data-ttu-id="258a6-244">Name</span><span class="sxs-lookup"><span data-stu-id="258a6-244">Name</span></span> | <span data-ttu-id="258a6-245">SAS portion</span><span class="sxs-lookup"><span data-stu-id="258a6-245">SAS portion</span></span> | <span data-ttu-id="258a6-246">Description</span><span class="sxs-lookup"><span data-stu-id="258a6-246">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="258a6-247">Resource URI</span><span class="sxs-lookup"><span data-stu-id="258a6-247">Resource URI</span></span> |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |<span data-ttu-id="258a6-248">The Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).</span><span class="sxs-lookup"><span data-stu-id="258a6-248">The Blob service endpoint, with parameters for getting service properties (when called with GET) or setting service properties (when called with SET).</span></span> |
| <span data-ttu-id="258a6-249">Services</span><span class="sxs-lookup"><span data-stu-id="258a6-249">Services</span></span> |`ss=bf` |<span data-ttu-id="258a6-250">The SAS applies to the Blob and File services</span><span class="sxs-lookup"><span data-stu-id="258a6-250">The SAS applies to the Blob and File services</span></span> |
| <span data-ttu-id="258a6-251">Resource types</span><span class="sxs-lookup"><span data-stu-id="258a6-251">Resource types</span></span> |`srt=s` |<span data-ttu-id="258a6-252">The SAS applies to service-level operations.</span><span class="sxs-lookup"><span data-stu-id="258a6-252">The SAS applies to service-level operations.</span></span> |
| <span data-ttu-id="258a6-253">Permissions</span><span class="sxs-lookup"><span data-stu-id="258a6-253">Permissions</span></span> |`sp=rw` |<span data-ttu-id="258a6-254">The permissions grant access to read and write operations.</span><span class="sxs-lookup"><span data-stu-id="258a6-254">The permissions grant access to read and write operations.</span></span> |

<span data-ttu-id="258a6-255">Given that permissions are restricted to the service level, accessible operations with this SAS are **Get Blob Service Properties** (read) and **Set Blob Service Properties** (write).</span><span class="sxs-lookup"><span data-stu-id="258a6-255">Given that permissions are restricted to the service level, accessible operations with this SAS are **Get Blob Service Properties** (read) and **Set Blob Service Properties** (write).</span></span> <span data-ttu-id="258a6-256">However, with a different resource URI, the same SAS token could also be used to delegate access to **Get Blob Service Stats** (read).</span><span class="sxs-lookup"><span data-stu-id="258a6-256">However, with a different resource URI, the same SAS token could also be used to delegate access to **Get Blob Service Stats** (read).</span></span>

## <a name="controlling-a-sas-with-a-stored-access-policy"></a><span data-ttu-id="258a6-257">Controlling a SAS with a stored access policy</span><span class="sxs-lookup"><span data-stu-id="258a6-257">Controlling a SAS with a stored access policy</span></span>
<span data-ttu-id="258a6-258">A shared access signature can take one of two forms:</span><span class="sxs-lookup"><span data-stu-id="258a6-258">A shared access signature can take one of two forms:</span></span>

* <span data-ttu-id="258a6-259">**Ad hoc SAS:** When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified in the SAS URI (or implied, in the case where start time is omitted).</span><span class="sxs-lookup"><span data-stu-id="258a6-259">**Ad hoc SAS:** When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified in the SAS URI (or implied, in the case where start time is omitted).</span></span> <span data-ttu-id="258a6-260">This type of SAS can be created as an account SAS or a service SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-260">This type of SAS can be created as an account SAS or a service SAS.</span></span>
* <span data-ttu-id="258a6-261">**SAS with stored access policy:** A stored access policy is defined on a resource container--a blob container, table, queue, or file share--and can be used to manage constraints for one or more shared access signatures.</span><span class="sxs-lookup"><span data-stu-id="258a6-261">**SAS with stored access policy:** A stored access policy is defined on a resource container--a blob container, table, queue, or file share--and can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="258a6-262">When you associate a SAS with a stored access policy, the SAS inherits the constraints--the start time, expiry time, and permissions--defined for the stored access policy.</span><span class="sxs-lookup"><span data-stu-id="258a6-262">When you associate a SAS with a stored access policy, the SAS inherits the constraints--the start time, expiry time, and permissions--defined for the stored access policy.</span></span>

> [!NOTE]
> <span data-ttu-id="258a6-263">Currently, an account SAS must be an ad hoc SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-263">Currently, an account SAS must be an ad hoc SAS.</span></span> <span data-ttu-id="258a6-264">Stored access policies are not yet supported for account SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-264">Stored access policies are not yet supported for account SAS.</span></span>

<span data-ttu-id="258a6-265">The difference between the two forms is important for one key scenario: revocation.</span><span class="sxs-lookup"><span data-stu-id="258a6-265">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="258a6-266">Because a SAS URI is a URL, anyone that obtains the SAS can use it, regardless of who originally created it.</span><span class="sxs-lookup"><span data-stu-id="258a6-266">Because a SAS URI is a URL, anyone that obtains the SAS can use it, regardless of who originally created it.</span></span> <span data-ttu-id="258a6-267">If a SAS is published publicly, it can be used by anyone in the world.</span><span class="sxs-lookup"><span data-stu-id="258a6-267">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="258a6-268">A SAS grants access to resources to anyone possessing it until one of four things happens:</span><span class="sxs-lookup"><span data-stu-id="258a6-268">A SAS grants access to resources to anyone possessing it until one of four things happens:</span></span>

1. <span data-ttu-id="258a6-269">The expiry time specified on the SAS is reached.</span><span class="sxs-lookup"><span data-stu-id="258a6-269">The expiry time specified on the SAS is reached.</span></span>
2. <span data-ttu-id="258a6-270">The expiry time specified on the stored access policy referenced by the SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span><span class="sxs-lookup"><span data-stu-id="258a6-270">The expiry time specified on the stored access policy referenced by the SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span></span> <span data-ttu-id="258a6-271">This can occur either because the interval elapses, or because you've modified the stored access policy with an expiry time in the past, which is one way to revoke the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-271">This can occur either because the interval elapses, or because you've modified the stored access policy with an expiry time in the past, which is one way to revoke the SAS.</span></span>
3. <span data-ttu-id="258a6-272">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-272">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="258a6-273">Note that if you recreate the stored access policy with exactly the same name, all existing SAS tokens will again be valid according to the permissions associated with that stored access policy (assuming that the expiry time on the SAS has not passed).</span><span class="sxs-lookup"><span data-stu-id="258a6-273">Note that if you recreate the stored access policy with exactly the same name, all existing SAS tokens will again be valid according to the permissions associated with that stored access policy (assuming that the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="258a6-274">If you are intending to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span><span class="sxs-lookup"><span data-stu-id="258a6-274">If you are intending to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>
4. <span data-ttu-id="258a6-275">The account key that was used to create the SAS is regenerated.</span><span class="sxs-lookup"><span data-stu-id="258a6-275">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="258a6-276">Regenerating an account key will cause all application components using that key to fail to authenticate until they're updated to use either the other valid account key or the newly regenerated account key.</span><span class="sxs-lookup"><span data-stu-id="258a6-276">Regenerating an account key will cause all application components using that key to fail to authenticate until they're updated to use either the other valid account key or the newly regenerated account key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="258a6-277">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span><span class="sxs-lookup"><span data-stu-id="258a6-277">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="258a6-278">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span><span class="sxs-lookup"><span data-stu-id="258a6-278">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

## <a name="authenticating-from-a-client-application-with-a-sas"></a><span data-ttu-id="258a6-279">Authenticating from a client application with a SAS</span><span class="sxs-lookup"><span data-stu-id="258a6-279">Authenticating from a client application with a SAS</span></span>
<span data-ttu-id="258a6-280">A client who is in possession of a SAS can use the SAS to authenticate a request against a storage account for which they do not possess the account keys.</span><span class="sxs-lookup"><span data-stu-id="258a6-280">A client who is in possession of a SAS can use the SAS to authenticate a request against a storage account for which they do not possess the account keys.</span></span> <span data-ttu-id="258a6-281">A SAS can be included in a connection string, or used directly from the appropriate constructor or method.</span><span class="sxs-lookup"><span data-stu-id="258a6-281">A SAS can be included in a connection string, or used directly from the appropriate constructor or method.</span></span>

### <a name="using-a-sas-in-a-connection-string"></a><span data-ttu-id="258a6-282">Using a SAS in a connection string</span><span class="sxs-lookup"><span data-stu-id="258a6-282">Using a SAS in a connection string</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a><span data-ttu-id="258a6-283">Using a SAS in a constructor or method</span><span class="sxs-lookup"><span data-stu-id="258a6-283">Using a SAS in a constructor or method</span></span>
<span data-ttu-id="258a6-284">Several Azure Storage client library constructors and method overloads offer a SAS parameter, so that you can authenticate a request to the service with a SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-284">Several Azure Storage client library constructors and method overloads offer a SAS parameter, so that you can authenticate a request to the service with a SAS.</span></span>

<span data-ttu-id="258a6-285">For example, here a SAS URI is used to create a reference to a block blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-285">For example, here a SAS URI is used to create a reference to a block blob.</span></span> <span data-ttu-id="258a6-286">The SAS provides the only credentials needed for the request.</span><span class="sxs-lookup"><span data-stu-id="258a6-286">The SAS provides the only credentials needed for the request.</span></span> <span data-ttu-id="258a6-287">The block blob reference is then used for a write operation:</span><span class="sxs-lookup"><span data-stu-id="258a6-287">The block blob reference is then used for a write operation:</span></span>

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with the specified name to the container.
// If the blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a><span data-ttu-id="258a6-288">Best practices when using SAS</span><span class="sxs-lookup"><span data-stu-id="258a6-288">Best practices when using SAS</span></span>
<span data-ttu-id="258a6-289">When you use shared access signatures in your applications, you need to be aware of two potential risks:</span><span class="sxs-lookup"><span data-stu-id="258a6-289">When you use shared access signatures in your applications, you need to be aware of two potential risks:</span></span>

* <span data-ttu-id="258a6-290">If a SAS is leaked, it can be used by anyone who obtains it, which can potentially compromise your storage account.</span><span class="sxs-lookup"><span data-stu-id="258a6-290">If a SAS is leaked, it can be used by anyone who obtains it, which can potentially compromise your storage account.</span></span>
* <span data-ttu-id="258a6-291">If a SAS provided to a client application expires and the application is unable to retrieve a new SAS from your service, then the application's functionality may be hindered.</span><span class="sxs-lookup"><span data-stu-id="258a6-291">If a SAS provided to a client application expires and the application is unable to retrieve a new SAS from your service, then the application's functionality may be hindered.</span></span>

<span data-ttu-id="258a6-292">The following recommendations for using shared access signatures can help mitigate these risks:</span><span class="sxs-lookup"><span data-stu-id="258a6-292">The following recommendations for using shared access signatures can help mitigate these risks:</span></span>

1. <span data-ttu-id="258a6-293">**Always use HTTPS** to create or distribute a SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-293">**Always use HTTPS** to create or distribute a SAS.</span></span> <span data-ttu-id="258a6-294">If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack is able to read the SAS and then use it just as the intended user could have, potentially compromising sensitive data or allowing for data corruption by the malicious user.</span><span class="sxs-lookup"><span data-stu-id="258a6-294">If a SAS is passed over HTTP and intercepted, an attacker performing a man-in-the-middle attack is able to read the SAS and then use it just as the intended user could have, potentially compromising sensitive data or allowing for data corruption by the malicious user.</span></span>
2. <span data-ttu-id="258a6-295">**Reference stored access policies where possible.**</span><span class="sxs-lookup"><span data-stu-id="258a6-295">**Reference stored access policies where possible.**</span></span> <span data-ttu-id="258a6-296">Stored access policies give you the option to revoke permissions without having to regenerate the storage account keys.</span><span class="sxs-lookup"><span data-stu-id="258a6-296">Stored access policies give you the option to revoke permissions without having to regenerate the storage account keys.</span></span> <span data-ttu-id="258a6-297">Set the expiration on these very far in the future (or infinite) and make sure it's regularly updated to move it farther into the future.</span><span class="sxs-lookup"><span data-stu-id="258a6-297">Set the expiration on these very far in the future (or infinite) and make sure it's regularly updated to move it farther into the future.</span></span>
3. <span data-ttu-id="258a6-298">**Use near-term expiration times on an ad hoc SAS.**</span><span class="sxs-lookup"><span data-stu-id="258a6-298">**Use near-term expiration times on an ad hoc SAS.**</span></span> <span data-ttu-id="258a6-299">In this way, even if a SAS is compromised, it's valid only for a short time.</span><span class="sxs-lookup"><span data-stu-id="258a6-299">In this way, even if a SAS is compromised, it's valid only for a short time.</span></span> <span data-ttu-id="258a6-300">This practice is especially important if you cannot reference a stored access policy.</span><span class="sxs-lookup"><span data-stu-id="258a6-300">This practice is especially important if you cannot reference a stored access policy.</span></span> <span data-ttu-id="258a6-301">Near-term expiration times also limit the amount of data that can be written to a blob by limiting the time available to upload to it.</span><span class="sxs-lookup"><span data-stu-id="258a6-301">Near-term expiration times also limit the amount of data that can be written to a blob by limiting the time available to upload to it.</span></span>
4. <span data-ttu-id="258a6-302">**Have clients automatically renew the SAS if necessary.**</span><span class="sxs-lookup"><span data-stu-id="258a6-302">**Have clients automatically renew the SAS if necessary.**</span></span> <span data-ttu-id="258a6-303">Clients should renew the SAS well before the expiration, in order to allow time for retries if the service providing the SAS is unavailable.</span><span class="sxs-lookup"><span data-stu-id="258a6-303">Clients should renew the SAS well before the expiration, in order to allow time for retries if the service providing the SAS is unavailable.</span></span> <span data-ttu-id="258a6-304">If your SAS is meant to be used for a small number of immediate, short-lived operations that are expected to be completed within the expiration period, then this may be unnecessary as the SAS is not expected to be renewed.</span><span class="sxs-lookup"><span data-stu-id="258a6-304">If your SAS is meant to be used for a small number of immediate, short-lived operations that are expected to be completed within the expiration period, then this may be unnecessary as the SAS is not expected to be renewed.</span></span> <span data-ttu-id="258a6-305">However, if you have client that is routinely making requests via SAS, then the possibility of expiration comes into play.</span><span class="sxs-lookup"><span data-stu-id="258a6-305">However, if you have client that is routinely making requests via SAS, then the possibility of expiration comes into play.</span></span> <span data-ttu-id="258a6-306">The key consideration is to balance the need for the SAS to be short-lived (as previously stated) with the need to ensure that the client is requesting renewal early enough (to avoid disruption due to the SAS expiring prior to successful renewal).</span><span class="sxs-lookup"><span data-stu-id="258a6-306">The key consideration is to balance the need for the SAS to be short-lived (as previously stated) with the need to ensure that the client is requesting renewal early enough (to avoid disruption due to the SAS expiring prior to successful renewal).</span></span>
5. <span data-ttu-id="258a6-307">**Be careful with SAS start time.**</span><span class="sxs-lookup"><span data-stu-id="258a6-307">**Be careful with SAS start time.**</span></span> <span data-ttu-id="258a6-308">If you set the start time for a SAS to **now**, then due to clock skew (differences in current time according to different machines), failures may be observed intermittently for the first few minutes.</span><span class="sxs-lookup"><span data-stu-id="258a6-308">If you set the start time for a SAS to **now**, then due to clock skew (differences in current time according to different machines), failures may be observed intermittently for the first few minutes.</span></span> <span data-ttu-id="258a6-309">In general, set the start time to be at least 15 minutes in the past.</span><span class="sxs-lookup"><span data-stu-id="258a6-309">In general, set the start time to be at least 15 minutes in the past.</span></span> <span data-ttu-id="258a6-310">Or, don't set it at all, which will make it valid immediately in all cases.</span><span class="sxs-lookup"><span data-stu-id="258a6-310">Or, don't set it at all, which will make it valid immediately in all cases.</span></span> <span data-ttu-id="258a6-311">The same generally applies to expiry time as well--remember that you may observe up to 15 minutes of clock skew in either direction on any request.</span><span class="sxs-lookup"><span data-stu-id="258a6-311">The same generally applies to expiry time as well--remember that you may observe up to 15 minutes of clock skew in either direction on any request.</span></span> <span data-ttu-id="258a6-312">For clients using a REST version prior to 2012-02-12, the maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.</span><span class="sxs-lookup"><span data-stu-id="258a6-312">For clients using a REST version prior to 2012-02-12, the maximum duration for a SAS that does not reference a stored access policy is 1 hour, and any policies specifying longer term than that will fail.</span></span>
6. <span data-ttu-id="258a6-313">**Be specific with the resource to be accessed.**</span><span class="sxs-lookup"><span data-stu-id="258a6-313">**Be specific with the resource to be accessed.**</span></span> <span data-ttu-id="258a6-314">A security best practice is to provide a user with the minimum required privileges.</span><span class="sxs-lookup"><span data-stu-id="258a6-314">A security best practice is to provide a user with the minimum required privileges.</span></span> <span data-ttu-id="258a6-315">If a user only needs read access to a single entity, then grant them read access to that single entity, and not read/write/delete access to all entities.</span><span class="sxs-lookup"><span data-stu-id="258a6-315">If a user only needs read access to a single entity, then grant them read access to that single entity, and not read/write/delete access to all entities.</span></span> <span data-ttu-id="258a6-316">This also helps lessen the damage if a SAS is compromised because the SAS has less power in the hands of an attacker.</span><span class="sxs-lookup"><span data-stu-id="258a6-316">This also helps lessen the damage if a SAS is compromised because the SAS has less power in the hands of an attacker.</span></span>
7. <span data-ttu-id="258a6-317">**Understand that your account will be billed for any usage, including that done with SAS.**</span><span class="sxs-lookup"><span data-stu-id="258a6-317">**Understand that your account will be billed for any usage, including that done with SAS.**</span></span> <span data-ttu-id="258a6-318">If you provide write access to a blob, a user may choose to upload a 200GB blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-318">If you provide write access to a blob, a user may choose to upload a 200GB blob.</span></span> <span data-ttu-id="258a6-319">If you've given them read access as well, they may choose to download it 10 times, incurring 2 TB in egress costs for you.</span><span class="sxs-lookup"><span data-stu-id="258a6-319">If you've given them read access as well, they may choose to download it 10 times, incurring 2 TB in egress costs for you.</span></span> <span data-ttu-id="258a6-320">Again, provide limited permissions to help mitigate the potential actions of malicious users.</span><span class="sxs-lookup"><span data-stu-id="258a6-320">Again, provide limited permissions to help mitigate the potential actions of malicious users.</span></span> <span data-ttu-id="258a6-321">Use short-lived SAS to reduce this threat (but be mindful of clock skew on the end time).</span><span class="sxs-lookup"><span data-stu-id="258a6-321">Use short-lived SAS to reduce this threat (but be mindful of clock skew on the end time).</span></span>
8. <span data-ttu-id="258a6-322">**Validate data written using SAS.**</span><span class="sxs-lookup"><span data-stu-id="258a6-322">**Validate data written using SAS.**</span></span> <span data-ttu-id="258a6-323">When a client application writes data to your storage account, keep in mind that there can be problems with that data.</span><span class="sxs-lookup"><span data-stu-id="258a6-323">When a client application writes data to your storage account, keep in mind that there can be problems with that data.</span></span> <span data-ttu-id="258a6-324">If your application requires that that data be validated or authorized before it is ready to use, you should perform this validation after the data is written and before it is used by your application.</span><span class="sxs-lookup"><span data-stu-id="258a6-324">If your application requires that that data be validated or authorized before it is ready to use, you should perform this validation after the data is written and before it is used by your application.</span></span> <span data-ttu-id="258a6-325">This practice also protects against corrupt or malicious data being written to your account, either by a user who properly acquired the SAS, or by a user exploiting a leaked SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-325">This practice also protects against corrupt or malicious data being written to your account, either by a user who properly acquired the SAS, or by a user exploiting a leaked SAS.</span></span>
9. <span data-ttu-id="258a6-326">**Don't always use SAS.**</span><span class="sxs-lookup"><span data-stu-id="258a6-326">**Don't always use SAS.**</span></span> <span data-ttu-id="258a6-327">Sometimes the risks associated with a particular operation against your storage account outweigh the benefits of SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-327">Sometimes the risks associated with a particular operation against your storage account outweigh the benefits of SAS.</span></span> <span data-ttu-id="258a6-328">For such operations, create a middle-tier service that writes to your storage account after performing business rule validation, authentication, and auditing.</span><span class="sxs-lookup"><span data-stu-id="258a6-328">For such operations, create a middle-tier service that writes to your storage account after performing business rule validation, authentication, and auditing.</span></span> <span data-ttu-id="258a6-329">Also, sometimes it's simpler to manage access in other ways.</span><span class="sxs-lookup"><span data-stu-id="258a6-329">Also, sometimes it's simpler to manage access in other ways.</span></span> <span data-ttu-id="258a6-330">For example, if you want to make all blobs in a container publically readable, you can make the container Public, rather than providing a SAS to every client for access.</span><span class="sxs-lookup"><span data-stu-id="258a6-330">For example, if you want to make all blobs in a container publically readable, you can make the container Public, rather than providing a SAS to every client for access.</span></span>
10. <span data-ttu-id="258a6-331">**Use Storage Analytics to monitor your application.**</span><span class="sxs-lookup"><span data-stu-id="258a6-331">**Use Storage Analytics to monitor your application.**</span></span> <span data-ttu-id="258a6-332">You can use logging and metrics to observe any spike in authentication failures due to an outage in your SAS provider service or to the inadvertent removal of a stored access policy.</span><span class="sxs-lookup"><span data-stu-id="258a6-332">You can use logging and metrics to observe any spike in authentication failures due to an outage in your SAS provider service or to the inadvertent removal of a stored access policy.</span></span> <span data-ttu-id="258a6-333">See the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) for additional information.</span><span class="sxs-lookup"><span data-stu-id="258a6-333">See the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) for additional information.</span></span>

## <a name="sas-examples"></a><span data-ttu-id="258a6-334">SAS examples</span><span class="sxs-lookup"><span data-stu-id="258a6-334">SAS examples</span></span>
<span data-ttu-id="258a6-335">Below are some examples of both types of shared access signatures, account SAS and service SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-335">Below are some examples of both types of shared access signatures, account SAS and service SAS.</span></span>

<span data-ttu-id="258a6-336">To run these C# examples, you need to reference the following NuGet packages in your project:</span><span class="sxs-lookup"><span data-stu-id="258a6-336">To run these C# examples, you need to reference the following NuGet packages in your project:</span></span>

* <span data-ttu-id="258a6-337">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x or later (to use account SAS).</span><span class="sxs-lookup"><span data-stu-id="258a6-337">[Azure Storage Client Library for .NET](http://www.nuget.org/packages/WindowsAzure.Storage), version 6.x or later (to use account SAS).</span></span>
* [<span data-ttu-id="258a6-338">Azure Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="258a6-338">Azure Configuration Manager</span></span>](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

<span data-ttu-id="258a6-339">For additional examples that show how to create and test a SAS, see [Azure Code Samples for Storage](https://azure.microsoft.com/documentation/samples/?service=storage).</span><span class="sxs-lookup"><span data-stu-id="258a6-339">For additional examples that show how to create and test a SAS, see [Azure Code Samples for Storage](https://azure.microsoft.com/documentation/samples/?service=storage).</span></span>

### <a name="example-create-and-use-an-account-sas"></a><span data-ttu-id="258a6-340">Example: Create and use an account SAS</span><span class="sxs-lookup"><span data-stu-id="258a6-340">Example: Create and use an account SAS</span></span>
<span data-ttu-id="258a6-341">The following code example creates an account SAS that is valid for the Blob and File services, and gives the client permissions read, write, and list permissions to access service-level APIs.</span><span class="sxs-lookup"><span data-stu-id="258a6-341">The following code example creates an account SAS that is valid for the Blob and File services, and gives the client permissions read, write, and list permissions to access service-level APIs.</span></span> <span data-ttu-id="258a6-342">The account SAS restricts the protocol to HTTPS, so the request must be made with HTTPS.</span><span class="sxs-lookup"><span data-stu-id="258a6-342">The account SAS restricts the protocol to HTTPS, so the request must be made with HTTPS.</span></span>

```csharp
static string GetAccountSASToken()
{
    // To create the account SAS, you need to use your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for the account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return the SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

<span data-ttu-id="258a6-343">To use the account SAS to access service-level APIs for the Blob service, construct a Blob client object using the SAS and the Blob storage endpoint for your storage account.</span><span class="sxs-lookup"><span data-stu-id="258a6-343">To use the account SAS to access service-level APIs for the Blob service, construct a Blob client object using the SAS and the Blob storage endpoint for your storage account.</span></span>

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using the SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and the account name to create a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set the service properties for the Blob client created with the SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // The permissions granted by the account SAS also permit you to retrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a><span data-ttu-id="258a6-344">Example: Create a stored access policy</span><span class="sxs-lookup"><span data-stu-id="258a6-344">Example: Create a stored access policy</span></span>
<span data-ttu-id="258a6-345">The following code creates a stored access policy on a container.</span><span class="sxs-lookup"><span data-stu-id="258a6-345">The following code creates a stored access policy on a container.</span></span> <span data-ttu-id="258a6-346">You can use the access policy to specify constraints for a service SAS on the container or its blobs.</span><span class="sxs-lookup"><span data-stu-id="258a6-346">You can use the access policy to specify constraints for a service SAS on the container or its blobs.</span></span>

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // The access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
        // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get the container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a><span data-ttu-id="258a6-347">Example: Create a service SAS on a container</span><span class="sxs-lookup"><span data-stu-id="258a6-347">Example: Create a service SAS on a container</span></span>
<span data-ttu-id="258a6-348">The following code creates a SAS on a container.</span><span class="sxs-lookup"><span data-stu-id="258a6-348">The following code creates a SAS on a container.</span></span> <span data-ttu-id="258a6-349">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-349">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span></span> <span data-ttu-id="258a6-350">If no stored access policy is provided, then the code creates an ad-hoc SAS on the container.</span><span class="sxs-lookup"><span data-stu-id="258a6-350">If no stored access policy is provided, then the code creates an ad-hoc SAS on the container.</span></span>

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate the shared access signature on the container, setting the constraints directly on the signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the container. In this case, all of the constraints for the
        // shared access signature are specified on the stored access policy, which is provided by name.
        // It is also possible to specify some constraints on an ad-hoc SAS and others on the stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a><span data-ttu-id="258a6-351">Example: Create a service SAS on a blob</span><span class="sxs-lookup"><span data-stu-id="258a6-351">Example: Create a service SAS on a blob</span></span>
<span data-ttu-id="258a6-352">The following code creates a SAS on a blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-352">The following code creates a SAS on a blob.</span></span> <span data-ttu-id="258a6-353">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span><span class="sxs-lookup"><span data-stu-id="258a6-353">If the name of an existing stored access policy is provided, that policy is associated with the SAS.</span></span> <span data-ttu-id="258a6-354">If no stored access policy is provided, then the code creates an ad-hoc SAS on the blob.</span><span class="sxs-lookup"><span data-stu-id="258a6-354">If no stored access policy is provided, then the code creates an ad-hoc SAS on the blob.</span></span>

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference to a blob within the container.
    // Note that the blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate the shared access signature on the blob, setting the constraints directly on the signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the blob. In this case, all of the constraints for the
        // shared access signature are specified on the container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a><span data-ttu-id="258a6-355">Conclusion</span><span class="sxs-lookup"><span data-stu-id="258a6-355">Conclusion</span></span>
<span data-ttu-id="258a6-356">Shared access signatures are useful for providing limited permissions to your storage account to clients that should not have the account key.</span><span class="sxs-lookup"><span data-stu-id="258a6-356">Shared access signatures are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="258a6-357">As such, they are a vital part of the security model for any application using Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="258a6-357">As such, they are a vital part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="258a6-358">If you follow the best practices listed here, you can use SAS to provide greater flexibility of access to resources in your storage account, without compromising the security of your application.</span><span class="sxs-lookup"><span data-stu-id="258a6-358">If you follow the best practices listed here, you can use SAS to provide greater flexibility of access to resources in your storage account, without compromising the security of your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="258a6-359">Next Steps</span><span class="sxs-lookup"><span data-stu-id="258a6-359">Next Steps</span></span>
* [<span data-ttu-id="258a6-360">Manage anonymous read access to containers and blobs</span><span class="sxs-lookup"><span data-stu-id="258a6-360">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="258a6-361">Delegating Access with a Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="258a6-361">Delegating Access with a Shared Access Signature</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="258a6-362">Introducing Table and Queue SAS</span><span class="sxs-lookup"><span data-stu-id="258a6-362">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png



