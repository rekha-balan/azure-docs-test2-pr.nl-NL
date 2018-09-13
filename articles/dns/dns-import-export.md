---
title: Import and export a domain zone file to Azure DNS using Azure CLI 2.0 | Microsoft Docs
description: Learn how to import and export a DNS zone file to Azure DNS by using Azure CLI 2.0
services: dns
documentationcenter: na
author: vhorne
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2018
ms.author: victorh
ms.openlocfilehash: 7578d078b147b5c4bf42f5343d3fdfdf6f0bc42e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44778952"
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-20"></a><span data-ttu-id="63860-103">Import and export a DNS zone file using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="63860-103">Import and export a DNS zone file using the Azure CLI 2.0</span></span> 

<span data-ttu-id="63860-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="63860-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 2.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="63860-105">Introduction to DNS zone migration</span><span class="sxs-lookup"><span data-stu-id="63860-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="63860-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span><span class="sxs-lookup"><span data-stu-id="63860-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="63860-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span><span class="sxs-lookup"><span data-stu-id="63860-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="63860-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="63860-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="63860-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="63860-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="63860-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="63860-111">The Azure CLI 2.0 is a cross-platform command-line tool used for managing Azure services.</span><span class="sxs-lookup"><span data-stu-id="63860-111">The Azure CLI 2.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="63860-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="63860-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="63860-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span><span class="sxs-lookup"><span data-stu-id="63860-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>


## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="63860-114">Obtain your existing DNS zone file</span><span class="sxs-lookup"><span data-stu-id="63860-114">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="63860-115">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-115">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="63860-116">The source of this file depends on where the DNS zone is currently hosted.</span><span class="sxs-lookup"><span data-stu-id="63860-116">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="63860-117">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-117">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="63860-118">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="63860-118">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="63860-119">The full path to each zone file also shows on the **General** tab of the DNS console.</span><span class="sxs-lookup"><span data-stu-id="63860-119">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="63860-120">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="63860-120">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="63860-121">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span><span class="sxs-lookup"><span data-stu-id="63860-121">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="63860-122">You need to correct this before you import these zone files into Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-122">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="63860-123">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span><span class="sxs-lookup"><span data-stu-id="63860-123">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="63860-124">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-124">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="63860-125">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span><span class="sxs-lookup"><span data-stu-id="63860-125">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="63860-126">(with a terminating ".").</span><span class="sxs-lookup"><span data-stu-id="63860-126">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="63860-127">Import a DNS zone file into Azure DNS</span><span class="sxs-lookup"><span data-stu-id="63860-127">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="63860-128">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span><span class="sxs-lookup"><span data-stu-id="63860-128">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="63860-129">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span><span class="sxs-lookup"><span data-stu-id="63860-129">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="63860-130">Merge behavior</span><span class="sxs-lookup"><span data-stu-id="63860-130">Merge behavior</span></span>

* <span data-ttu-id="63860-131">By default, existing and new record sets are merged.</span><span class="sxs-lookup"><span data-stu-id="63860-131">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="63860-132">Identical records within a merged record set are de-duplicated.</span><span class="sxs-lookup"><span data-stu-id="63860-132">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="63860-133">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span><span class="sxs-lookup"><span data-stu-id="63860-133">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span>
* <span data-ttu-id="63860-134">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-134">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file.</span></span> <span data-ttu-id="63860-135">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-135">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="63860-136">An imported CNAME record does not replace an existing CNAME record with the same name.</span><span class="sxs-lookup"><span data-stu-id="63860-136">An imported CNAME record does not replace an existing CNAME record with the same name.</span></span>  
* <span data-ttu-id="63860-137">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span><span class="sxs-lookup"><span data-stu-id="63860-137">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> 

### <a name="additional-information-about-importing"></a><span data-ttu-id="63860-138">Additional information about importing</span><span class="sxs-lookup"><span data-stu-id="63860-138">Additional information about importing</span></span>

<span data-ttu-id="63860-139">The following notes provide additional technical details about the zone import process.</span><span class="sxs-lookup"><span data-stu-id="63860-139">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="63860-140">The `$TTL` directive is optional, and it is supported.</span><span class="sxs-lookup"><span data-stu-id="63860-140">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="63860-141">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span><span class="sxs-lookup"><span data-stu-id="63860-141">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="63860-142">When two records in the same record set specify different TTLs, the lower value is used.</span><span class="sxs-lookup"><span data-stu-id="63860-142">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="63860-143">The `$ORIGIN` directive is optional, and it is supported.</span><span class="sxs-lookup"><span data-stu-id="63860-143">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="63860-144">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span><span class="sxs-lookup"><span data-stu-id="63860-144">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="63860-145">The `$INCLUDE` and `$GENERATE` directives are not supported.</span><span class="sxs-lookup"><span data-stu-id="63860-145">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="63860-146">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span><span class="sxs-lookup"><span data-stu-id="63860-146">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="63860-147">The SOA record is created automatically by Azure DNS when a zone is created.</span><span class="sxs-lookup"><span data-stu-id="63860-147">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="63860-148">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span><span class="sxs-lookup"><span data-stu-id="63860-148">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="63860-149">This parameter uses the value provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-149">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="63860-150">This is because this parameter must refer to the primary name server provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-150">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="63860-151">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span><span class="sxs-lookup"><span data-stu-id="63860-151">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="63860-152">Only the TTL of this record set is imported.</span><span class="sxs-lookup"><span data-stu-id="63860-152">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="63860-153">These records contain the name server names provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-153">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="63860-154">The record data is not overwritten by the values contained in the imported zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-154">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="63860-155">During Public Preview, Azure DNS supports only single-string TXT records.</span><span class="sxs-lookup"><span data-stu-id="63860-155">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="63860-156">Multistring TXT records are be concatenated and truncated to 255 characters.</span><span class="sxs-lookup"><span data-stu-id="63860-156">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="63860-157">CLI format and values</span><span class="sxs-lookup"><span data-stu-id="63860-157">CLI format and values</span></span>

<span data-ttu-id="63860-158">The format of the Azure CLI command to import a DNS zone is:</span><span class="sxs-lookup"><span data-stu-id="63860-158">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
az network dns zone import -g <resource group> -n <zone name> -f <zone file name>
```

<span data-ttu-id="63860-159">Values:</span><span class="sxs-lookup"><span data-stu-id="63860-159">Values:</span></span>

* <span data-ttu-id="63860-160">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-160">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="63860-161">`<zone name>` is the name of the zone.</span><span class="sxs-lookup"><span data-stu-id="63860-161">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="63860-162">`<zone file name>` is the path/name of the zone file to be imported.</span><span class="sxs-lookup"><span data-stu-id="63860-162">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="63860-163">If a zone with this name does not exist in the resource group, it is created for you.</span><span class="sxs-lookup"><span data-stu-id="63860-163">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="63860-164">If the zone already exists, the imported record sets are merged with existing record sets.</span><span class="sxs-lookup"><span data-stu-id="63860-164">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> 


### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="63860-165">Step 1.</span><span class="sxs-lookup"><span data-stu-id="63860-165">Step 1.</span></span> <span data-ttu-id="63860-166">Import a zone file</span><span class="sxs-lookup"><span data-stu-id="63860-166">Import a zone file</span></span>

<span data-ttu-id="63860-167">To import a zone file for the zone **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="63860-167">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="63860-168">If you don't have one already, you need to create a Resource Manager resource group.</span><span class="sxs-lookup"><span data-stu-id="63860-168">If you don't have one already, you need to create a Resource Manager resource group.</span></span>

    ```azurecli
    az group create --group myresourcegroup -l westeurope
    ```

2. <span data-ttu-id="63860-169">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, you will run the command `az network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="63860-169">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, you will run the command `az network dns zone import`.</span></span><BR><span data-ttu-id="63860-170">This command loads the zone file and parses it.</span><span class="sxs-lookup"><span data-stu-id="63860-170">This command loads the zone file and parses it.</span></span> <span data-ttu-id="63860-171">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span><span class="sxs-lookup"><span data-stu-id="63860-171">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="63860-172">The command reports progress in the console window, along with any errors or warnings.</span><span class="sxs-lookup"><span data-stu-id="63860-172">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="63860-173">Because record sets are created in series, it may take a few minutes to import a large zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-173">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    az network dns zone import -g myresourcegroup -n contoso.com -f contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="63860-174">Step 2.</span><span class="sxs-lookup"><span data-stu-id="63860-174">Step 2.</span></span> <span data-ttu-id="63860-175">Verify the zone</span><span class="sxs-lookup"><span data-stu-id="63860-175">Verify the zone</span></span>

<span data-ttu-id="63860-176">To verify the DNS zone after you import the file, you can use any one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="63860-176">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="63860-177">You can list the records by using the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="63860-177">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    az network dns record-set list -g myresourcegroup -z contoso.com
    ```

* <span data-ttu-id="63860-178">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="63860-178">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="63860-179">You can use `nslookup` to verify name resolution for the records.</span><span class="sxs-lookup"><span data-stu-id="63860-179">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="63860-180">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span><span class="sxs-lookup"><span data-stu-id="63860-180">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="63860-181">The following sample shows how to retrieve the name server names assigned to the zone.</span><span class="sxs-lookup"><span data-stu-id="63860-181">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="63860-182">This also shows how to query the "www" record by using `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="63860-182">This also shows how to query the "www" record by using `nslookup`.</span></span>

    ```azurecli
    az network dns record-set ns list -g myresourcegroup -z  --output json 
    ```

    ```json
    [
      {
       .......
       "name": "@",
        "nsRecords": [
          {
            "additionalProperties": {},
            "nsdname": "ns1-03.azure-dns.com."
          },
          {
            "additionalProperties": {},
            "nsdname": "ns2-03.azure-dns.net."
          },
          {
            "additionalProperties": {},
            "nsdname": "ns3-03.azure-dns.org."
          },
          {
            "additionalProperties": {},
            "nsdname": "ns4-03.azure-dns.info."
          }
        ],
        "resourceGroup": "myresourcegroup",
        "ttl": 86400,
        "type": "Microsoft.Network/dnszones/NS"
      }
    ]
    ```

    ```cmd
    nslookup www.contoso.com ns1-03.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221
    ```

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="63860-183">Step 3.</span><span class="sxs-lookup"><span data-stu-id="63860-183">Step 3.</span></span> <span data-ttu-id="63860-184">Update DNS delegation</span><span class="sxs-lookup"><span data-stu-id="63860-184">Update DNS delegation</span></span>

<span data-ttu-id="63860-185">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="63860-185">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="63860-186">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="63860-186">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="63860-187">Export a DNS zone file from Azure DNS</span><span class="sxs-lookup"><span data-stu-id="63860-187">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="63860-188">The format of the Azure CLI command to import a DNS zone is:</span><span class="sxs-lookup"><span data-stu-id="63860-188">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
az network dns zone export -g <resource group> -n <zone name> -f <zone file name>
```

<span data-ttu-id="63860-189">Values:</span><span class="sxs-lookup"><span data-stu-id="63860-189">Values:</span></span>

* <span data-ttu-id="63860-190">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="63860-190">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="63860-191">`<zone name>` is the name of the zone.</span><span class="sxs-lookup"><span data-stu-id="63860-191">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="63860-192">`<zone file name>` is the path/name of the zone file to be exported.</span><span class="sxs-lookup"><span data-stu-id="63860-192">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="63860-193">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="63860-193">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="63860-194">To export a zone file</span><span class="sxs-lookup"><span data-stu-id="63860-194">To export a zone file</span></span>

<span data-ttu-id="63860-195">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="63860-195">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="63860-196">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span><span class="sxs-lookup"><span data-stu-id="63860-196">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```
    az network dns zone export -g myresourcegroup -n contoso.com -f contoso.com.txt
    ```
