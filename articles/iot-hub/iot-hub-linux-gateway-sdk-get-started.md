---
title: Get started with the Azure IoT Gateway SDK (Linux) | Microsoft Docs
description: How to build a gateway on a Linux machine and learn about key concepts in the Azure IoT Gateway SDK such as modules and JSON configuration files.
services: iot-hub
documentationcenter: ''
author: chipalost
manager: timlt
editor: ''
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 856ffeeeb8f9d8296ba972a9e070686171f7fde8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661890"
---
# <a name="explore-the-iot-gateway-sdk-architecture-on-linux"></a><span data-ttu-id="37c05-103">Explore the IoT Gateway SDK architecture on Linux</span><span class="sxs-lookup"><span data-stu-id="37c05-103">Explore the IoT Gateway SDK architecture on Linux</span></span>

[!INCLUDE [iot-hub-gateway-sdk-getstarted-selector](../../includes/iot-hub-gateway-sdk-getstarted-selector.md)]

## <a name="how-to-build-the-sample"></a><span data-ttu-id="37c05-104">How to build the sample</span><span class="sxs-lookup"><span data-stu-id="37c05-104">How to build the sample</span></span>

<span data-ttu-id="37c05-105">Before you get started, you must [set up your development environment][lnk-setupdevbox] for working with the SDK on Linux.</span><span class="sxs-lookup"><span data-stu-id="37c05-105">Before you get started, you must [set up your development environment][lnk-setupdevbox] for working with the SDK on Linux.</span></span>

1. <span data-ttu-id="37c05-106">Open a shell.</span><span class="sxs-lookup"><span data-stu-id="37c05-106">Open a shell.</span></span>
1. <span data-ttu-id="37c05-107">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="37c05-107">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
1. <span data-ttu-id="37c05-108">Run the **tools/build.sh** script.</span><span class="sxs-lookup"><span data-stu-id="37c05-108">Run the **tools/build.sh** script.</span></span> <span data-ttu-id="37c05-109">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **azure-iot-gateway-sdk** repository and generate a makefile.</span><span class="sxs-lookup"><span data-stu-id="37c05-109">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **azure-iot-gateway-sdk** repository and generate a makefile.</span></span> <span data-ttu-id="37c05-110">The script then builds the solution, skipping unit tests and end to end tests.</span><span class="sxs-lookup"><span data-stu-id="37c05-110">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="37c05-111">Add the **--run-unittests** parameter if you want to build and run the unit tests.</span><span class="sxs-lookup"><span data-stu-id="37c05-111">Add the **--run-unittests** parameter if you want to build and run the unit tests.</span></span> <span data-ttu-id="37c05-112">Add the **--run-e2e-tests** if you want to build and run the end to end tests.</span><span class="sxs-lookup"><span data-stu-id="37c05-112">Add the **--run-e2e-tests** if you want to build and run the end to end tests.</span></span>

> [!NOTE]
> <span data-ttu-id="37c05-113">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="37c05-113">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span></span>

## <a name="how-to-run-the-sample"></a><span data-ttu-id="37c05-114">How to run the sample</span><span class="sxs-lookup"><span data-stu-id="37c05-114">How to run the sample</span></span>

1. <span data-ttu-id="37c05-115">The **build.sh** script generates its output in the **build** folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="37c05-115">The **build.sh** script generates its output in the **build** folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span> <span data-ttu-id="37c05-116">This output includes the two modules used in this sample.</span><span class="sxs-lookup"><span data-stu-id="37c05-116">This output includes the two modules used in this sample.</span></span>

    <span data-ttu-id="37c05-117">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span><span class="sxs-lookup"><span data-stu-id="37c05-117">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="37c05-118">Use these paths for the **module path** value as shown in the following example JSON settings file.</span><span class="sxs-lookup"><span data-stu-id="37c05-118">Use these paths for the **module path** value as shown in the following example JSON settings file.</span></span>
1. <span data-ttu-id="37c05-119">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span><span class="sxs-lookup"><span data-stu-id="37c05-119">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="37c05-120">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="37c05-120">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="37c05-121">This configuration file works as is unless you modify the build script to place modules or sample executables in non-default locations.</span><span class="sxs-lookup"><span data-stu-id="37c05-121">This configuration file works as is unless you modify the build script to place modules or sample executables in non-default locations.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37c05-122">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span><span class="sxs-lookup"><span data-stu-id="37c05-122">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="37c05-123">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span><span class="sxs-lookup"><span data-stu-id="37c05-123">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

    ```json
    {
        "modules" :
        [
            {
              "name" : "logger",
              "loader": {
                "name": "native",
                "entrypoint": {
                  "module.path": "./modules/logger/liblogger.so"
                }
              },
              "args" : {"filename":"log.txt"}
            },
            {
                "name" : "hello_world",
              "loader": {
                "name": "native",
                "entrypoint": {
                  "module.path": "./modules/hello_world/libhello_world.so"
                }
              },
                "args" : null
            }
        ],
        "links":
        [
            {
                "source": "hello_world",
                "sink": "logger"
            }
        ]
    }
    ```
1. <span data-ttu-id="37c05-124">Navigate to **build** folder.</span><span class="sxs-lookup"><span data-stu-id="37c05-124">Navigate to **build** folder.</span></span>
1. <span data-ttu-id="37c05-125">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="37c05-125">Run the following command:</span></span>

   `./samples/hello_world/hello_world_sample ./../samples/hello_world/src/hello_world_lin.json`

[!INCLUDE [iot-hub-gateway-sdk-getstarted-code](../../includes/iot-hub-gateway-sdk-getstarted-code.md)]

<!-- Links -->
[lnk-setupdevbox]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/doc/devbox_setup.md
