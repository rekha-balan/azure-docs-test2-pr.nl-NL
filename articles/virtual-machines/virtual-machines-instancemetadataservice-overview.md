---
title: Azure Instance Metadata Service Overview | Microsoft Docs
description: RESTful interface to get information about VM's compute, network and upcoming maintenance events.
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: ''
author: harijay
manager: timlt
editor: ''
tags: ''
ms.service: azure-instancemetadataservice
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: b5c0268e1a0ebfcb33781678a367090cad865907
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661015"
---
# <a name="azures-instance-metadata-service---preview"></a><span data-ttu-id="6c6e5-103">Azure's Instance Metadata Service --Preview</span><span class="sxs-lookup"><span data-stu-id="6c6e5-103">Azure's Instance Metadata Service --Preview</span></span>

> [!NOTE] 
> <span data-ttu-id="6c6e5-104">Previews are made available to you on the condition that you agree to the terms of use.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="6c6e5-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews.] (https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="6c6e5-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews.] (https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span></span>
>

<span data-ttu-id="6c6e5-106">Instance metadata service provides information regarding your running virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-106">Instance metadata service provides information regarding your running virtual machine instances.</span></span> <span data-ttu-id="6c6e5-107">This information can be used to manage and configure your instances on Azure.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-107">This information can be used to manage and configure your instances on Azure.</span></span> <span data-ttu-id="6c6e5-108">Azure's Instance metadata service is a RESTful endpoint available to all IaaS VMs created via new [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="6c6e5-108">Azure's Instance metadata service is a RESTful endpoint available to all IaaS VMs created via new [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/?redirectedfrom=MSDN).</span></span> <span data-ttu-id="6c6e5-109">The endpoint is available at a well-known non routable IP address (*169.254.169.254*) that can be accessed only from within the VM.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-109">The endpoint is available at a well-known non routable IP address (*169.254.169.254*) that can be accessed only from within the VM.</span></span> <span data-ttu-id="6c6e5-110">This service would provide important data regarding virtual machine instance, its network configuration, and upcoming maintenance events.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-110">This service would provide important data regarding virtual machine instance, its network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="6c6e5-111">For additional information See [metadata categories](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="6c6e5-111">For additional information See [metadata categories](#instance-metadata-data-categories).</span></span>

### <a name="important-information"></a><span data-ttu-id="6c6e5-112">Important information</span><span class="sxs-lookup"><span data-stu-id="6c6e5-112">Important information</span></span>
<span data-ttu-id="6c6e5-113">Currently this service is in **preview** and hosts information regarding virtual machine instance and upcoming maintenance events.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-113">Currently this service is in **preview** and hosts information regarding virtual machine instance and upcoming maintenance events.</span></span> <span data-ttu-id="6c6e5-114">Service continues to receive updates and this page reflects the specific [data categories](#instance-metadata-data-categories) available.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-114">Service continues to receive updates and this page reflects the specific [data categories](#instance-metadata-data-categories) available.</span></span>


## <a name="service-availability"></a><span data-ttu-id="6c6e5-115">Service Availability</span><span class="sxs-lookup"><span data-stu-id="6c6e5-115">Service Availability</span></span>
<span data-ttu-id="6c6e5-116">The current Preview is available in **West US Central** Region of Azure.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-116">The current Preview is available in **West US Central** Region of Azure.</span></span> <span data-ttu-id="6c6e5-117">This following table is updated on regions where the service preview becomes available.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-117">This following table is updated on regions where the service preview becomes available.</span></span>
<span data-ttu-id="6c6e5-118">For trying out Instance metadata service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/?redirectedfrom=MSDN) or [Azure portal](http://portal.azure.com) and follow the examples in the examples section to access metadata service.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-118">For trying out Instance metadata service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/?redirectedfrom=MSDN) or [Azure portal](http://portal.azure.com) and follow the examples in the examples section to access metadata service.</span></span> 

<span data-ttu-id="6c6e5-119">Regions where Instance metadata service preview is available</span><span class="sxs-lookup"><span data-stu-id="6c6e5-119">Regions where Instance metadata service preview is available</span></span>|
------------------------------------------------------------|
<span data-ttu-id="6c6e5-120">West Central US</span><span class="sxs-lookup"><span data-stu-id="6c6e5-120">West Central US</span></span> |



## <a name="retrieving-instance-metadata"></a><span data-ttu-id="6c6e5-121">Retrieving Instance metadata</span><span class="sxs-lookup"><span data-stu-id="6c6e5-121">Retrieving Instance metadata</span></span> 

<span data-ttu-id="6c6e5-122">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="6c6e5-122">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/?redirectedfrom=MSDN).</span></span> <span data-ttu-id="6c6e5-123">Access all data categories for a virtual machine instance use the following URI</span><span class="sxs-lookup"><span data-stu-id="6c6e5-123">Access all data categories for a virtual machine instance use the following URI</span></span>

```
 curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-03-01"
```

<span data-ttu-id="6c6e5-124">The default output for all Instance metadata is in json format(content type Application/json)</span><span class="sxs-lookup"><span data-stu-id="6c6e5-124">The default output for all Instance metadata is in json format(content type Application/json)</span></span>

## <a name="usage-examples"></a><span data-ttu-id="6c6e5-125">Usage Examples</span><span class="sxs-lookup"><span data-stu-id="6c6e5-125">Usage Examples</span></span>
<span data-ttu-id="6c6e5-126">Following are set of examples and usage semantics for Instance metadata service</span><span class="sxs-lookup"><span data-stu-id="6c6e5-126">Following are set of examples and usage semantics for Instance metadata service</span></span>

### <a name="versioning"></a><span data-ttu-id="6c6e5-127">Versioning</span><span class="sxs-lookup"><span data-stu-id="6c6e5-127">Versioning</span></span> 
<span data-ttu-id="6c6e5-128">Instance metadata service is versioned.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-128">Instance metadata service is versioned.</span></span> <span data-ttu-id="6c6e5-129">Versions are mandatory and the current preview version is 2017-03-01.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-129">Versions are mandatory and the current preview version is 2017-03-01.</span></span>


```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-03-01"
```

<span data-ttu-id="6c6e5-130">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-130">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="6c6e5-131">Note, current preview version may not be available once the service is generally available.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-131">Note, current preview version may not be available once the service is generally available.</span></span>


### <a name="data-output"></a><span data-ttu-id="6c6e5-132">Data output</span><span class="sxs-lookup"><span data-stu-id="6c6e5-132">Data output</span></span>
<span data-ttu-id="6c6e5-133">By default Instance metadata returns data in json (content type=application/json).Different node elements can return data in different default format as applicable, following table is a quick reference for data formats</span><span class="sxs-lookup"><span data-stu-id="6c6e5-133">By default Instance metadata returns data in json (content type=application/json).Different node elements can return data in different default format as applicable, following table is a quick reference for data formats</span></span> 

<span data-ttu-id="6c6e5-134">Element</span><span class="sxs-lookup"><span data-stu-id="6c6e5-134">Element</span></span> | <span data-ttu-id="6c6e5-135">Default Data Format</span><span class="sxs-lookup"><span data-stu-id="6c6e5-135">Default Data Format</span></span> | <span data-ttu-id="6c6e5-136">Other formats</span><span class="sxs-lookup"><span data-stu-id="6c6e5-136">Other formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="6c6e5-137">/instance</span><span class="sxs-lookup"><span data-stu-id="6c6e5-137">/instance</span></span> | <span data-ttu-id="6c6e5-138">json</span><span class="sxs-lookup"><span data-stu-id="6c6e5-138">json</span></span> | <span data-ttu-id="6c6e5-139">text</span><span class="sxs-lookup"><span data-stu-id="6c6e5-139">text</span></span>
<span data-ttu-id="6c6e5-140">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="6c6e5-140">/scheduledevents</span></span> | <span data-ttu-id="6c6e5-141">json</span><span class="sxs-lookup"><span data-stu-id="6c6e5-141">json</span></span> | <span data-ttu-id="6c6e5-142">none</span><span class="sxs-lookup"><span data-stu-id="6c6e5-142">none</span></span>

<span data-ttu-id="6c6e5-143">For text format use format=text in the request URL, for example</span><span class="sxs-lookup"><span data-stu-id="6c6e5-143">For text format use format=text in the request URL, for example</span></span> 

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-03-01&format=text"
```
### <a name="security"></a><span data-ttu-id="6c6e5-144">Security</span><span class="sxs-lookup"><span data-stu-id="6c6e5-144">Security</span></span>
<span data-ttu-id="6c6e5-145">Instance metadata endpoint is accessible only from within the running virtual machine instance on a non-routable 169.254.169.254 IP address.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-145">Instance metadata endpoint is accessible only from within the running virtual machine instance on a non-routable 169.254.169.254 IP address.</span></span> <span data-ttu-id="6c6e5-146">In addition, any request with **X-Forwarded-For header** is rejected by the metadata service.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-146">In addition, any request with **X-Forwarded-For header** is rejected by the metadata service.</span></span> <span data-ttu-id="6c6e5-147">We also require requests to contain **Metadata:true** header being sent to ensure that the actual request was directly intended and not a part of unintentional redirection.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-147">We also require requests to contain **Metadata:true** header being sent to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 
### <a name="error"></a><span data-ttu-id="6c6e5-148">Error</span><span class="sxs-lookup"><span data-stu-id="6c6e5-148">Error</span></span>
<span data-ttu-id="6c6e5-149">If there is a data element not found or malformed requests Instance metadata service returns standard HTTP Error, following are the few examples of return codes</span><span class="sxs-lookup"><span data-stu-id="6c6e5-149">If there is a data element not found or malformed requests Instance metadata service returns standard HTTP Error, following are the few examples of return codes</span></span> 

<span data-ttu-id="6c6e5-150">HTTP Return Code</span><span class="sxs-lookup"><span data-stu-id="6c6e5-150">HTTP Return Code</span></span> | <span data-ttu-id="6c6e5-151">Reason</span><span class="sxs-lookup"><span data-stu-id="6c6e5-151">Reason</span></span>
----------------|-------
<span data-ttu-id="6c6e5-152">200</span><span class="sxs-lookup"><span data-stu-id="6c6e5-152">200</span></span> | <span data-ttu-id="6c6e5-153">OK</span><span class="sxs-lookup"><span data-stu-id="6c6e5-153">OK</span></span>
<span data-ttu-id="6c6e5-154">400</span><span class="sxs-lookup"><span data-stu-id="6c6e5-154">400</span></span> | <span data-ttu-id="6c6e5-155">Bad Request, missing header, pass -H Metadata:true</span><span class="sxs-lookup"><span data-stu-id="6c6e5-155">Bad Request, missing header, pass -H Metadata:true</span></span>
<span data-ttu-id="6c6e5-156">404</span><span class="sxs-lookup"><span data-stu-id="6c6e5-156">404</span></span> | <span data-ttu-id="6c6e5-157">Not Found, requested element does’t exist</span><span class="sxs-lookup"><span data-stu-id="6c6e5-157">Not Found, requested element does’t exist</span></span> 
<span data-ttu-id="6c6e5-158">405</span><span class="sxs-lookup"><span data-stu-id="6c6e5-158">405</span></span> | <span data-ttu-id="6c6e5-159">Method not supported</span><span class="sxs-lookup"><span data-stu-id="6c6e5-159">Method not supported</span></span> 
<span data-ttu-id="6c6e5-160">429</span><span class="sxs-lookup"><span data-stu-id="6c6e5-160">429</span></span> | <span data-ttu-id="6c6e5-161">Too many requests, currently we only support maximum of 5 queries per second</span><span class="sxs-lookup"><span data-stu-id="6c6e5-161">Too many requests, currently we only support maximum of 5 queries per second</span></span>

### <a name="examples"></a><span data-ttu-id="6c6e5-162">Examples</span><span class="sxs-lookup"><span data-stu-id="6c6e5-162">Examples</span></span>
#### <a name="retrieving-the-network-information"></a><span data-ttu-id="6c6e5-163">Retrieving the network information</span><span class="sxs-lookup"><span data-stu-id="6c6e5-163">Retrieving the network information</span></span> 

<span data-ttu-id="6c6e5-164">**Request**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-164">**Request**</span></span>
```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-03-01"

```
<span data-ttu-id="6c6e5-165">**Response**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-165">**Response**</span></span>
> [!NOTE] 
> <span data-ttu-id="6c6e5-166">The response is a json string.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-166">The response is a json string.</span></span> <span data-ttu-id="6c6e5-167">Following output is formatted json with utility like [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="6c6e5-167">Following output is formatted json with utility like [jq](https://stedolan.github.io/jq/).</span></span>
>

```
{
  "interface": [
    {
      "ipv4": {
        "ipaddress": [
          {
            "ipaddress": "10.0.0.4",
            "publicip": "<>.<>.<>.<>"
          }
        ],
        "subnet": [
          {
            "address": "10.0.0.0",
            "dnsservers": [
              {
                "ipaddress": "10.0.0.2"
              },
              {
                "ipaddress": "10.0.0.3"
              }
            ],
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipaddress": []
      },
      "mac": "000D3A00FA89"
    }
  ]
}
```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="6c6e5-168">Retrieving public IP address</span><span class="sxs-lookup"><span data-stu-id="6c6e5-168">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipaddress/0/publicip?api-version=2017-03-01&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="6c6e5-169">Retrieving all metadata for an instance</span><span class="sxs-lookup"><span data-stu-id="6c6e5-169">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="6c6e5-170">**Request**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-170">**Request**</span></span>
```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-03-01"
```
<span data-ttu-id="6c6e5-171">**Response**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-171">**Response**</span></span>
> [!NOTE]
> <span data-ttu-id="6c6e5-172">The response is a json string.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-172">The response is a json string.</span></span> <span data-ttu-id="6c6e5-173">Following output is formatted json with utility like [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="6c6e5-173">Following output is formatted json with utility like [jq](https://stedolan.github.io/jq/).</span></span>
>

```
{
"compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipaddress": [
            {
              "ipaddress": "10.0.0.4",
              "publicip": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.0.0",
              "dnsservers": [
                {
                  "ipaddress": "10.0.0.2"
                },
                {
                  "ipaddress": "10.0.0.3"
                }
              ],
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipaddress": []
        },
        "mac": "000D3A00FA89"
      }
    ]
  }
}

```
#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="6c6e5-174">Retrieving metadata in Windows Virtual machine</span><span class="sxs-lookup"><span data-stu-id="6c6e5-174">Retrieving metadata in Windows Virtual machine</span></span>

<span data-ttu-id="6c6e5-175">Instance metadata can be retrieved in Windows via Powershell utility curl.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-175">Instance metadata can be retrieved in Windows via Powershell utility curl.</span></span> <span data-ttu-id="6c6e5-176">From a Powershell prompt, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="6c6e5-176">From a Powershell prompt, run the following commands:</span></span> 

<span data-ttu-id="6c6e5-177">**Request**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-177">**Request**</span></span>
```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-03-01 | select -ExpandProperty Content
```
<span data-ttu-id="6c6e5-178">**Response**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-178">**Response**</span></span>
>[!NOTE]
> <span data-ttu-id="6c6e5-179">The response is a json string.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-179">The response is a json string.</span></span> <span data-ttu-id="6c6e5-180">Following output is formatted json with ConvertTo-Json Powershell utility.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-180">Following output is formatted json with ConvertTo-Json Powershell utility.</span></span>
> 

```
{
    "compute":  {
                    "location":  "CentralUSEUAP",
                    "name":  "SQLTest",
                    "offer":  "SQL2016SP1-WS2016",
                    "osType":  "Windows",
                    "platformFaultDomain":  "0",
                    "platformUpdateDomain":  "0",
                    "publisher":  "MicrosoftSQLServer",
                    "sku":  "Enterprise",
                    "version":  "13.0.400110",
                    "vmId":  "453945c8-3923-4366-b2d3-ea4c80e9b70e",
                    "vmSize":  "Standard_DS2"
                },
    "network":  {
                    "interface":  [
                                      "@{ipv4=; ipv6=; mac=002248020E1E}"
                                  ]
                }
}
```


## <a name="instance-metadata-data-categories"></a><span data-ttu-id="6c6e5-181">Instance metadata data categories</span><span class="sxs-lookup"><span data-stu-id="6c6e5-181">Instance metadata data categories</span></span>
<span data-ttu-id="6c6e5-182">Following table has a list of all data categories available via Instance metadata</span><span class="sxs-lookup"><span data-stu-id="6c6e5-182">Following table has a list of all data categories available via Instance metadata</span></span>

<span data-ttu-id="6c6e5-183">Data</span><span class="sxs-lookup"><span data-stu-id="6c6e5-183">Data</span></span> | <span data-ttu-id="6c6e5-184">Description</span><span class="sxs-lookup"><span data-stu-id="6c6e5-184">Description</span></span>
-----|------------
<span data-ttu-id="6c6e5-185">location</span><span class="sxs-lookup"><span data-stu-id="6c6e5-185">location</span></span> | <span data-ttu-id="6c6e5-186">Azure Region the VM is running</span><span class="sxs-lookup"><span data-stu-id="6c6e5-186">Azure Region the VM is running</span></span> 
<span data-ttu-id="6c6e5-187">name</span><span class="sxs-lookup"><span data-stu-id="6c6e5-187">name</span></span> | <span data-ttu-id="6c6e5-188">Name of the VM</span><span class="sxs-lookup"><span data-stu-id="6c6e5-188">Name of the VM</span></span> 
<span data-ttu-id="6c6e5-189">offer</span><span class="sxs-lookup"><span data-stu-id="6c6e5-189">offer</span></span> | <span data-ttu-id="6c6e5-190">Offer information for the VM image, these values are present only for images deployed from Azure image gallery</span><span class="sxs-lookup"><span data-stu-id="6c6e5-190">Offer information for the VM image, these values are present only for images deployed from Azure image gallery</span></span> 
<span data-ttu-id="6c6e5-191">publisher</span><span class="sxs-lookup"><span data-stu-id="6c6e5-191">publisher</span></span> | <span data-ttu-id="6c6e5-192">Publisher of the VM image</span><span class="sxs-lookup"><span data-stu-id="6c6e5-192">Publisher of the VM image</span></span>
<span data-ttu-id="6c6e5-193">sku</span><span class="sxs-lookup"><span data-stu-id="6c6e5-193">sku</span></span> | <span data-ttu-id="6c6e5-194">Specific SKU for the VM image</span><span class="sxs-lookup"><span data-stu-id="6c6e5-194">Specific SKU for the VM image</span></span>  
<span data-ttu-id="6c6e5-195">version</span><span class="sxs-lookup"><span data-stu-id="6c6e5-195">version</span></span> | <span data-ttu-id="6c6e5-196">Version of the VM Image</span><span class="sxs-lookup"><span data-stu-id="6c6e5-196">Version of the VM Image</span></span> 
<span data-ttu-id="6c6e5-197">osType</span><span class="sxs-lookup"><span data-stu-id="6c6e5-197">osType</span></span> | <span data-ttu-id="6c6e5-198">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="6c6e5-198">Linux or Windows</span></span> 
<span data-ttu-id="6c6e5-199">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="6c6e5-199">platformUpdateDomain</span></span> |  <span data-ttu-id="6c6e5-200">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-200">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in.</span></span> 
<span data-ttu-id="6c6e5-201">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="6c6e5-201">platformFaultDomain</span></span> | <span data-ttu-id="6c6e5-202">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-202">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in.</span></span>
<span data-ttu-id="6c6e5-203">vmId</span><span class="sxs-lookup"><span data-stu-id="6c6e5-203">vmId</span></span> | <span data-ttu-id="6c6e5-204">Unique identifier for the VM, more info [here](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)</span><span class="sxs-lookup"><span data-stu-id="6c6e5-204">Unique identifier for the VM, more info [here](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)</span></span>
<span data-ttu-id="6c6e5-205">vmSize</span><span class="sxs-lookup"><span data-stu-id="6c6e5-205">vmSize</span></span> | [<span data-ttu-id="6c6e5-206">VM size</span><span class="sxs-lookup"><span data-stu-id="6c6e5-206">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="6c6e5-207">ipv4/ipaddress</span><span class="sxs-lookup"><span data-stu-id="6c6e5-207">ipv4/ipaddress</span></span> | <span data-ttu-id="6c6e5-208">Local IP address of the VM</span><span class="sxs-lookup"><span data-stu-id="6c6e5-208">Local IP address of the VM</span></span> 
<span data-ttu-id="6c6e5-209">ipv4/publicip</span><span class="sxs-lookup"><span data-stu-id="6c6e5-209">ipv4/publicip</span></span> | <span data-ttu-id="6c6e5-210">Public IP address for the Instance</span><span class="sxs-lookup"><span data-stu-id="6c6e5-210">Public IP address for the Instance</span></span> 
<span data-ttu-id="6c6e5-211">subnet/address</span><span class="sxs-lookup"><span data-stu-id="6c6e5-211">subnet/address</span></span> | <span data-ttu-id="6c6e5-212">Address for subnet</span><span class="sxs-lookup"><span data-stu-id="6c6e5-212">Address for subnet</span></span> 
<span data-ttu-id="6c6e5-213">subnet/dnsservers/ipaddress1</span><span class="sxs-lookup"><span data-stu-id="6c6e5-213">subnet/dnsservers/ipaddress1</span></span> | <span data-ttu-id="6c6e5-214">Primary DNS server</span><span class="sxs-lookup"><span data-stu-id="6c6e5-214">Primary DNS server</span></span>
<span data-ttu-id="6c6e5-215">subnet/dnsservers/ipaddress2</span><span class="sxs-lookup"><span data-stu-id="6c6e5-215">subnet/dnsservers/ipaddress2</span></span> | <span data-ttu-id="6c6e5-216">Secondary DNS server</span><span class="sxs-lookup"><span data-stu-id="6c6e5-216">Secondary DNS server</span></span>
<span data-ttu-id="6c6e5-217">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="6c6e5-217">subnet/prefix</span></span> | <span data-ttu-id="6c6e5-218">Subnet prefix, example 24</span><span class="sxs-lookup"><span data-stu-id="6c6e5-218">Subnet prefix, example 24</span></span>
<span data-ttu-id="6c6e5-219">ipv6/ipaddress</span><span class="sxs-lookup"><span data-stu-id="6c6e5-219">ipv6/ipaddress</span></span> | <span data-ttu-id="6c6e5-220">IPv6 address for the VM</span><span class="sxs-lookup"><span data-stu-id="6c6e5-220">IPv6 address for the VM</span></span>
<span data-ttu-id="6c6e5-221">mac</span><span class="sxs-lookup"><span data-stu-id="6c6e5-221">mac</span></span> | <span data-ttu-id="6c6e5-222">VM mac address</span><span class="sxs-lookup"><span data-stu-id="6c6e5-222">VM mac address</span></span> 
<span data-ttu-id="6c6e5-223">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="6c6e5-223">scheduledevents</span></span> | <span data-ttu-id="6c6e5-224">see [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="6c6e5-224">see [scheduledevents](virtual-machines-scheduled-events.md)</span></span>



## <a name="example-scenarios-for-usage"></a><span data-ttu-id="6c6e5-225">Example Scenarios for usage</span><span class="sxs-lookup"><span data-stu-id="6c6e5-225">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="6c6e5-226">Tracking VM running on Azure</span><span class="sxs-lookup"><span data-stu-id="6c6e5-226">Tracking VM running on Azure</span></span> 

<span data-ttu-id="6c6e5-227">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-227">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="6c6e5-228">To be able to get a unique ID for a VM use vmId field from Instance metadata service</span><span class="sxs-lookup"><span data-stu-id="6c6e5-228">To be able to get a unique ID for a VM use vmId field from Instance metadata service</span></span> 

<span data-ttu-id="6c6e5-229">**Request**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-229">**Request**</span></span>
```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-03-01&format=text"
```
<span data-ttu-id="6c6e5-230">**Response**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-230">**Response**</span></span>
```
5c08b38e-4d57-4c23-ac45-aca61037f084

```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="6c6e5-231">Placement of containers, data-partitions based Fault/Update domain</span><span class="sxs-lookup"><span data-stu-id="6c6e5-231">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="6c6e5-232">For certain scenarios where placement of different replicas is of prime important.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-232">For certain scenarios where placement of different replicas is of prime important.</span></span> <span data-ttu-id="6c6e5-233">For example [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps), or for container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) you require to know the platformFaultDomain and platformUpdateDomain the VM is running on.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-233">For example [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps), or for container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) you require to know the platformFaultDomain and platformUpdateDomain the VM is running on.</span></span> <span data-ttu-id="6c6e5-234">You can query this data point directly via instance metadata</span><span class="sxs-lookup"><span data-stu-id="6c6e5-234">You can query this data point directly via instance metadata</span></span>

<span data-ttu-id="6c6e5-235">**Request**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-235">**Request**</span></span>
```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-03-01&format=text" 
```
<span data-ttu-id="6c6e5-236">**Response**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-236">**Response**</span></span>
```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="6c6e5-237">Getting more information about the VM during support case</span><span class="sxs-lookup"><span data-stu-id="6c6e5-237">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="6c6e5-238">As a service provider you may get a support call where you would like to know more information about the VM.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-238">As a service provider you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="6c6e5-239">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-239">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="6c6e5-240">**Request**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-240">**Request**</span></span>
```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-03-01"
```
<span data-ttu-id="6c6e5-241">**Response**</span><span class="sxs-lookup"><span data-stu-id="6c6e5-241">**Response**</span></span>
> [!NOTE] 
> <span data-ttu-id="6c6e5-242">The response is a json string.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-242">The response is a json string.</span></span> <span data-ttu-id="6c6e5-243">Following output is formatted json with utility like [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="6c6e5-243">Following output is formatted json with utility like [jq](https://stedolan.github.io/jq/).</span></span>
>

```
{
"compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }

}
```

## <a name="faq"></a><span data-ttu-id="6c6e5-244">FAQ</span><span class="sxs-lookup"><span data-stu-id="6c6e5-244">FAQ</span></span>
1. <span data-ttu-id="6c6e5-245">I am getting error 400 Bad request, Required metadata header not specified.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-245">I am getting error 400 Bad request, Required metadata header not specified.</span></span> <span data-ttu-id="6c6e5-246">What does this mean?</span><span class="sxs-lookup"><span data-stu-id="6c6e5-246">What does this mean?</span></span>
   * <span data-ttu-id="6c6e5-247">Instance metadata service requires header Metadata:true to be passed in the request.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-247">Instance metadata service requires header Metadata:true to be passed in the request.</span></span> <span data-ttu-id="6c6e5-248">Passing header in the REST call allows access to Instance metadata service.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-248">Passing header in the REST call allows access to Instance metadata service.</span></span> 
2. <span data-ttu-id="6c6e5-249">Why am I not getting compute information for my VM?</span><span class="sxs-lookup"><span data-stu-id="6c6e5-249">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="6c6e5-250">Currently Instance metadata service supports Azure Resource Manager created instances only, in future we may add support for Cloud Services VMs.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-250">Currently Instance metadata service supports Azure Resource Manager created instances only, in future we may add support for Cloud Services VMs.</span></span> 
3. <span data-ttu-id="6c6e5-251">I created my Virtual Machine through Azure Resource Manager a while back.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-251">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="6c6e5-252">Why am I not see compute metadata information?</span><span class="sxs-lookup"><span data-stu-id="6c6e5-252">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="6c6e5-253">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-253">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="6c6e5-254">For older VM (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-254">For older VM (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="6c6e5-255">Why am I getting error 500 - Internal server error?</span><span class="sxs-lookup"><span data-stu-id="6c6e5-255">Why am I getting error 500 - Internal server error?</span></span>
   * <span data-ttu-id="6c6e5-256">Currently Instance metadata Preview is available only in West US Central Region.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-256">Currently Instance metadata Preview is available only in West US Central Region.</span></span> <span data-ttu-id="6c6e5-257">Deploy your VMs in the supported regions.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-257">Deploy your VMs in the supported regions.</span></span>  
4. <span data-ttu-id="6c6e5-258">Where do I share Additional questions/comments?</span><span class="sxs-lookup"><span data-stu-id="6c6e5-258">Where do I share Additional questions/comments?</span></span>
   * <span data-ttu-id="6c6e5-259">Send your comments on feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6c6e5-259">Send your comments on feedback.azure.com.</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="6c6e5-260">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6c6e5-260">Next Steps</span></span>

<span data-ttu-id="6c6e5-261">Learn more about [scheduledevents] (virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="6c6e5-261">Learn more about [scheduledevents] (virtual-machines-scheduled-events.md)</span></span>
