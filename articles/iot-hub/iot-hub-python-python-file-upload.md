---
title: Upload files from devices to Azure IoT Hub with Python | Microsoft Docs
description: How to upload files from a device to the cloud using Azure IoT device SDK for Python. Uploaded files are stored in an Azure storage blob container.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 03/05/2018
ms.author: kgremban
ms.openlocfilehash: eb5e7ce608f434bd880baae4d6780dd5038099f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867256"
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="1f7a1-104">Upload files from your device to the cloud with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1f7a1-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="1f7a1-105">This tutorial follows how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.yml).</span><span class="sxs-lookup"><span data-stu-id="1f7a1-105">This tutorial follows how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.yml).</span></span> <span data-ttu-id="1f7a1-106">The tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="1f7a1-107">Securely provide a storage container for uploading a file.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-107">Securely provide a storage container for uploading a file.</span></span>
- <span data-ttu-id="1f7a1-108">Use the Python client to upload a file through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-108">Use the Python client to upload a file through your IoT hub.</span></span>

<span data-ttu-id="1f7a1-109">The [Get started with IoT Hub](quickstart-send-telemetry-node.md) tutorial demonstrates the basic device-to-cloud messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-109">The [Get started with IoT Hub](quickstart-send-telemetry-node.md) tutorial demonstrates the basic device-to-cloud messaging functionality of IoT Hub.</span></span> <span data-ttu-id="1f7a1-110">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-110">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="1f7a1-111">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-111">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="1f7a1-112">IoT Hub Python SDK currently only supports uploading character-based files such as **.txt** files.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-112">IoT Hub Python SDK currently only supports uploading character-based files such as **.txt** files.</span></span>

<span data-ttu-id="1f7a1-113">At the end of this tutorial you run the Python console app:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-113">At the end of this tutorial you run the Python console app:</span></span>

* <span data-ttu-id="1f7a1-114">**FileUpload.py**, which uploads a file to storage using the Python Device SDK.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-114">**FileUpload.py**, which uploads a file to storage using the Python Device SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="1f7a1-115">IoT Hub supports many device platforms and languages (including C, .NET, Javascript, Python, and Java) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-115">IoT Hub supports many device platforms and languages (including C, .NET, Javascript, Python, and Java) through Azure IoT device SDKs.</span></span> <span data-ttu-id="1f7a1-116">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-116">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="1f7a1-117">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1f7a1-118">[Python 2.x or 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="1f7a1-118">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="1f7a1-119">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-119">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="1f7a1-120">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-120">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="1f7a1-121">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="1f7a1-121">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="1f7a1-122">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-122">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="1f7a1-123">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-123">An active Azure account.</span></span> <span data-ttu-id="1f7a1-124">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="1f7a1-124">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>


[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]


## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="1f7a1-125">Upload a file from a device app</span><span class="sxs-lookup"><span data-stu-id="1f7a1-125">Upload a file from a device app</span></span>

<span data-ttu-id="1f7a1-126">In this section, you create the device app to upload a file to IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-126">In this section, you create the device app to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="1f7a1-127">At your command prompt, run the following command to install the **azure-iothub-device-client** package:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-127">At your command prompt, run the following command to install the **azure-iothub-device-client** package:</span></span>

    ```cmd/sh
    pip install azure-iothub-device-client
    ```

1. <span data-ttu-id="1f7a1-128">Using a text editor, create a **FileUpload.py** file in your working folder.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-128">Using a text editor, create a **FileUpload.py** file in your working folder.</span></span>

1. <span data-ttu-id="1f7a1-129">Add the following `import` statements and variables at the start of the **FileUpload.py** file.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-129">Add the following `import` statements and variables at the start of the **FileUpload.py** file.</span></span> <span data-ttu-id="1f7a1-130">Replace `deviceConnectionString` with the connection string of your IoT hub device:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-130">Replace `deviceConnectionString` with the connection string of your IoT hub device:</span></span>

    ```python
    import time
    import sys
    import iothub_client
    import os
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult, IoTHubError

    CONNECTION_STRING = "[Device Connection String]"
    PROTOCOL = IoTHubTransportProvider.HTTP

    PATHTOFILE = "[Full path to file]"
    FILENAME = "[File name on storage after upload]"
    ```

1. <span data-ttu-id="1f7a1-131">Create a callback for the **upload_blob** function:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-131">Create a callback for the **upload_blob** function:</span></span>

    ```python
    def blob_upload_conf_callback(result, user_context):
        if str(result) == 'OK':
            print ( "...file uploaded successfully." )
        else:
            print ( "...file upload callback returned: " + str(result) )
    ```

1. <span data-ttu-id="1f7a1-132">Add the following code to connect the client and upload the file.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-132">Add the following code to connect the client and upload the file.</span></span> <span data-ttu-id="1f7a1-133">Also include the `main` routine:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-133">Also include the `main` routine:</span></span>

    ```python
    def iothub_file_upload_sample_run():
        try:
            print ( "IoT Hub file upload sample, press Ctrl-C to exit" )

            client = IoTHubClient(CONNECTION_STRING, PROTOCOL)

            f = open(PATHTOFILE, "r")
            content = f.read()

            client.upload_blob_async(FILENAME, content, len(content), blob_upload_conf_callback, 0)

            print ( "" )
            print ( "File upload initiated..." )

            while True:
                time.sleep(30)

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
        except:
            print ( "generic error" )

    if __name__ == '__main__':
        print ( "Simulating a file upload using the Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_file_upload_sample_run()
    ```

1. <span data-ttu-id="1f7a1-134">Save and close the **UploadFile.py** file.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-134">Save and close the **UploadFile.py** file.</span></span>

1. <span data-ttu-id="1f7a1-135">Copy a sample text file to the working folder and rename it `sample.txt`.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-135">Copy a sample text file to the working folder and rename it `sample.txt`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f7a1-136">IoT Hub Python SDK currently only supports uploading character-based files such as **.txt** files.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-136">IoT Hub Python SDK currently only supports uploading character-based files such as **.txt** files.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="1f7a1-137">Run the application</span><span class="sxs-lookup"><span data-stu-id="1f7a1-137">Run the application</span></span>

<span data-ttu-id="1f7a1-138">Now you are ready to run the application.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-138">Now you are ready to run the application.</span></span>

1. <span data-ttu-id="1f7a1-139">At a command prompt in your working folder, run the following command:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-139">At a command prompt in your working folder, run the following command:</span></span>

    ```cmd/sh
    python FileUpload.py
    ```

1. <span data-ttu-id="1f7a1-140">The following screenshot shows the output from the **FileUpload** app:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-140">The following screenshot shows the output from the **FileUpload** app:</span></span>

    ![Output from simulated-device app](./media/iot-hub-python-python-file-upload/1.png)

1. <span data-ttu-id="1f7a1-142">You can use the portal to view the uploaded file in the storage container you configured:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-142">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

    ![Uploaded file](./media/iot-hub-python-python-file-upload/2.png)


## <a name="next-steps"></a><span data-ttu-id="1f7a1-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f7a1-144">Next steps</span></span>

<span data-ttu-id="1f7a1-145">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span><span class="sxs-lookup"><span data-stu-id="1f7a1-145">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="1f7a1-146">You can continue to explore IoT hub features and scenarios with the following articles:</span><span class="sxs-lookup"><span data-stu-id="1f7a1-146">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="1f7a1-147">[Create an IoT hub programmatically][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="1f7a1-147">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="1f7a1-148">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="1f7a1-148">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="1f7a1-149">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="1f7a1-149">[Azure IoT SDKs][lnk-sdks]</span></span>

<!-- Links -->
[Azure IoT Developer Center]: http://azure.microsoft.com/develop/iot

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
