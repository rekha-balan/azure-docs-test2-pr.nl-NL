---
title: Provision Windows devices to remote monitoring in C - Azure | Microsoft Docs
description: Describes how to connect a device to the Remote Monitoring solution accelerator using an application written in C running on Windows.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 03/14/2018
ms.author: dobett
ms.openlocfilehash: 139daea3e885636b352d4c9a1ba2651a24195b21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867449"
---
# <a name="connect-your-device-to-the-remote-monitoring-solution-accelerator-windows"></a><span data-ttu-id="f3ae0-103">Connect your device to the Remote Monitoring solution accelerator (Windows)</span><span class="sxs-lookup"><span data-stu-id="f3ae0-103">Connect your device to the Remote Monitoring solution accelerator (Windows)</span></span>

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

<span data-ttu-id="f3ae0-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span></span>

## <a name="create-a-c-client-solution-on-windows"></a><span data-ttu-id="f3ae0-105">Create a C client solution on Windows</span><span class="sxs-lookup"><span data-stu-id="f3ae0-105">Create a C client solution on Windows</span></span>

<span data-ttu-id="f3ae0-106">As with most embedded applications that run on constrained devices, the client code for the device application is written in C. In this tutorial, you build the application on a machine running Windows.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-106">As with most embedded applications that run on constrained devices, the client code for the device application is written in C. In this tutorial, you build the application on a machine running Windows.</span></span>

### <a name="create-the-starter-project"></a><span data-ttu-id="f3ae0-107">Create the starter project</span><span class="sxs-lookup"><span data-stu-id="f3ae0-107">Create the starter project</span></span>

<span data-ttu-id="f3ae0-108">Create a starter project in Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-108">Create a starter project in Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="f3ae0-109">In Visual Studio, create a C console application using the Visual C++ **Windows Console Application** template.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-109">In Visual Studio, create a C console application using the Visual C++ **Windows Console Application** template.</span></span> <span data-ttu-id="f3ae0-110">Name the project **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-110">Name the project **RMDevice**.</span></span>

    ![Create Visual C++ Windows Console Application](./media/iot-accelerators-connecting-devices/visualstudio01.png)

1. <span data-ttu-id="f3ae0-112">In **Solution Explorer**, delete the files `stdafx.h`, `targetver.h`, and `stdafx.cpp`.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-112">In **Solution Explorer**, delete the files `stdafx.h`, `targetver.h`, and `stdafx.cpp`.</span></span>

1. <span data-ttu-id="f3ae0-113">In **Solution Explorer**, rename the file `RMDevice.cpp` to `RMDevice.c`.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-113">In **Solution Explorer**, rename the file `RMDevice.cpp` to `RMDevice.c`.</span></span>

    ![Solution Explorer showing renamed RMDevice.c file](./media/iot-accelerators-connecting-devices/visualstudio02.png)

1. <span data-ttu-id="f3ae0-115">In **Solution Explorer**, right-click the **RMDevice** project and then click **Manage NuGet packages**.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-115">In **Solution Explorer**, right-click the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="f3ae0-116">Choose **Browse**, then search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-116">Choose **Browse**, then search for and install the following NuGet packages:</span></span>

    * <span data-ttu-id="f3ae0-117">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="f3ae0-117">Microsoft.Azure.IoTHub.Serializer</span></span>
    * <span data-ttu-id="f3ae0-118">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="f3ae0-118">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
    * <span data-ttu-id="f3ae0-119">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="f3ae0-119">Microsoft.Azure.IoTHub.MqttTransport</span></span>

    ![NuGet package manager shows installed Microsoft.Azure.IoTHub packages](./media/iot-accelerators-connecting-devices/visualstudio03.png)

1. <span data-ttu-id="f3ae0-121">In **Solution Explorer**, right-click on the **RMDevice** project and then choose **Properties** to open the project's **Property Pages** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-121">In **Solution Explorer**, right-click on the **RMDevice** project and then choose **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="f3ae0-122">For details, see [Setting Visual C++ Project Properties](https://docs.microsoft.com/cpp/ide/working-with-project-properties).</span><span class="sxs-lookup"><span data-stu-id="f3ae0-122">For details, see [Setting Visual C++ Project Properties](https://docs.microsoft.com/cpp/ide/working-with-project-properties).</span></span>

1. <span data-ttu-id="f3ae0-123">Choose the **C/C++** folder, then choose the **Precompiled Headers** property page.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-123">Choose the **C/C++** folder, then choose the **Precompiled Headers** property page.</span></span>

1. <span data-ttu-id="f3ae0-124">Set **Precompiled Header** to **Not Using Precompiled Headers**.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-124">Set **Precompiled Header** to **Not Using Precompiled Headers**.</span></span> <span data-ttu-id="f3ae0-125">Then choose **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-125">Then choose **Apply**.</span></span>

    ![Project properties show project not using precompiled headers](./media/iot-accelerators-connecting-devices/visualstudio04.png)

1. <span data-ttu-id="f3ae0-127">Choose the **Linker** folder, then choose the **Input** property page.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-127">Choose the **Linker** folder, then choose the **Input** property page.</span></span>

1. <span data-ttu-id="f3ae0-128">Add `crypt32.lib` to the **Additional Dependencies** property.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-128">Add `crypt32.lib` to the **Additional Dependencies** property.</span></span> <span data-ttu-id="f3ae0-129">To save the project property values, choose **OK** and then **OK** again.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-129">To save the project property values, choose **OK** and then **OK** again.</span></span>

    ![Project properties show Linker including crypt32.lib](./media/iot-accelerators-connecting-devices/visualstudio05.png)

### <a name="add-the-parson-json-library"></a><span data-ttu-id="f3ae0-131">Add the Parson JSON library</span><span class="sxs-lookup"><span data-stu-id="f3ae0-131">Add the Parson JSON library</span></span>

<span data-ttu-id="f3ae0-132">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-132">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="f3ae0-133">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-133">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```cmd
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="f3ae0-134">Copy the `parson.h` and `parson.c` files from the local copy of the Parson repository to your **RMDevice** project folder.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-134">Copy the `parson.h` and `parson.c` files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="f3ae0-135">In Visual Studio, right-click the **RMDevice** project, choose **Add**, and then choose **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-135">In Visual Studio, right-click the **RMDevice** project, choose **Add**, and then choose **Existing Item**.</span></span>

1. <span data-ttu-id="f3ae0-136">In the **Add Existing Item** dialog, select the `parson.h` and `parson.c` files in the **RMDevice** project folder.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-136">In the **Add Existing Item** dialog, select the `parson.h` and `parson.c` files in the **RMDevice** project folder.</span></span> <span data-ttu-id="f3ae0-137">To add these two files to your project, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-137">To add these two files to your project, choose **Add**.</span></span>

    ![Solution Explorer shows parson.h and parson.c files](./media/iot-accelerators-connecting-devices/visualstudio06.png)

1. <span data-ttu-id="f3ae0-139">In Visual Studio, open the `RMDevice.c` file.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-139">In Visual Studio, open the `RMDevice.c` file.</span></span> <span data-ttu-id="f3ae0-140">Replace the existing `#include` statements with the following code:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-140">Replace the existing `#include` statements with the following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include <string.h>
    ```

    > [!NOTE]
    > <span data-ttu-id="f3ae0-141">Now you can verify that your project has the correct dependencies set up by building the solution.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-141">Now you can verify that your project has the correct dependencies set up by building the solution.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="f3ae0-142">Build and run the sample</span><span class="sxs-lookup"><span data-stu-id="f3ae0-142">Build and run the sample</span></span>

<span data-ttu-id="f3ae0-143">Add code to invoke the **remote\_monitoring\_run** function, then build and run the device application:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-143">Add code to invoke the **remote\_monitoring\_run** function, then build and run the device application:</span></span>

1. <span data-ttu-id="f3ae0-144">To invoke the **remote\_monitoring\_run** function, replace the **main** function with following code:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-144">To invoke the **remote\_monitoring\_run** function, replace the **main** function with following code:</span></span>

    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="f3ae0-145">Choose **Build** and then **Build Solution** to build the device application.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-145">Choose **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="f3ae0-146">In **Solution Explorer**, right-click the **RMDevice** project, choose **Debug**, and then choose **Start new instance** to run the sample.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-146">In **Solution Explorer**, right-click the **RMDevice** project, choose **Debug**, and then choose **Start new instance** to run the sample.</span></span> <span data-ttu-id="f3ae0-147">The console displays messages as:</span><span class="sxs-lookup"><span data-stu-id="f3ae0-147">The console displays messages as:</span></span>

    * <span data-ttu-id="f3ae0-148">The application sends sample telemetry to the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-148">The application sends sample telemetry to the solution accelerator.</span></span>
    * <span data-ttu-id="f3ae0-149">Receives desired property values set in the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-149">Receives desired property values set in the solution dashboard.</span></span>
    * <span data-ttu-id="f3ae0-150">Responds to methods invoked from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="f3ae0-150">Responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]
