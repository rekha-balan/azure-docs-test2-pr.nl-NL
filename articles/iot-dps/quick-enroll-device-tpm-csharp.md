---
title: Enroll TPM device to Azure Device Provisioning Service using C# | Microsoft Docs
description: Azure Quickstart - Enroll TPM device to Azure IoT Hub Device Provisioning Service using C# service SDK
author: wesmc7777
ms.author: wesmc
ms.date: 01/16/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 5c0ac54996f66f44d39389d8ed1bc0c40793933b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869986"
---
# <a name="enroll-tpm-device-to-iot-hub-device-provisioning-service-using-c-service-sdk"></a><span data-ttu-id="35c8d-103">Enroll TPM device to IoT Hub Device Provisioning Service using C# service SDK</span><span class="sxs-lookup"><span data-stu-id="35c8d-103">Enroll TPM device to IoT Hub Device Provisioning Service using C# service SDK</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-tpm](../../includes/iot-dps-selector-quick-enroll-device-tpm.md)]


<span data-ttu-id="35c8d-104">These steps show how to programmatically create an individual enrollment for a TPM device in the Azure IoT Hub Device Provisioning Service using the [C# Service SDK](https://github.com/Azure/azure-iot-sdk-csharp) and a sample C# .NET Core application.</span><span class="sxs-lookup"><span data-stu-id="35c8d-104">These steps show how to programmatically create an individual enrollment for a TPM device in the Azure IoT Hub Device Provisioning Service using the [C# Service SDK](https://github.com/Azure/azure-iot-sdk-csharp) and a sample C# .NET Core application.</span></span> <span data-ttu-id="35c8d-105">You can optionally enroll a simulated TPM device to the provisioning service using this individual enrollment entry.</span><span class="sxs-lookup"><span data-stu-id="35c8d-105">You can optionally enroll a simulated TPM device to the provisioning service using this individual enrollment entry.</span></span> <span data-ttu-id="35c8d-106">Although these steps work on both Windows and Linux machines, this article uses a Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="35c8d-106">Although these steps work on both Windows and Linux machines, this article uses a Windows development machine.</span></span>

## <a name="prepare-the-development-environment"></a><span data-ttu-id="35c8d-107">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="35c8d-107">Prepare the development environment</span></span>

1. <span data-ttu-id="35c8d-108">Make sure you have [Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="35c8d-108">Make sure you have [Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span></span> 
2. <span data-ttu-id="35c8d-109">Make sure you have the [.Net Core SDK](https://www.microsoft.com/net/download/windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="35c8d-109">Make sure you have the [.Net Core SDK](https://www.microsoft.com/net/download/windows) installed on your machine.</span></span> 
3. <span data-ttu-id="35c8d-110">Make sure to complete the steps in [Set up the IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span><span class="sxs-lookup"><span data-stu-id="35c8d-110">Make sure to complete the steps in [Set up the IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) before you proceed.</span></span>
4. <span data-ttu-id="35c8d-111">(Optional) If you want to enroll a simulated device at the end of this Quickstart, follow the steps in [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) up to the step where you get an endorsement key for the device.</span><span class="sxs-lookup"><span data-stu-id="35c8d-111">(Optional) If you want to enroll a simulated device at the end of this Quickstart, follow the steps in [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) up to the step where you get an endorsement key for the device.</span></span> <span data-ttu-id="35c8d-112">Note down the endorsement key, registration ID, and, optionally, the device ID, you need to use them later in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="35c8d-112">Note down the endorsement key, registration ID, and, optionally, the device ID, you need to use them later in this Quickstart.</span></span> <span data-ttu-id="35c8d-113">**Do not follow the steps to create an individual enrollment using the Azure portal.**</span><span class="sxs-lookup"><span data-stu-id="35c8d-113">**Do not follow the steps to create an individual enrollment using the Azure portal.**</span></span>

## <a name="get-the-connection-string-for-your-provisioning-service"></a><span data-ttu-id="35c8d-114">Get the connection string for your provisioning service</span><span class="sxs-lookup"><span data-stu-id="35c8d-114">Get the connection string for your provisioning service</span></span>

<span data-ttu-id="35c8d-115">For the sample in this Quickstart, you need the connection string for your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="35c8d-115">For the sample in this Quickstart, you need the connection string for your provisioning service.</span></span>
1. <span data-ttu-id="35c8d-116">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="35c8d-116">Log in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning Service.</span></span> 
2. <span data-ttu-id="35c8d-117">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span><span class="sxs-lookup"><span data-stu-id="35c8d-117">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span></span> <span data-ttu-id="35c8d-118">In the **Access Policy** window, copy and note down the primary key connection string.</span><span class="sxs-lookup"><span data-stu-id="35c8d-118">In the **Access Policy** window, copy and note down the primary key connection string.</span></span> 

    ![Get provisioning service connection string from the portal](media/quick-enroll-device-tpm-csharp/get-service-connection-string.png)

## <a name="create-the-individual-enrollment-sample"></a><span data-ttu-id="35c8d-120">Create the individual enrollment sample</span><span class="sxs-lookup"><span data-stu-id="35c8d-120">Create the individual enrollment sample</span></span> 

<span data-ttu-id="35c8d-121">The steps in this section show how to create a .NET Core console app that adds an individual enrollment for a TPM device to your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="35c8d-121">The steps in this section show how to create a .NET Core console app that adds an individual enrollment for a TPM device to your provisioning service.</span></span> <span data-ttu-id="35c8d-122">With some modification, you can also follow these steps to create a [Windows IoT Core](https://developer.microsoft.com/en-us/windows/iot) console app to add the individual enrollment.</span><span class="sxs-lookup"><span data-stu-id="35c8d-122">With some modification, you can also follow these steps to create a [Windows IoT Core](https://developer.microsoft.com/en-us/windows/iot) console app to add the individual enrollment.</span></span> <span data-ttu-id="35c8d-123">To learn more about developing with IoT Core, see the [Windows IoT Core developer documentation](https://docs.microsoft.com/windows/iot-core/).</span><span class="sxs-lookup"><span data-stu-id="35c8d-123">To learn more about developing with IoT Core, see the [Windows IoT Core developer documentation](https://docs.microsoft.com/windows/iot-core/).</span></span>
1. <span data-ttu-id="35c8d-124">In Visual Studio, add a Visual C# .NET Core Console App project to a new solution by using the **Console App (.NET Core)** project template.</span><span class="sxs-lookup"><span data-stu-id="35c8d-124">In Visual Studio, add a Visual C# .NET Core Console App project to a new solution by using the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="35c8d-125">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="35c8d-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="35c8d-126">Name the project **CreateTpmEnrollment**.</span><span class="sxs-lookup"><span data-stu-id="35c8d-126">Name the project **CreateTpmEnrollment**.</span></span>

    ![New Visual C# Windows Classic Desktop project](media//quick-enroll-device-tpm-csharp/create-app.png)

2. <span data-ttu-id="35c8d-128">In Solution Explorer, right-click the **CreateTpmEnrollment** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="35c8d-128">In Solution Explorer, right-click the **CreateTpmEnrollment** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="35c8d-129">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Provisioning.Service**, select **Install** to install the **Microsoft.Azure.Devices.Provisioning.Service** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="35c8d-129">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Provisioning.Service**, select **Install** to install the **Microsoft.Azure.Devices.Provisioning.Service** package, and accept the terms of use.</span></span> <span data-ttu-id="35c8d-130">This procedure downloads, installs, and adds a reference to the [Azure IoT Provisioning Service Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Provisioning.Service/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="35c8d-130">This procedure downloads, installs, and adds a reference to the [Azure IoT Provisioning Service Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Provisioning.Service/) NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window](media//quick-enroll-device-tpm-csharp/add-nuget.png)

4. <span data-ttu-id="35c8d-132">Add the following `using` statements after the other `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="35c8d-132">Add the following `using` statements after the other `using` statements at the top of the **Program.cs** file:</span></span>
   
   ```csharp
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Provisioning.Service;
   ```
    
5. <span data-ttu-id="35c8d-133">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="35c8d-133">Add the following fields to the **Program** class.</span></span>  
   - <span data-ttu-id="35c8d-134">Replace the **ProvisioningConnectionString** placeholder value with the connection string of the provisioning service that you want to create the enrollment for.</span><span class="sxs-lookup"><span data-stu-id="35c8d-134">Replace the **ProvisioningConnectionString** placeholder value with the connection string of the provisioning service that you want to create the enrollment for.</span></span>
   - <span data-ttu-id="35c8d-135">You may optionally change the registration ID, endorsement key, device ID, and provisioning status.</span><span class="sxs-lookup"><span data-stu-id="35c8d-135">You may optionally change the registration ID, endorsement key, device ID, and provisioning status.</span></span> 
   - <span data-ttu-id="35c8d-136">If you are using this Quickstart together with the [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) Quickstart to provision a simulated device, replace the endorsement key and registration ID with the values that you noted down in that Quickstart.</span><span class="sxs-lookup"><span data-stu-id="35c8d-136">If you are using this Quickstart together with the [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) Quickstart to provision a simulated device, replace the endorsement key and registration ID with the values that you noted down in that Quickstart.</span></span> <span data-ttu-id="35c8d-137">You can replace the device ID with the value suggested in that Quickstart, use your own value, or use the default value in this sample.</span><span class="sxs-lookup"><span data-stu-id="35c8d-137">You can replace the device ID with the value suggested in that Quickstart, use your own value, or use the default value in this sample.</span></span>
        
   ```csharp
   private static string ProvisioningConnectionString = "{Your provisioning service connection string}";
   private const string RegistrationId = "sample-registrationid-csharp";
   private const string TpmEndorsementKey =
       "AToAAQALAAMAsgAgg3GXZ0SEs/gakMyNRqXXJP1S124GUgtk8qHaGzMUaaoABgCAAEMAEAgAAAAAAAEAxsj2gUS" +
       "cTk1UjuioeTlfGYZrrimExB+bScH75adUMRIi2UOMxG1kw4y+9RW/IVoMl4e620VxZad0ARX2gUqVjYO7KPVt3d" +
       "yKhZS3dkcvfBisBhP1XH9B33VqHG9SHnbnQXdBUaCgKAfxome8UmBKfe+naTsE5fkvjb/do3/dD6l4sGBwFCnKR" +
       "dln4XpM03zLpoHFao8zOwt8l/uP3qUIxmCYv9A7m69Ms+5/pCkTu/rK4mRDsfhZ0QLfbzVI6zQFOKF/rwsfBtFe" +
       "WlWtcuJMKlXdD8TXWElTzgh7JS4qhFzreL0c1mI0GCj+Aws0usZh7dLIVPnlgZcBhgy1SSDQMQ==";
       
   // Optional parameters
   private const string OptionalDeviceId = "myCSharpDevice";
   private const ProvisioningStatus OptionalProvisioningStatus = ProvisioningStatus.Enabled;
   ```
    
6. <span data-ttu-id="35c8d-138">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="35c8d-138">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="35c8d-139">This code creates individual enrollment entry and then calls the **CreateOrUpdateIndividualEnrollmentAsync** method on the **ProvisioningServiceClient** to add the individual enrollment to the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="35c8d-139">This code creates individual enrollment entry and then calls the **CreateOrUpdateIndividualEnrollmentAsync** method on the **ProvisioningServiceClient** to add the individual enrollment to the provisioning service.</span></span>
   
   ```csharp
   public static async Task RunSample()
   {
       Console.WriteLine("Starting sample...");

       using (ProvisioningServiceClient provisioningServiceClient =
               ProvisioningServiceClient.CreateFromConnectionString(ProvisioningConnectionString))
       {
           #region Create a new individualEnrollment config
           Console.WriteLine("\nCreating a new individualEnrollment...");
           Attestation attestation = new TpmAttestation(TpmEndorsementKey);
           IndividualEnrollment individualEnrollment =
                   new IndividualEnrollment(
                           RegistrationId,
                           attestation);

           // The following parameters are optional. Remove them if you don't need them.
           individualEnrollment.DeviceId = OptionalDeviceId;
           individualEnrollment.ProvisioningStatus = OptionalProvisioningStatus;
           #endregion

           #region Create the individualEnrollment
           Console.WriteLine("\nAdding new individualEnrollment...");
           IndividualEnrollment individualEnrollmentResult =
               await provisioningServiceClient.CreateOrUpdateIndividualEnrollmentAsync(individualEnrollment).ConfigureAwait(false);
           Console.WriteLine("\nIndividualEnrollment created with success.");
           Console.WriteLine(individualEnrollmentResult);
           #endregion
        
       }
   }
   ```
       
7. <span data-ttu-id="35c8d-140">Finally, replace the body of the **Main** method with the following lines:</span><span class="sxs-lookup"><span data-stu-id="35c8d-140">Finally, replace the body of the **Main** method with the following lines:</span></span>
   
   ```csharp
   RunSample().GetAwaiter().GetResult();
   Console.WriteLine("\nHit <Enter> to exit ...");
   Console.ReadLine();
   ```
        
8. <span data-ttu-id="35c8d-141">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="35c8d-141">Build the solution.</span></span>

## <a name="run-the-individual-enrollment-sample"></a><span data-ttu-id="35c8d-142">Run the individual enrollment sample</span><span class="sxs-lookup"><span data-stu-id="35c8d-142">Run the individual enrollment sample</span></span>
  
1. <span data-ttu-id="35c8d-143">Run the sample in Visual Studio to create the individual enrollment for your TPM device.</span><span class="sxs-lookup"><span data-stu-id="35c8d-143">Run the sample in Visual Studio to create the individual enrollment for your TPM device.</span></span>
 
2. <span data-ttu-id="35c8d-144">On successful creation, the command window displays the properties of the new individual enrollment.</span><span class="sxs-lookup"><span data-stu-id="35c8d-144">On successful creation, the command window displays the properties of the new individual enrollment.</span></span>

    ![Enrollment properties in the command output](media/quick-enroll-device-tpm-csharp/output.png)

3. <span data-ttu-id="35c8d-146">To verify that the individual enrollment has been created, on the Device Provisioning Service summary blade in the Azure portal, select **Manage enrollments**, then select the **Individual Enrollments** tab. You should see a new enrollment entry that corresponds to the registration ID you used in the sample.</span><span class="sxs-lookup"><span data-stu-id="35c8d-146">To verify that the individual enrollment has been created, on the Device Provisioning Service summary blade in the Azure portal, select **Manage enrollments**, then select the **Individual Enrollments** tab. You should see a new enrollment entry that corresponds to the registration ID you used in the sample.</span></span> <span data-ttu-id="35c8d-147">Click the entry to verify the endorsement key and other properties for the entry.</span><span class="sxs-lookup"><span data-stu-id="35c8d-147">Click the entry to verify the endorsement key and other properties for the entry.</span></span>

    ![Enrollment properties in the portal](media/quick-enroll-device-tpm-csharp/verify-enrollment-portal.png)
 
4. <span data-ttu-id="35c8d-149">(Optional) If you've been following the steps in the [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) Quickstart, you can continue with the remaining steps in that Quickstart to enroll your simulated device.</span><span class="sxs-lookup"><span data-stu-id="35c8d-149">(Optional) If you've been following the steps in the [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) Quickstart, you can continue with the remaining steps in that Quickstart to enroll your simulated device.</span></span> <span data-ttu-id="35c8d-150">Be sure to skip the steps to create an individual enrollment using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35c8d-150">Be sure to skip the steps to create an individual enrollment using the Azure portal.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="35c8d-151">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="35c8d-151">Clean up resources</span></span>
<span data-ttu-id="35c8d-152">If you plan to explore the C# service sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="35c8d-152">If you plan to explore the C# service sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="35c8d-153">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="35c8d-153">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="35c8d-154">Close the C# sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="35c8d-154">Close the C# sample output window on your machine.</span></span>
2. <span data-ttu-id="35c8d-155">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Individual Enrollments** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart, and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="35c8d-155">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Individual Enrollments** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart, and click the **Delete** button at the top of the blade.</span></span> 
3. <span data-ttu-id="35c8d-156">If you followed the steps in the [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) Quickstart to create a simulated TPM device:</span><span class="sxs-lookup"><span data-stu-id="35c8d-156">If you followed the steps in the [Create and provision a simulated TPM device using C# device SDK](quick-create-simulated-device-tpm-csharp.md) Quickstart to create a simulated TPM device:</span></span> 

    1. <span data-ttu-id="35c8d-157">Close the TPM simulator window and the sample output window for the simulated device.</span><span class="sxs-lookup"><span data-stu-id="35c8d-157">Close the TPM simulator window and the sample output window for the simulated device.</span></span>
    2. <span data-ttu-id="35c8d-158">In the Azure portal, navigate to the IoT Hub where your device was provisioned.</span><span class="sxs-lookup"><span data-stu-id="35c8d-158">In the Azure portal, navigate to the IoT Hub where your device was provisioned.</span></span> <span data-ttu-id="35c8d-159">In the left-hand menu under **Explorers**, click **IoT Devices**, select the check box next to your device, and then click **Delete** at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="35c8d-159">In the left-hand menu under **Explorers**, click **IoT Devices**, select the check box next to your device, and then click **Delete** at the top of the window.</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="35c8d-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="35c8d-160">Next steps</span></span>
<span data-ttu-id="35c8d-161">In this Quickstart, you’ve programmatically created an individual enrollment entry for a TPM device, and, optionally, created a TPM simulated device on your machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="35c8d-161">In this Quickstart, you’ve programmatically created an individual enrollment entry for a TPM device, and, optionally, created a TPM simulated device on your machine and provisioned it to your IoT hub using the Azure IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="35c8d-162">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35c8d-162">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="35c8d-163">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="35c8d-163">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)

