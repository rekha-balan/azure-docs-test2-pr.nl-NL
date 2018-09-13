---
title: Publish-WebApplicationVM | Microsoft Docs
description: Learn how to deploy a web application to a virtual machine. This script creates the required resources in your Azure subscription if they don't exist.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: tarcher
ms.openlocfilehash: 1a44130f37e0167f8ab4c842b11d1a630eec0287
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660582"
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="db1d9-104">Publish-WebApplicationVM (Windows PowerShell script)</span><span class="sxs-lookup"><span data-stu-id="db1d9-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="db1d9-105">Deploys a web application to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="db1d9-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="db1d9-106">The script creates the required resources in your Azure subscription if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="db1d9-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="db1d9-107">Configuration</span><span class="sxs-lookup"><span data-stu-id="db1d9-107">Configuration</span></span>
<span data-ttu-id="db1d9-108">The path to the JSON configuration file that describes the details of the deployment.</span><span class="sxs-lookup"><span data-stu-id="db1d9-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="db1d9-109">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-109">Aliases</span></span> | <span data-ttu-id="db1d9-110">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-111">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-111">Required?</span></span> |<span data-ttu-id="db1d9-112">true</span><span class="sxs-lookup"><span data-stu-id="db1d9-112">true</span></span> |
| <span data-ttu-id="db1d9-113">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-113">Position</span></span> |<span data-ttu-id="db1d9-114">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-114">named</span></span> |
| <span data-ttu-id="db1d9-115">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-115">Default value</span></span> |<span data-ttu-id="db1d9-116">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-116">none</span></span> |
| <span data-ttu-id="db1d9-117">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-117">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-118">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-118">false</span></span> |
| <span data-ttu-id="db1d9-119">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-119">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-120">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="db1d9-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="db1d9-121">SubscriptionName</span></span>
<span data-ttu-id="db1d9-122">The name of the Azure subscription in which you want to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="db1d9-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="db1d9-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-123">Aliases</span></span> | <span data-ttu-id="db1d9-124">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-125">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-125">Required?</span></span> |<span data-ttu-id="db1d9-126">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-126">false</span></span> |
| <span data-ttu-id="db1d9-127">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-127">Position</span></span> |<span data-ttu-id="db1d9-128">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-128">named</span></span> |
| <span data-ttu-id="db1d9-129">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-129">Default value</span></span> |<span data-ttu-id="db1d9-130">Uses the first subscription in the subscription file</span><span class="sxs-lookup"><span data-stu-id="db1d9-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="db1d9-131">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-131">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-132">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-132">false</span></span> |
| <span data-ttu-id="db1d9-133">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-133">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-134">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="db1d9-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="db1d9-135">WebDeployPackage</span></span>
<span data-ttu-id="db1d9-136">The path to the web deployment package to publish to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="db1d9-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="db1d9-137">You can create this package by using the Publish Web wizard in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db1d9-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="db1d9-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="db1d9-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="db1d9-139">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-139">Aliases</span></span> | <span data-ttu-id="db1d9-140">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-141">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-141">Required?</span></span> |<span data-ttu-id="db1d9-142">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-142">false</span></span> |
| <span data-ttu-id="db1d9-143">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-143">Position</span></span> |<span data-ttu-id="db1d9-144">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-144">named</span></span> |
| <span data-ttu-id="db1d9-145">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-145">Default value</span></span> |<span data-ttu-id="db1d9-146">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-146">none</span></span> |
| <span data-ttu-id="db1d9-147">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-147">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-148">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-148">false</span></span> |
| <span data-ttu-id="db1d9-149">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-149">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-150">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="db1d9-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="db1d9-151">AllowUntrusted</span></span>
<span data-ttu-id="db1d9-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span><span class="sxs-lookup"><span data-stu-id="db1d9-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="db1d9-153">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-153">Aliases</span></span> | <span data-ttu-id="db1d9-154">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-155">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-155">Required?</span></span> |<span data-ttu-id="db1d9-156">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-156">false</span></span> |
| <span data-ttu-id="db1d9-157">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-157">Position</span></span> |<span data-ttu-id="db1d9-158">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-158">named</span></span> |
| <span data-ttu-id="db1d9-159">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-159">Default value</span></span> |<span data-ttu-id="db1d9-160">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-160">false</span></span> |
| <span data-ttu-id="db1d9-161">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-161">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-162">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-162">false</span></span> |
| <span data-ttu-id="db1d9-163">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-163">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-164">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="db1d9-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="db1d9-165">VMPassword</span></span>
<span data-ttu-id="db1d9-166">The credentials for the virtual machine account.</span><span class="sxs-lookup"><span data-stu-id="db1d9-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="db1d9-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="db1d9-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="db1d9-168">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-168">Aliases</span></span> | <span data-ttu-id="db1d9-169">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-170">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-170">Required?</span></span> |<span data-ttu-id="db1d9-171">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-171">false</span></span> |
| <span data-ttu-id="db1d9-172">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-172">Position</span></span> |<span data-ttu-id="db1d9-173">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-173">named</span></span> |
| <span data-ttu-id="db1d9-174">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-174">Default value</span></span> |<span data-ttu-id="db1d9-175">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-175">none</span></span> |
| <span data-ttu-id="db1d9-176">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-176">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-177">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-177">false</span></span> |
| <span data-ttu-id="db1d9-178">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-178">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-179">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="db1d9-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="db1d9-180">DatabaseServerPassword</span></span>
<span data-ttu-id="db1d9-181">The credentials for the SQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="db1d9-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="db1d9-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="db1d9-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="db1d9-183">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-183">Aliases</span></span> | <span data-ttu-id="db1d9-184">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-185">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-185">Required?</span></span> |<span data-ttu-id="db1d9-186">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-186">false</span></span> |
| <span data-ttu-id="db1d9-187">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-187">Position</span></span> |<span data-ttu-id="db1d9-188">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-188">named</span></span> |
| <span data-ttu-id="db1d9-189">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-189">Default value</span></span> |<span data-ttu-id="db1d9-190">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-190">none</span></span> |
| <span data-ttu-id="db1d9-191">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-191">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-192">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-192">false</span></span> |
| <span data-ttu-id="db1d9-193">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-193">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-194">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="db1d9-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="db1d9-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="db1d9-196">If true, print messages from the script to the output stream.</span><span class="sxs-lookup"><span data-stu-id="db1d9-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="db1d9-197">Aliases</span><span class="sxs-lookup"><span data-stu-id="db1d9-197">Aliases</span></span> | <span data-ttu-id="db1d9-198">none</span><span class="sxs-lookup"><span data-stu-id="db1d9-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="db1d9-199">Required?</span><span class="sxs-lookup"><span data-stu-id="db1d9-199">Required?</span></span> |<span data-ttu-id="db1d9-200">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-200">false</span></span> |
| <span data-ttu-id="db1d9-201">Position</span><span class="sxs-lookup"><span data-stu-id="db1d9-201">Position</span></span> |<span data-ttu-id="db1d9-202">named</span><span class="sxs-lookup"><span data-stu-id="db1d9-202">named</span></span> |
| <span data-ttu-id="db1d9-203">Default value</span><span class="sxs-lookup"><span data-stu-id="db1d9-203">Default value</span></span> |<span data-ttu-id="db1d9-204">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-204">false</span></span> |
| <span data-ttu-id="db1d9-205">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="db1d9-205">Accept pipeline input?</span></span> |<span data-ttu-id="db1d9-206">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-206">false</span></span> |
| <span data-ttu-id="db1d9-207">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="db1d9-207">Accept wildcard characters?</span></span> |<span data-ttu-id="db1d9-208">false</span><span class="sxs-lookup"><span data-stu-id="db1d9-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="db1d9-209">Remarks</span><span class="sxs-lookup"><span data-stu-id="db1d9-209">Remarks</span></span>
<span data-ttu-id="db1d9-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="db1d9-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="db1d9-211">The JSON configuration file specifies the details of what is to be deployed.</span><span class="sxs-lookup"><span data-stu-id="db1d9-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="db1d9-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="db1d9-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="db1d9-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span><span class="sxs-lookup"><span data-stu-id="db1d9-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="db1d9-214">The following code shows an example JSON configuration file:</span><span class="sxs-lookup"><span data-stu-id="db1d9-214">The following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="db1d9-215">You can edit the JSON configuration file to change what is provisioned.</span><span class="sxs-lookup"><span data-stu-id="db1d9-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="db1d9-216">A virtual machine and a cloud service are required, but the database section is optional.</span><span class="sxs-lookup"><span data-stu-id="db1d9-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

