---
title: Network Resource Provider Overview | Microsoft Docs
description: Learn about the new Network Resource Provider in Azure Resource Manager
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 9e2d6cabe281099a0c9a425e7722317e2273ebd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562787"
---
# <a name="network-resource-provider"></a><span data-ttu-id="c35fc-103">Network Resource Provider</span><span class="sxs-lookup"><span data-stu-id="c35fc-103">Network Resource Provider</span></span>
<span data-ttu-id="c35fc-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span><span class="sxs-lookup"><span data-stu-id="c35fc-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="c35fc-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span><span class="sxs-lookup"><span data-stu-id="c35fc-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="c35fc-106">Such resources are managed through various resource providers under Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c35fc-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="c35fc-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span><span class="sxs-lookup"><span data-stu-id="c35fc-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="c35fc-108">There are three main resource providers: Network, Storage and Compute.</span><span class="sxs-lookup"><span data-stu-id="c35fc-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="c35fc-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span><span class="sxs-lookup"><span data-stu-id="c35fc-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="c35fc-110">**Metadata** – you can add information to resources using tags.</span><span class="sxs-lookup"><span data-stu-id="c35fc-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="c35fc-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c35fc-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="c35fc-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span><span class="sxs-lookup"><span data-stu-id="c35fc-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="c35fc-113">This means you have more flexibility in managing the networking resources.</span><span class="sxs-lookup"><span data-stu-id="c35fc-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="c35fc-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span><span class="sxs-lookup"><span data-stu-id="c35fc-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="c35fc-115">This has drastically reduced configuration time.</span><span class="sxs-lookup"><span data-stu-id="c35fc-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="c35fc-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span><span class="sxs-lookup"><span data-stu-id="c35fc-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="c35fc-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="c35fc-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="c35fc-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span><span class="sxs-lookup"><span data-stu-id="c35fc-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="c35fc-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span><span class="sxs-lookup"><span data-stu-id="c35fc-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="c35fc-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span><span class="sxs-lookup"><span data-stu-id="c35fc-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="c35fc-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span><span class="sxs-lookup"><span data-stu-id="c35fc-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="c35fc-122">REST based API</span><span class="sxs-lookup"><span data-stu-id="c35fc-122">REST based API</span></span>
  * <span data-ttu-id="c35fc-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c35fc-123">PowerShell</span></span>
  * <span data-ttu-id="c35fc-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="c35fc-124">.NET SDK</span></span>
  * <span data-ttu-id="c35fc-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="c35fc-125">Node.JS SDK</span></span>
  * <span data-ttu-id="c35fc-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="c35fc-126">Java SDK</span></span>
  * <span data-ttu-id="c35fc-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c35fc-127">Azure CLI</span></span>
  * <span data-ttu-id="c35fc-128">Preview Portal</span><span class="sxs-lookup"><span data-stu-id="c35fc-128">Preview Portal</span></span>
  * <span data-ttu-id="c35fc-129">Resource Manager template language</span><span class="sxs-lookup"><span data-stu-id="c35fc-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="c35fc-130">Network resources</span><span class="sxs-lookup"><span data-stu-id="c35fc-130">Network resources</span></span>
<span data-ttu-id="c35fc-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span><span class="sxs-lookup"><span data-stu-id="c35fc-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="c35fc-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span><span class="sxs-lookup"><span data-stu-id="c35fc-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="c35fc-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span><span class="sxs-lookup"><span data-stu-id="c35fc-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="c35fc-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span><span class="sxs-lookup"><span data-stu-id="c35fc-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Network resource model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/resource-groups-networking/Figure2.png)

<span data-ttu-id="c35fc-136">Every resource contains a common set of properties, and their individual property set.</span><span class="sxs-lookup"><span data-stu-id="c35fc-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="c35fc-137">The common properties are:</span><span class="sxs-lookup"><span data-stu-id="c35fc-137">The common properties are:</span></span>

| <span data-ttu-id="c35fc-138">Property</span><span class="sxs-lookup"><span data-stu-id="c35fc-138">Property</span></span> | <span data-ttu-id="c35fc-139">Description</span><span class="sxs-lookup"><span data-stu-id="c35fc-139">Description</span></span> | <span data-ttu-id="c35fc-140">Sample values</span><span class="sxs-lookup"><span data-stu-id="c35fc-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c35fc-141">**name**</span><span class="sxs-lookup"><span data-stu-id="c35fc-141">**name**</span></span> |<span data-ttu-id="c35fc-142">Unique resource name.</span><span class="sxs-lookup"><span data-stu-id="c35fc-142">Unique resource name.</span></span> <span data-ttu-id="c35fc-143">Each resource type has its own naming restrictions.</span><span class="sxs-lookup"><span data-stu-id="c35fc-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="c35fc-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="c35fc-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="c35fc-145">**location**</span><span class="sxs-lookup"><span data-stu-id="c35fc-145">**location**</span></span> |<span data-ttu-id="c35fc-146">Azure region in which the resource resides</span><span class="sxs-lookup"><span data-stu-id="c35fc-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="c35fc-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="c35fc-147">westus, eastus</span></span> |
| <span data-ttu-id="c35fc-148">**id**</span><span class="sxs-lookup"><span data-stu-id="c35fc-148">**id**</span></span> |<span data-ttu-id="c35fc-149">Unique URI based identification</span><span class="sxs-lookup"><span data-stu-id="c35fc-149">Unique URI based identification</span></span> |<span data-ttu-id="c35fc-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="c35fc-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="c35fc-151">You can check the individual properties of resources in the sections below.</span><span class="sxs-lookup"><span data-stu-id="c35fc-151">You can check the individual properties of resources in the sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="c35fc-152">Management interfaces</span><span class="sxs-lookup"><span data-stu-id="c35fc-152">Management interfaces</span></span>
<span data-ttu-id="c35fc-153">You can manage your Azure networking resources using different interfaces.</span><span class="sxs-lookup"><span data-stu-id="c35fc-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="c35fc-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span><span class="sxs-lookup"><span data-stu-id="c35fc-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="c35fc-155">REST API</span><span class="sxs-lookup"><span data-stu-id="c35fc-155">REST API</span></span>
<span data-ttu-id="c35fc-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span><span class="sxs-lookup"><span data-stu-id="c35fc-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="c35fc-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span><span class="sxs-lookup"><span data-stu-id="c35fc-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="c35fc-158">The general URI structure of the API is presented below:</span><span class="sxs-lookup"><span data-stu-id="c35fc-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="c35fc-159">And the parameters in braces represent the following elements:</span><span class="sxs-lookup"><span data-stu-id="c35fc-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="c35fc-160">**subscription-id** - your Azure subscription id.</span><span class="sxs-lookup"><span data-stu-id="c35fc-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="c35fc-161">**resource-provider-namespace** - namespace for the provider being used.</span><span class="sxs-lookup"><span data-stu-id="c35fc-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="c35fc-162">THe value for the network resource provider is *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="c35fc-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="c35fc-163">**region-name** - the Azure region name</span><span class="sxs-lookup"><span data-stu-id="c35fc-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="c35fc-164">The following HTTP methods are supported when making calls to the REST API:</span><span class="sxs-lookup"><span data-stu-id="c35fc-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="c35fc-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span><span class="sxs-lookup"><span data-stu-id="c35fc-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="c35fc-166">**GET** - used to retrieve information for a provisioned resource.</span><span class="sxs-lookup"><span data-stu-id="c35fc-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="c35fc-167">**DELETE** - used to delete an existing resource.</span><span class="sxs-lookup"><span data-stu-id="c35fc-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="c35fc-168">Both the request and response conform to a JSON payload format.</span><span class="sxs-lookup"><span data-stu-id="c35fc-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="c35fc-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="c35fc-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="c35fc-170">Resource Manager template language</span><span class="sxs-lookup"><span data-stu-id="c35fc-170">Resource Manager template language</span></span>
<span data-ttu-id="c35fc-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span><span class="sxs-lookup"><span data-stu-id="c35fc-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="c35fc-172">A sample representation of a template is provided below –</span><span class="sxs-lookup"><span data-stu-id="c35fc-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="c35fc-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span><span class="sxs-lookup"><span data-stu-id="c35fc-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="c35fc-174">The example below can be used to create a virtual network with 2 subnets.</span><span class="sxs-lookup"><span data-stu-id="c35fc-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="c35fc-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span><span class="sxs-lookup"><span data-stu-id="c35fc-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="c35fc-176">The example below shows a possible set of parameter values to be used with the template above:</span><span class="sxs-lookup"><span data-stu-id="c35fc-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="c35fc-177">The main advantages of using templates are:</span><span class="sxs-lookup"><span data-stu-id="c35fc-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="c35fc-178">You can build a complex infrastructure in a resource group in a declarative style.</span><span class="sxs-lookup"><span data-stu-id="c35fc-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="c35fc-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c35fc-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="c35fc-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span><span class="sxs-lookup"><span data-stu-id="c35fc-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="c35fc-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c35fc-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="c35fc-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="c35fc-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="c35fc-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c35fc-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="c35fc-184">The sample template above uses the virtual network and subnet resources.</span><span class="sxs-lookup"><span data-stu-id="c35fc-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="c35fc-185">There are other network resources you can use as listed below:</span><span class="sxs-lookup"><span data-stu-id="c35fc-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="c35fc-186">Using a template</span><span class="sxs-lookup"><span data-stu-id="c35fc-186">Using a template</span></span>
<span data-ttu-id="c35fc-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span><span class="sxs-lookup"><span data-stu-id="c35fc-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="c35fc-188">To deploy services from a template in GitHub, execute the following steps:</span><span class="sxs-lookup"><span data-stu-id="c35fc-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="c35fc-189">Open the template3 file from GitHub.</span><span class="sxs-lookup"><span data-stu-id="c35fc-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="c35fc-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="c35fc-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="c35fc-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span><span class="sxs-lookup"><span data-stu-id="c35fc-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="c35fc-192">Verify the template, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c35fc-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="c35fc-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span><span class="sxs-lookup"><span data-stu-id="c35fc-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="c35fc-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c35fc-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="c35fc-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span><span class="sxs-lookup"><span data-stu-id="c35fc-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="c35fc-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span><span class="sxs-lookup"><span data-stu-id="c35fc-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="c35fc-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c35fc-197">Click **Create**.</span></span> <span data-ttu-id="c35fc-198">Notice the tile displaying **Provisioning Template deployment**.</span><span class="sxs-lookup"><span data-stu-id="c35fc-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="c35fc-199">Once the deployment is done, you will see a screen similar to one below.</span><span class="sxs-lookup"><span data-stu-id="c35fc-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![Sample template deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="c35fc-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="c35fc-201">Next steps</span></span>
[<span data-ttu-id="c35fc-202">Azure Resource Manager Template Language</span><span class="sxs-lookup"><span data-stu-id="c35fc-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="c35fc-203">Azure Networking – commonly used templates</span><span class="sxs-lookup"><span data-stu-id="c35fc-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="c35fc-204">Azure Resource Manager vs. classic deployment</span><span class="sxs-lookup"><span data-stu-id="c35fc-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="c35fc-205">Azure Resource Manager Overview</span><span class="sxs-lookup"><span data-stu-id="c35fc-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)



