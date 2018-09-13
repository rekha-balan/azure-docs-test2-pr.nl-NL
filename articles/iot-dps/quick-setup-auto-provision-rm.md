---
title: Set up Device Provisioning using an Azure Resource Manager template | Microsoft Docs
description: Azure Quickstart - Set up the Azure IoT Hub Device Provisioning Service using a template
author: wesmc7777
ms.author: wesmc
ms.date: 06/18/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: e3aa2cf93e529fcc430162ac90be06a75690fb21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867953"
---
# <a name="set-up-the-iot-hub-device-provisioning-service-with-an-azure-resource-manager-template"></a><span data-ttu-id="46f26-103">Set up the IoT Hub Device Provisioning Service with an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="46f26-103">Set up the IoT Hub Device Provisioning Service with an Azure Resource Manager template</span></span>

<span data-ttu-id="46f26-104">You can use [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) to programmatically set up the Azure cloud resources necessary for provisioning your devices.</span><span class="sxs-lookup"><span data-stu-id="46f26-104">You can use [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) to programmatically set up the Azure cloud resources necessary for provisioning your devices.</span></span> <span data-ttu-id="46f26-105">These steps show how to create an IoT hub, a new IoT Hub Device Provisioning Service, and link the two services together using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="46f26-105">These steps show how to create an IoT hub, a new IoT Hub Device Provisioning Service, and link the two services together using an Azure Resource Manager template.</span></span> <span data-ttu-id="46f26-106">This Quickstart uses [Azure CLI 2.0](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) to perform the programmatic steps necessary to create a resource group and deploy the template, but you can easily use the [Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-portal), [PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy), .NET, ruby, or other programming languages to perform these steps and deploy your template.</span><span class="sxs-lookup"><span data-stu-id="46f26-106">This Quickstart uses [Azure CLI 2.0](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) to perform the programmatic steps necessary to create a resource group and deploy the template, but you can easily use the [Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-portal), [PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy), .NET, ruby, or other programming languages to perform these steps and deploy your template.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="46f26-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="46f26-107">Prerequisites</span></span>

- <span data-ttu-id="46f26-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="46f26-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
- <span data-ttu-id="46f26-109">This Quickstart requires that you run the Azure CLI locally.</span><span class="sxs-lookup"><span data-stu-id="46f26-109">This Quickstart requires that you run the Azure CLI locally.</span></span> <span data-ttu-id="46f26-110">You must have the Azure CLI version 2.0 or later installed.</span><span class="sxs-lookup"><span data-stu-id="46f26-110">You must have the Azure CLI version 2.0 or later installed.</span></span> <span data-ttu-id="46f26-111">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="46f26-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="46f26-112">If you need to install or upgrade the CLI, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46f26-112">If you need to install or upgrade the CLI, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>


## <a name="sign-in-to-azure-and-create-a-resource-group"></a><span data-ttu-id="46f26-113">Sign in to Azure and create a resource group</span><span class="sxs-lookup"><span data-stu-id="46f26-113">Sign in to Azure and create a resource group</span></span>

<span data-ttu-id="46f26-114">Sign in to your Azure account and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="46f26-114">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="46f26-115">At the command prompt, run the [login command][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="46f26-115">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="46f26-116">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span><span class="sxs-lookup"><span data-stu-id="46f26-116">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="46f26-117">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="46f26-117">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="46f26-118">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span><span class="sxs-lookup"><span data-stu-id="46f26-118">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="46f26-119">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="46f26-119">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="46f26-120">You can use either the subscription name or ID from the output of the previous command:</span><span class="sxs-lookup"><span data-stu-id="46f26-120">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

3. <span data-ttu-id="46f26-121">When you create Azure cloud resources like IoT hubs and provisioning services, you create them in a resource group.</span><span class="sxs-lookup"><span data-stu-id="46f26-121">When you create Azure cloud resources like IoT hubs and provisioning services, you create them in a resource group.</span></span> <span data-ttu-id="46f26-122">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="46f26-122">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="46f26-123">The previous example creates the resource group in the West US location.</span><span class="sxs-lookup"><span data-stu-id="46f26-123">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="46f26-124">You can view a list of available locations by running the command `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="46f26-124">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

## <a name="create-a-resource-manager-template"></a><span data-ttu-id="46f26-125">Create a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="46f26-125">Create a Resource Manager template</span></span>

<span data-ttu-id="46f26-126">Use a JSON template to create a provisioning service and a linked IoT hub in your resource group.</span><span class="sxs-lookup"><span data-stu-id="46f26-126">Use a JSON template to create a provisioning service and a linked IoT hub in your resource group.</span></span> <span data-ttu-id="46f26-127">You can also use an Azure Resource Manager template to make changes to an existing provisioning service or IoT hub.</span><span class="sxs-lookup"><span data-stu-id="46f26-127">You can also use an Azure Resource Manager template to make changes to an existing provisioning service or IoT hub.</span></span>

1. <span data-ttu-id="46f26-128">Use a text editor to create an Azure Resource Manager template called **template.json** with the following skeleton content.</span><span class="sxs-lookup"><span data-stu-id="46f26-128">Use a text editor to create an Azure Resource Manager template called **template.json** with the following skeleton content.</span></span> 

   ```json
   {
       "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0.0.0",
       "parameters": {},
       "variables": {},
       "resources": []
   }
   ```

2. <span data-ttu-id="46f26-129">Replace the **parameters** section with the following content.</span><span class="sxs-lookup"><span data-stu-id="46f26-129">Replace the **parameters** section with the following content.</span></span> <span data-ttu-id="46f26-130">The parameters section specifies parameters that can be passed in from another file.</span><span class="sxs-lookup"><span data-stu-id="46f26-130">The parameters section specifies parameters that can be passed in from another file.</span></span> <span data-ttu-id="46f26-131">This section specifies the name of the IoT hub and provisioning service to create.</span><span class="sxs-lookup"><span data-stu-id="46f26-131">This section specifies the name of the IoT hub and provisioning service to create.</span></span> <span data-ttu-id="46f26-132">It also specifies the location for both the IoT hub and provisioning service.</span><span class="sxs-lookup"><span data-stu-id="46f26-132">It also specifies the location for both the IoT hub and provisioning service.</span></span> <span data-ttu-id="46f26-133">The values are restricted to Azure regions that support IoT hubs and provisioning services.</span><span class="sxs-lookup"><span data-stu-id="46f26-133">The values are restricted to Azure regions that support IoT hubs and provisioning services.</span></span> <span data-ttu-id="46f26-134">For a list of supported locations for Device Provisioning Service, you can run the following command `az provider show --namespace Microsoft.Devices --query "resourceTypes[?resourceType=='ProvisioningServices'].locations | [0]" --out table` or go to the [Azure Status](https://azure.microsoft.com/status/) page and search on "Device Provisioning Service".</span><span class="sxs-lookup"><span data-stu-id="46f26-134">For a list of supported locations for Device Provisioning Service, you can run the following command `az provider show --namespace Microsoft.Devices --query "resourceTypes[?resourceType=='ProvisioningServices'].locations | [0]" --out table` or go to the [Azure Status](https://azure.microsoft.com/status/) page and search on "Device Provisioning Service".</span></span>

   ```json
    "parameters": {
        "iotHubName": {
            "type": "string"
        },
        "provisioningServiceName": {
            "type": "string"
        },
        "hubLocation": {
            "type": "string",
            "allowedValues": [
                "eastus",
                "westus",
                "westeurope",
                "northeurope",
                "southeastasia",
                "eastasia"
            ]
        }
    },

   ```

3. <span data-ttu-id="46f26-135">Replace the **variables** section with the following content.</span><span class="sxs-lookup"><span data-stu-id="46f26-135">Replace the **variables** section with the following content.</span></span> <span data-ttu-id="46f26-136">This section defines values that are used later to construct the IoT hub connection string, which is needed to link the provisioning service and the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="46f26-136">This section defines values that are used later to construct the IoT hub connection string, which is needed to link the provisioning service and the IoT hub.</span></span> 
 
   ```json
    "variables": {        
        "iotHubResourceId": "[resourceId('Microsoft.Devices/Iothubs', parameters('iotHubName'))]",
        "iotHubKeyName": "iothubowner",
        "iotHubKeyResource": "[resourceId('Microsoft.Devices/Iothubs/Iothubkeys', parameters('iotHubName'), variables('iotHubKeyName'))]"
    },

   ```

4. <span data-ttu-id="46f26-137">To create an IoT hub, add the following lines to the **resources** collection.</span><span class="sxs-lookup"><span data-stu-id="46f26-137">To create an IoT hub, add the following lines to the **resources** collection.</span></span> <span data-ttu-id="46f26-138">The JSON specifies the minimum properties required to create an IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="46f26-138">The JSON specifies the minimum properties required to create an IoT Hub.</span></span> <span data-ttu-id="46f26-139">The **name** and **location** properties are passed as parameters.</span><span class="sxs-lookup"><span data-stu-id="46f26-139">The **name** and **location** properties are passed as parameters.</span></span> <span data-ttu-id="46f26-140">To learn more about the properties you can specify for an IoT Hub in a template, see [Microsoft.Devices/IotHubs template reference](https://docs.microsoft.com/azure/templates/microsoft.devices/iothubs).</span><span class="sxs-lookup"><span data-stu-id="46f26-140">To learn more about the properties you can specify for an IoT Hub in a template, see [Microsoft.Devices/IotHubs template reference](https://docs.microsoft.com/azure/templates/microsoft.devices/iothubs).</span></span>

   ```json
        {
            "apiVersion": "2017-07-01",
            "type": "Microsoft.Devices/IotHubs",
            "name": "[parameters('iotHubName')]",
            "location": "[parameters('hubLocation')]",
            "sku": {
                "name": "S1",
                "capacity": 1
            },
            "tags": {
            },
            "properties": {
            }            
        },

   ``` 

5. <span data-ttu-id="46f26-141">To create the provisioning service, add the following lines after the IoT hub specification in the **resources** collection.</span><span class="sxs-lookup"><span data-stu-id="46f26-141">To create the provisioning service, add the following lines after the IoT hub specification in the **resources** collection.</span></span> <span data-ttu-id="46f26-142">The **name** and **location** of the provisioning service are passed in parameters.</span><span class="sxs-lookup"><span data-stu-id="46f26-142">The **name** and **location** of the provisioning service are passed in parameters.</span></span> <span data-ttu-id="46f26-143">Specify the IoT hubs to link to the provisioning service in the **iotHubs** collection.</span><span class="sxs-lookup"><span data-stu-id="46f26-143">Specify the IoT hubs to link to the provisioning service in the **iotHubs** collection.</span></span> <span data-ttu-id="46f26-144">At a minimum, you must specify the **connectionString** and **location** properties for each linked IoT hub.</span><span class="sxs-lookup"><span data-stu-id="46f26-144">At a minimum, you must specify the **connectionString** and **location** properties for each linked IoT hub.</span></span> <span data-ttu-id="46f26-145">You can also set properties like **allocationWeight** and **applyAllocationPolicy** on each IoT hub, as well as properties like **allocationPolicy** and **authorizationPolicies** on the provisioning service itself.</span><span class="sxs-lookup"><span data-stu-id="46f26-145">You can also set properties like **allocationWeight** and **applyAllocationPolicy** on each IoT hub, as well as properties like **allocationPolicy** and **authorizationPolicies** on the provisioning service itself.</span></span> <span data-ttu-id="46f26-146">To learn more, see [Microsoft.Devices/provisioningServices template reference](https://docs.microsoft.com/azure/templates/microsoft.devices/provisioningservices).</span><span class="sxs-lookup"><span data-stu-id="46f26-146">To learn more, see [Microsoft.Devices/provisioningServices template reference](https://docs.microsoft.com/azure/templates/microsoft.devices/provisioningservices).</span></span>

   <span data-ttu-id="46f26-147">The **dependsOn** property is used to ensure that Resource Manager creates the IoT hub before it creates the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="46f26-147">The **dependsOn** property is used to ensure that Resource Manager creates the IoT hub before it creates the provisioning service.</span></span> <span data-ttu-id="46f26-148">The template requires the connection string of the IoT hub to specify its linkage to the provisioning service, so the hub and its keys must be created first.</span><span class="sxs-lookup"><span data-stu-id="46f26-148">The template requires the connection string of the IoT hub to specify its linkage to the provisioning service, so the hub and its keys must be created first.</span></span> <span data-ttu-id="46f26-149">The template uses functions like **concat** and **listKeys** to create the connection string.</span><span class="sxs-lookup"><span data-stu-id="46f26-149">The template uses functions like **concat** and **listKeys** to create the connection string.</span></span> <span data-ttu-id="46f26-150">To learn more, see [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions).</span><span class="sxs-lookup"><span data-stu-id="46f26-150">To learn more, see [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions).</span></span>

   ```json
        {
            "type": "Microsoft.Devices/provisioningServices",
            "sku": {
                "name": "S1",
                "capacity": 1
            },
            "name": "[parameters('provisioningServiceName')]",
            "apiVersion": "2017-11-15",
            "location": "[parameters('hubLocation')]",
            "tags": {},
            "properties": {
                "iotHubs": [
                    {
                        "connectionString": "[concat('HostName=', reference(variables('iotHubResourceId')).hostName, ';SharedAccessKeyName=', variables('iotHubKeyName'), ';SharedAccessKey=', listkeys(variables('iotHubKeyResource'), '2017-07-01').primaryKey)]",
                        "location": "[parameters('hubLocation')]",
                        "name": "[concat(parameters('iotHubName'),'.azure-devices.net')]"
                    }
                ]
            },
            "dependsOn": ["[parameters('iotHubName')]"]
        }

   ```

6. <span data-ttu-id="46f26-151">Save the template file.</span><span class="sxs-lookup"><span data-stu-id="46f26-151">Save the template file.</span></span> <span data-ttu-id="46f26-152">The finished template should look like the following:</span><span class="sxs-lookup"><span data-stu-id="46f26-152">The finished template should look like the following:</span></span>

   ```json
   {
       "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0.0.0",
       "parameters": {
           "iotHubName": {
               "type": "string"
           },
           "provisioningServiceName": {
               "type": "string"
           },
           "hubLocation": {
               "type": "string",
               "allowedValues": [
                   "eastus",
                   "westus",
                   "westeurope",
                   "northeurope",
                   "southeastasia",
                   "eastasia"
               ]
           }
       },
       "variables": {        
           "iotHubResourceId": "[resourceId('Microsoft.Devices/Iothubs', parameters('iotHubName'))]",
           "iotHubKeyName": "iothubowner",
           "iotHubKeyResource": "[resourceId('Microsoft.Devices/Iothubs/Iothubkeys', parameters('iotHubName'), variables('iotHubKeyName'))]"
       },
       "resources": [
           {
               "apiVersion": "2017-07-01",
               "type": "Microsoft.Devices/IotHubs",
               "name": "[parameters('iotHubName')]",
               "location": "[parameters('hubLocation')]",
               "sku": {
                   "name": "S1",
                   "capacity": 1
               },
               "tags": {
               },
               "properties": {
               }            
           },
           {
               "type": "Microsoft.Devices/provisioningServices",
               "sku": {
                   "name": "S1",
                   "capacity": 1
               },
               "name": "[parameters('provisioningServiceName')]",
               "apiVersion": "2017-11-15",
               "location": "[parameters('hubLocation')]",
               "tags": {},
               "properties": {
                   "iotHubs": [
                       {
                           "connectionString": "[concat('HostName=', reference(variables('iotHubResourceId')).hostName, ';SharedAccessKeyName=', variables('iotHubKeyName'), ';SharedAccessKey=', listkeys(variables('iotHubKeyResource'), '2017-07-01').primaryKey)]",
                           "location": "[parameters('hubLocation')]",
                           "name": "[concat(parameters('iotHubName'),'.azure-devices.net')]"
                       }
                   ]
               },
               "dependsOn": ["[parameters('iotHubName')]"]
           }
       ]
   }
   ```

## <a name="create-a-resource-manager-parameter-file"></a><span data-ttu-id="46f26-153">Create a Resource Manager parameter file</span><span class="sxs-lookup"><span data-stu-id="46f26-153">Create a Resource Manager parameter file</span></span>

<span data-ttu-id="46f26-154">The template that you defined in the last step uses parameters to specify the name of the IoT Hub, the name of the provisioning service, and the location (Azure region) to create them.</span><span class="sxs-lookup"><span data-stu-id="46f26-154">The template that you defined in the last step uses parameters to specify the name of the IoT Hub, the name of the provisioning service, and the location (Azure region) to create them.</span></span> <span data-ttu-id="46f26-155">You pass these parameters in a separate file.</span><span class="sxs-lookup"><span data-stu-id="46f26-155">You pass these parameters in a separate file.</span></span> <span data-ttu-id="46f26-156">Doing so enables you to reuse the same template for multiple deployments.</span><span class="sxs-lookup"><span data-stu-id="46f26-156">Doing so enables you to reuse the same template for multiple deployments.</span></span> <span data-ttu-id="46f26-157">To create the parameter file, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="46f26-157">To create the parameter file, follow these steps:</span></span>

1. <span data-ttu-id="46f26-158">Use a text editor to create an Azure Resource Manager parameter file called **parameters.json** with the following skeleton content:</span><span class="sxs-lookup"><span data-stu-id="46f26-158">Use a text editor to create an Azure Resource Manager parameter file called **parameters.json** with the following skeleton content:</span></span> 

   ```json
   {
       "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
       "contentVersion": "1.0.0.0",
       "parameters": {}
       }
   }
   ```

2. <span data-ttu-id="46f26-159">Add the **iotHubName** value to the parameter section.</span><span class="sxs-lookup"><span data-stu-id="46f26-159">Add the **iotHubName** value to the parameter section.</span></span> <span data-ttu-id="46f26-160">If you change the name, make sure it follows proper naming conventions for an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="46f26-160">If you change the name, make sure it follows proper naming conventions for an IoT hub.</span></span> <span data-ttu-id="46f26-161">It should be 3-50 characters in length and can contain only upper or lower case alphanumeric characters or hyphens ('-').</span><span class="sxs-lookup"><span data-stu-id="46f26-161">It should be 3-50 characters in length and can contain only upper or lower case alphanumeric characters or hyphens ('-').</span></span> 

   ```json
    "parameters": {
        "iotHubName": {
            "value": "my-sample-iot-hub"
        },
    }
   
   ```

3. <span data-ttu-id="46f26-162">Add the **provisioningServiceName** value to the parameter section.</span><span class="sxs-lookup"><span data-stu-id="46f26-162">Add the **provisioningServiceName** value to the parameter section.</span></span> <span data-ttu-id="46f26-163">If you change the name, make sure it follows proper naming conventions for an IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="46f26-163">If you change the name, make sure it follows proper naming conventions for an IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="46f26-164">It should be 3-64 characters in length and can contain only upper or lower case alphanumeric characters or hyphens ('-').</span><span class="sxs-lookup"><span data-stu-id="46f26-164">It should be 3-64 characters in length and can contain only upper or lower case alphanumeric characters or hyphens ('-').</span></span>

   ```json
    "parameters": {
        "iotHubName": {
            "value": "my-sample-iot-hub"
        },
        "provisioningServiceName": {
            "value": "my-sample-provisioning-service"
        },
    }

   ```

4. <span data-ttu-id="46f26-165">Add the **hubLocation** value to the parameter section.</span><span class="sxs-lookup"><span data-stu-id="46f26-165">Add the **hubLocation** value to the parameter section.</span></span> <span data-ttu-id="46f26-166">This value specifies the location for both the IoT hub and provisioning service.</span><span class="sxs-lookup"><span data-stu-id="46f26-166">This value specifies the location for both the IoT hub and provisioning service.</span></span> <span data-ttu-id="46f26-167">The value must correspond to one of the locations specified in the **allowedValues** collection in the parameter definition in the template file.</span><span class="sxs-lookup"><span data-stu-id="46f26-167">The value must correspond to one of the locations specified in the **allowedValues** collection in the parameter definition in the template file.</span></span> <span data-ttu-id="46f26-168">This collection restricts the values to Azure locations that support both IoT hubs and provisioning services.</span><span class="sxs-lookup"><span data-stu-id="46f26-168">This collection restricts the values to Azure locations that support both IoT hubs and provisioning services.</span></span> <span data-ttu-id="46f26-169">For a list of supported locations for Device Provisioning Service, you can run the following command `az provider show --namespace Microsoft.Devices --query "resourceTypes[?resourceType=='ProvisioningServices'].locations | [0]" --out table` or go to the [Azure Status](https://azure.microsoft.com/status/) page and search on "Device Provisioning Service".</span><span class="sxs-lookup"><span data-stu-id="46f26-169">For a list of supported locations for Device Provisioning Service, you can run the following command `az provider show --namespace Microsoft.Devices --query "resourceTypes[?resourceType=='ProvisioningServices'].locations | [0]" --out table` or go to the [Azure Status](https://azure.microsoft.com/status/) page and search on "Device Provisioning Service".</span></span>

   ```json
    "parameters": {
        "iotHubName": {
            "value": "my-sample-iot-hub"
        },
        "provisioningServiceName": {
            "value": "my-sample-provisioning-service"
        },
        "hubLocation": {
            "value": "westus"
        }
    }

   ```

5. <span data-ttu-id="46f26-170">Save the file.</span><span class="sxs-lookup"><span data-stu-id="46f26-170">Save the file.</span></span> 


> [!IMPORTANT]
> <span data-ttu-id="46f26-171">Both the IoT hub and the provisioning service will be publicly discoverable as DNS endpoints, so make sure to avoid any sensitive information when naming them.</span><span class="sxs-lookup"><span data-stu-id="46f26-171">Both the IoT hub and the provisioning service will be publicly discoverable as DNS endpoints, so make sure to avoid any sensitive information when naming them.</span></span>
>

## <a name="deploy-the-template"></a><span data-ttu-id="46f26-172">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="46f26-172">Deploy the template</span></span>

<span data-ttu-id="46f26-173">Use the following Azure CLI commands to deploy your templates and verify the deployment.</span><span class="sxs-lookup"><span data-stu-id="46f26-173">Use the following Azure CLI commands to deploy your templates and verify the deployment.</span></span>

1. <span data-ttu-id="46f26-174">To deploy your template, run the following [command to start a deployment](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create):</span><span class="sxs-lookup"><span data-stu-id="46f26-174">To deploy your template, run the following [command to start a deployment](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create):</span></span>
    
    ```azurecli
     az group deployment create -g {your resource group name} --template-file template.json --parameters @parameters.json
    ```

   <span data-ttu-id="46f26-175">Look for the **provisioningState** property set to "Succeeded" in the output.</span><span class="sxs-lookup"><span data-stu-id="46f26-175">Look for the **provisioningState** property set to "Succeeded" in the output.</span></span> 

   ![Provisioning output](./media/quick-setup-auto-provision-rm/output.png) 


2. <span data-ttu-id="46f26-177">To verify your deployment, run the following [command to list resources](https://docs.microsoft.com/cli/azure/resource?view=azure-cli-latest#az-resource-list) and look for the new provisioning service and IoT hub in the output:</span><span class="sxs-lookup"><span data-stu-id="46f26-177">To verify your deployment, run the following [command to list resources](https://docs.microsoft.com/cli/azure/resource?view=azure-cli-latest#az-resource-list) and look for the new provisioning service and IoT hub in the output:</span></span>

    ```azurecli
     az resource list -g {your resource group name}
    ```


## <a name="clean-up-resources"></a><span data-ttu-id="46f26-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="46f26-178">Clean up resources</span></span>

<span data-ttu-id="46f26-179">Other Quickstarts in this collection build upon this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="46f26-179">Other Quickstarts in this collection build upon this Quickstart.</span></span> <span data-ttu-id="46f26-180">If you plan to continue on to work with subsequent Quickstarts or with the tutorials, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="46f26-180">If you plan to continue on to work with subsequent Quickstarts or with the tutorials, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="46f26-181">If you do not plan to continue, you can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub or a provisioning service, or to delete a resource group and all its resources.</span><span class="sxs-lookup"><span data-stu-id="46f26-181">If you do not plan to continue, you can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub or a provisioning service, or to delete a resource group and all its resources.</span></span>

<span data-ttu-id="46f26-182">To delete the provisioning service, run the following command:</span><span class="sxs-lookup"><span data-stu-id="46f26-182">To delete the provisioning service, run the following command:</span></span>

```azurecli
az iot hub delete --name {your provisioning service name} --resource-group {your resource group name}
```
<span data-ttu-id="46f26-183">To delete an IoT hub, run the following command:</span><span class="sxs-lookup"><span data-stu-id="46f26-183">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="46f26-184">To delete a resource group and all its resources, run the following command:</span><span class="sxs-lookup"><span data-stu-id="46f26-184">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

<span data-ttu-id="46f26-185">You can also delete resource groups and individual resources using the Azure portal, PowerShell, or REST APIs or supported platform SDKs published for Azure Resource Manager or IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="46f26-185">You can also delete resource groups and individual resources using the Azure portal, PowerShell, or REST APIs or supported platform SDKs published for Azure Resource Manager or IoT Hub Device Provisioning Service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46f26-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="46f26-186">Next steps</span></span>

<span data-ttu-id="46f26-187">In this Quickstart, you’ve deployed an IoT hub and a Device Provisioning Service instance, and linked the two resources.</span><span class="sxs-lookup"><span data-stu-id="46f26-187">In this Quickstart, you’ve deployed an IoT hub and a Device Provisioning Service instance, and linked the two resources.</span></span> <span data-ttu-id="46f26-188">To learn how to use this set up to provision a simulated device, continue to the Quickstart for creating simulated device.</span><span class="sxs-lookup"><span data-stu-id="46f26-188">To learn how to use this set up to provision a simulated device, continue to the Quickstart for creating simulated device.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46f26-189">Quickstart to create simulated device</span><span class="sxs-lookup"><span data-stu-id="46f26-189">Quickstart to create simulated device</span></span>](./quick-create-simulated-device.md)


<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
