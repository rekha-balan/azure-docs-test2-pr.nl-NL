---
title: Create an Azure IoT Hub using a template (.NET) | Microsoft Docs
description: How to use an Azure Resource Manager template to create an IoT Hub with a C# program.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/08/2017
ms.author: dobett
ms.openlocfilehash: c9ff71b3b4f1d2190f112b81835cdd98ceb3357e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554233"
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="4fcdc-103">Create an IoT hub using Azure Resource Manager template (.NET)</span><span class="sxs-lookup"><span data-stu-id="4fcdc-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>
[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="4fcdc-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="4fcdc-104">Introduction</span></span>
<span data-ttu-id="4fcdc-105">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-105">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="4fcdc-106">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-106">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="4fcdc-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4fcdc-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="4fcdc-108">This article covers using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-108">This article covers using the Azure Resource Manager deployment model.</span></span>
> 
> 

<span data-ttu-id="4fcdc-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="4fcdc-110">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="4fcdc-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-111">An active Azure account.</span></span> <br/><span data-ttu-id="4fcdc-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="4fcdc-113">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-113">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="4fcdc-114">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-114">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="4fcdc-115">Prepare your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="4fcdc-115">Prepare your Visual Studio project</span></span>
1. <span data-ttu-id="4fcdc-116">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-116">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="4fcdc-117">Name the project **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-117">Name the project **CreateIoTHub**.</span></span>
2. <span data-ttu-id="4fcdc-118">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-118">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="4fcdc-119">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-119">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="4fcdc-120">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-120">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>
4. <span data-ttu-id="4fcdc-121">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-121">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="4fcdc-122">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-122">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>
5. <span data-ttu-id="4fcdc-123">In Program.cs, replace the existing **using** statements with the following code:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-123">In Program.cs, replace the existing **using** statements with the following code:</span></span>
   
    ```
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
6. <span data-ttu-id="4fcdc-124">In Program.cs, add the following static variables replacing the placeholder values.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-124">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="4fcdc-125">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-125">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="4fcdc-126">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-126">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="4fcdc-127">**Resource group name** is the name of the resource group you use when you create the IoT Hub, it can be a pre-existing resource group or a new one.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-127">**Resource group name** is the name of the resource group you use when you create the IoT Hub, it can be a pre-existing resource group or a new one.</span></span> <span data-ttu-id="4fcdc-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>
   
    ```
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-an-azure-resource-manager-template-to-create-an-iot-hub"></a><span data-ttu-id="4fcdc-129">Submit an Azure Resource Manager template to create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4fcdc-129">Submit an Azure Resource Manager template to create an IoT hub</span></span>
<span data-ttu-id="4fcdc-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="4fcdc-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="4fcdc-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="4fcdc-133">Add a JSON file called **template.json** to your project.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-133">Add a JSON file called **template.json** to your project.</span></span>
2. <span data-ttu-id="4fcdc-134">Replace the contents of **template.json** with the following resource definition to add a standard IoT hub to the **East US** region.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-134">Replace the contents of **template.json** with the following resource definition to add a standard IoT hub to the **East US** region.</span></span> <span data-ttu-id="4fcdc-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>
   
    ```
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```
3. <span data-ttu-id="4fcdc-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="4fcdc-137">Add a JSON file called **parameters.json** to your project.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-137">Add a JSON file called **parameters.json** to your project.</span></span>
4. <span data-ttu-id="4fcdc-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="4fcdc-139">The IoT hub name must be globally unique so it should include your name or initials:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>
   
    ```
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
5. <span data-ttu-id="4fcdc-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="4fcdc-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>
6. <span data-ttu-id="4fcdc-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="4fcdc-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="4fcdc-144">The URLs of the blobs containing the JSON data are:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-144">The URLs of the blobs containing the JSON data are:</span></span>
   
    ```
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="4fcdc-145">Add the following method to Program.cs:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-145">Add the following method to Program.cs:</span></span>
   
    ```
    static void CreateIoTHub(ResourceManagementClient client)
    {
   
    }
    ```
8. <span data-ttu-id="4fcdc-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>
   
    ```
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```
9. <span data-ttu-id="4fcdc-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>
   
    ```
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);
   
    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="4fcdc-148">Complete and run the application</span><span class="sxs-lookup"><span data-stu-id="4fcdc-148">Complete and run the application</span></span>
<span data-ttu-id="4fcdc-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="4fcdc-150">Add the following code to the end of the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-150">Add the following code to the end of the **Main** method:</span></span>
   
    ```
    CreateIoTHub(client);
    Console.ReadLine();
    ```
2. <span data-ttu-id="4fcdc-151">Click **Build** and then **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="4fcdc-152">Correct any errors.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-152">Correct any errors.</span></span>
3. <span data-ttu-id="4fcdc-153">Click **Debug** and then **Start Debugging** to run the application.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="4fcdc-154">It may take several minutes for the deployment to run.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-154">It may take several minutes for the deployment to run.</span></span>
4. <span data-ttu-id="4fcdc-155">You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-155">You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4fcdc-156">This example application adds an S1 Standard IoT Hub for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-156">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="4fcdc-157">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-157">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4fcdc-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="4fcdc-158">Next steps</span></span>
<span data-ttu-id="4fcdc-159">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-159">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="4fcdc-160">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="4fcdc-160">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="4fcdc-161">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fcdc-161">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="4fcdc-162">To learn more about developing for IoT Hub, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-162">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="4fcdc-163">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="4fcdc-163">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="4fcdc-164">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="4fcdc-164">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="4fcdc-165">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="4fcdc-165">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4fcdc-166">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="4fcdc-166">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azureps-cmdlets-docs
[lnk-rest-api]: https://msdn.microsoft.com/library/mt589014.aspx
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]: ../storage/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
