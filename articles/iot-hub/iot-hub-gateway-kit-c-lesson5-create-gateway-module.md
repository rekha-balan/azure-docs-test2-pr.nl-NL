---
title: Create your first Azure IoT Gateway module | Microsoft Docs
description: Create a module and add it to a sample app to customize module behaviors.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: ''
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: ''
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e034a76efe01f8350f1141dbd2372010fd929e01
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661254"
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="94cf1-103">Lesson 5: Create your first Azure IoT Gateway module</span><span class="sxs-lookup"><span data-stu-id="94cf1-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="94cf1-104">While the Gateway SDK allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span><span class="sxs-lookup"><span data-stu-id="94cf1-104">While the Gateway SDK allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="94cf1-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="94cf1-105">What you will do</span></span>

- <span data-ttu-id="94cf1-106">Compile and run the hello_world sample app on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="94cf1-107">Create a module and compile it on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="94cf1-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="94cf1-109">The new module prints out "hello_world" messages with a timestamp.</span><span class="sxs-lookup"><span data-stu-id="94cf1-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="94cf1-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="94cf1-110">What you will learn</span></span>

- <span data-ttu-id="94cf1-111">How to compile and run a sample app on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="94cf1-112">How to create a module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-112">How to create a module.</span></span>
- <span data-ttu-id="94cf1-113">How to add module to a sample app.</span><span class="sxs-lookup"><span data-stu-id="94cf1-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="94cf1-114">What you need</span><span class="sxs-lookup"><span data-stu-id="94cf1-114">What you need</span></span>

<span data-ttu-id="94cf1-115">The Azure IoT Gateway SDK that has been installed on your host computer.</span><span class="sxs-lookup"><span data-stu-id="94cf1-115">The Azure IoT Gateway SDK that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="94cf1-116">Folder structure</span><span class="sxs-lookup"><span data-stu-id="94cf1-116">Folder structure</span></span>

<span data-ttu-id="94cf1-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span><span class="sxs-lookup"><span data-stu-id="94cf1-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="94cf1-119">The `module/my_module` folder contains the source code and script to build the module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="94cf1-120">The `sample` folder contains the source code and script to build the sample app.</span><span class="sxs-lookup"><span data-stu-id="94cf1-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="94cf1-121">Compile and run the hello_world sample app on Intel NUC</span><span class="sxs-lookup"><span data-stu-id="94cf1-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="94cf1-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span><span class="sxs-lookup"><span data-stu-id="94cf1-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="94cf1-123">The gateway logs a "hello world" message to a file every 5 seconds.</span><span class="sxs-lookup"><span data-stu-id="94cf1-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="94cf1-124">In this section, you compile and run the `hello_world` app with its default module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="94cf1-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span><span class="sxs-lookup"><span data-stu-id="94cf1-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="94cf1-126">Initialize the configuration files by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="94cf1-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="94cf1-127">Update the gateway configuration file with the MAC address of Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="94cf1-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span><span class="sxs-lookup"><span data-stu-id="94cf1-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="94cf1-129">Open the gateway configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="94cf1-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span><span class="sxs-lookup"><span data-stu-id="94cf1-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="94cf1-131">Compile the sample source code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="94cf1-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span><span class="sxs-lookup"><span data-stu-id="94cf1-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="94cf1-133">Run the `hello_world` app on Intel NUC by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="94cf1-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="94cf1-136">Create a new module and compile it on Intel NUC</span><span class="sxs-lookup"><span data-stu-id="94cf1-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="94cf1-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="94cf1-138">The module prints out messages with a timestamp upon receiving them.</span><span class="sxs-lookup"><span data-stu-id="94cf1-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="94cf1-139">You will create your first customized gateway module in this section.</span><span class="sxs-lookup"><span data-stu-id="94cf1-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="94cf1-140">Any Azure IoT Gateway SDK module must implement the following interfaces:</span><span class="sxs-lookup"><span data-stu-id="94cf1-140">Any Azure IoT Gateway SDK module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="94cf1-141">You can optionally implement the following interface:</span><span class="sxs-lookup"><span data-stu-id="94cf1-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="94cf1-142">The following diagram shows the important state paths of a module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="94cf1-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span><span class="sxs-lookup"><span data-stu-id="94cf1-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="94cf1-144">The ovals are major states the module can be in.</span><span class="sxs-lookup"><span data-stu-id="94cf1-144">The ovals are major states the module can be in.</span></span>

![state_path](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="94cf1-146">Now let’s create a module based on the template:</span><span class="sxs-lookup"><span data-stu-id="94cf1-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="94cf1-147">Open the template folder by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="94cf1-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="94cf1-150">The template declares the interfaces.</span><span class="sxs-lookup"><span data-stu-id="94cf1-150">The template declares the interfaces.</span></span> <span data-ttu-id="94cf1-151">All you need to do is to add logic to the `MyModule_Receive` function.</span><span class="sxs-lookup"><span data-stu-id="94cf1-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="94cf1-152">`build.sh` is the build script to compile the module on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="94cf1-153">Open the `src/my_module.c` file and include two header files:</span><span class="sxs-lookup"><span data-stu-id="94cf1-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="94cf1-154">Add the following code to the `MyModule_Receive` function:</span><span class="sxs-lookup"><span data-stu-id="94cf1-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="94cf1-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94cf1-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="94cf1-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span><span class="sxs-lookup"><span data-stu-id="94cf1-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="94cf1-157">Open the `config.json` file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="94cf1-158">Update `config.json` with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="94cf1-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="94cf1-160">Compile the module by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="94cf1-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="94cf1-162">Add the module to the hello_world sample app and run the app on Intel NUC</span><span class="sxs-lookup"><span data-stu-id="94cf1-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="94cf1-163">To perform this task, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="94cf1-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="94cf1-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="94cf1-165">The binary path of `my_module` that you compiled should be listed as below:</span><span class="sxs-lookup"><span data-stu-id="94cf1-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="94cf1-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span><span class="sxs-lookup"><span data-stu-id="94cf1-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="94cf1-167">Add `my_module` to the `hello_world` sample app:</span><span class="sxs-lookup"><span data-stu-id="94cf1-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="94cf1-168">Open the `hello_world.json` file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="94cf1-169">Add the following code to the `modules` section:</span><span class="sxs-lookup"><span data-stu-id="94cf1-169">Add the following code to the `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="94cf1-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="94cf1-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="94cf1-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span><span class="sxs-lookup"><span data-stu-id="94cf1-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="94cf1-172">Add the following code to the `links` section:</span><span class="sxs-lookup"><span data-stu-id="94cf1-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="94cf1-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span><span class="sxs-lookup"><span data-stu-id="94cf1-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="94cf1-175">Run the `hello_world` sample app by running the following command:</span><span class="sxs-lookup"><span data-stu-id="94cf1-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="94cf1-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span><span class="sxs-lookup"><span data-stu-id="94cf1-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="94cf1-178">Congratulations.</span><span class="sxs-lookup"><span data-stu-id="94cf1-178">Congratulations.</span></span> <span data-ttu-id="94cf1-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span><span class="sxs-lookup"><span data-stu-id="94cf1-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94cf1-180">Next Steps</span><span class="sxs-lookup"><span data-stu-id="94cf1-180">Next Steps</span></span>

<span data-ttu-id="94cf1-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span><span class="sxs-lookup"><span data-stu-id="94cf1-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="94cf1-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="94cf1-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md







