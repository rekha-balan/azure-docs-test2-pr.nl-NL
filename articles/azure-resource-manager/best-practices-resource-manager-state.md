---
title: Pass complex values between Azure templates | Microsoft Docs
description: Shows recommended approaches for using complex objects to share state data with Azure Resource Manager templates and linked templates.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660742"
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="282b4-103">Share state to and from Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="282b4-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="282b4-104">This topic shows best practices for managing and sharing state within templates.</span><span class="sxs-lookup"><span data-stu-id="282b4-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="282b4-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span><span class="sxs-lookup"><span data-stu-id="282b4-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="282b4-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span><span class="sxs-lookup"><span data-stu-id="282b4-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="282b4-107">This topic is part of a larger whitepaper.</span><span class="sxs-lookup"><span data-stu-id="282b4-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="282b4-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="282b4-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="282b4-109">Provide standard configuration settings</span><span class="sxs-lookup"><span data-stu-id="282b4-109">Provide standard configuration settings</span></span>
<span data-ttu-id="282b4-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span><span class="sxs-lookup"><span data-stu-id="282b4-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="282b4-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span><span class="sxs-lookup"><span data-stu-id="282b4-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="282b4-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="282b4-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="282b4-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span><span class="sxs-lookup"><span data-stu-id="282b4-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="282b4-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span><span class="sxs-lookup"><span data-stu-id="282b4-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="282b4-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span><span class="sxs-lookup"><span data-stu-id="282b4-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="282b4-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span><span class="sxs-lookup"><span data-stu-id="282b4-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="282b4-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span><span class="sxs-lookup"><span data-stu-id="282b4-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="282b4-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span><span class="sxs-lookup"><span data-stu-id="282b4-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="282b4-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span><span class="sxs-lookup"><span data-stu-id="282b4-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="282b4-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="282b4-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="282b4-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span><span class="sxs-lookup"><span data-stu-id="282b4-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="282b4-122">You can then reference these variables later in the template.</span><span class="sxs-lookup"><span data-stu-id="282b4-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="282b4-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span><span class="sxs-lookup"><span data-stu-id="282b4-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="282b4-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span><span class="sxs-lookup"><span data-stu-id="282b4-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="282b4-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="282b4-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="282b4-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="282b4-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="282b4-127">Pass state to a template</span><span class="sxs-lookup"><span data-stu-id="282b4-127">Pass state to a template</span></span>
<span data-ttu-id="282b4-128">You share state into a template through parameters that you provide directly during deployment.</span><span class="sxs-lookup"><span data-stu-id="282b4-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="282b4-129">The following table lists commonly used parameters in templates.</span><span class="sxs-lookup"><span data-stu-id="282b4-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="282b4-130">Name</span><span class="sxs-lookup"><span data-stu-id="282b4-130">Name</span></span> | <span data-ttu-id="282b4-131">Value</span><span class="sxs-lookup"><span data-stu-id="282b4-131">Value</span></span> | <span data-ttu-id="282b4-132">Description</span><span class="sxs-lookup"><span data-stu-id="282b4-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="282b4-133">location</span><span class="sxs-lookup"><span data-stu-id="282b4-133">location</span></span> |<span data-ttu-id="282b4-134">String from a constrained list of Azure regions</span><span class="sxs-lookup"><span data-stu-id="282b4-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="282b4-135">The location where the resources are deployed.</span><span class="sxs-lookup"><span data-stu-id="282b4-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="282b4-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="282b4-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="282b4-137">String</span><span class="sxs-lookup"><span data-stu-id="282b4-137">String</span></span> |<span data-ttu-id="282b4-138">Unique DNS name for the Storage Account where the VM's disks are placed</span><span class="sxs-lookup"><span data-stu-id="282b4-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="282b4-139">domainName</span><span class="sxs-lookup"><span data-stu-id="282b4-139">domainName</span></span> |<span data-ttu-id="282b4-140">String</span><span class="sxs-lookup"><span data-stu-id="282b4-140">String</span></span> |<span data-ttu-id="282b4-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="282b4-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="282b4-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="282b4-142">adminUsername</span></span> |<span data-ttu-id="282b4-143">String</span><span class="sxs-lookup"><span data-stu-id="282b4-143">String</span></span> |<span data-ttu-id="282b4-144">Username for the VMs</span><span class="sxs-lookup"><span data-stu-id="282b4-144">Username for the VMs</span></span> |
| <span data-ttu-id="282b4-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="282b4-145">adminPassword</span></span> |<span data-ttu-id="282b4-146">String</span><span class="sxs-lookup"><span data-stu-id="282b4-146">String</span></span> |<span data-ttu-id="282b4-147">Password for the VMs</span><span class="sxs-lookup"><span data-stu-id="282b4-147">Password for the VMs</span></span> |
| <span data-ttu-id="282b4-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="282b4-148">tshirtSize</span></span> |<span data-ttu-id="282b4-149">String from a constrained list of offered t-shirt sizes</span><span class="sxs-lookup"><span data-stu-id="282b4-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="282b4-150">The named scale unit size to provision.</span><span class="sxs-lookup"><span data-stu-id="282b4-150">The named scale unit size to provision.</span></span> <span data-ttu-id="282b4-151">For example, "Small", "Medium", "Large"</span><span class="sxs-lookup"><span data-stu-id="282b4-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="282b4-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="282b4-152">virtualNetworkName</span></span> |<span data-ttu-id="282b4-153">String</span><span class="sxs-lookup"><span data-stu-id="282b4-153">String</span></span> |<span data-ttu-id="282b4-154">Name of the virtual network that the consumer wants to use.</span><span class="sxs-lookup"><span data-stu-id="282b4-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="282b4-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="282b4-155">enableJumpbox</span></span> |<span data-ttu-id="282b4-156">String from a constrained list (enabled/disabled)</span><span class="sxs-lookup"><span data-stu-id="282b4-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="282b4-157">Parameter that identifies whether to enable a jumpbox for the environment.</span><span class="sxs-lookup"><span data-stu-id="282b4-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="282b4-158">Values: "enabled", "disabled"</span><span class="sxs-lookup"><span data-stu-id="282b4-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="282b4-159">The **tshirtSize** parameter used in the previous section is defined as:</span><span class="sxs-lookup"><span data-stu-id="282b4-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="282b4-160">Pass state to linked templates</span><span class="sxs-lookup"><span data-stu-id="282b4-160">Pass state to linked templates</span></span>
<span data-ttu-id="282b4-161">When connecting to linked templates, you often use a mix of static and generated variables.</span><span class="sxs-lookup"><span data-stu-id="282b4-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="282b4-162">Static variables</span><span class="sxs-lookup"><span data-stu-id="282b4-162">Static variables</span></span>
<span data-ttu-id="282b4-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span><span class="sxs-lookup"><span data-stu-id="282b4-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="282b4-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span><span class="sxs-lookup"><span data-stu-id="282b4-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="282b4-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span><span class="sxs-lookup"><span data-stu-id="282b4-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="282b4-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span><span class="sxs-lookup"><span data-stu-id="282b4-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="282b4-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span><span class="sxs-lookup"><span data-stu-id="282b4-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="282b4-168">Generated variables</span><span class="sxs-lookup"><span data-stu-id="282b4-168">Generated variables</span></span>
<span data-ttu-id="282b4-169">In addition to static variables, several variables are generated dynamically.</span><span class="sxs-lookup"><span data-stu-id="282b4-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="282b4-170">This section identifies some of the common types of generated variables.</span><span class="sxs-lookup"><span data-stu-id="282b4-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="282b4-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="282b4-171">tshirtSize</span></span>
<span data-ttu-id="282b4-172">You are familiar with this generated variable from the examples above.</span><span class="sxs-lookup"><span data-stu-id="282b4-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="282b4-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="282b4-173">networkSettings</span></span>
<span data-ttu-id="282b4-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span><span class="sxs-lookup"><span data-stu-id="282b4-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="282b4-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span><span class="sxs-lookup"><span data-stu-id="282b4-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="282b4-176">An example of communicating network settings can be seen below.</span><span class="sxs-lookup"><span data-stu-id="282b4-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="282b4-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="282b4-177">availabilitySettings</span></span>
<span data-ttu-id="282b4-178">Resources created in linked templates are often placed in an availability set.</span><span class="sxs-lookup"><span data-stu-id="282b4-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="282b4-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span><span class="sxs-lookup"><span data-stu-id="282b4-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="282b4-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span><span class="sxs-lookup"><span data-stu-id="282b4-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="282b4-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="282b4-181">storageSettings</span></span>
<span data-ttu-id="282b4-182">Storage details are often shared with linked templates.</span><span class="sxs-lookup"><span data-stu-id="282b4-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="282b4-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span><span class="sxs-lookup"><span data-stu-id="282b4-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="282b4-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="282b4-184">osSettings</span></span>
<span data-ttu-id="282b4-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span><span class="sxs-lookup"><span data-stu-id="282b4-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="282b4-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span><span class="sxs-lookup"><span data-stu-id="282b4-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="282b4-187">The following example shows an object for *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="282b4-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="282b4-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="282b4-188">machineSettings</span></span>
<span data-ttu-id="282b4-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span><span class="sxs-lookup"><span data-stu-id="282b4-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="282b4-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span><span class="sxs-lookup"><span data-stu-id="282b4-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="282b4-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span><span class="sxs-lookup"><span data-stu-id="282b4-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="282b4-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span><span class="sxs-lookup"><span data-stu-id="282b4-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="282b4-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="282b4-193">vmScripts</span></span>
<span data-ttu-id="282b4-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span><span class="sxs-lookup"><span data-stu-id="282b4-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="282b4-195">Outside references include the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="282b4-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="282b4-196">Inside references include the installed software installed and configuration.</span><span class="sxs-lookup"><span data-stu-id="282b4-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="282b4-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span><span class="sxs-lookup"><span data-stu-id="282b4-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="282b4-198">This object also contains references to command-line arguments for different types of actions.</span><span class="sxs-lookup"><span data-stu-id="282b4-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="282b4-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span><span class="sxs-lookup"><span data-stu-id="282b4-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="282b4-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span><span class="sxs-lookup"><span data-stu-id="282b4-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="282b4-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span><span class="sxs-lookup"><span data-stu-id="282b4-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="282b4-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span><span class="sxs-lookup"><span data-stu-id="282b4-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="282b4-203">Return state from a template</span><span class="sxs-lookup"><span data-stu-id="282b4-203">Return state from a template</span></span>
<span data-ttu-id="282b4-204">Not only can you pass data into a template, you can also share data back to the calling template.</span><span class="sxs-lookup"><span data-stu-id="282b4-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="282b4-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span><span class="sxs-lookup"><span data-stu-id="282b4-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="282b4-206">The following example shows how to pass the private IP address generated in a linked template.</span><span class="sxs-lookup"><span data-stu-id="282b4-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="282b4-207">Within the main template, you can use that data with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="282b4-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="282b4-208">You can use this expression in either the outputs section or the resources section of the main template.</span><span class="sxs-lookup"><span data-stu-id="282b4-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="282b4-209">You cannot use the expression in the variables section because it relies on the runtime state.</span><span class="sxs-lookup"><span data-stu-id="282b4-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="282b4-210">To return this value from the main template, use:</span><span class="sxs-lookup"><span data-stu-id="282b4-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="282b4-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="282b4-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="282b4-212">Define authentication settings for virtual machine</span><span class="sxs-lookup"><span data-stu-id="282b4-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="282b4-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="282b4-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="282b4-214">You create a parameter for passing in the type of authentication.</span><span class="sxs-lookup"><span data-stu-id="282b4-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="282b4-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span><span class="sxs-lookup"><span data-stu-id="282b4-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="282b4-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span><span class="sxs-lookup"><span data-stu-id="282b4-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="282b4-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="282b4-217">Next steps</span></span>
* <span data-ttu-id="282b4-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="282b4-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="282b4-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="282b4-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
