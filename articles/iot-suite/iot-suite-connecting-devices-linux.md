---
title: Connect a device using C on Linux | Microsoft Docs
description: Describes how to connect a device to the Azure IoT Suite preconfigured remote monitoring solution using an application written in C running on Linux.
services: ''
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/17/2017
ms.author: dobett
ms.openlocfilehash: 4a1615c4bea8c54d506c3252e2de42642bb55e46
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671668"
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="64e46-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span><span class="sxs-lookup"><span data-stu-id="64e46-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="64e46-104">Build and run a sample C client Linux</span><span class="sxs-lookup"><span data-stu-id="64e46-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="64e46-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="64e46-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="64e46-106">This application is written in C and built and run on Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="64e46-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="64e46-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span><span class="sxs-lookup"><span data-stu-id="64e46-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="64e46-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span><span class="sxs-lookup"><span data-stu-id="64e46-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="64e46-109">Install the client libraries on your device</span><span class="sxs-lookup"><span data-stu-id="64e46-109">Install the client libraries on your device</span></span>
<span data-ttu-id="64e46-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span><span class="sxs-lookup"><span data-stu-id="64e46-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="64e46-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span><span class="sxs-lookup"><span data-stu-id="64e46-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="64e46-112">In a shell, add the AzureIoT repository to your computer:</span><span class="sxs-lookup"><span data-stu-id="64e46-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="64e46-113">Install the azure-iot-sdk-c-dev package</span><span class="sxs-lookup"><span data-stu-id="64e46-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="64e46-114">Install the Parson JSON parser</span><span class="sxs-lookup"><span data-stu-id="64e46-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="64e46-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span><span class="sxs-lookup"><span data-stu-id="64e46-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="64e46-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span><span class="sxs-lookup"><span data-stu-id="64e46-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="64e46-117">Prepare your project</span><span class="sxs-lookup"><span data-stu-id="64e46-117">Prepare your project</span></span>
<span data-ttu-id="64e46-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="64e46-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="64e46-119">In the **remote\_monitoring** folder:</span><span class="sxs-lookup"><span data-stu-id="64e46-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="64e46-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="64e46-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="64e46-121">Create folder called **parson**.</span><span class="sxs-lookup"><span data-stu-id="64e46-121">Create folder called **parson**.</span></span>

<span data-ttu-id="64e46-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span><span class="sxs-lookup"><span data-stu-id="64e46-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="64e46-123">In a text editor, open the **remote\_monitoring.c** file.</span><span class="sxs-lookup"><span data-stu-id="64e46-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="64e46-124">Add the following `#include` statements:</span><span class="sxs-lookup"><span data-stu-id="64e46-124">Add the following `#include` statements:</span></span>
   
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

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="64e46-125">Call the remote\_monitoring\_run function</span><span class="sxs-lookup"><span data-stu-id="64e46-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="64e46-126">In a text editor, open the **remote_monitoring.h** file.</span><span class="sxs-lookup"><span data-stu-id="64e46-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="64e46-127">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="64e46-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="64e46-128">In a text editor, open the **main.c** file.</span><span class="sxs-lookup"><span data-stu-id="64e46-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="64e46-129">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="64e46-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="64e46-130">Build and run the application</span><span class="sxs-lookup"><span data-stu-id="64e46-130">Build and run the application</span></span>
<span data-ttu-id="64e46-131">The following steps describe how to use *CMake* to build your client application.</span><span class="sxs-lookup"><span data-stu-id="64e46-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="64e46-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span><span class="sxs-lookup"><span data-stu-id="64e46-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="64e46-133">Add the following instructions to define how to build your client application:</span><span class="sxs-lookup"><span data-stu-id="64e46-133">Add the following instructions to define how to build your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER ".." "../parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h
    _files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="64e46-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span><span class="sxs-lookup"><span data-stu-id="64e46-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="64e46-135">Run the client application and send telemetry to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="64e46-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

