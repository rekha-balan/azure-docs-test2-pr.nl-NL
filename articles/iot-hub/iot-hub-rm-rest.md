---
title: Create an Azure IoT hub using the resource provider REST API | Microsoft Docs
description: How to use the resource provider REST API to create an IoT Hub.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: dobett
ms.openlocfilehash: 40fb14d600121fa3d8734e264da41c86ff28083f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563374"
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="686a5-103">Create an IoT hub using the resource provider REST API (.NET)</span><span class="sxs-lookup"><span data-stu-id="686a5-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>
[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="686a5-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="686a5-104">Introduction</span></span>
<span data-ttu-id="686a5-105">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span><span class="sxs-lookup"><span data-stu-id="686a5-105">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="686a5-106">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span><span class="sxs-lookup"><span data-stu-id="686a5-106">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="686a5-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="686a5-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="686a5-108">This article covers using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="686a5-108">This article covers using the Azure Resource Manager deployment model.</span></span>
> 
> 

<span data-ttu-id="686a5-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="686a5-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="686a5-110">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="686a5-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="686a5-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="686a5-111">An active Azure account.</span></span> <br/><span data-ttu-id="686a5-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="686a5-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="686a5-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span><span class="sxs-lookup"><span data-stu-id="686a5-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="686a5-114">Prepare your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="686a5-114">Prepare your Visual Studio project</span></span>
1. <span data-ttu-id="686a5-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="686a5-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="686a5-116">Name the project **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="686a5-116">Name the project **CreateIoTHubREST**.</span></span>
2. <span data-ttu-id="686a5-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="686a5-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="686a5-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="686a5-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="686a5-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span><span class="sxs-lookup"><span data-stu-id="686a5-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>
4. <span data-ttu-id="686a5-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="686a5-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="686a5-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span><span class="sxs-lookup"><span data-stu-id="686a5-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>
5. <span data-ttu-id="686a5-122">In Program.cs, replace the existing **using** statements with the following code:</span><span class="sxs-lookup"><span data-stu-id="686a5-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>
   
    ```
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```
6. <span data-ttu-id="686a5-123">In Program.cs, add the following static variables replacing the placeholder values.</span><span class="sxs-lookup"><span data-stu-id="686a5-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="686a5-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="686a5-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="686a5-125">**Resource group name** is the name of the resource group you use when you create the IoT hub, it can be a pre-existing resource group or a new one.</span><span class="sxs-lookup"><span data-stu-id="686a5-125">**Resource group name** is the name of the resource group you use when you create the IoT hub, it can be a pre-existing resource group or a new one.</span></span> <span data-ttu-id="686a5-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub** (this name must be globally unique, so it should include your name or initials).</span><span class="sxs-lookup"><span data-stu-id="686a5-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub** (this name must be globally unique, so it should include your name or initials).</span></span> <span data-ttu-id="686a5-127">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="686a5-127">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>
   
    ```
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
   
    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="686a5-128">Use the resource provider REST API to create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="686a5-128">Use the resource provider REST API to create an IoT hub</span></span>
<span data-ttu-id="686a5-129">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span><span class="sxs-lookup"><span data-stu-id="686a5-129">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="686a5-130">You can also use the resource provider REST API to make changes to an existing IoT hub.</span><span class="sxs-lookup"><span data-stu-id="686a5-130">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="686a5-131">Add the following method to Program.cs:</span><span class="sxs-lookup"><span data-stu-id="686a5-131">Add the following method to Program.cs:</span></span>
   
    ```
    static void CreateIoTHub(string token)
    {
   
    }
    ```
2. <span data-ttu-id="686a5-132">Add the following code to the **CreateIoTHub** method.</span><span class="sxs-lookup"><span data-stu-id="686a5-132">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="686a5-133">This code creates an **HttpClient** object with the authentication token in the headers:</span><span class="sxs-lookup"><span data-stu-id="686a5-133">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>
   
    ```
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```
3. <span data-ttu-id="686a5-134">Add the following code to the **CreateIoTHub** method.</span><span class="sxs-lookup"><span data-stu-id="686a5-134">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="686a5-135">This code describes the IoT hub to create and generates a JSON representation.</span><span class="sxs-lookup"><span data-stu-id="686a5-135">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="686a5-136">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="686a5-136">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>
   
    ```
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };
   
    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```
4. <span data-ttu-id="686a5-137">Add the following code to the **CreateIoTHub** method.</span><span class="sxs-lookup"><span data-stu-id="686a5-137">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="686a5-138">This code submits the REST request to Azure, checks the response, and retrieves the URL you can use to monitor the state of the deployment task:</span><span class="sxs-lookup"><span data-stu-id="686a5-138">This code submits the REST request to Azure, checks the response, and retrieves the URL you can use to monitor the state of the deployment task:</span></span>
   
    ```
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;
   
    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }
   
    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```
5. <span data-ttu-id="686a5-139">Add the following code to the end of the **CreateIoTHub** method.</span><span class="sxs-lookup"><span data-stu-id="686a5-139">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="686a5-140">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span><span class="sxs-lookup"><span data-stu-id="686a5-140">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>
   
    ```
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```
6. <span data-ttu-id="686a5-141">Add the following code to the end of the **CreateIoTHub** method.</span><span class="sxs-lookup"><span data-stu-id="686a5-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="686a5-142">This code retrieves the keys of the IoT hub you created and prints them to the console:</span><span class="sxs-lookup"><span data-stu-id="686a5-142">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>
   
    ```
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;
   
    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="686a5-143">Complete and run the application</span><span class="sxs-lookup"><span data-stu-id="686a5-143">Complete and run the application</span></span>
<span data-ttu-id="686a5-144">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span><span class="sxs-lookup"><span data-stu-id="686a5-144">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="686a5-145">Add the following code to the end of the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="686a5-145">Add the following code to the end of the **Main** method:</span></span>
   
    ```
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```
2. <span data-ttu-id="686a5-146">Click **Build** and then **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="686a5-146">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="686a5-147">Correct any errors.</span><span class="sxs-lookup"><span data-stu-id="686a5-147">Correct any errors.</span></span>
3. <span data-ttu-id="686a5-148">Click **Debug** and then **Start Debugging** to run the application.</span><span class="sxs-lookup"><span data-stu-id="686a5-148">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="686a5-149">It may take several minutes for the deployment to run.</span><span class="sxs-lookup"><span data-stu-id="686a5-149">It may take several minutes for the deployment to run.</span></span>
4. <span data-ttu-id="686a5-150">You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="686a5-150">You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="686a5-151">This example application adds an S1 Standard IoT Hub for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="686a5-151">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="686a5-152">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span><span class="sxs-lookup"><span data-stu-id="686a5-152">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="686a5-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="686a5-153">Next steps</span></span>
<span data-ttu-id="686a5-154">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span><span class="sxs-lookup"><span data-stu-id="686a5-154">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="686a5-155">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="686a5-155">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="686a5-156">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="686a5-156">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="686a5-157">To learn more about developing for IoT Hub, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="686a5-157">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="686a5-158">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="686a5-158">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="686a5-159">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="686a5-159">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="686a5-160">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="686a5-160">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="686a5-161">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="686a5-161">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azureps-cmdlets-docs
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
