---
title: Publish-WebApplicationWebSite (Windows PowerShell script) | Microsoft Docs
description: Learn how to publish a web project to an Azure website. This script creates the required resources in your Azure subscription if they don't exist.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: tarcher
ms.openlocfilehash: ed1a5bdd0a7fb84579b248fdbb3b295c9d904ee5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549611"
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="a1d06-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span><span class="sxs-lookup"><span data-stu-id="a1d06-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="a1d06-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="a1d06-105">Syntax</span></span>
<span data-ttu-id="a1d06-106">Publishes a web project to an Azure website.</span><span class="sxs-lookup"><span data-stu-id="a1d06-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="a1d06-107">The script creates the required resources in your Azure subscription if they don't exist.</span><span class="sxs-lookup"><span data-stu-id="a1d06-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="a1d06-108">Configuration</span><span class="sxs-lookup"><span data-stu-id="a1d06-108">Configuration</span></span>
<span data-ttu-id="a1d06-109">The path to the JSON configuration file that describes the details of the deployment.</span><span class="sxs-lookup"><span data-stu-id="a1d06-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="a1d06-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="a1d06-110">Parameter</span></span> | <span data-ttu-id="a1d06-111">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1d06-112">Aliases</span><span class="sxs-lookup"><span data-stu-id="a1d06-112">Aliases</span></span> |<span data-ttu-id="a1d06-113">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-113">none</span></span> |
| <span data-ttu-id="a1d06-114">Required?</span><span class="sxs-lookup"><span data-stu-id="a1d06-114">Required?</span></span> |<span data-ttu-id="a1d06-115">true</span><span class="sxs-lookup"><span data-stu-id="a1d06-115">true</span></span> |
| <span data-ttu-id="a1d06-116">Position</span><span class="sxs-lookup"><span data-stu-id="a1d06-116">Position</span></span> |<span data-ttu-id="a1d06-117">named</span><span class="sxs-lookup"><span data-stu-id="a1d06-117">named</span></span> |
| <span data-ttu-id="a1d06-118">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-118">Default value</span></span> |<span data-ttu-id="a1d06-119">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-119">none</span></span> |
| <span data-ttu-id="a1d06-120">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="a1d06-120">Accept pipeline input?</span></span> |<span data-ttu-id="a1d06-121">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-121">false</span></span> |
| <span data-ttu-id="a1d06-122">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="a1d06-122">Accept wildcard characters?</span></span> |<span data-ttu-id="a1d06-123">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="a1d06-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="a1d06-124">SubscriptionName</span></span>
<span data-ttu-id="a1d06-125">The name of the Azure subscription that you want to create the website in.</span><span class="sxs-lookup"><span data-stu-id="a1d06-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="a1d06-126">Parameter</span><span class="sxs-lookup"><span data-stu-id="a1d06-126">Parameter</span></span> | <span data-ttu-id="a1d06-127">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1d06-128">Aliases</span><span class="sxs-lookup"><span data-stu-id="a1d06-128">Aliases</span></span> |<span data-ttu-id="a1d06-129">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-129">none</span></span> |
| <span data-ttu-id="a1d06-130">Required?</span><span class="sxs-lookup"><span data-stu-id="a1d06-130">Required?</span></span> |<span data-ttu-id="a1d06-131">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-131">false</span></span> |
| <span data-ttu-id="a1d06-132">Position</span><span class="sxs-lookup"><span data-stu-id="a1d06-132">Position</span></span> |<span data-ttu-id="a1d06-133">named</span><span class="sxs-lookup"><span data-stu-id="a1d06-133">named</span></span> |
| <span data-ttu-id="a1d06-134">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-134">Default value</span></span> |<span data-ttu-id="a1d06-135">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-135">none</span></span> |
| <span data-ttu-id="a1d06-136">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="a1d06-136">Accept pipeline input?</span></span> |<span data-ttu-id="a1d06-137">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-137">false</span></span> |
| <span data-ttu-id="a1d06-138">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="a1d06-138">Accept wildcard characters?</span></span> |<span data-ttu-id="a1d06-139">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="a1d06-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="a1d06-140">WebDeployPackage</span></span>
<span data-ttu-id="a1d06-141">The path to the web deployment package to publish to the website.</span><span class="sxs-lookup"><span data-stu-id="a1d06-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="a1d06-142">You can create this package by using the Publish Web wizard in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1d06-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="a1d06-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="a1d06-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="a1d06-144">Parameter</span><span class="sxs-lookup"><span data-stu-id="a1d06-144">Parameter</span></span> | <span data-ttu-id="a1d06-145">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1d06-146">Aliases</span><span class="sxs-lookup"><span data-stu-id="a1d06-146">Aliases</span></span> |<span data-ttu-id="a1d06-147">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-147">none</span></span> |
| <span data-ttu-id="a1d06-148">Required?</span><span class="sxs-lookup"><span data-stu-id="a1d06-148">Required?</span></span> |<span data-ttu-id="a1d06-149">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-149">false</span></span> |
| <span data-ttu-id="a1d06-150">Position</span><span class="sxs-lookup"><span data-stu-id="a1d06-150">Position</span></span> |<span data-ttu-id="a1d06-151">named</span><span class="sxs-lookup"><span data-stu-id="a1d06-151">named</span></span> |
| <span data-ttu-id="a1d06-152">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-152">Default value</span></span> |<span data-ttu-id="a1d06-153">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-153">none</span></span> |
| <span data-ttu-id="a1d06-154">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="a1d06-154">Accept pipeline input?</span></span> |<span data-ttu-id="a1d06-155">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-155">false</span></span> |
| <span data-ttu-id="a1d06-156">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="a1d06-156">Accept wildcard characters?</span></span> |<span data-ttu-id="a1d06-157">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="a1d06-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="a1d06-158">DatabaseServerPassword</span></span>
<span data-ttu-id="a1d06-159">The username and password for the SQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="a1d06-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="a1d06-160">Parameter</span><span class="sxs-lookup"><span data-stu-id="a1d06-160">Parameter</span></span> | <span data-ttu-id="a1d06-161">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1d06-162">Aliases</span><span class="sxs-lookup"><span data-stu-id="a1d06-162">Aliases</span></span> |<span data-ttu-id="a1d06-163">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-163">none</span></span> |
| <span data-ttu-id="a1d06-164">Required?</span><span class="sxs-lookup"><span data-stu-id="a1d06-164">Required?</span></span> |<span data-ttu-id="a1d06-165">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-165">false</span></span> |
| <span data-ttu-id="a1d06-166">Position</span><span class="sxs-lookup"><span data-stu-id="a1d06-166">Position</span></span> |<span data-ttu-id="a1d06-167">named</span><span class="sxs-lookup"><span data-stu-id="a1d06-167">named</span></span> |
| <span data-ttu-id="a1d06-168">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-168">Default value</span></span> |<span data-ttu-id="a1d06-169">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-169">none</span></span> |
| <span data-ttu-id="a1d06-170">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="a1d06-170">Accept pipeline input?</span></span> |<span data-ttu-id="a1d06-171">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-171">false</span></span> |
| <span data-ttu-id="a1d06-172">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="a1d06-172">Accept wildcard characters?</span></span> |<span data-ttu-id="a1d06-173">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="a1d06-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="a1d06-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="a1d06-175">If true, print messages from the script to the output stream.</span><span class="sxs-lookup"><span data-stu-id="a1d06-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="a1d06-176">Parameter</span><span class="sxs-lookup"><span data-stu-id="a1d06-176">Parameter</span></span> | <span data-ttu-id="a1d06-177">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1d06-178">Aliases</span><span class="sxs-lookup"><span data-stu-id="a1d06-178">Aliases</span></span> |<span data-ttu-id="a1d06-179">none</span><span class="sxs-lookup"><span data-stu-id="a1d06-179">none</span></span> |
| <span data-ttu-id="a1d06-180">Required?</span><span class="sxs-lookup"><span data-stu-id="a1d06-180">Required?</span></span> |<span data-ttu-id="a1d06-181">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-181">false</span></span> |
| <span data-ttu-id="a1d06-182">Position</span><span class="sxs-lookup"><span data-stu-id="a1d06-182">Position</span></span> |<span data-ttu-id="a1d06-183">named</span><span class="sxs-lookup"><span data-stu-id="a1d06-183">named</span></span> |
| <span data-ttu-id="a1d06-184">Default value</span><span class="sxs-lookup"><span data-stu-id="a1d06-184">Default value</span></span> |<span data-ttu-id="a1d06-185">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-185">false</span></span> |
| <span data-ttu-id="a1d06-186">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="a1d06-186">Accept pipeline input?</span></span> |<span data-ttu-id="a1d06-187">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-187">false</span></span> |
| <span data-ttu-id="a1d06-188">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="a1d06-188">Accept wildcard characters?</span></span> |<span data-ttu-id="a1d06-189">false</span><span class="sxs-lookup"><span data-stu-id="a1d06-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="a1d06-190">Remarks</span><span class="sxs-lookup"><span data-stu-id="a1d06-190">Remarks</span></span>
<span data-ttu-id="a1d06-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="a1d06-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="a1d06-192">The JSON configuration file specifies the details of what is to be deployed.</span><span class="sxs-lookup"><span data-stu-id="a1d06-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="a1d06-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span><span class="sxs-lookup"><span data-stu-id="a1d06-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="a1d06-194">It also includes the database to provision, if any.</span><span class="sxs-lookup"><span data-stu-id="a1d06-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="a1d06-195">The following code shows an example JSON configuration file:</span><span class="sxs-lookup"><span data-stu-id="a1d06-195">The following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="a1d06-196">You can edit the JSON configuration file to change what is deployed.</span><span class="sxs-lookup"><span data-stu-id="a1d06-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="a1d06-197">A webSite section is required, but the database section is optional.</span><span class="sxs-lookup"><span data-stu-id="a1d06-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d06-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1d06-198">Next steps</span></span>
<span data-ttu-id="a1d06-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="a1d06-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

