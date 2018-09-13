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
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: a5768041a13d5ddc355c054dc85ba651b0752aba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969383"
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="93524-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span><span class="sxs-lookup"><span data-stu-id="93524-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-v1-selector-connecting](../../includes/iot-suite-v1-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="93524-104">Build and run a sample C client Linux</span><span class="sxs-lookup"><span data-stu-id="93524-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="93524-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="93524-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="93524-106">This application is written in C and built and run on Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="93524-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="93524-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span><span class="sxs-lookup"><span data-stu-id="93524-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="93524-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span><span class="sxs-lookup"><span data-stu-id="93524-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="93524-109">Install the client libraries on your device</span><span class="sxs-lookup"><span data-stu-id="93524-109">Install the client libraries on your device</span></span>
<span data-ttu-id="93524-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span><span class="sxs-lookup"><span data-stu-id="93524-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="93524-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span><span class="sxs-lookup"><span data-stu-id="93524-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="93524-112">In a shell, add the AzureIoT repository to your computer:</span><span class="sxs-lookup"><span data-stu-id="93524-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="93524-113">Install the azure-iot-sdk-c-dev package</span><span class="sxs-lookup"><span data-stu-id="93524-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="93524-114">Install the Parson JSON parser</span><span class="sxs-lookup"><span data-stu-id="93524-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="93524-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span><span class="sxs-lookup"><span data-stu-id="93524-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="93524-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span><span class="sxs-lookup"><span data-stu-id="93524-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="93524-117">Prepare your project</span><span class="sxs-lookup"><span data-stu-id="93524-117">Prepare your project</span></span>
<span data-ttu-id="93524-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="93524-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="93524-119">In the **remote\_monitoring** folder:</span><span class="sxs-lookup"><span data-stu-id="93524-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="93524-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="93524-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="93524-121">Create folder called **parson**.</span><span class="sxs-lookup"><span data-stu-id="93524-121">Create folder called **parson**.</span></span>

<span data-ttu-id="93524-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span><span class="sxs-lookup"><span data-stu-id="93524-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="93524-123">In a text editor, open the **remote\_monitoring.c** file.</span><span class="sxs-lookup"><span data-stu-id="93524-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="93524-124">Add the following `#include` statements:</span><span class="sxs-lookup"><span data-stu-id="93524-124">Add the following `#include` statements:</span></span>
   
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

[!INCLUDE [iot-suite-v1-connecting-code](../../includes/iot-suite-v1-connecting-code.md)]

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="93524-125">Call the remote\_monitoring\_run function</span><span class="sxs-lookup"><span data-stu-id="93524-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="93524-126">In a text editor, open the **remote_monitoring.h** file.</span><span class="sxs-lookup"><span data-stu-id="93524-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="93524-127">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="93524-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="93524-128">In a text editor, open the **main.c** file.</span><span class="sxs-lookup"><span data-stu-id="93524-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="93524-129">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="93524-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="93524-130">Build and run the application</span><span class="sxs-lookup"><span data-stu-id="93524-130">Build and run the application</span></span>
<span data-ttu-id="93524-131">The following steps describe how to use *CMake* to build your client application.</span><span class="sxs-lookup"><span data-stu-id="93524-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="93524-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span><span class="sxs-lookup"><span data-stu-id="93524-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="93524-133">Add the following instructions to define how to build your client application:</span><span class="sxs-lookup"><span data-stu-id="93524-133">Add the following instructions to define how to build your client application:</span></span>
   
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
1. <span data-ttu-id="93524-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span><span class="sxs-lookup"><span data-stu-id="93524-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="93524-135">Run the client application and send telemetry to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="93524-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-v1-visualize-connecting](../../includes/iot-suite-v1-visualize-connecting.md)]

