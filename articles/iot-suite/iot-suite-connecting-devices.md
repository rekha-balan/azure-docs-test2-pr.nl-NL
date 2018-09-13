---
title: Connect a device using C on Windows | Microsoft Docs
description: Describes how to connect a device to the Azure IoT Suite preconfigured remote monitoring solution using an application written in C running on Windows.
services: ''
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/08/2017
ms.author: dobett
ms.openlocfilehash: 3536777690a9b00ded7c7fdf4d5f39638dad71b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540641"
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="31d43-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span><span class="sxs-lookup"><span data-stu-id="31d43-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="31d43-104">Create a C sample solution on Windows</span><span class="sxs-lookup"><span data-stu-id="31d43-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="31d43-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="31d43-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="31d43-106">This application is written in C and built and run on Windows.</span><span class="sxs-lookup"><span data-stu-id="31d43-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="31d43-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="31d43-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="31d43-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span><span class="sxs-lookup"><span data-stu-id="31d43-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="31d43-109">Name the project **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="31d43-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="31d43-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span><span class="sxs-lookup"><span data-stu-id="31d43-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="31d43-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="31d43-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="31d43-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="31d43-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="31d43-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span><span class="sxs-lookup"><span data-stu-id="31d43-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="31d43-114">Click **Browse**, then search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="31d43-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="31d43-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="31d43-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="31d43-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="31d43-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="31d43-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="31d43-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="31d43-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span><span class="sxs-lookup"><span data-stu-id="31d43-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="31d43-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="31d43-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="31d43-120">Click the **Linker** folder, then click the **Input** property page.</span><span class="sxs-lookup"><span data-stu-id="31d43-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="31d43-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span><span class="sxs-lookup"><span data-stu-id="31d43-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="31d43-122">Click **OK** and then **OK** again to save the project property values.</span><span class="sxs-lookup"><span data-stu-id="31d43-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="31d43-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span><span class="sxs-lookup"><span data-stu-id="31d43-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="31d43-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span><span class="sxs-lookup"><span data-stu-id="31d43-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="31d43-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span><span class="sxs-lookup"><span data-stu-id="31d43-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="31d43-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="31d43-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="31d43-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span><span class="sxs-lookup"><span data-stu-id="31d43-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="31d43-128">Then click **Add** to add these two files to your project.</span><span class="sxs-lookup"><span data-stu-id="31d43-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="31d43-129">In Visual Studio, open the RMDevice.c file.</span><span class="sxs-lookup"><span data-stu-id="31d43-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="31d43-130">Replace the existing `#include` statements with the following code:</span><span class="sxs-lookup"><span data-stu-id="31d43-130">Replace the existing `#include` statements with the following code:</span></span>
   
    ```
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="31d43-131">Now you can verify that your project has the correct dependencies set up by building it.</span><span class="sxs-lookup"><span data-stu-id="31d43-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="31d43-132">Build and run the sample</span><span class="sxs-lookup"><span data-stu-id="31d43-132">Build and run the sample</span></span>

<span data-ttu-id="31d43-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span><span class="sxs-lookup"><span data-stu-id="31d43-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="31d43-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span><span class="sxs-lookup"><span data-stu-id="31d43-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="31d43-135">Click **Build** and then **Build Solution** to build the device application.</span><span class="sxs-lookup"><span data-stu-id="31d43-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="31d43-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span><span class="sxs-lookup"><span data-stu-id="31d43-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="31d43-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="31d43-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
