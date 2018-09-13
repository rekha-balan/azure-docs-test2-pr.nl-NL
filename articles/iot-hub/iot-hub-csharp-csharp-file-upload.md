---
title: Upload files from devices using Azure IoT Hub | Microsoft Docs
description: How to upload files from a device to the cloud using Azure IoT device SDK for .NET. Uploaded files are stored in an Azure storage blob container.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: ''
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/08/2017
ms.author: elioda
ms.openlocfilehash: 30341e1df83c806e79377e82c50a3214ade1ff18
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661258"
---
# <a name="upload-files-from-your-simulated-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="671f7-104">Upload files from your simulated device to the cloud with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="671f7-104">Upload files from your simulated device to the cloud with IoT Hub</span></span>
## <a name="introduction"></a><span data-ttu-id="671f7-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="671f7-105">Introduction</span></span>
<span data-ttu-id="671f7-106">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="671f7-106">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="671f7-107">The ([Get started with IoT Hub] and [Send Cloud-to-Device messages with IoT Hub]) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-107">The ([Get started with IoT Hub] and [Send Cloud-to-Device messages with IoT Hub]) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="671f7-108">The [Process Device-to-Cloud messages] tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="671f7-108">The [Process Device-to-Cloud messages] tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="671f7-109">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span><span class="sxs-lookup"><span data-stu-id="671f7-109">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="671f7-110">For example, large files that contain images, videos, vibration data sampled at high frequency, or some form of preprocessed data.</span><span class="sxs-lookup"><span data-stu-id="671f7-110">For example, large files that contain images, videos, vibration data sampled at high frequency, or some form of preprocessed data.</span></span> <span data-ttu-id="671f7-111">These files are typically batch processed in the cloud using tools such as [Azure Data Factory] or the [Hadoop] stack.</span><span class="sxs-lookup"><span data-stu-id="671f7-111">These files are typically batch processed in the cloud using tools such as [Azure Data Factory] or the [Hadoop] stack.</span></span> <span data-ttu-id="671f7-112">When file uploads from a device are preferred to sending events, you can still use IoT Hub security and reliability functionality.</span><span class="sxs-lookup"><span data-stu-id="671f7-112">When file uploads from a device are preferred to sending events, you can still use IoT Hub security and reliability functionality.</span></span>

<span data-ttu-id="671f7-113">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub] tutorial to show you how to use the file upload capabilities of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-113">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub] tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="671f7-114">It shows you how to:</span><span class="sxs-lookup"><span data-stu-id="671f7-114">It shows you how to:</span></span>

- <span data-ttu-id="671f7-115">Securely provide a device with an Azure blob URI for uploading a file.</span><span class="sxs-lookup"><span data-stu-id="671f7-115">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="671f7-116">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span><span class="sxs-lookup"><span data-stu-id="671f7-116">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="671f7-117">At the end of this tutorial you run two .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="671f7-117">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="671f7-118">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="671f7-118">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="671f7-119">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-119">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="671f7-120">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-120">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="671f7-121">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="671f7-121">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="671f7-122">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-122">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>
> 
> 

<span data-ttu-id="671f7-123">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="671f7-123">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="671f7-124">Visual Studio 2015 or Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="671f7-124">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="671f7-125">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="671f7-125">An active Azure account.</span></span> <span data-ttu-id="671f7-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="671f7-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="associate-an-azure-storage-account-to-iot-hub"></a><span data-ttu-id="671f7-127">Associate an Azure Storage account to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="671f7-127">Associate an Azure Storage account to IoT Hub</span></span>
<span data-ttu-id="671f7-128">Because the simulated device app uploads a file to a blob, you must have an [Azure Storage] account associated to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-128">Because the simulated device app uploads a file to a blob, you must have an [Azure Storage] account associated to IoT Hub.</span></span> <span data-ttu-id="671f7-129">When you associate an Azure Storage account with an IoT hub, the IoT hub generates a SAS URI.</span><span class="sxs-lookup"><span data-stu-id="671f7-129">When you associate an Azure Storage account with an IoT hub, the IoT hub generates a SAS URI.</span></span> <span data-ttu-id="671f7-130">A device can use this SAS URI to securely upload a file to a blob container.</span><span class="sxs-lookup"><span data-stu-id="671f7-130">A device can use this SAS URI to securely upload a file to a blob container.</span></span> <span data-ttu-id="671f7-131">The IoT Hub service and the device SDKs coordinate the process that generates the SAS URI and makes it available to a device to use to upload a file.</span><span class="sxs-lookup"><span data-stu-id="671f7-131">The IoT Hub service and the device SDKs coordinate the process that generates the SAS URI and makes it available to a device to use to upload a file.</span></span>

<span data-ttu-id="671f7-132">Follow the instructions in [Configure file uploads using the Azure portal][lnk-configure-upload] to associate an Azure Storage account to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-132">Follow the instructions in [Configure file uploads using the Azure portal][lnk-configure-upload] to associate an Azure Storage account to your IoT hub.</span></span> <span data-ttu-id="671f7-133">Make sure that a blob container is associated with your IoT hub and the file notifications are enabled.</span><span class="sxs-lookup"><span data-stu-id="671f7-133">Make sure that a blob container is associated with your IoT hub and the file notifications are enabled.</span></span> 
   
![Enable File Notifications in portal][3]


## <a name="upload-a-file-from-a-simulated-device-app"></a><span data-ttu-id="671f7-135">Upload a file from a simulated device app</span><span class="sxs-lookup"><span data-stu-id="671f7-135">Upload a file from a simulated device app</span></span>
<span data-ttu-id="671f7-136">In this section, you modify the simulated device app you created in [Send Cloud-to-Device messages with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-136">In this section, you modify the simulated device app you created in [Send Cloud-to-Device messages with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="671f7-137">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="671f7-137">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="671f7-138">Navigate to an image file and include it in your project.</span><span class="sxs-lookup"><span data-stu-id="671f7-138">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="671f7-139">This tutorial assumes the image is named `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="671f7-139">This tutorial assumes the image is named `image.jpg`.</span></span>
2. <span data-ttu-id="671f7-140">Right-click on the image, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="671f7-140">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="671f7-141">Make sure that **Copy to Output Directory** is set to **Copy always**.</span><span class="sxs-lookup"><span data-stu-id="671f7-141">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>
   
    ![][1]
3. <span data-ttu-id="671f7-142">In the **Program.cs** file, add the following statements at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="671f7-142">In the **Program.cs** file, add the following statements at the top of the file:</span></span>
   
        using System.IO;
4. <span data-ttu-id="671f7-143">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="671f7-143">Add the following method to the **Program** class:</span></span>
   
        private static async void SendToBlobAsync()
        {
            string fileName = "image.jpg";
            Console.WriteLine("Uploading file: {0}", fileName);
            var watch = System.Diagnostics.Stopwatch.StartNew();
   
            using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
            {
                await deviceClient.UploadToBlobAsync(fileName, sourceData);
            }
   
            watch.Stop();
            Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
        }
   
    <span data-ttu-id="671f7-144">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span><span class="sxs-lookup"><span data-stu-id="671f7-144">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="671f7-145">The console app displays the time it takes to upload the file.</span><span class="sxs-lookup"><span data-stu-id="671f7-145">The console app displays the time it takes to upload the file.</span></span>
5. <span data-ttu-id="671f7-146">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span><span class="sxs-lookup"><span data-stu-id="671f7-146">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        SendToBlobAsync();

> [!NOTE]
> <span data-ttu-id="671f7-147">For simplicity's sake, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="671f7-147">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="671f7-148">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="671f7-148">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="671f7-149">Receive a file upload notification</span><span class="sxs-lookup"><span data-stu-id="671f7-149">Receive a file upload notification</span></span>
<span data-ttu-id="671f7-150">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="671f7-150">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="671f7-151">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span><span class="sxs-lookup"><span data-stu-id="671f7-151">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="671f7-152">Name the project **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="671f7-152">Name the project **ReadFileUploadNotification**.</span></span>
   
    ![New project in Visual Studio][2]
2. <span data-ttu-id="671f7-154">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="671f7-154">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>
       
3. <span data-ttu-id="671f7-155">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="671f7-155">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="671f7-156">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span><span class="sxs-lookup"><span data-stu-id="671f7-156">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

4. <span data-ttu-id="671f7-157">In the **Program.cs** file, add the following statements at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="671f7-157">In the **Program.cs** file, add the following statements at the top of the file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="671f7-158">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="671f7-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="671f7-159">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="671f7-159">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="671f7-160">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="671f7-160">Add the following method to the **Program** class:</span></span>
   
        private async static Task ReceiveFileUploadNotificationAsync()
        {
            var notificationReceiver = serviceClient.GetFileNotificationReceiver();
   
            Console.WriteLine("\nReceiving file upload notification from service");
            while (true)
            {
                var fileUploadNotification = await notificationReceiver.ReceiveAsync();
                if (fileUploadNotification == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
                Console.ResetColor();
   
                await notificationReceiver.CompleteAsync(fileUploadNotification);
            }
        }
   
    <span data-ttu-id="671f7-161">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span><span class="sxs-lookup"><span data-stu-id="671f7-161">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
7. <span data-ttu-id="671f7-162">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="671f7-162">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Receive file upload notifications\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        ReceiveFileUploadNotificationAsync().Wait();
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="671f7-163">Run the applications</span><span class="sxs-lookup"><span data-stu-id="671f7-163">Run the applications</span></span>
<span data-ttu-id="671f7-164">Now you are ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="671f7-164">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="671f7-165">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="671f7-165">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="671f7-166">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="671f7-166">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>
2. <span data-ttu-id="671f7-167">Press **F5**.</span><span class="sxs-lookup"><span data-stu-id="671f7-167">Press **F5**.</span></span> <span data-ttu-id="671f7-168">Both applications should start.</span><span class="sxs-lookup"><span data-stu-id="671f7-168">Both applications should start.</span></span> <span data-ttu-id="671f7-169">You should see the upload completed in one console app and the upload notification message received by the other console app.</span><span class="sxs-lookup"><span data-stu-id="671f7-169">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="671f7-170">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="671f7-170">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>
   
   ![][50]

## <a name="next-steps"></a><span data-ttu-id="671f7-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="671f7-171">Next steps</span></span>
<span data-ttu-id="671f7-172">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span><span class="sxs-lookup"><span data-stu-id="671f7-172">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="671f7-173">You can continue to explore IoT hub features and scenarios with the following articles:</span><span class="sxs-lookup"><span data-stu-id="671f7-173">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="671f7-174">[Create an IoT hub programmatically][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="671f7-174">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="671f7-175">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="671f7-175">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="671f7-176">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="671f7-176">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="671f7-177">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="671f7-177">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="671f7-178">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="671f7-178">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

<!-- Images. -->

[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->

[Azure portal]: https://portal.azure.com/

[Azure Data Factory]: https://azure.microsoft.com/documentation/services/data-factory/
[Hadoop]: https://azure.microsoft.com/documentation/services/hdinsight/

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]: ../storage/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-windows-gateway-sdk-simulated-device.md






