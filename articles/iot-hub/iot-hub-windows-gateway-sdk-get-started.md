---
title: Get started with the Azure IoT Gateway SDK (Windows) | Microsoft Docs
description: How to build a gateway on a Windows machine and learn about key concepts in the Azure IoT Gateway SDK such as modules and JSON configuration files.
services: iot-hub
documentationcenter: ''
author: chipalost
manager: timlt
editor: ''
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3cc32daac5059e816c885c88f4a7d36b6fc897e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660787"
---
# <a name="explore-the-iot-gateway-sdk-architecture-on-windows"></a><span data-ttu-id="b4684-103">Explore the IoT Gateway SDK architecture on Windows</span><span class="sxs-lookup"><span data-stu-id="b4684-103">Explore the IoT Gateway SDK architecture on Windows</span></span>

[!INCLUDE [iot-hub-gateway-sdk-getstarted-selector](../../includes/iot-hub-gateway-sdk-getstarted-selector.md)]

## <a name="how-to-build-the-sample"></a><span data-ttu-id="b4684-104">How to build the sample</span><span class="sxs-lookup"><span data-stu-id="b4684-104">How to build the sample</span></span>

<span data-ttu-id="b4684-105">Before you get started, you must [set up your development environment][lnk-setupdevbox] for working with the SDK on Windows.</span><span class="sxs-lookup"><span data-stu-id="b4684-105">Before you get started, you must [set up your development environment][lnk-setupdevbox] for working with the SDK on Windows.</span></span>

1. <span data-ttu-id="b4684-106">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span><span class="sxs-lookup"><span data-stu-id="b4684-106">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>
1. <span data-ttu-id="b4684-107">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="b4684-107">Navigate to the root folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span>
1. <span data-ttu-id="b4684-108">Run the **tools\\build.cmd** script.</span><span class="sxs-lookup"><span data-stu-id="b4684-108">Run the **tools\\build.cmd** script.</span></span> <span data-ttu-id="b4684-109">This script creates a Visual Studio solution file and builds the solution.</span><span class="sxs-lookup"><span data-stu-id="b4684-109">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="b4684-110">You can find the Visual Studio solution in the **build** folder in your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="b4684-110">You can find the Visual Studio solution in the **build** folder in your local copy of the **azure-iot-gateway-sdk** repository.</span></span> <span data-ttu-id="b4684-111">Additional parameters can be given to the script to build and run unit and end-to-end tests.</span><span class="sxs-lookup"><span data-stu-id="b4684-111">Additional parameters can be given to the script to build and run unit and end-to-end tests.</span></span> <span data-ttu-id="b4684-112">These parameters are **--run-unittests** and **--run-e2e-tests** respectively.</span><span class="sxs-lookup"><span data-stu-id="b4684-112">These parameters are **--run-unittests** and **--run-e2e-tests** respectively.</span></span>

## <a name="how-to-run-the-sample"></a><span data-ttu-id="b4684-113">How to run the sample</span><span class="sxs-lookup"><span data-stu-id="b4684-113">How to run the sample</span></span>

1. <span data-ttu-id="b4684-114">The **build.cmd** script creates a folder called **build** in your local copy of the repository.</span><span class="sxs-lookup"><span data-stu-id="b4684-114">The **build.cmd** script creates a folder called **build** in your local copy of the repository.</span></span> <span data-ttu-id="b4684-115">This folder contains the two modules used in this sample.</span><span class="sxs-lookup"><span data-stu-id="b4684-115">This folder contains the two modules used in this sample.</span></span>

    <span data-ttu-id="b4684-116">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span><span class="sxs-lookup"><span data-stu-id="b4684-116">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="b4684-117">Use these paths for the **module path** values as shown in the following JSON settings file.</span><span class="sxs-lookup"><span data-stu-id="b4684-117">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>
1. <span data-ttu-id="b4684-118">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span><span class="sxs-lookup"><span data-stu-id="b4684-118">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="b4684-119">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="b4684-119">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="b4684-120">This configuration file works as is unless you modify the build script to place modules or sample executables in non-default locations.</span><span class="sxs-lookup"><span data-stu-id="b4684-120">This configuration file works as is unless you modify the build script to place modules or sample executables in non-default locations.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b4684-121">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span><span class="sxs-lookup"><span data-stu-id="b4684-121">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="b4684-122">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span><span class="sxs-lookup"><span data-stu-id="b4684-122">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

    ```json
    {
      "modules": [
        {
          "name": "logger",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
            }
          },
          "args": { "filename": "log.txt" }
        },
        {
          "name": "hello_world",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
            }
          },
          "args": null
          }
      ],
      "links": [
        {
          "source": "hello_world",
          "sink": "logger"
        }
      ]
    }
    ```

1. <span data-ttu-id="b4684-123">Navigate to the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span><span class="sxs-lookup"><span data-stu-id="b4684-123">Navigate to the root folder of your local copy of the **azure-iot-gateway-sdk** repository.</span></span>

1. <span data-ttu-id="b4684-124">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="b4684-124">Run the following command:</span></span>

   `build\samples\hello_world\Debug\hello_world_sample.exe samples\hello_world\src\hello_world_win.json`

[!INCLUDE [iot-hub-gateway-sdk-getstarted-code](../../includes/iot-hub-gateway-sdk-getstarted-code.md)]

<!-- Links -->
[lnk-setupdevbox]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/doc/devbox_setup.md
