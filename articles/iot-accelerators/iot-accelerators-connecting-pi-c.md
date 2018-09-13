---
title: Provision Raspberry Pi to Remote Monitoring using C - Azure | Microsoft Docs
description: Describes how to connect a Raspberry Pi device to the Remote Monitoring solution accelerator using an application written in C.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 03/14/2018
ms.author: dobett
ms.openlocfilehash: 23e84a8d577bb1c4950de3acd76b0f8528551ae0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966942"
---
# <a name="connect-your-raspberry-pi-device-to-the-remote-monitoring-solution-accelerator-c"></a><span data-ttu-id="d1fc7-103">Connect your Raspberry Pi device to the Remote Monitoring solution accelerator (C)</span><span class="sxs-lookup"><span data-stu-id="d1fc7-103">Connect your Raspberry Pi device to the Remote Monitoring solution accelerator (C)</span></span>

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

<span data-ttu-id="d1fc7-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-104">This tutorial shows you how to connect a physical device to the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="d1fc7-105">As with most embedded applications that run on constrained devices, the client code for the Raspberry Pi device application is written in C. In this tutorial, you build the application on a Raspberry Pi running the Raspbian OS.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-105">As with most embedded applications that run on constrained devices, the client code for the Raspberry Pi device application is written in C. In this tutorial, you build the application on a Raspberry Pi running the Raspbian OS.</span></span>

### <a name="required-hardware"></a><span data-ttu-id="d1fc7-106">Required hardware</span><span class="sxs-lookup"><span data-stu-id="d1fc7-106">Required hardware</span></span>

<span data-ttu-id="d1fc7-107">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-107">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="d1fc7-108">[Microsoft IoT Starter Kit for Raspberry Pi 3](https://azure.microsoft.com/develop/iot/starter-kits/) or equivalent components.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-108">[Microsoft IoT Starter Kit for Raspberry Pi 3](https://azure.microsoft.com/develop/iot/starter-kits/) or equivalent components.</span></span> <span data-ttu-id="d1fc7-109">This tutorial uses the following items from the kit:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-109">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="d1fc7-110">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d1fc7-110">Raspberry Pi 3</span></span>
- <span data-ttu-id="d1fc7-111">MicroSD Card (with NOOBS)</span><span class="sxs-lookup"><span data-stu-id="d1fc7-111">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="d1fc7-112">A USB Mini cable</span><span class="sxs-lookup"><span data-stu-id="d1fc7-112">A USB Mini cable</span></span>
- <span data-ttu-id="d1fc7-113">An Ethernet cable</span><span class="sxs-lookup"><span data-stu-id="d1fc7-113">An Ethernet cable</span></span>

### <a name="required-desktop-software"></a><span data-ttu-id="d1fc7-114">Required desktop software</span><span class="sxs-lookup"><span data-stu-id="d1fc7-114">Required desktop software</span></span>

<span data-ttu-id="d1fc7-115">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-115">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="d1fc7-116">Windows does not include an SSH client.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-116">Windows does not include an SSH client.</span></span> <span data-ttu-id="d1fc7-117">We recommend using [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="d1fc7-117">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="d1fc7-118">Most Linux distributions and Mac OS include the command-line SSH utility.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-118">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="d1fc7-119">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="d1fc7-119">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-raspberry-pi-software"></a><span data-ttu-id="d1fc7-120">Required Raspberry Pi software</span><span class="sxs-lookup"><span data-stu-id="d1fc7-120">Required Raspberry Pi software</span></span>

<span data-ttu-id="d1fc7-121">This article assumes you have installed the latest version of the [Raspbian OS on your Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/quickstart/).</span><span class="sxs-lookup"><span data-stu-id="d1fc7-121">This article assumes you have installed the latest version of the [Raspbian OS on your Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/quickstart/).</span></span>

<span data-ttu-id="d1fc7-122">The following steps show you how to prepare your Raspberry Pi for building a C application that connects to the solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-122">The following steps show you how to prepare your Raspberry Pi for building a C application that connects to the solution accelerator:</span></span>

1. <span data-ttu-id="d1fc7-123">Connect to your Raspberry Pi using **ssh**.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-123">Connect to your Raspberry Pi using **ssh**.</span></span> <span data-ttu-id="d1fc7-124">For more information, see [SSH (Secure Shell)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md) on the [Raspberry Pi website](https://www.raspberrypi.org/).</span><span class="sxs-lookup"><span data-stu-id="d1fc7-124">For more information, see [SSH (Secure Shell)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md) on the [Raspberry Pi website](https://www.raspberrypi.org/).</span></span>

1. <span data-ttu-id="d1fc7-125">Use the following command to update your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-125">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="d1fc7-126">Use the following command to add the required development tools and libraries to your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-126">Use the following command to add the required development tools and libraries to your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get install g++ make cmake gcc git libssl1.0-dev build-essential curl libcurl4-openssl-dev uuid-dev
    ```

1. <span data-ttu-id="d1fc7-127">Use the following commands to download, build, and install the IoT Hub client libraries on your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-127">Use the following commands to download, build, and install the IoT Hub client libraries on your Raspberry Pi:</span></span>

    ```sh
    cd ~
    git clone --recursive https://github.com/azure/azure-iot-sdk-c.git
    mkdir cmake
    cd cmake
    cmake ..
    make
    sudo make install
    ```

## <a name="create-a-project"></a><span data-ttu-id="d1fc7-128">Create a project</span><span class="sxs-lookup"><span data-stu-id="d1fc7-128">Create a project</span></span>

<span data-ttu-id="d1fc7-129">Complete the following steps using the **ssh** connection to your Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-129">Complete the following steps using the **ssh** connection to your Raspberry Pi:</span></span>

1. <span data-ttu-id="d1fc7-130">Create a folder called `remote_monitoring` in your home folder on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-130">Create a folder called `remote_monitoring` in your home folder on the Raspberry Pi.</span></span> <span data-ttu-id="d1fc7-131">Navigate to this folder in your shell:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-131">Navigate to this folder in your shell:</span></span>

    ```sh
    cd ~
    mkdir remote_monitoring
    cd remote_monitoring
    ```

1. <span data-ttu-id="d1fc7-132">Create the four files **main.c**, **remote_monitoring.c**, **remote_monitoring.h**, and **CMakeLists.txt** in the `remote_monitoring` folder.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-132">Create the four files **main.c**, **remote_monitoring.c**, **remote_monitoring.h**, and **CMakeLists.txt** in the `remote_monitoring` folder.</span></span>

1. <span data-ttu-id="d1fc7-133">In a text editor, open the **remote_monitoring.c** file.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-133">In a text editor, open the **remote_monitoring.c** file.</span></span> <span data-ttu-id="d1fc7-134">On the Raspberry Pi, you can use either the **nano** or **vi** text editor.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-134">On the Raspberry Pi, you can use either the **nano** or **vi** text editor.</span></span> <span data-ttu-id="d1fc7-135">Add the following `#include` statements:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-135">Add the following `#include` statements:</span></span>

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

<span data-ttu-id="d1fc7-136">Save the **remote_monitoring.c** file and exit the editor.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-136">Save the **remote_monitoring.c** file and exit the editor.</span></span>

## <a name="add-code-to-run-the-app"></a><span data-ttu-id="d1fc7-137">Add code to run the app</span><span class="sxs-lookup"><span data-stu-id="d1fc7-137">Add code to run the app</span></span>

<span data-ttu-id="d1fc7-138">In a text editor, open the **remote_monitoring.h** file.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-138">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="d1fc7-139">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-139">Add the following code:</span></span>

```c
void remote_monitoring_run(void);
```

<span data-ttu-id="d1fc7-140">Save the **remote_monitoring.h** file and exit the editor.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-140">Save the **remote_monitoring.h** file and exit the editor.</span></span>

<span data-ttu-id="d1fc7-141">In a text editor, open the **main.c** file.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-141">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="d1fc7-142">Add the following code:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-142">Add the following code:</span></span>

```c
#include "remote_monitoring.h"

int main(void)
{
  remote_monitoring_run();

  return 0;
}
```

<span data-ttu-id="d1fc7-143">Save the **main.c** file and exit the editor.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-143">Save the **main.c** file and exit the editor.</span></span>

## <a name="build-and-run-the-application"></a><span data-ttu-id="d1fc7-144">Build and run the application</span><span class="sxs-lookup"><span data-stu-id="d1fc7-144">Build and run the application</span></span>

<span data-ttu-id="d1fc7-145">The following steps describe how to use *CMake* to build your client application.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-145">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="d1fc7-146">In a text editor, open the **CMakeLists.txt** file in the `remote_monitoring` folder.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-146">In a text editor, open the **CMakeLists.txt** file in the `remote_monitoring` folder.</span></span>

1. <span data-ttu-id="d1fc7-147">Add the following instructions to define how to build your client application:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-147">Add the following instructions to define how to build your client application:</span></span>

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

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "/usr/local/include/azureiot")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
      serializer
      iothub_client_mqtt_transport
      umqtt
      iothub_client
      aziotsharedutil
      parson
      pthread
      curl
      ssl
      crypto
      m
    )
    ```

1. <span data-ttu-id="d1fc7-148">Save the **CMakeLists.txt** file and exit the editor.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-148">Save the **CMakeLists.txt** file and exit the editor.</span></span>

1. <span data-ttu-id="d1fc7-149">In the `remote_monitoring` folder, create a folder to store the *make* files that CMake generates.</span><span class="sxs-lookup"><span data-stu-id="d1fc7-149">In the `remote_monitoring` folder, create a folder to store the *make* files that CMake generates.</span></span> <span data-ttu-id="d1fc7-150">Then run the **cmake** and **make** commands as follows:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-150">Then run the **cmake** and **make** commands as follows:</span></span>

    ```sh
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="d1fc7-151">Run the client application and send telemetry to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d1fc7-151">Run the client application and send telemetry to IoT Hub:</span></span>

    ```sh
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]
