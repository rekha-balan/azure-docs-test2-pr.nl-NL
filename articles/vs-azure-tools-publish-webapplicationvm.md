---
title: Publish-WebApplicationVM | Microsoft Docs
description: Learn how to deploy a web application to a virtual machine. This script creates the required resources in your Azure subscription if they don't exist.
services: visual-studio-online
author: ghogen
manager: douge
assetId: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: c2dc6057eeb4eba1306309785e13192674bc43c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804250"
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="1148f-104">Publish-WebApplicationVM (Windows PowerShell script)</span><span class="sxs-lookup"><span data-stu-id="1148f-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="1148f-105">Deploys a web application to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1148f-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="1148f-106">The script creates the required resources in your Azure subscription if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="1148f-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

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

### <a name="configuration"></a><span data-ttu-id="1148f-107">Configuration</span><span class="sxs-lookup"><span data-stu-id="1148f-107">Configuration</span></span>
<span data-ttu-id="1148f-108">The path to the JSON configuration file that describes the details of the deployment.</span><span class="sxs-lookup"><span data-stu-id="1148f-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="1148f-109">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-109">Aliases</span></span> | <span data-ttu-id="1148f-110">none</span><span class="sxs-lookup"><span data-stu-id="1148f-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-111">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-111">Required?</span></span> |<span data-ttu-id="1148f-112">true</span><span class="sxs-lookup"><span data-stu-id="1148f-112">true</span></span> |
| <span data-ttu-id="1148f-113">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-113">Position</span></span> |<span data-ttu-id="1148f-114">named</span><span class="sxs-lookup"><span data-stu-id="1148f-114">named</span></span> |
| <span data-ttu-id="1148f-115">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-115">Default value</span></span> |<span data-ttu-id="1148f-116">none</span><span class="sxs-lookup"><span data-stu-id="1148f-116">none</span></span> |
| <span data-ttu-id="1148f-117">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-117">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-118">false</span><span class="sxs-lookup"><span data-stu-id="1148f-118">false</span></span> |
| <span data-ttu-id="1148f-119">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-119">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-120">false</span><span class="sxs-lookup"><span data-stu-id="1148f-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="1148f-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="1148f-121">SubscriptionName</span></span>
<span data-ttu-id="1148f-122">The name of the Azure subscription in which you want to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1148f-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="1148f-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-123">Aliases</span></span> | <span data-ttu-id="1148f-124">none</span><span class="sxs-lookup"><span data-stu-id="1148f-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-125">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-125">Required?</span></span> |<span data-ttu-id="1148f-126">false</span><span class="sxs-lookup"><span data-stu-id="1148f-126">false</span></span> |
| <span data-ttu-id="1148f-127">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-127">Position</span></span> |<span data-ttu-id="1148f-128">named</span><span class="sxs-lookup"><span data-stu-id="1148f-128">named</span></span> |
| <span data-ttu-id="1148f-129">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-129">Default value</span></span> |<span data-ttu-id="1148f-130">Uses the first subscription in the subscription file</span><span class="sxs-lookup"><span data-stu-id="1148f-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="1148f-131">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-131">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-132">false</span><span class="sxs-lookup"><span data-stu-id="1148f-132">false</span></span> |
| <span data-ttu-id="1148f-133">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-133">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-134">false</span><span class="sxs-lookup"><span data-stu-id="1148f-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="1148f-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="1148f-135">WebDeployPackage</span></span>
<span data-ttu-id="1148f-136">The path to the web deployment package to publish to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1148f-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="1148f-137">You can create this package by using the Publish Web wizard in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1148f-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="1148f-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="1148f-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="1148f-139">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-139">Aliases</span></span> | <span data-ttu-id="1148f-140">none</span><span class="sxs-lookup"><span data-stu-id="1148f-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-141">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-141">Required?</span></span> |<span data-ttu-id="1148f-142">false</span><span class="sxs-lookup"><span data-stu-id="1148f-142">false</span></span> |
| <span data-ttu-id="1148f-143">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-143">Position</span></span> |<span data-ttu-id="1148f-144">named</span><span class="sxs-lookup"><span data-stu-id="1148f-144">named</span></span> |
| <span data-ttu-id="1148f-145">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-145">Default value</span></span> |<span data-ttu-id="1148f-146">none</span><span class="sxs-lookup"><span data-stu-id="1148f-146">none</span></span> |
| <span data-ttu-id="1148f-147">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-147">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-148">false</span><span class="sxs-lookup"><span data-stu-id="1148f-148">false</span></span> |
| <span data-ttu-id="1148f-149">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-149">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-150">false</span><span class="sxs-lookup"><span data-stu-id="1148f-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="1148f-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="1148f-151">AllowUntrusted</span></span>
<span data-ttu-id="1148f-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span><span class="sxs-lookup"><span data-stu-id="1148f-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="1148f-153">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-153">Aliases</span></span> | <span data-ttu-id="1148f-154">none</span><span class="sxs-lookup"><span data-stu-id="1148f-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-155">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-155">Required?</span></span> |<span data-ttu-id="1148f-156">false</span><span class="sxs-lookup"><span data-stu-id="1148f-156">false</span></span> |
| <span data-ttu-id="1148f-157">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-157">Position</span></span> |<span data-ttu-id="1148f-158">named</span><span class="sxs-lookup"><span data-stu-id="1148f-158">named</span></span> |
| <span data-ttu-id="1148f-159">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-159">Default value</span></span> |<span data-ttu-id="1148f-160">false</span><span class="sxs-lookup"><span data-stu-id="1148f-160">false</span></span> |
| <span data-ttu-id="1148f-161">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-161">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-162">false</span><span class="sxs-lookup"><span data-stu-id="1148f-162">false</span></span> |
| <span data-ttu-id="1148f-163">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-163">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-164">false</span><span class="sxs-lookup"><span data-stu-id="1148f-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="1148f-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="1148f-165">VMPassword</span></span>
<span data-ttu-id="1148f-166">The credentials for the virtual machine account.</span><span class="sxs-lookup"><span data-stu-id="1148f-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="1148f-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="1148f-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="1148f-168">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-168">Aliases</span></span> | <span data-ttu-id="1148f-169">none</span><span class="sxs-lookup"><span data-stu-id="1148f-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-170">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-170">Required?</span></span> |<span data-ttu-id="1148f-171">false</span><span class="sxs-lookup"><span data-stu-id="1148f-171">false</span></span> |
| <span data-ttu-id="1148f-172">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-172">Position</span></span> |<span data-ttu-id="1148f-173">named</span><span class="sxs-lookup"><span data-stu-id="1148f-173">named</span></span> |
| <span data-ttu-id="1148f-174">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-174">Default value</span></span> |<span data-ttu-id="1148f-175">none</span><span class="sxs-lookup"><span data-stu-id="1148f-175">none</span></span> |
| <span data-ttu-id="1148f-176">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-176">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-177">false</span><span class="sxs-lookup"><span data-stu-id="1148f-177">false</span></span> |
| <span data-ttu-id="1148f-178">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-178">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-179">false</span><span class="sxs-lookup"><span data-stu-id="1148f-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="1148f-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="1148f-180">DatabaseServerPassword</span></span>
<span data-ttu-id="1148f-181">The credentials for the SQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="1148f-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="1148f-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="1148f-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="1148f-183">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-183">Aliases</span></span> | <span data-ttu-id="1148f-184">none</span><span class="sxs-lookup"><span data-stu-id="1148f-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-185">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-185">Required?</span></span> |<span data-ttu-id="1148f-186">false</span><span class="sxs-lookup"><span data-stu-id="1148f-186">false</span></span> |
| <span data-ttu-id="1148f-187">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-187">Position</span></span> |<span data-ttu-id="1148f-188">named</span><span class="sxs-lookup"><span data-stu-id="1148f-188">named</span></span> |
| <span data-ttu-id="1148f-189">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-189">Default value</span></span> |<span data-ttu-id="1148f-190">none</span><span class="sxs-lookup"><span data-stu-id="1148f-190">none</span></span> |
| <span data-ttu-id="1148f-191">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-191">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-192">false</span><span class="sxs-lookup"><span data-stu-id="1148f-192">false</span></span> |
| <span data-ttu-id="1148f-193">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-193">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-194">false</span><span class="sxs-lookup"><span data-stu-id="1148f-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="1148f-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="1148f-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="1148f-196">If true, print messages from the script to the output stream.</span><span class="sxs-lookup"><span data-stu-id="1148f-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="1148f-197">Aliases</span><span class="sxs-lookup"><span data-stu-id="1148f-197">Aliases</span></span> | <span data-ttu-id="1148f-198">none</span><span class="sxs-lookup"><span data-stu-id="1148f-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="1148f-199">Required?</span><span class="sxs-lookup"><span data-stu-id="1148f-199">Required?</span></span> |<span data-ttu-id="1148f-200">false</span><span class="sxs-lookup"><span data-stu-id="1148f-200">false</span></span> |
| <span data-ttu-id="1148f-201">Position</span><span class="sxs-lookup"><span data-stu-id="1148f-201">Position</span></span> |<span data-ttu-id="1148f-202">named</span><span class="sxs-lookup"><span data-stu-id="1148f-202">named</span></span> |
| <span data-ttu-id="1148f-203">Default value</span><span class="sxs-lookup"><span data-stu-id="1148f-203">Default value</span></span> |<span data-ttu-id="1148f-204">false</span><span class="sxs-lookup"><span data-stu-id="1148f-204">false</span></span> |
| <span data-ttu-id="1148f-205">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="1148f-205">Accept pipeline input?</span></span> |<span data-ttu-id="1148f-206">false</span><span class="sxs-lookup"><span data-stu-id="1148f-206">false</span></span> |
| <span data-ttu-id="1148f-207">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="1148f-207">Accept wildcard characters?</span></span> |<span data-ttu-id="1148f-208">false</span><span class="sxs-lookup"><span data-stu-id="1148f-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="1148f-209">Remarks</span><span class="sxs-lookup"><span data-stu-id="1148f-209">Remarks</span></span>
<span data-ttu-id="1148f-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="1148f-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="1148f-211">The JSON configuration file specifies the details of what is to be deployed.</span><span class="sxs-lookup"><span data-stu-id="1148f-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="1148f-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1148f-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="1148f-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span><span class="sxs-lookup"><span data-stu-id="1148f-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="1148f-214">The following code shows an example JSON configuration file:</span><span class="sxs-lookup"><span data-stu-id="1148f-214">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="1148f-215">You can edit the JSON configuration file to change what is provisioned.</span><span class="sxs-lookup"><span data-stu-id="1148f-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="1148f-216">A virtual machine and a cloud service are required, but the database section is optional.</span><span class="sxs-lookup"><span data-stu-id="1148f-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

