---
title: This quickstart shows you how to enroll X.509 device to the Azure Device Provisioning Service using C# | Microsoft Docs
description: In this quickstart, you will enroll X.509 devices to the Azure IoT Hub Device Provisioning Service using C#
author: wesmc7777
ms.author: wesmc
ms.date: 01/21/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: cf2a2dfbb46b8958e10431ba61e4bd8bc7ae18d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867300"
---
# <a name="quickstart-enroll-x509-devices-to-the-device-provisioning-service-using-c"></a><span data-ttu-id="e2e3d-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using C#</span><span class="sxs-lookup"><span data-stu-id="e2e3d-103">Quickstart: Enroll X.509 devices to the Device Provisioning Service using C#</span></span>

[!INCLUDE [iot-dps-selector-quick-enroll-device-x509](../../includes/iot-dps-selector-quick-enroll-device-x509.md)]


<span data-ttu-id="e2e3d-104">This quickstart shows how to use C# to programmatically create an [Enrollment group](concepts-service.md#enrollment-group) that uses intermediate or root CA X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-104">This quickstart shows how to use C# to programmatically create an [Enrollment group](concepts-service.md#enrollment-group) that uses intermediate or root CA X.509 certificates.</span></span> <span data-ttu-id="e2e3d-105">The enrollment group is created using the [Microsoft Azure IoT SDK for .NET](https://github.com/Azure/azure-iot-sdk-csharp) and a sample C# .NET Core application.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-105">The enrollment group is created using the [Microsoft Azure IoT SDK for .NET](https://github.com/Azure/azure-iot-sdk-csharp) and a sample C# .NET Core application.</span></span> <span data-ttu-id="e2e3d-106">An enrollment group controls access to the provisioning service for devices that share a common signing certificate in their certificate chain.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-106">An enrollment group controls access to the provisioning service for devices that share a common signing certificate in their certificate chain.</span></span> <span data-ttu-id="e2e3d-107">To learn more, see [Controlling device access to the provisioning service with X.509 certificates](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-107">To learn more, see [Controlling device access to the provisioning service with X.509 certificates](./concepts-security.md#controlling-device-access-to-the-provisioning-service-with-x509-certificates).</span></span> <span data-ttu-id="e2e3d-108">For more information about using X.509 certificate-based Public Key Infrastructure (PKI) with Azure IoT Hub and Device Provisioning Service, see [X.509 CA certificate security overview](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-108">For more information about using X.509 certificate-based Public Key Infrastructure (PKI) with Azure IoT Hub and Device Provisioning Service, see [X.509 CA certificate security overview](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview).</span></span> 

<span data-ttu-id="e2e3d-109">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-109">This quickstart expects you have already created an IoT hub and Device Provisioning Service instance.</span></span> <span data-ttu-id="e2e3d-110">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-110">If you have not already created these resources, complete the [Set up IoT Hub Device Provisioning Service with the Azure portal](./quick-setup-auto-provision.md) quickstart before proceeding with this article.</span></span>

<span data-ttu-id="e2e3d-111">Although the steps in this article work on both Windows and Linux machines, this article is developed for a Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-111">Although the steps in this article work on both Windows and Linux machines, this article is developed for a Windows development machine.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="e2e3d-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e2e3d-112">Prerequisites</span></span>

* <span data-ttu-id="e2e3d-113">Install [Visual Studio 2017](https://www.visualstudio.com/vs/).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-113">Install [Visual Studio 2017](https://www.visualstudio.com/vs/).</span></span>
* <span data-ttu-id="e2e3d-114">Install [.Net Core SDK](https://www.microsoft.com/net/download/windows).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-114">Install [.Net Core SDK](https://www.microsoft.com/net/download/windows).</span></span>
* <span data-ttu-id="e2e3d-115">Install [Git](https://git-scm.com/download/).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-115">Install [Git](https://git-scm.com/download/).</span></span>



## <a name="prepare-test-certificates"></a><span data-ttu-id="e2e3d-116">Prepare test certificates</span><span class="sxs-lookup"><span data-stu-id="e2e3d-116">Prepare test certificates</span></span>

<span data-ttu-id="e2e3d-117">For this quickstart, you must have a .pem or a .cer file that contains the public portion of an intermediate or root CA X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-117">For this quickstart, you must have a .pem or a .cer file that contains the public portion of an intermediate or root CA X.509 certificate.</span></span> <span data-ttu-id="e2e3d-118">This certificate must be uploaded to your provisioning service, and verified by the service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-118">This certificate must be uploaded to your provisioning service, and verified by the service.</span></span> 

<span data-ttu-id="e2e3d-119">The [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) contains test tooling that can help you create an X.509 certificate chain, upload a root or intermediate certificate from that chain, and perform proof-of-possession with the service to verify the certificate.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-119">The [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) contains test tooling that can help you create an X.509 certificate chain, upload a root or intermediate certificate from that chain, and perform proof-of-possession with the service to verify the certificate.</span></span> <span data-ttu-id="e2e3d-120">Certificates created with the SDK tooling are designed to be used for **development testing only**.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-120">Certificates created with the SDK tooling are designed to be used for **development testing only**.</span></span> <span data-ttu-id="e2e3d-121">These certificates **must not be used in production**.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-121">These certificates **must not be used in production**.</span></span> <span data-ttu-id="e2e3d-122">They contain hard-coded passwords ("1234") that expire after 30 days.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-122">They contain hard-coded passwords ("1234") that expire after 30 days.</span></span> <span data-ttu-id="e2e3d-123">To learn about obtaining certificates suitable for production use, see [How to get an X.509 CA certificate](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in the Azure IoT Hub documentation.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-123">To learn about obtaining certificates suitable for production use, see [How to get an X.509 CA certificate](https://docs.microsoft.com/azure/iot-hub/iot-hub-x509ca-overview#how-to-get-an-x509-ca-certificate) in the Azure IoT Hub documentation.</span></span>

<span data-ttu-id="e2e3d-124">To use this test tooling to generate certificates, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2e3d-124">To use this test tooling to generate certificates, perform the following steps:</span></span> 
 
1. <span data-ttu-id="e2e3d-125">Open a command prompt or Git Bash shell, and change to a working folder on your machine.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-125">Open a command prompt or Git Bash shell, and change to a working folder on your machine.</span></span> <span data-ttu-id="e2e3d-126">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span><span class="sxs-lookup"><span data-stu-id="e2e3d-126">Execute the following command to clone the [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) GitHub repository:</span></span>
    
  ```cmd/sh
  git clone https://github.com/Azure/azure-iot-sdk-c.git --recursive
  ```

  <span data-ttu-id="e2e3d-127">The size of this repository is currently around 220 MB.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-127">The size of this repository is currently around 220 MB.</span></span> <span data-ttu-id="e2e3d-128">You should expect this operation to take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-128">You should expect this operation to take several minutes to complete.</span></span>

  <span data-ttu-id="e2e3d-129">The test tooling is located in the *azure-iot-sdk-c/tools/CACertificates* of the repository you cloned.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-129">The test tooling is located in the *azure-iot-sdk-c/tools/CACertificates* of the repository you cloned.</span></span>    

2. <span data-ttu-id="e2e3d-130">Follow the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-130">Follow the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span></span> 

<span data-ttu-id="e2e3d-131">In addition to the tooling in the C SDK, the [Group certificate verification sample](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/provisioning/service/samples/GroupCertificateVerificationSample) in the *Microsoft Azure IoT SDK for .NET* shows how to perform proof-of-possession in C# with an existing X.509 intermediate or root CA certificate.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-131">In addition to the tooling in the C SDK, the [Group certificate verification sample](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/provisioning/service/samples/GroupCertificateVerificationSample) in the *Microsoft Azure IoT SDK for .NET* shows how to perform proof-of-possession in C# with an existing X.509 intermediate or root CA certificate.</span></span> 


## <a name="get-the-connection-string-for-your-provisioning-service"></a><span data-ttu-id="e2e3d-132">Get the connection string for your provisioning service</span><span class="sxs-lookup"><span data-stu-id="e2e3d-132">Get the connection string for your provisioning service</span></span>

<span data-ttu-id="e2e3d-133">For the sample in this quickstart, you need the connection string for your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-133">For the sample in this quickstart, you need the connection string for your provisioning service.</span></span>
1. <span data-ttu-id="e2e3d-134">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-134">Sign in to the Azure portal, click on the **All resources** button on the left-hand menu and open your Device Provisioning Service.</span></span> 
2. <span data-ttu-id="e2e3d-135">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-135">Click **Shared access policies**, then click the access policy you want to use to open its properties.</span></span> <span data-ttu-id="e2e3d-136">In the **Access Policy** window, copy and note down the primary key connection string.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-136">In the **Access Policy** window, copy and note down the primary key connection string.</span></span> 

    ![Get provisioning service connection string from the portal](media/quick-enroll-device-x509-csharp/get-service-connection-string.png)

## <a name="create-the-enrollment-group-sample"></a><span data-ttu-id="e2e3d-138">Create the enrollment group sample</span><span class="sxs-lookup"><span data-stu-id="e2e3d-138">Create the enrollment group sample</span></span> 

<span data-ttu-id="e2e3d-139">The steps in this section show how to create a .NET Core console app that adds an enrollment group to your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-139">The steps in this section show how to create a .NET Core console app that adds an enrollment group to your provisioning service.</span></span> <span data-ttu-id="e2e3d-140">With some modification, you can also follow these steps to create a [Windows IoT Core](https://developer.microsoft.com/en-us/windows/iot) console app to add the enrollment group.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-140">With some modification, you can also follow these steps to create a [Windows IoT Core](https://developer.microsoft.com/en-us/windows/iot) console app to add the enrollment group.</span></span> <span data-ttu-id="e2e3d-141">To learn more about developing with IoT Core, see the [Windows IoT Core developer documentation](https://docs.microsoft.com/windows/iot-core/).</span><span class="sxs-lookup"><span data-stu-id="e2e3d-141">To learn more about developing with IoT Core, see the [Windows IoT Core developer documentation](https://docs.microsoft.com/windows/iot-core/).</span></span>
1. <span data-ttu-id="e2e3d-142">In Visual Studio, add a Visual C# .NET Core Console App project to a new solution by using the **Console App (.NET Core)** project template.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-142">In Visual Studio, add a Visual C# .NET Core Console App project to a new solution by using the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="e2e3d-143">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-143">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="e2e3d-144">Name the project **CreateEnrollmentGroup**.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-144">Name the project **CreateEnrollmentGroup**.</span></span>

    ![New Visual C# Windows Classic Desktop project](media//quick-enroll-device-x509-csharp/create-app.png)

2. <span data-ttu-id="e2e3d-146">In Solution Explorer, right-click the **CreateEnrollmentGroup** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-146">In Solution Explorer, right-click the **CreateEnrollmentGroup** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="e2e3d-147">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Provisioning.Service**, select **Install** to install the **Microsoft.Azure.Devices.Provisioning.Service** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-147">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Provisioning.Service**, select **Install** to install the **Microsoft.Azure.Devices.Provisioning.Service** package, and accept the terms of use.</span></span> <span data-ttu-id="e2e3d-148">This procedure downloads, installs, and adds a reference to the [Azure IoT Provisioning Service Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Provisioning.Service/) NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-148">This procedure downloads, installs, and adds a reference to the [Azure IoT Provisioning Service Client SDK](https://www.nuget.org/packages/Microsoft.Azure.Devices.Provisioning.Service/) NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window](media//quick-enroll-device-x509-csharp/add-nuget.png)

4. <span data-ttu-id="e2e3d-150">Add the following `using` statements after the other `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="e2e3d-150">Add the following `using` statements after the other `using` statements at the top of the **Program.cs** file:</span></span>
   
   ```csharp
   using System.Security.Cryptography.X509Certificates;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Provisioning.Service;
   ```
    
5. <span data-ttu-id="e2e3d-151">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-151">Add the following fields to the **Program** class.</span></span>  
   - <span data-ttu-id="e2e3d-152">Replace the **ProvisioningConnectionString** placeholder value with the connection string of the provisioning service that you want to create the enrollment for.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-152">Replace the **ProvisioningConnectionString** placeholder value with the connection string of the provisioning service that you want to create the enrollment for.</span></span>
   - <span data-ttu-id="e2e3d-153">Replace the **X509RootCertPath** placeholder value with the path to a .pem or .cer file that represents the public part of an intermediate or root CA X.509 certificate that has been previously uploaded and verified with your provisioning service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-153">Replace the **X509RootCertPath** placeholder value with the path to a .pem or .cer file that represents the public part of an intermediate or root CA X.509 certificate that has been previously uploaded and verified with your provisioning service.</span></span>
   - <span data-ttu-id="e2e3d-154">You may optionally change the **EnrollmentGroupId** value.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-154">You may optionally change the **EnrollmentGroupId** value.</span></span> <span data-ttu-id="e2e3d-155">The string can contain only lower case characters and hyphens.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-155">The string can contain only lower case characters and hyphens.</span></span> 

   > [!IMPORTANT]
   > <span data-ttu-id="e2e3d-156">In production code, be aware of the following security considerations:</span><span class="sxs-lookup"><span data-stu-id="e2e3d-156">In production code, be aware of the following security considerations:</span></span>
   >
   > - <span data-ttu-id="e2e3d-157">Hard-coding the connection string for the provisioning service administrator is against security best practices.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-157">Hard-coding the connection string for the provisioning service administrator is against security best practices.</span></span> <span data-ttu-id="e2e3d-158">Instead, the connection string should be held in a secure manner, such as in a secure configuration file or in the registry.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-158">Instead, the connection string should be held in a secure manner, such as in a secure configuration file or in the registry.</span></span>
   > - <span data-ttu-id="e2e3d-159">Be sure to upload only the public part of the signing certificate.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-159">Be sure to upload only the public part of the signing certificate.</span></span> <span data-ttu-id="e2e3d-160">Never upload .pfx (PKCS12) or .pem files containing private keys to the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-160">Never upload .pfx (PKCS12) or .pem files containing private keys to the provisioning service.</span></span>
        
   ```csharp
   private static string ProvisioningConnectionString = "{Your provisioning service connection string}";
   private static string EnrollmentGroupId = "enrollmentgrouptest";
   private static string X509RootCertPath = @"{Path to a .cer or .pem file for a verified root CA or intermediate CA X.509 certificate}";
   ```
    
6. <span data-ttu-id="e2e3d-161">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-161">Add the following method to the **Program** class.</span></span> <span data-ttu-id="e2e3d-162">This code creates an enrollment group entry and then calls the **CreateOrUpdateEnrollmentGroupAsync** method on the **ProvisioningServiceClient** to add the enrollment group to the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-162">This code creates an enrollment group entry and then calls the **CreateOrUpdateEnrollmentGroupAsync** method on the **ProvisioningServiceClient** to add the enrollment group to the provisioning service.</span></span>
   
   ```csharp
   public static async Task RunSample()
   {
       Console.WriteLine("Starting sample...");
 
       using (ProvisioningServiceClient provisioningServiceClient =
               ProvisioningServiceClient.CreateFromConnectionString(ProvisioningConnectionString))
       {
           #region Create a new enrollmentGroup config
           Console.WriteLine("\nCreating a new enrollmentGroup...");
           var certificate = new X509Certificate2(X509RootCertPath);
           Attestation attestation = X509Attestation.CreateFromRootCertificates(certificate);
           EnrollmentGroup enrollmentGroup =
                   new EnrollmentGroup(
                           EnrollmentGroupId,
                           attestation)
                   {
                       ProvisioningStatus = ProvisioningStatus.Enabled
                   };
           Console.WriteLine(enrollmentGroup);
           #endregion
 
           #region Create the enrollmentGroup
           Console.WriteLine("\nAdding new enrollmentGroup...");
           EnrollmentGroup enrollmentGroupResult =
               await provisioningServiceClient.CreateOrUpdateEnrollmentGroupAsync(enrollmentGroup).ConfigureAwait(false);
           Console.WriteLine("\nEnrollmentGroup created with success.");
           Console.WriteLine(enrollmentGroupResult);
           #endregion
 
       }
   }
   ```

7. <span data-ttu-id="e2e3d-163">Finally, replace the body of the **Main** method with the following lines:</span><span class="sxs-lookup"><span data-stu-id="e2e3d-163">Finally, replace the body of the **Main** method with the following lines:</span></span>
   
   ```csharp
   RunSample().GetAwaiter().GetResult();
   Console.WriteLine("\nHit <Enter> to exit ...");
   Console.ReadLine();
   ```
        
8. <span data-ttu-id="e2e3d-164">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-164">Build the solution.</span></span>

## <a name="run-the-enrollment-group-sample"></a><span data-ttu-id="e2e3d-165">Run the enrollment group sample</span><span class="sxs-lookup"><span data-stu-id="e2e3d-165">Run the enrollment group sample</span></span>
  
1. <span data-ttu-id="e2e3d-166">Run the sample in Visual Studio to create the enrollment group.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-166">Run the sample in Visual Studio to create the enrollment group.</span></span>
 
2. <span data-ttu-id="e2e3d-167">On successful creation, the command window displays the properties of the new enrollment group.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-167">On successful creation, the command window displays the properties of the new enrollment group.</span></span>

    ![Enrollment properties in the command output](media/quick-enroll-device-x509-csharp/output.png)

3. <span data-ttu-id="e2e3d-169">To verify that the enrollment group has been created, on the Device Provisioning Service summary blade in the Azure portal, select **Manage enrollments**, then select the **Enrollment Groups** tab. You should see a new enrollment entry that corresponds to the registration ID you used in the sample.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-169">To verify that the enrollment group has been created, on the Device Provisioning Service summary blade in the Azure portal, select **Manage enrollments**, then select the **Enrollment Groups** tab. You should see a new enrollment entry that corresponds to the registration ID you used in the sample.</span></span> <span data-ttu-id="e2e3d-170">Click the entry to verify the certificate thumbprint and other properties for the entry.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-170">Click the entry to verify the certificate thumbprint and other properties for the entry.</span></span>

    ![Enrollment properties in the portal](media/quick-enroll-device-x509-csharp/verify-enrollment-portal.png)
 
## <a name="clean-up-resources"></a><span data-ttu-id="e2e3d-172">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e2e3d-172">Clean up resources</span></span>
<span data-ttu-id="e2e3d-173">If you plan to explore the C# service sample, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-173">If you plan to explore the C# service sample, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="e2e3d-174">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-174">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="e2e3d-175">Close the C# sample output window on your machine.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-175">Close the C# sample output window on your machine.</span></span>
2. <span data-ttu-id="e2e3d-176">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart and click the **Delete** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-176">Navigate to your Device Provisioning service in the Azure portal, click **Manage enrollments**, and then select the **Enrollment Groups** tab. Select the *Registration ID* for the enrollment entry you created using this Quickstart and click the **Delete** button at the top of the blade.</span></span>  
3. <span data-ttu-id="e2e3d-177">From your Device Provisioning service in the Azure portal, click **Certificates**, click the certificate you uploaded for this Quickstart, and click the **Delete** button at the top of the **Certificate Details** window.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-177">From your Device Provisioning service in the Azure portal, click **Certificates**, click the certificate you uploaded for this Quickstart, and click the **Delete** button at the top of the **Certificate Details** window.</span></span>  
 
## <a name="next-steps"></a><span data-ttu-id="e2e3d-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2e3d-178">Next steps</span></span>
<span data-ttu-id="e2e3d-179">In this Quickstart, you created an enrollment group for an X.509 intermediate or root CA certificate using the Azure IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-179">In this Quickstart, you created an enrollment group for an X.509 intermediate or root CA certificate using the Azure IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="e2e3d-180">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e2e3d-180">To learn about device provisioning in depth, continue to the tutorial for the Device Provisioning Service setup in the Azure portal.</span></span> 
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="e2e3d-181">Azure IoT Hub Device Provisioning Service tutorials</span><span class="sxs-lookup"><span data-stu-id="e2e3d-181">Azure IoT Hub Device Provisioning Service tutorials</span></span>](./tutorial-set-up-cloud.md)
