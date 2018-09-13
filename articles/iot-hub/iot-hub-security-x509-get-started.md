---
title: Tutorial for X.509 security in Azure IoT Hub | Microsoft Docs
description: Get started on the X.509 based security in your Azure IoT hub in a simulated environment.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 10/10/2017
ms.author: dobett
ms.openlocfilehash: 19f6f5d360981c743d819da81eb2f68db1853c8b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871676"
---
# <a name="set-up-x509-security-in-your-azure-iot-hub"></a><span data-ttu-id="d0add-103">Set up X.509 security in your Azure IoT hub</span><span class="sxs-lookup"><span data-stu-id="d0add-103">Set up X.509 security in your Azure IoT hub</span></span>

<span data-ttu-id="d0add-104">This tutorial simulates the steps you need to secure your Azure IoT hub using the *X.509 Certificate Authentication*.</span><span class="sxs-lookup"><span data-stu-id="d0add-104">This tutorial simulates the steps you need to secure your Azure IoT hub using the *X.509 Certificate Authentication*.</span></span> <span data-ttu-id="d0add-105">For the purpose of illustration, we will show how to use the open source tool OpenSSL to create certificates locally on your Windows machine.</span><span class="sxs-lookup"><span data-stu-id="d0add-105">For the purpose of illustration, we will show how to use the open source tool OpenSSL to create certificates locally on your Windows machine.</span></span> <span data-ttu-id="d0add-106">We recommend that you use this tutorial for test purposes only.</span><span class="sxs-lookup"><span data-stu-id="d0add-106">We recommend that you use this tutorial for test purposes only.</span></span> <span data-ttu-id="d0add-107">For production environment, you should purchase the certificates from a *root certificate authority (CA)*.</span><span class="sxs-lookup"><span data-stu-id="d0add-107">For production environment, you should purchase the certificates from a *root certificate authority (CA)*.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d0add-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0add-108">Prerequisites</span></span>
<span data-ttu-id="d0add-109">This tutorial requires that you have the following resources ready:</span><span class="sxs-lookup"><span data-stu-id="d0add-109">This tutorial requires that you have the following resources ready:</span></span>

- <span data-ttu-id="d0add-110">You have created an IoT hub with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d0add-110">You have created an IoT hub with your Azure subscription.</span></span> <span data-ttu-id="d0add-111">See [Create an IoT hub through portal](iot-hub-create-through-portal.md) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="d0add-111">See [Create an IoT hub through portal](iot-hub-create-through-portal.md) for detailed steps.</span></span> 
- <span data-ttu-id="d0add-112">You have [Visual Studio 2015 or Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="d0add-112">You have [Visual Studio 2015 or Visual Studio 2017](https://www.visualstudio.com/vs/) installed on your machine.</span></span> 

<a id="getcerts"></a>

## <a name="get-x509-ca-certificates"></a><span data-ttu-id="d0add-113">Get X.509 CA certificates</span><span class="sxs-lookup"><span data-stu-id="d0add-113">Get X.509 CA certificates</span></span>
<span data-ttu-id="d0add-114">The X.509 certificate-based security in the IoT Hub requires you to start with an [X.509 certificate chain](https://en.wikipedia.org/wiki/X.509#Certificate_chains_and_cross-certification), which includes the root certificate as well as any intermediate certificates up until the leaf certificate.</span><span class="sxs-lookup"><span data-stu-id="d0add-114">The X.509 certificate-based security in the IoT Hub requires you to start with an [X.509 certificate chain](https://en.wikipedia.org/wiki/X.509#Certificate_chains_and_cross-certification), which includes the root certificate as well as any intermediate certificates up until the leaf certificate.</span></span> 

<span data-ttu-id="d0add-115">You may choose either of the following ways to get your certificates:</span><span class="sxs-lookup"><span data-stu-id="d0add-115">You may choose either of the following ways to get your certificates:</span></span>
- <span data-ttu-id="d0add-116">Purchase X.509 certificates from a *root certificate authority (CA)*.</span><span class="sxs-lookup"><span data-stu-id="d0add-116">Purchase X.509 certificates from a *root certificate authority (CA)*.</span></span> <span data-ttu-id="d0add-117">This is recommended for production environments.</span><span class="sxs-lookup"><span data-stu-id="d0add-117">This is recommended for production environments.</span></span>
<span data-ttu-id="d0add-118">OR,</span><span class="sxs-lookup"><span data-stu-id="d0add-118">OR,</span></span>
- <span data-ttu-id="d0add-119">Create your own X.509 certificates using a third party tool such as [OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="d0add-119">Create your own X.509 certificates using a third party tool such as [OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="d0add-120">This will be fine for test and development purposes.</span><span class="sxs-lookup"><span data-stu-id="d0add-120">This will be fine for test and development purposes.</span></span> <span data-ttu-id="d0add-121">See [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) for information about generating test CA certificates using PowerShell or Bash.</span><span class="sxs-lookup"><span data-stu-id="d0add-121">See [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) for information about generating test CA certificates using PowerShell or Bash.</span></span> <span data-ttu-id="d0add-122">The rest of this tutorial uses test CA certificates generated by following the instructions in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span><span class="sxs-lookup"><span data-stu-id="d0add-122">The rest of this tutorial uses test CA certificates generated by following the instructions in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span></span>


<a id="registercerts"></a>

## <a name="register-x509-ca-certificates-to-your-iot-hub"></a><span data-ttu-id="d0add-123">Register X.509 CA certificates to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="d0add-123">Register X.509 CA certificates to your IoT hub</span></span>

<span data-ttu-id="d0add-124">These steps show you how to add a new Certificate Authority to your IoT hub through the portal.</span><span class="sxs-lookup"><span data-stu-id="d0add-124">These steps show you how to add a new Certificate Authority to your IoT hub through the portal.</span></span>

1. <span data-ttu-id="d0add-125">In the Azure portal, navigate to your IoT hub and open the **SETTINGS** > **Certificates** menu.</span><span class="sxs-lookup"><span data-stu-id="d0add-125">In the Azure portal, navigate to your IoT hub and open the **SETTINGS** > **Certificates** menu.</span></span> 
2. <span data-ttu-id="d0add-126">Click **Add** to add a new certificate.</span><span class="sxs-lookup"><span data-stu-id="d0add-126">Click **Add** to add a new certificate.</span></span>
3. <span data-ttu-id="d0add-127">Enter a friendly display name to your certificate.</span><span class="sxs-lookup"><span data-stu-id="d0add-127">Enter a friendly display name to your certificate.</span></span> <span data-ttu-id="d0add-128">Select the root certificate file named *RootCA.cer* created in the previous section, from your machine.</span><span class="sxs-lookup"><span data-stu-id="d0add-128">Select the root certificate file named *RootCA.cer* created in the previous section, from your machine.</span></span> <span data-ttu-id="d0add-129">Click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="d0add-129">Click **Upload**.</span></span>
4. <span data-ttu-id="d0add-130">Once you get a notification that your certificate is successfully uploaded, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d0add-130">Once you get a notification that your certificate is successfully uploaded, click **Save**.</span></span>

    ![Upload certificate](./media/iot-hub-security-x509-get-started/add-new-cert.png)  

   <span data-ttu-id="d0add-132">This will show your certificate in the **Certificate Explorer** list.</span><span class="sxs-lookup"><span data-stu-id="d0add-132">This will show your certificate in the **Certificate Explorer** list.</span></span> <span data-ttu-id="d0add-133">Note the **STATUS** of this certificate is *Unverified*.</span><span class="sxs-lookup"><span data-stu-id="d0add-133">Note the **STATUS** of this certificate is *Unverified*.</span></span>

5. <span data-ttu-id="d0add-134">Click on the certificate that you added in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d0add-134">Click on the certificate that you added in the previous step.</span></span>

6. <span data-ttu-id="d0add-135">In the **Certificate Details** blade, click **Generate Verification Code**.</span><span class="sxs-lookup"><span data-stu-id="d0add-135">In the **Certificate Details** blade, click **Generate Verification Code**.</span></span>

7. <span data-ttu-id="d0add-136">It creates a **Verification Code** to validate the certificate ownership.</span><span class="sxs-lookup"><span data-stu-id="d0add-136">It creates a **Verification Code** to validate the certificate ownership.</span></span> <span data-ttu-id="d0add-137">Copy the code to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="d0add-137">Copy the code to your clipboard.</span></span> 

   ![Verify certificate](./media/iot-hub-security-x509-get-started/verify-cert.png)  

8. <span data-ttu-id="d0add-139">Now, you need to sign this *Verification Code* with the private key associate with your X.509 CA certificate, which generates a signature.</span><span class="sxs-lookup"><span data-stu-id="d0add-139">Now, you need to sign this *Verification Code* with the private key associate with your X.509 CA certificate, which generates a signature.</span></span> <span data-ttu-id="d0add-140">There are tools available to perform this signing process, for example, OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="d0add-140">There are tools available to perform this signing process, for example, OpenSSL.</span></span> <span data-ttu-id="d0add-141">This is known as the [Proof of possession](https://tools.ietf.org/html/rfc5280#section-3.1).</span><span class="sxs-lookup"><span data-stu-id="d0add-141">This is known as the [Proof of possession](https://tools.ietf.org/html/rfc5280#section-3.1).</span></span> <span data-ttu-id="d0add-142">Step 3 in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) generates a verification code.</span><span class="sxs-lookup"><span data-stu-id="d0add-142">Step 3 in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) generates a verification code.</span></span>
 
9. <span data-ttu-id="d0add-143">Upload the resulting signature from step 8 above to your IoT hub in the portal.</span><span class="sxs-lookup"><span data-stu-id="d0add-143">Upload the resulting signature from step 8 above to your IoT hub in the portal.</span></span> <span data-ttu-id="d0add-144">In the **Certificate Details** blade on the Azure portal, navigate to the **Verification Certificate .pem or .cer file**, and select the signature, for example, *VerifyCert4.cer* created by the sample PowerShell command using the _File Explorer_ icon besides it.</span><span class="sxs-lookup"><span data-stu-id="d0add-144">In the **Certificate Details** blade on the Azure portal, navigate to the **Verification Certificate .pem or .cer file**, and select the signature, for example, *VerifyCert4.cer* created by the sample PowerShell command using the _File Explorer_ icon besides it.</span></span>

10. <span data-ttu-id="d0add-145">Once the certificate is successfuly uploaded, click **Verify**.</span><span class="sxs-lookup"><span data-stu-id="d0add-145">Once the certificate is successfuly uploaded, click **Verify**.</span></span> <span data-ttu-id="d0add-146">The **STATUS** of your certificate changes to **_Verified_** in the **Certificates** blade.</span><span class="sxs-lookup"><span data-stu-id="d0add-146">The **STATUS** of your certificate changes to **_Verified_** in the **Certificates** blade.</span></span> <span data-ttu-id="d0add-147">Click **Refresh** if it does not update automatically.</span><span class="sxs-lookup"><span data-stu-id="d0add-147">Click **Refresh** if it does not update automatically.</span></span>

   ![Upload certificate verification](./media/iot-hub-security-x509-get-started/upload-cert-verification.png)  


<a id="createdevice"></a>

## <a name="create-an-x509-device-for-your-iot-hub"></a><span data-ttu-id="d0add-149">Create an X.509 device for your IoT hub</span><span class="sxs-lookup"><span data-stu-id="d0add-149">Create an X.509 device for your IoT hub</span></span>

1. <span data-ttu-id="d0add-150">In the Azure portal, navigate to your IoT hub's **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d0add-150">In the Azure portal, navigate to your IoT hub's **Device Explorer**.</span></span>

2. <span data-ttu-id="d0add-151">Click **Add** to add a new device.</span><span class="sxs-lookup"><span data-stu-id="d0add-151">Click **Add** to add a new device.</span></span> 

3. <span data-ttu-id="d0add-152">Give a friendly display name for the **Device ID**, and select **_X.509 CA Signed_** as the **Authentication Type**.</span><span class="sxs-lookup"><span data-stu-id="d0add-152">Give a friendly display name for the **Device ID**, and select **_X.509 CA Signed_** as the **Authentication Type**.</span></span> <span data-ttu-id="d0add-153">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d0add-153">Click **Save**.</span></span>

   ![Create X.509 device in portal](./media/iot-hub-security-x509-get-started/create-x509-device.png)



<a id="authenticatedevice"></a>

## <a name="authenticate-your-x509-device-with-the-x509-certificates"></a><span data-ttu-id="d0add-155">Authenticate your X.509 device with the X.509 certificates</span><span class="sxs-lookup"><span data-stu-id="d0add-155">Authenticate your X.509 device with the X.509 certificates</span></span>

<span data-ttu-id="d0add-156">To authenticate your X.509 device, you need to first sign the device with the CA certificate.</span><span class="sxs-lookup"><span data-stu-id="d0add-156">To authenticate your X.509 device, you need to first sign the device with the CA certificate.</span></span> <span data-ttu-id="d0add-157">Signing of leaf devices is normally done at the manufacturing plant, where manufacturing tools have been enabled accordingly.</span><span class="sxs-lookup"><span data-stu-id="d0add-157">Signing of leaf devices is normally done at the manufacturing plant, where manufacturing tools have been enabled accordingly.</span></span> <span data-ttu-id="d0add-158">As the device goes from one manufacturer to another, each manufacturer’s signing action is captured as an intermediate certificate within the chain.</span><span class="sxs-lookup"><span data-stu-id="d0add-158">As the device goes from one manufacturer to another, each manufacturer’s signing action is captured as an intermediate certificate within the chain.</span></span> <span data-ttu-id="d0add-159">The end result is a certificate chain from the CA certificate to the device’s leaf certificate.</span><span class="sxs-lookup"><span data-stu-id="d0add-159">The end result is a certificate chain from the CA certificate to the device’s leaf certificate.</span></span> <span data-ttu-id="d0add-160">Step 4 in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) generates a device certificate.</span><span class="sxs-lookup"><span data-stu-id="d0add-160">Step 4 in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) generates a device certificate.</span></span>

<span data-ttu-id="d0add-161">Next, we will show you how to create a C# application to simulate the X.509 device registered for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d0add-161">Next, we will show you how to create a C# application to simulate the X.509 device registered for your IoT hub.</span></span> <span data-ttu-id="d0add-162">We will send temperature and humidity values from the simulated device to your hub.</span><span class="sxs-lookup"><span data-stu-id="d0add-162">We will send temperature and humidity values from the simulated device to your hub.</span></span> <span data-ttu-id="d0add-163">Note that in this tutorial, we will create only the device application.</span><span class="sxs-lookup"><span data-stu-id="d0add-163">Note that in this tutorial, we will create only the device application.</span></span> <span data-ttu-id="d0add-164">It is left as an exercise to the readers to create the IoT Hub service application that will send response to the events sent by this simulated device.</span><span class="sxs-lookup"><span data-stu-id="d0add-164">It is left as an exercise to the readers to create the IoT Hub service application that will send response to the events sent by this simulated device.</span></span> <span data-ttu-id="d0add-165">The C# application assumes that you have followed the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span><span class="sxs-lookup"><span data-stu-id="d0add-165">The C# application assumes that you have followed the steps in [Managing test CA certificates for samples and tutorials](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md).</span></span>

1. <span data-ttu-id="d0add-166">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the Console Application project template.</span><span class="sxs-lookup"><span data-stu-id="d0add-166">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the Console Application project template.</span></span> <span data-ttu-id="d0add-167">Name the project **SimulateX509Device**.</span><span class="sxs-lookup"><span data-stu-id="d0add-167">Name the project **SimulateX509Device**.</span></span>
   <span data-ttu-id="d0add-168">![Create X.509 device project in Visual Studio](./media/iot-hub-security-x509-get-started/create-device-project.png)</span><span class="sxs-lookup"><span data-stu-id="d0add-168">![Create X.509 device project in Visual Studio](./media/iot-hub-security-x509-get-started/create-device-project.png)</span></span>

2. <span data-ttu-id="d0add-169">In Solution Explorer, right-click the **SimulateX509Device** project, and then click **Manage NuGet Packages...**. In the NuGet Package Manager window, select **Browse** and search for **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="d0add-169">In Solution Explorer, right-click the **SimulateX509Device** project, and then click **Manage NuGet Packages...**. In the NuGet Package Manager window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="d0add-170">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="d0add-170">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="d0add-171">This procedure downloads, installs, and adds a reference to the Azure IoT device SDK NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="d0add-171">This procedure downloads, installs, and adds a reference to the Azure IoT device SDK NuGet package and its dependencies.</span></span>
   <span data-ttu-id="d0add-172">![Add device SDK NuGet package in Visual Studio](./media/iot-hub-security-x509-get-started/device-sdk-nuget.png)</span><span class="sxs-lookup"><span data-stu-id="d0add-172">![Add device SDK NuGet package in Visual Studio](./media/iot-hub-security-x509-get-started/device-sdk-nuget.png)</span></span>

3. <span data-ttu-id="d0add-173">Add the following lines of code at the top of the *Program.cs* file:</span><span class="sxs-lookup"><span data-stu-id="d0add-173">Add the following lines of code at the top of the *Program.cs* file:</span></span>
    
    ```CSharp
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using System.Security.Cryptography.X509Certificates;
    ```

4. <span data-ttu-id="d0add-174">Add the following lines of code inside the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="d0add-174">Add the following lines of code inside the **Program** class:</span></span>
    
    ```CSharp
        private static int MESSAGE_COUNT = 5;
        private const int TEMPERATURE_THRESHOLD = 30;
        private static String deviceId = "<your-device-id>";
        private static float temperature;
        private static float humidity;
        private static Random rnd = new Random();
    ```
   <span data-ttu-id="d0add-175">Use the friendly device name you used in the preceding section in place of _<your_device_id>_ placeholder.</span><span class="sxs-lookup"><span data-stu-id="d0add-175">Use the friendly device name you used in the preceding section in place of _<your_device_id>_ placeholder.</span></span>

5. <span data-ttu-id="d0add-176">Add the following function to create random numbers for temperature and humidity and send these values to the hub:</span><span class="sxs-lookup"><span data-stu-id="d0add-176">Add the following function to create random numbers for temperature and humidity and send these values to the hub:</span></span>
    ```CSharp
    static async Task SendEvent(DeviceClient deviceClient)
    {
        string dataBuffer;
        Console.WriteLine("Device sending {0} messages to IoTHub...\n", MESSAGE_COUNT);

        for (int count = 0; count < MESSAGE_COUNT; count++)
        {
            temperature = rnd.Next(20, 35);
            humidity = rnd.Next(60, 80);
            dataBuffer = string.Format("{{\"deviceId\":\"{0}\",\"messageId\":{1},\"temperature\":{2},\"humidity\":{3}}}", deviceId, count, temperature, humidity);
            Message eventMessage = new Message(Encoding.UTF8.GetBytes(dataBuffer));
            eventMessage.Properties.Add("temperatureAlert", (temperature > TEMPERATURE_THRESHOLD) ? "true" : "false");
            Console.WriteLine("\t{0}> Sending message: {1}, Data: [{2}]", DateTime.Now.ToLocalTime(), count, dataBuffer);

            await deviceClient.SendEventAsync(eventMessage);
        }
    }
    ```

6. <span data-ttu-id="d0add-177">Finally, add the following lines of code to the **Main** function, replacing the placeholders _device-id_, _your-iot-hub-name_ and _absolute-path-to-your-device-pfx-file_ as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="d0add-177">Finally, add the following lines of code to the **Main** function, replacing the placeholders _device-id_, _your-iot-hub-name_ and _absolute-path-to-your-device-pfx-file_ as required by your setup.</span></span>
    ```CSharp
    try
    {
        var cert = new X509Certificate2(@"<absolute-path-to-your-device-pfx-file>", "1234");
        var auth = new DeviceAuthenticationWithX509Certificate("<device-id>", cert);
        var deviceClient = DeviceClient.Create("<your-iot-hub-name>.azure-devices.net", auth, TransportType.Amqp_Tcp_Only);

        if (deviceClient == null)
        {
            Console.WriteLine("Failed to create DeviceClient!");
        }
        else
        {
            Console.WriteLine("Successfully created DeviceClient!");
            SendEvent(deviceClient).Wait();
        }

        Console.WriteLine("Exiting...\n");
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error in sample: {0}", ex.Message);
    }
    ```
   <span data-ttu-id="d0add-178">This code connects to your IoT hub by creating the connection string for your X.509 device.</span><span class="sxs-lookup"><span data-stu-id="d0add-178">This code connects to your IoT hub by creating the connection string for your X.509 device.</span></span> <span data-ttu-id="d0add-179">Once successfully connected, it then sends temperature and humidity events to the hub, and waits for its response.</span><span class="sxs-lookup"><span data-stu-id="d0add-179">Once successfully connected, it then sends temperature and humidity events to the hub, and waits for its response.</span></span> 
7. <span data-ttu-id="d0add-180">Since this application accesses a *.pfx* file, you may need to execute this in *Admin* mode.</span><span class="sxs-lookup"><span data-stu-id="d0add-180">Since this application accesses a *.pfx* file, you may need to execute this in *Admin* mode.</span></span> <span data-ttu-id="d0add-181">Build the Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="d0add-181">Build the Visual Studio solution.</span></span> <span data-ttu-id="d0add-182">Open a new command window as an **Administrator**, and navigate to the folder containing this solution.</span><span class="sxs-lookup"><span data-stu-id="d0add-182">Open a new command window as an **Administrator**, and navigate to the folder containing this solution.</span></span> <span data-ttu-id="d0add-183">Navigate to the *bin/Debug* path within the solution folder.</span><span class="sxs-lookup"><span data-stu-id="d0add-183">Navigate to the *bin/Debug* path within the solution folder.</span></span> <span data-ttu-id="d0add-184">Run the application **SimulateX509Device.exe** from the _Admin_ command window.</span><span class="sxs-lookup"><span data-stu-id="d0add-184">Run the application **SimulateX509Device.exe** from the _Admin_ command window.</span></span> <span data-ttu-id="d0add-185">You should see your device successfully connecting to the hub and sending the events.</span><span class="sxs-lookup"><span data-stu-id="d0add-185">You should see your device successfully connecting to the hub and sending the events.</span></span> 
   <span data-ttu-id="d0add-186">![Run device app](./media/iot-hub-security-x509-get-started/device-app-success.png)</span><span class="sxs-lookup"><span data-stu-id="d0add-186">![Run device app](./media/iot-hub-security-x509-get-started/device-app-success.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="d0add-187">See also</span><span class="sxs-lookup"><span data-stu-id="d0add-187">See also</span></span>
<span data-ttu-id="d0add-188">To learn more about securing your IoT solution, see:</span><span class="sxs-lookup"><span data-stu-id="d0add-188">To learn more about securing your IoT solution, see:</span></span>

* <span data-ttu-id="d0add-189">[IoT Security Best Practices][lnk-security-best-practices]</span><span class="sxs-lookup"><span data-stu-id="d0add-189">[IoT Security Best Practices][lnk-security-best-practices]</span></span>
* <span data-ttu-id="d0add-190">[IoT Security Architecture][lnk-security-architecture]</span><span class="sxs-lookup"><span data-stu-id="d0add-190">[IoT Security Architecture][lnk-security-architecture]</span></span>
* <span data-ttu-id="d0add-191">[Secure your IoT deployment][lnk-security-deployment]</span><span class="sxs-lookup"><span data-stu-id="d0add-191">[Secure your IoT deployment][lnk-security-deployment]</span></span>

<span data-ttu-id="d0add-192">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="d0add-192">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d0add-193">[Deploying AI to edge devices with Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d0add-193">[Deploying AI to edge devices with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-security-best-practices]: ../iot-fundamentals/iot-security-best-practices.md
[lnk-security-architecture]: ../iot-fundamentals/iot-security-architecture.md
[lnk-security-deployment]: ../iot-fundamentals/iot-security-deployment.md

[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md
