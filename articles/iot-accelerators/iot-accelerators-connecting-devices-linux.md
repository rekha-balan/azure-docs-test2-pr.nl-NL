---
title: Provision Linux devices to Remote Monitoring in C - Azure | Microsoft Docs
description: Describes how to connect a device to the Remote Monitoring solution accelerator using an application written in C running on Linux.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 03/14/2018
ms.author: dobett
ms.openlocfilehash: 5d7d6522dc663f13ce40cc638ba90ac4043d435c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871609"
---
# <a name="connect-your-device-to-the-remote-monitoring-solution-accelerator-linux"></a><span data-ttu-id="45c9c-103">Connect your device to the Remote Monitoring solution accelerator (Linux)</span><span class="sxs-lookup"><span data-stu-id="45c9c-103">Connect your device to the Remote Monitoring solution accelerator (Linux)</span></span>

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

<span data-ttu-id="45c9c-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="45c9c-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span></span>

## <a name="create-a-c-client-project-on-linux"></a><span data-ttu-id="45c9c-105">Create a C client project on Linux</span><span class="sxs-lookup"><span data-stu-id="45c9c-105">Create a C client project on Linux</span></span>

<span data-ttu-id="45c9c-106">As with most embedded applications that run on constrained devices, the client code for the device application is written in C. In this tutorial, you build the application on a machine running Ubuntu (Linux).</span><span class="sxs-lookup"><span data-stu-id="45c9c-106">As with most embedded applications that run on constrained devices, the client code for the device application is written in C. In this tutorial, you build the application on a machine running Ubuntu (Linux).</span></span>

<span data-ttu-id="45c9c-107">To complete these steps, you need a device running Ubuntu version 15.04 or later.</span><span class="sxs-lookup"><span data-stu-id="45c9c-107">To complete these steps, you need a device running Ubuntu version 15.04 or later.</span></span> <span data-ttu-id="45c9c-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span><span class="sxs-lookup"><span data-stu-id="45c9c-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```sh
sudo apt-get install cmake gcc g++
```

### <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="45c9c-109">Install the client libraries on your device</span><span class="sxs-lookup"><span data-stu-id="45c9c-109">Install the client libraries on your device</span></span>

<span data-ttu-id="45c9c-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span><span class="sxs-lookup"><span data-stu-id="45c9c-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="45c9c-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span><span class="sxs-lookup"><span data-stu-id="45c9c-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="45c9c-112">In a shell, add the AzureIoT repository to your computer:</span><span class="sxs-lookup"><span data-stu-id="45c9c-112">In a shell, add the AzureIoT repository to your computer:</span></span>

    ```sh
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```

1. <span data-ttu-id="45c9c-113">Install the azure-iot-sdk-c-dev package</span><span class="sxs-lookup"><span data-stu-id="45c9c-113">Install the azure-iot-sdk-c-dev package</span></span>

    ```sh
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

### <a name="install-the-parson-json-parser"></a><span data-ttu-id="45c9c-114">Install the Parson JSON parser</span><span class="sxs-lookup"><span data-stu-id="45c9c-114">Install the Parson JSON parser</span></span>

<span data-ttu-id="45c9c-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span><span class="sxs-lookup"><span data-stu-id="45c9c-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="45c9c-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span><span class="sxs-lookup"><span data-stu-id="45c9c-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```sh
git clone https://github.com/kgabis/parson.git
```

### <a name="prepare-your-project"></a><span data-ttu-id="45c9c-117">Prepare your project</span><span class="sxs-lookup"><span data-stu-id="45c9c-117">Prepare your project</span></span>

<span data-ttu-id="45c9c-118">On your Ubuntu machine, create a folder called `remote_monitoring`.</span><span class="sxs-lookup"><span data-stu-id="45c9c-118">On your Ubuntu machine, create a folder called `remote_monitoring`.</span></span> <span data-ttu-id="45c9c-119">In the `remote_monitoring` folder:</span><span class="sxs-lookup"><span data-stu-id="45c9c-119">In the `remote_monitoring` folder:</span></span>

- <span data-ttu-id="45c9c-120">Create the four files `main.c`, `remote_monitoring.c`, `remote_monitoring.h`, and `CMakeLists.txt`.</span><span class="sxs-lookup"><span data-stu-id="45c9c-120">Create the four files `main.c`, `remote_monitoring.c`, `remote_monitoring.h`, and `CMakeLists.txt`.</span></span>
- <span data-ttu-id="45c9c-121">Create folder called `parson`.</span><span class="sxs-lookup"><span data-stu-id="45c9c-121">Create folder called `parson`.</span></span>

<span data-ttu-id="45c9c-122">Copy the files `parson.c` and `parson.h` from your local copy of the Parson repository into the `remote_monitoring/parson` folder.</span><span class="sxs-lookup"><span data-stu-id="45c9c-122">Copy the files `parson.c` and `parson.h` from your local copy of the Parson repository into the `remote_monitoring/parson` folder.</span></span>

<span data-ttu-id="45c9c-123">In a text editor, open the `remote_monitoring.c` file.</span><span class="sxs-lookup"><span data-stu-id="45c9c-123">In a text editor, open the `remote_monitoring.c` file.</span></span> <span data-ttu-id="45c9c-124">Add the following `#include` statements:</span><span class="sxs-lookup"><span data-stu-id="45c9c-124">Add the following `#include` statements:</span></span>

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

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="add-code-to-run-the-app"></a><span data-ttu-id="45c9c-125">Add code to run the app</span><span class="sxs-lookup"><span data-stu-id="45c9c-125">Add code to run the app</span></span>

<span data-ttu-id="45c9c-126">In a text editor, open the `remote_monitoring.h` file.</span><span class="sxs-lookup"><span data-stu-id="45c9c-126">In a text editor, open the `remote_monitoring.h` file.</span></span> <span data-ttu-id="45c9c-127">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="45c9c-127">Add the following code:</span></span>

```c
void remote_monitoring_run(void);
```

<span data-ttu-id="45c9c-128">In a text editor, open the `main.c` file.</span><span class="sxs-lookup"><span data-stu-id="45c9c-128">In a text editor, open the `main.c` file.</span></span> <span data-ttu-id="45c9c-129">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="45c9c-129">Add the following code:</span></span>

```c
#include "remote_monitoring.h"

int main(void)
{
  remote_monitoring_run();

  return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="45c9c-130">Build and run the application</span><span class="sxs-lookup"><span data-stu-id="45c9c-130">Build and run the application</span></span>

<span data-ttu-id="45c9c-131">The following steps describe how to use *CMake* to build your client application.</span><span class="sxs-lookup"><span data-stu-id="45c9c-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="45c9c-132">In a text editor, open the **CMakeLists.txt** file in the `remote_monitoring` folder.</span><span class="sxs-lookup"><span data-stu-id="45c9c-132">In a text editor, open the **CMakeLists.txt** file in the `remote_monitoring` folder.</span></span>

1. <span data-ttu-id="45c9c-133">Add the following instructions to define how to build your client application:</span><span class="sxs-lookup"><span data-stu-id="45c9c-133">Add the following instructions to define how to build your client application:</span></span>

    ```cmake
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

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

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

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

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

1. <span data-ttu-id="45c9c-134">In the `remote_monitoring` folder, create a folder to store the *make* files that CMake generates.</span><span class="sxs-lookup"><span data-stu-id="45c9c-134">In the `remote_monitoring` folder, create a folder to store the *make* files that CMake generates.</span></span> <span data-ttu-id="45c9c-135">Then run the **cmake** and **make** commands as follows:</span><span class="sxs-lookup"><span data-stu-id="45c9c-135">Then run the **cmake** and **make** commands as follows:</span></span>

    ```sh
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="45c9c-136">Run the client application and send telemetry to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="45c9c-136">Run the client application and send telemetry to IoT Hub:</span></span>

    ```sh
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]
