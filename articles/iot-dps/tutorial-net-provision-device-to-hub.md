---
title: Provision a device using Azure IoT Hub Device Provisioning Service (.NET) | Microsoft Docs
description: Provision your device to a single IoT hub using the Azure IoT Hub Device Provisioning Service (.NET)
author: wesmc7777
ms.author: wesmc
ms.date: 09/05/2017
ms.topic: tutorial
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 84072c7e5f7aa37e89fc1b93c1585167dd6d9f4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865503"
---
# <a name="enroll-the-device-to-an-iot-hub-using-the-azure-iot-hub-provisioning-service-client-net"></a><span data-ttu-id="d96c1-103">Enroll the device to an IoT hub using the Azure IoT Hub Provisioning Service Client (.NET)</span><span class="sxs-lookup"><span data-stu-id="d96c1-103">Enroll the device to an IoT hub using the Azure IoT Hub Provisioning Service Client (.NET)</span></span>

<span data-ttu-id="d96c1-104">In the previous tutorial, you learned how to set up a device to connect to your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="d96c1-104">In the previous tutorial, you learned how to set up a device to connect to your Device Provisioning service.</span></span> <span data-ttu-id="d96c1-105">In this tutorial, you learn how to use this service to provision your device to a single IoT hub, using both **_Individual Enrollment_** and **_Enrollment Groups_**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-105">In this tutorial, you learn how to use this service to provision your device to a single IoT hub, using both **_Individual Enrollment_** and **_Enrollment Groups_**.</span></span> <span data-ttu-id="d96c1-106">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="d96c1-106">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d96c1-107">Enroll the device</span><span class="sxs-lookup"><span data-stu-id="d96c1-107">Enroll the device</span></span>
> * <span data-ttu-id="d96c1-108">Start the device</span><span class="sxs-lookup"><span data-stu-id="d96c1-108">Start the device</span></span>
> * <span data-ttu-id="d96c1-109">Verify the device is registered</span><span class="sxs-lookup"><span data-stu-id="d96c1-109">Verify the device is registered</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d96c1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d96c1-110">Prerequisites</span></span>

<span data-ttu-id="d96c1-111">Before you proceed, make sure to configure your device and its *Hardware Security Module* as discussed in the tutorial [Set up a device to provision using Azure IoT Hub Device Provisioning Service](./tutorial-set-up-device.md).</span><span class="sxs-lookup"><span data-stu-id="d96c1-111">Before you proceed, make sure to configure your device and its *Hardware Security Module* as discussed in the tutorial [Set up a device to provision using Azure IoT Hub Device Provisioning Service](./tutorial-set-up-device.md).</span></span>

* <span data-ttu-id="d96c1-112">Visual Studio 2015 or Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d96c1-112">Visual Studio 2015 or Visual Studio 2017</span></span>

> [!NOTE]
> <span data-ttu-id="d96c1-113">Visual Studio is not required.</span><span class="sxs-lookup"><span data-stu-id="d96c1-113">Visual Studio is not required.</span></span> <span data-ttu-id="d96c1-114">The installation of [.NET](https://www.microsoft.com/net) is sufficient and developers can use their preferred editor on Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="d96c1-114">The installation of [.NET](https://www.microsoft.com/net) is sufficient and developers can use their preferred editor on Windows or Linux.</span></span>  

<span data-ttu-id="d96c1-115">This tutorial simulates the period during or right after the hardware manufacturing process, when device information is added to the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="d96c1-115">This tutorial simulates the period during or right after the hardware manufacturing process, when device information is added to the provisioning service.</span></span> <span data-ttu-id="d96c1-116">This code is usually run on a PC or a factory device that can run .NET code and should not be added to the devices themselves.</span><span class="sxs-lookup"><span data-stu-id="d96c1-116">This code is usually run on a PC or a factory device that can run .NET code and should not be added to the devices themselves.</span></span>


## <a name="enroll-the-device"></a><span data-ttu-id="d96c1-117">Enroll the device</span><span class="sxs-lookup"><span data-stu-id="d96c1-117">Enroll the device</span></span>

<span data-ttu-id="d96c1-118">This step involves adding the device's unique security artifacts to the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="d96c1-118">This step involves adding the device's unique security artifacts to the Device Provisioning Service.</span></span> <span data-ttu-id="d96c1-119">These security artifacts are as follows:</span><span class="sxs-lookup"><span data-stu-id="d96c1-119">These security artifacts are as follows:</span></span>

- <span data-ttu-id="d96c1-120">For TPM-based devices:</span><span class="sxs-lookup"><span data-stu-id="d96c1-120">For TPM-based devices:</span></span>
    - <span data-ttu-id="d96c1-121">The *Endorsement Key* that is unique to each TPM chip or simulation.</span><span class="sxs-lookup"><span data-stu-id="d96c1-121">The *Endorsement Key* that is unique to each TPM chip or simulation.</span></span> <span data-ttu-id="d96c1-122">Read the [Understand TPM Endorsement Key](https://technet.microsoft.com/library/cc770443.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="d96c1-122">Read the [Understand TPM Endorsement Key](https://technet.microsoft.com/library/cc770443.aspx) for more information.</span></span>
    - <span data-ttu-id="d96c1-123">The *Registration ID* that is used to uniquely identify a device in the namespace/scope.</span><span class="sxs-lookup"><span data-stu-id="d96c1-123">The *Registration ID* that is used to uniquely identify a device in the namespace/scope.</span></span> <span data-ttu-id="d96c1-124">This may or may not be the same as the device ID.</span><span class="sxs-lookup"><span data-stu-id="d96c1-124">This may or may not be the same as the device ID.</span></span> <span data-ttu-id="d96c1-125">The ID is mandatory for every device.</span><span class="sxs-lookup"><span data-stu-id="d96c1-125">The ID is mandatory for every device.</span></span> <span data-ttu-id="d96c1-126">For TPM-based devices, the registration ID may be derived from the TPM itself, for example, an SHA-256 hash of the TPM Endorsement Key.</span><span class="sxs-lookup"><span data-stu-id="d96c1-126">For TPM-based devices, the registration ID may be derived from the TPM itself, for example, an SHA-256 hash of the TPM Endorsement Key.</span></span>

- <span data-ttu-id="d96c1-127">For X.509 based devices:</span><span class="sxs-lookup"><span data-stu-id="d96c1-127">For X.509 based devices:</span></span>
    - <span data-ttu-id="d96c1-128">The [X.509 certificate issued to the device](https://msdn.microsoft.com/library/windows/desktop/bb540819.aspx), in the form of either a *.pem* or a *.cer* file.</span><span class="sxs-lookup"><span data-stu-id="d96c1-128">The [X.509 certificate issued to the device](https://msdn.microsoft.com/library/windows/desktop/bb540819.aspx), in the form of either a *.pem* or a *.cer* file.</span></span> <span data-ttu-id="d96c1-129">For individual enrollment, you need to use the *leaf certificate* for your X.509 system, while for enrollment groups, you need to use the *root certificate* or an equivalent *signer certificate*.</span><span class="sxs-lookup"><span data-stu-id="d96c1-129">For individual enrollment, you need to use the *leaf certificate* for your X.509 system, while for enrollment groups, you need to use the *root certificate* or an equivalent *signer certificate*.</span></span>
    - <span data-ttu-id="d96c1-130">The *Registration ID* that is used to uniquely identify a device in the namespace/scope.</span><span class="sxs-lookup"><span data-stu-id="d96c1-130">The *Registration ID* that is used to uniquely identify a device in the namespace/scope.</span></span> <span data-ttu-id="d96c1-131">This may or may not be the same as the device ID.</span><span class="sxs-lookup"><span data-stu-id="d96c1-131">This may or may not be the same as the device ID.</span></span> <span data-ttu-id="d96c1-132">The ID is mandatory for every device.</span><span class="sxs-lookup"><span data-stu-id="d96c1-132">The ID is mandatory for every device.</span></span> <span data-ttu-id="d96c1-133">For X.509 based devices, the registration ID is derived from the certificate's common name (CN).</span><span class="sxs-lookup"><span data-stu-id="d96c1-133">For X.509 based devices, the registration ID is derived from the certificate's common name (CN).</span></span> <span data-ttu-id="d96c1-134">For further information on these requirements see [Device concepts](https://docs.microsoft.com/azure/iot-dps/concepts-device).</span><span class="sxs-lookup"><span data-stu-id="d96c1-134">For further information on these requirements see [Device concepts](https://docs.microsoft.com/azure/iot-dps/concepts-device).</span></span>

<span data-ttu-id="d96c1-135">There are two ways to enroll the device to the Device Provisioning Service:</span><span class="sxs-lookup"><span data-stu-id="d96c1-135">There are two ways to enroll the device to the Device Provisioning Service:</span></span>

- <span data-ttu-id="d96c1-136">**Individual Enrollments** This represents an entry for a single device that may register with the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="d96c1-136">**Individual Enrollments** This represents an entry for a single device that may register with the Device Provisioning Service.</span></span> <span data-ttu-id="d96c1-137">Individual enrollments may use either X.509 certificates or SAS tokens (in a real or virtual TPM) as attestation mechanisms.</span><span class="sxs-lookup"><span data-stu-id="d96c1-137">Individual enrollments may use either X.509 certificates or SAS tokens (in a real or virtual TPM) as attestation mechanisms.</span></span> <span data-ttu-id="d96c1-138">We recommend using individual enrollments for devices, which require unique initial configurations, or for devices that can only use SAS tokens via TPM as the attestation mechanism.</span><span class="sxs-lookup"><span data-stu-id="d96c1-138">We recommend using individual enrollments for devices, which require unique initial configurations, or for devices that can only use SAS tokens via TPM as the attestation mechanism.</span></span> <span data-ttu-id="d96c1-139">Individual enrollments may have the desired IoT hub device ID specified.</span><span class="sxs-lookup"><span data-stu-id="d96c1-139">Individual enrollments may have the desired IoT hub device ID specified.</span></span>

- <span data-ttu-id="d96c1-140">**Enrollment Groups** This represents a group of devices that share a specific attestation mechanism.</span><span class="sxs-lookup"><span data-stu-id="d96c1-140">**Enrollment Groups** This represents a group of devices that share a specific attestation mechanism.</span></span> <span data-ttu-id="d96c1-141">We recommend using an enrollment group for a large number of devices, which share a desired initial configuration, or for devices all going to the same tenant.</span><span class="sxs-lookup"><span data-stu-id="d96c1-141">We recommend using an enrollment group for a large number of devices, which share a desired initial configuration, or for devices all going to the same tenant.</span></span> <span data-ttu-id="d96c1-142">Enrollment groups are X.509 only and all share a signing certificate in their X.509 certificate chain.</span><span class="sxs-lookup"><span data-stu-id="d96c1-142">Enrollment groups are X.509 only and all share a signing certificate in their X.509 certificate chain.</span></span>

### <a name="enroll-the-device-using-individual-enrollments"></a><span data-ttu-id="d96c1-143">Enroll the device using Individual Enrollments</span><span class="sxs-lookup"><span data-stu-id="d96c1-143">Enroll the device using Individual Enrollments</span></span>

1. <span data-ttu-id="d96c1-144">In Visual Studio, create a Visual C# Console Application project by using the **Console App** project template.</span><span class="sxs-lookup"><span data-stu-id="d96c1-144">In Visual Studio, create a Visual C# Console Application project by using the **Console App** project template.</span></span> <span data-ttu-id="d96c1-145">Name the project **DeviceProvisioning**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-145">Name the project **DeviceProvisioning**.</span></span>
    
1. <span data-ttu-id="d96c1-146">In Solution Explorer, right-click the **DeviceProvisioning** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-146">In Solution Explorer, right-click the **DeviceProvisioning** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="d96c1-147">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.provisioning.service**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-147">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.provisioning.service**.</span></span> <span data-ttu-id="d96c1-148">Select the entry and click **Install** to install the **Microsoft.Azure.Devices.Provisioning.Service** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="d96c1-148">Select the entry and click **Install** to install the **Microsoft.Azure.Devices.Provisioning.Service** package, and accept the terms of use.</span></span> <span data-ttu-id="d96c1-149">This procedure downloads, installs, and adds a reference to the [Azure IoT Device Provisioning Service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Provisioning.Service/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="d96c1-149">This procedure downloads, installs, and adds a reference to the [Azure IoT Device Provisioning Service SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Provisioning.Service/) NuGet package and its dependencies.</span></span>

1. <span data-ttu-id="d96c1-150">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="d96c1-150">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using Microsoft.Azure.Devices.Provisioning.Service;
    ```

1. <span data-ttu-id="d96c1-151">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d96c1-151">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="d96c1-152">Replace the placeholder value with the Device Provisioning Service connection string noted in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d96c1-152">Replace the placeholder value with the Device Provisioning Service connection string noted in the previous section.</span></span>
   
    ```csharp
    static readonly string ServiceConnectionString = "{Device Provisioning Service connection string}";

    private const string SampleRegistrationId = "sample-individual-csharp";
    private const string SampleTpmEndorsementKey =
            "AToAAQALAAMAsgAgg3GXZ0SEs/gakMyNRqXXJP1S124GUgtk8qHaGzMUaaoABgCAAEMAEAgAAAAAAAEAxsj2gUS" +
            "cTk1UjuioeTlfGYZrrimExB+bScH75adUMRIi2UOMxG1kw4y+9RW/IVoMl4e620VxZad0ARX2gUqVjYO7KPVt3d" +
            "yKhZS3dkcvfBisBhP1XH9B33VqHG9SHnbnQXdBUaCgKAfxome8UmBKfe+naTsE5fkvjb/do3/dD6l4sGBwFCnKR" +
            "dln4XpM03zLpoHFao8zOwt8l/uP3qUIxmCYv9A7m69Ms+5/pCkTu/rK4mRDsfhZ0QLfbzVI6zQFOKF/rwsfBtFe" +
            "WlWtcuJMKlXdD8TXWElTzgh7JS4qhFzreL0c1mI0GCj+Aws0usZh7dLIVPnlgZcBhgy1SSDQMQ==";
    private const string OptionalDeviceId = "myCSharpDevice";
    private const ProvisioningStatus OptionalProvisioningStatus = ProvisioningStatus.Enabled;
    ```

1. <span data-ttu-id="d96c1-153">Add the following to implement the enrollment for the device:</span><span class="sxs-lookup"><span data-stu-id="d96c1-153">Add the following to implement the enrollment for the device:</span></span>

    ```csharp
    static async Task SetRegistrationDataAsync()
    {
        Console.WriteLine("Starting SetRegistrationData");

        Attestation attestation = new TpmAttestation(SampleTpmEndorsementKey);

        IndividualEnrollment individualEnrollment = new IndividualEnrollment(SampleRegistrationId, attestation);

        individualEnrollment.DeviceId = OptionalDeviceId;
        individualEnrollment.ProvisioningStatus = OptionalProvisioningStatus;

        Console.WriteLine("\nAdding new individualEnrollment...");
        var serviceClient = ProvisioningServiceClient.CreateFromConnectionString(ServiceConnectionString);

        IndividualEnrollment individualEnrollmentResult =
            await serviceClient.CreateOrUpdateIndividualEnrollmentAsync(individualEnrollment).ConfigureAwait(false);

        Console.WriteLine("\nIndividualEnrollment created with success.");
        Console.WriteLine(individualEnrollmentResult);
    }
    ```

1. <span data-ttu-id="d96c1-154">Finally, add the following code to the **Main** method to open the connection to your IoT hub and begin the enrollment:</span><span class="sxs-lookup"><span data-stu-id="d96c1-154">Finally, add the following code to the **Main** method to open the connection to your IoT hub and begin the enrollment:</span></span>
   
    ```csharp
    try
    {
        Console.WriteLine("IoT Device Provisioning example");

        SetRegistrationDataAsync().GetAwaiter().GetResult();
            
        Console.WriteLine("Done, hit enter to exit.");
        Console.ReadLine();
    }
    catch (Exception ex)
    {
        Console.WriteLine();
        Console.WriteLine("Error in sample: {0}", ex.Message);
    }
    ```
        
1. <span data-ttu-id="d96c1-155">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select the **DeviceProvisioning** project in the dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="d96c1-155">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select the **DeviceProvisioning** project in the dropdown menu.</span></span>  

1. <span data-ttu-id="d96c1-156">Run the .NET device app **DeviceProvisiong**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-156">Run the .NET device app **DeviceProvisiong**.</span></span> <span data-ttu-id="d96c1-157">It should set up provisioning for the device:</span><span class="sxs-lookup"><span data-stu-id="d96c1-157">It should set up provisioning for the device:</span></span> 

    ![Individual registration run](./media/tutorial-net-provision-device-to-hub/individual.png)

<span data-ttu-id="d96c1-159">When the device is successfully enrolled, you should see it displayed in the portal as following:</span><span class="sxs-lookup"><span data-stu-id="d96c1-159">When the device is successfully enrolled, you should see it displayed in the portal as following:</span></span>

   ![Successful enrollment in the portal](./media/tutorial-net-provision-device-to-hub/individual-portal.png)

### <a name="enroll-the-device-using-enrollment-groups"></a><span data-ttu-id="d96c1-161">Enroll the device using Enrollment Groups</span><span class="sxs-lookup"><span data-stu-id="d96c1-161">Enroll the device using Enrollment Groups</span></span>

> [!NOTE]
> <span data-ttu-id="d96c1-162">The enrollment group sample requires an X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="d96c1-162">The enrollment group sample requires an X.509 certificate.</span></span>

1. <span data-ttu-id="d96c1-163">In the Visual Studio Solution Explorer, open the **DeviceProvisioning** project created above.</span><span class="sxs-lookup"><span data-stu-id="d96c1-163">In the Visual Studio Solution Explorer, open the **DeviceProvisioning** project created above.</span></span> 

1. <span data-ttu-id="d96c1-164">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="d96c1-164">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using System.Security.Cryptography.X509Certificates;
    ```

1. <span data-ttu-id="d96c1-165">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d96c1-165">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="d96c1-166">Replace the placeholder value with the X509 certificate location.</span><span class="sxs-lookup"><span data-stu-id="d96c1-166">Replace the placeholder value with the X509 certificate location.</span></span>
   
    ```csharp
    private const string X509RootCertPathVar = "{X509 Certificate Location}";
    private const string SampleEnrollmentGroupId = "sample-group-csharp";
    ```

1. <span data-ttu-id="d96c1-167">Add the following to **Program.cs** implement the enrollment for the group:</span><span class="sxs-lookup"><span data-stu-id="d96c1-167">Add the following to **Program.cs** implement the enrollment for the group:</span></span>

    ```csharp
    public static async Task SetGroupRegistrationDataAsync()
    {
        Console.WriteLine("Starting SetGroupRegistrationData");

        using (ProvisioningServiceClient provisioningServiceClient =
                ProvisioningServiceClient.CreateFromConnectionString(ServiceConnectionString))
        {
            Console.WriteLine("\nCreating a new enrollmentGroup...");

            var certificate = new X509Certificate2(X509RootCertPathVar);

            Attestation attestation = X509Attestation.CreateFromRootCertificates(certificate);

            EnrollmentGroup enrollmentGroup = new EnrollmentGroup(SampleEnrollmentGroupId, attestation);

            Console.WriteLine(enrollmentGroup);
            Console.WriteLine("\nAdding new enrollmentGroup...");

            EnrollmentGroup enrollmentGroupResult =
                await provisioningServiceClient.CreateOrUpdateEnrollmentGroupAsync(enrollmentGroup).ConfigureAwait(false);

            Console.WriteLine("\nEnrollmentGroup created with success.");
            Console.WriteLine(enrollmentGroupResult);
        }
    }
    ```

1. <span data-ttu-id="d96c1-168">Finally, replace the following code to the **Main** method to open the connection to your IoT hub and begin the group enrollment:</span><span class="sxs-lookup"><span data-stu-id="d96c1-168">Finally, replace the following code to the **Main** method to open the connection to your IoT hub and begin the group enrollment:</span></span>
   
    ```csharp
    try
    {
        Console.WriteLine("IoT Device Group Provisioning example");

        SetGroupRegistrationDataAsync().GetAwaiter().GetResult();
            
        Console.WriteLine("Done, hit enter to exit.");
        Console.ReadLine();
    }
    catch (Exception ex)
    {
        Console.WriteLine();
        Console.WriteLine("Error in sample: {0}", ex.Message);
    }
    ```

1. <span data-ttu-id="d96c1-169">Run the .NET device app **DeviceProvisiong**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-169">Run the .NET device app **DeviceProvisiong**.</span></span> <span data-ttu-id="d96c1-170">It should set up group provisioning for the device:</span><span class="sxs-lookup"><span data-stu-id="d96c1-170">It should set up group provisioning for the device:</span></span> 

    ![Group registration run](./media/tutorial-net-provision-device-to-hub/group.png)

    <span data-ttu-id="d96c1-172">When the device group is successfully enrolled, you should see it displayed in the portal as following:</span><span class="sxs-lookup"><span data-stu-id="d96c1-172">When the device group is successfully enrolled, you should see it displayed in the portal as following:</span></span>

   ![Successful group enrollment in the portal](./media/tutorial-net-provision-device-to-hub/group-portal.png)


## <a name="start-the-device"></a><span data-ttu-id="d96c1-174">Start the device</span><span class="sxs-lookup"><span data-stu-id="d96c1-174">Start the device</span></span>

<span data-ttu-id="d96c1-175">At this point, the following setup is ready for device registration:</span><span class="sxs-lookup"><span data-stu-id="d96c1-175">At this point, the following setup is ready for device registration:</span></span>

1. <span data-ttu-id="d96c1-176">Your device or group of devices are enrolled to your Device Provisioning service, and</span><span class="sxs-lookup"><span data-stu-id="d96c1-176">Your device or group of devices are enrolled to your Device Provisioning service, and</span></span> 
2. <span data-ttu-id="d96c1-177">Your device is ready with the security configured and accessible through the application using the Device Provisioning Service client SDK.</span><span class="sxs-lookup"><span data-stu-id="d96c1-177">Your device is ready with the security configured and accessible through the application using the Device Provisioning Service client SDK.</span></span>

<span data-ttu-id="d96c1-178">Start the device to allow your client application to start the registration with your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="d96c1-178">Start the device to allow your client application to start the registration with your Device Provisioning service.</span></span>  


## <a name="verify-the-device-is-registered"></a><span data-ttu-id="d96c1-179">Verify the device is registered</span><span class="sxs-lookup"><span data-stu-id="d96c1-179">Verify the device is registered</span></span>

<span data-ttu-id="d96c1-180">Once your device boots, the following actions should take place.</span><span class="sxs-lookup"><span data-stu-id="d96c1-180">Once your device boots, the following actions should take place.</span></span> <span data-ttu-id="d96c1-181">See the TPM simulator sample application [dps_client_sample](https://github.com/Azure/azure-iot-device-auth/blob/master/dps_client/samples/dps_client_sample/dps_client_sample.c) for more details.</span><span class="sxs-lookup"><span data-stu-id="d96c1-181">See the TPM simulator sample application [dps_client_sample](https://github.com/Azure/azure-iot-device-auth/blob/master/dps_client/samples/dps_client_sample/dps_client_sample.c) for more details.</span></span> 

1. <span data-ttu-id="d96c1-182">The device sends a registration request to your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="d96c1-182">The device sends a registration request to your Device Provisioning service.</span></span>
2. <span data-ttu-id="d96c1-183">For TPM devices, the Device Provisioning Service sends back a registration challenge to which your device responds.</span><span class="sxs-lookup"><span data-stu-id="d96c1-183">For TPM devices, the Device Provisioning Service sends back a registration challenge to which your device responds.</span></span> 
3. <span data-ttu-id="d96c1-184">On successful registration, the Device Provisioning Service sends the IoT hub URI, device ID, and the encrypted key back to the device.</span><span class="sxs-lookup"><span data-stu-id="d96c1-184">On successful registration, the Device Provisioning Service sends the IoT hub URI, device ID, and the encrypted key back to the device.</span></span> 
4. <span data-ttu-id="d96c1-185">The IoT Hub client application on the device then connects to your hub.</span><span class="sxs-lookup"><span data-stu-id="d96c1-185">The IoT Hub client application on the device then connects to your hub.</span></span> 
5. <span data-ttu-id="d96c1-186">On successful connection to the hub, you should see the device appear in the IoT hub's **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d96c1-186">On successful connection to the hub, you should see the device appear in the IoT hub's **Device Explorer**.</span></span> 

    ![Successful connection to hub in the portal](./media/tutorial-net-provision-device-to-hub/hub-connect-success.png)

## <a name="next-steps"></a><span data-ttu-id="d96c1-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="d96c1-188">Next steps</span></span>
<span data-ttu-id="d96c1-189">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="d96c1-189">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d96c1-190">Enroll the device</span><span class="sxs-lookup"><span data-stu-id="d96c1-190">Enroll the device</span></span>
> * <span data-ttu-id="d96c1-191">Start the device</span><span class="sxs-lookup"><span data-stu-id="d96c1-191">Start the device</span></span>
> * <span data-ttu-id="d96c1-192">Verify the device is registered</span><span class="sxs-lookup"><span data-stu-id="d96c1-192">Verify the device is registered</span></span>

<span data-ttu-id="d96c1-193">Advance to the next tutorial to learn how to provision multiple devices across load-balanced hubs.</span><span class="sxs-lookup"><span data-stu-id="d96c1-193">Advance to the next tutorial to learn how to provision multiple devices across load-balanced hubs.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d96c1-194">Provision devices across load-balanced IoT hubs</span><span class="sxs-lookup"><span data-stu-id="d96c1-194">Provision devices across load-balanced IoT hubs</span></span>](./tutorial-provision-multiple-hubs.md)
