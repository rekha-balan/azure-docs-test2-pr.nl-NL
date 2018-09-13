---
title: Import and export a domain zone file to Azure DNS using CLI| Microsoft Docs
description: Learn how to import and export a DNS zone file to Azure DNS by using Azure CLI
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 765a30f360cf8d3f8bde08aa94b20eba0d4537c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550956"
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli"></a><span data-ttu-id="a49ae-103">Import and export a DNS zone file using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a49ae-103">Import and export a DNS zone file using the Azure CLI</span></span>

<span data-ttu-id="a49ae-104">This article will walk you through how to import and export DNS zone files for Azure DNS using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a49ae-104">This article will walk you through how to import and export DNS zone files for Azure DNS using the Azure CLI.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="a49ae-105">Introduction to DNS zone migration</span><span class="sxs-lookup"><span data-stu-id="a49ae-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="a49ae-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="a49ae-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span><span class="sxs-lookup"><span data-stu-id="a49ae-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="a49ae-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="a49ae-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="a49ae-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="a49ae-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a49ae-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="a49ae-111">The Azure CLI is a cross-platform command-line tool used for managing Azure services.</span><span class="sxs-lookup"><span data-stu-id="a49ae-111">The Azure CLI is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="a49ae-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a49ae-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="a49ae-113">Cross-platform support is particularly important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span><span class="sxs-lookup"><span data-stu-id="a49ae-113">Cross-platform support is particularly important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="a49ae-114">There are currently two versions of the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a49ae-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="a49ae-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span><span class="sxs-lookup"><span data-stu-id="a49ae-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="a49ae-116">CLI2.0 is based on Python and has commands beginning with "az".</span><span class="sxs-lookup"><span data-stu-id="a49ae-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="a49ae-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span><span class="sxs-lookup"><span data-stu-id="a49ae-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="a49ae-118">Obtain your existing DNS zone file</span><span class="sxs-lookup"><span data-stu-id="a49ae-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="a49ae-119">Before you import a DNS zone file into Azure DNS, you will need to obtain a copy of the zone file.</span><span class="sxs-lookup"><span data-stu-id="a49ae-119">Before you import a DNS zone file into Azure DNS, you will need to obtain a copy of the zone file.</span></span> <span data-ttu-id="a49ae-120">The source of this file will depend on where the DNS zone is currently hosted.</span><span class="sxs-lookup"><span data-stu-id="a49ae-120">The source of this file will depend on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="a49ae-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span><span class="sxs-lookup"><span data-stu-id="a49ae-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="a49ae-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="a49ae-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="a49ae-123">The full path to each zone file also shows on the **General** tab of the DNS service management console.</span><span class="sxs-lookup"><span data-stu-id="a49ae-123">The full path to each zone file also shows on the **General** tab of the DNS service management console.</span></span>
* <span data-ttu-id="a49ae-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="a49ae-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="a49ae-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span><span class="sxs-lookup"><span data-stu-id="a49ae-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="a49ae-126">You need to correct this before you import these zone files into Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="a49ae-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span><span class="sxs-lookup"><span data-stu-id="a49ae-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="a49ae-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="a49ae-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span><span class="sxs-lookup"><span data-stu-id="a49ae-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="a49ae-130">(with a terminating ".").</span><span class="sxs-lookup"><span data-stu-id="a49ae-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="a49ae-131">Import a DNS zone file into Azure DNS</span><span class="sxs-lookup"><span data-stu-id="a49ae-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="a49ae-132">Importing a zone file will create a new zone in Azure DNS if one does not already exist.</span><span class="sxs-lookup"><span data-stu-id="a49ae-132">Importing a zone file will create a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="a49ae-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span><span class="sxs-lookup"><span data-stu-id="a49ae-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="a49ae-134">Merge behavior</span><span class="sxs-lookup"><span data-stu-id="a49ae-134">Merge behavior</span></span>

* <span data-ttu-id="a49ae-135">By default, existing and new record sets are merged.</span><span class="sxs-lookup"><span data-stu-id="a49ae-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="a49ae-136">Identical records within a merged record set are de-duplicated.</span><span class="sxs-lookup"><span data-stu-id="a49ae-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="a49ae-137">Alternatively, by specifying the `--force` option, the import process will replace existing record sets with new record sets.</span><span class="sxs-lookup"><span data-stu-id="a49ae-137">Alternatively, by specifying the `--force` option, the import process will replace existing record sets with new record sets.</span></span> <span data-ttu-id="a49ae-138">Existing record sets that do not have a corresponding record set in the imported zone file will not be removed.</span><span class="sxs-lookup"><span data-stu-id="a49ae-138">Existing record sets that do not have a corresponding record set in the imported zone file will not be removed.</span></span>
* <span data-ttu-id="a49ae-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span><span class="sxs-lookup"><span data-stu-id="a49ae-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="a49ae-140">When `--force` is used, the TTL of the new record set is used.</span><span class="sxs-lookup"><span data-stu-id="a49ae-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="a49ae-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span><span class="sxs-lookup"><span data-stu-id="a49ae-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="a49ae-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span><span class="sxs-lookup"><span data-stu-id="a49ae-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="a49ae-143">An imported CNAME record will not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span><span class="sxs-lookup"><span data-stu-id="a49ae-143">An imported CNAME record will not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="a49ae-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span><span class="sxs-lookup"><span data-stu-id="a49ae-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="a49ae-145">This is independent of the use of `--force`.</span><span class="sxs-lookup"><span data-stu-id="a49ae-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="a49ae-146">Additional information about importing</span><span class="sxs-lookup"><span data-stu-id="a49ae-146">Additional information about importing</span></span>

<span data-ttu-id="a49ae-147">The following notes provide additional technical details about the zone import process.</span><span class="sxs-lookup"><span data-stu-id="a49ae-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="a49ae-148">The `$TTL` directive is optional, and it is supported.</span><span class="sxs-lookup"><span data-stu-id="a49ae-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="a49ae-149">When no `$TTL` directive is given, records without an explicit TTL will be imported set to a default TTL of 3600 seconds.</span><span class="sxs-lookup"><span data-stu-id="a49ae-149">When no `$TTL` directive is given, records without an explicit TTL will be imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="a49ae-150">When two records in the same record set specify different TTLs, the lower value is used.</span><span class="sxs-lookup"><span data-stu-id="a49ae-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="a49ae-151">The `$ORIGIN` directive is optional, and it is supported.</span><span class="sxs-lookup"><span data-stu-id="a49ae-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="a49ae-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span><span class="sxs-lookup"><span data-stu-id="a49ae-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="a49ae-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span><span class="sxs-lookup"><span data-stu-id="a49ae-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="a49ae-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span><span class="sxs-lookup"><span data-stu-id="a49ae-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="a49ae-155">The SOA record is created automatically by Azure DNS when a zone is created.</span><span class="sxs-lookup"><span data-stu-id="a49ae-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="a49ae-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span><span class="sxs-lookup"><span data-stu-id="a49ae-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="a49ae-157">This parameter uses the value provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="a49ae-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="a49ae-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span><span class="sxs-lookup"><span data-stu-id="a49ae-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="a49ae-160">Only the TTL of this record set is imported.</span><span class="sxs-lookup"><span data-stu-id="a49ae-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="a49ae-161">These records contain the name server names provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="a49ae-162">The record data is not overwritten by the values contained in the imported zone file.</span><span class="sxs-lookup"><span data-stu-id="a49ae-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="a49ae-163">During Public Preview, Azure DNS supports only single-string TXT records.</span><span class="sxs-lookup"><span data-stu-id="a49ae-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="a49ae-164">Multistring TXT records will be concatenated and truncated to 255 characters.</span><span class="sxs-lookup"><span data-stu-id="a49ae-164">Multistring TXT records will be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="a49ae-165">CLI format and values</span><span class="sxs-lookup"><span data-stu-id="a49ae-165">CLI format and values</span></span>

<span data-ttu-id="a49ae-166">The format of the Azure CLI command to import a DNS zone is:</span><span class="sxs-lookup"><span data-stu-id="a49ae-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="a49ae-167">Values:</span><span class="sxs-lookup"><span data-stu-id="a49ae-167">Values:</span></span>

* <span data-ttu-id="a49ae-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="a49ae-169">`<zone name>` is the name of the zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="a49ae-170">`<zone file name>` is the path/name of the zone file to be imported.</span><span class="sxs-lookup"><span data-stu-id="a49ae-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="a49ae-171">If a zone with this name does not exist in the resource group, it will be created for you.</span><span class="sxs-lookup"><span data-stu-id="a49ae-171">If a zone with this name does not exist in the resource group, it will be created for you.</span></span> <span data-ttu-id="a49ae-172">If the zone already exists, the imported record sets will be merged with existing record sets.</span><span class="sxs-lookup"><span data-stu-id="a49ae-172">If the zone already exists, the imported record sets will be merged with existing record sets.</span></span> <span data-ttu-id="a49ae-173">To overwrite the existing record sets, use the `--force` option.</span><span class="sxs-lookup"><span data-stu-id="a49ae-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="a49ae-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span><span class="sxs-lookup"><span data-stu-id="a49ae-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="a49ae-175">Step 1.</span><span class="sxs-lookup"><span data-stu-id="a49ae-175">Step 1.</span></span> <span data-ttu-id="a49ae-176">Import a zone file</span><span class="sxs-lookup"><span data-stu-id="a49ae-176">Import a zone file</span></span>

<span data-ttu-id="a49ae-177">To import a zone file for the zone **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a49ae-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="a49ae-178">Sign in to your Azure subscription by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a49ae-178">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="a49ae-179">Select the subscription where you want to create your new DNS zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="a49ae-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="a49ae-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="a49ae-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span><span class="sxs-lookup"><span data-stu-id="a49ae-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="a49ae-182">(This is a one-time operation for each subscription.)</span><span class="sxs-lookup"><span data-stu-id="a49ae-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="a49ae-183">If you don't have one already, you also need to create a Resource Manager resource group.</span><span class="sxs-lookup"><span data-stu-id="a49ae-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="a49ae-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="a49ae-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="a49ae-185">This command will load the zone file and parse it.</span><span class="sxs-lookup"><span data-stu-id="a49ae-185">This command will load the zone file and parse it.</span></span> <span data-ttu-id="a49ae-186">The command will execute a series of commands on the Azure DNS service to create the zone and all of the record sets in the zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-186">The command will execute a series of commands on the Azure DNS service to create the zone and all of the record sets in the zone.</span></span> <span data-ttu-id="a49ae-187">The command will also report progress in the console window, along with any errors or warnings.</span><span class="sxs-lookup"><span data-stu-id="a49ae-187">The command will also report progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="a49ae-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span><span class="sxs-lookup"><span data-stu-id="a49ae-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="a49ae-189">Step 2.</span><span class="sxs-lookup"><span data-stu-id="a49ae-189">Step 2.</span></span> <span data-ttu-id="a49ae-190">Verify the zone</span><span class="sxs-lookup"><span data-stu-id="a49ae-190">Verify the zone</span></span>

<span data-ttu-id="a49ae-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="a49ae-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="a49ae-192">You can list the records by using the following Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="a49ae-192">You can list the records by using the following Azure CLI command.</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="a49ae-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="a49ae-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="a49ae-194">You can use `nslookup` to verify name resolution for the records.</span><span class="sxs-lookup"><span data-stu-id="a49ae-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="a49ae-195">Because the zone isn't delegated yet, you will need to specify the correct Azure DNS name servers explicitly.</span><span class="sxs-lookup"><span data-stu-id="a49ae-195">Because the zone isn't delegated yet, you will need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="a49ae-196">The sample below shows how to retrieve the name server names assigned to the zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-196">The sample below shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="a49ae-197">IT also shows how to query the "www" record by using `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="a49ae-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="a49ae-198">Step 3.</span><span class="sxs-lookup"><span data-stu-id="a49ae-198">Step 3.</span></span> <span data-ttu-id="a49ae-199">Update DNS delegation</span><span class="sxs-lookup"><span data-stu-id="a49ae-199">Update DNS delegation</span></span>

<span data-ttu-id="a49ae-200">After you have verified that the zone has been imported correctly, you will need to update the DNS delegation to point to the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="a49ae-200">After you have verified that the zone has been imported correctly, you will need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="a49ae-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a49ae-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="a49ae-202">Export a DNS zone file from Azure DNS</span><span class="sxs-lookup"><span data-stu-id="a49ae-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="a49ae-203">The format of the Azure CLI command to import a DNS zone is:</span><span class="sxs-lookup"><span data-stu-id="a49ae-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

    ```azurecli
    azure network dns zone export [options] <resource group> <zone name> <zone file name>
    ```

<span data-ttu-id="a49ae-204">Values:</span><span class="sxs-lookup"><span data-stu-id="a49ae-204">Values:</span></span>

* <span data-ttu-id="a49ae-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a49ae-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="a49ae-206">`<zone name>` is the name of the zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="a49ae-207">`<zone file name>` is the path/name of the zone file to be exported.</span><span class="sxs-lookup"><span data-stu-id="a49ae-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="a49ae-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="a49ae-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="a49ae-209">To export a zone file</span><span class="sxs-lookup"><span data-stu-id="a49ae-209">To export a zone file</span></span>

1. <span data-ttu-id="a49ae-210">Sign in to your Azure subscription by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a49ae-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="a49ae-211">Select the subscription where you want to create your new DNS zone.</span><span class="sxs-lookup"><span data-stu-id="a49ae-211">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="a49ae-212">Azure DNS is an Azure Resource Manager-only service.</span><span class="sxs-lookup"><span data-stu-id="a49ae-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="a49ae-213">The Azure CLI must be switched to Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="a49ae-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="a49ae-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="a49ae-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="a49ae-215">This command will call the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span><span class="sxs-lookup"><span data-stu-id="a49ae-215">This command will call the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
