---
title: IoT deploy custom simulated devices - Azure | Microsoft Docs
description: This how-to guide shows you how to deploy custom simulated devices to the Remote Monitoring solution accelerator.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 08/15/2018
ms.topic: conceptual
ms.openlocfilehash: f073637810e9ed1acdf37b0e541ca3f1d518de2a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864539"
---
# <a name="deploy-a-new-simulated-device"></a><span data-ttu-id="a41e2-103">Deploy a new simulated device</span><span class="sxs-lookup"><span data-stu-id="a41e2-103">Deploy a new simulated device</span></span>

<span data-ttu-id="a41e2-104">The Remote Monitoring and Device Simulation solution accelerators both let you define your own simulated devices.</span><span class="sxs-lookup"><span data-stu-id="a41e2-104">The Remote Monitoring and Device Simulation solution accelerators both let you define your own simulated devices.</span></span> <span data-ttu-id="a41e2-105">This article shows you how to deploy a customized chiller device type and a new lightbulb device type to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="a41e2-105">This article shows you how to deploy a customized chiller device type and a new lightbulb device type to the Remote Monitoring solution accelerator.</span></span>

<span data-ttu-id="a41e2-106">The steps in this article assume you've completed the [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md) how-to guide and have the files that define the customized chiller and new lightbulb device types.</span><span class="sxs-lookup"><span data-stu-id="a41e2-106">The steps in this article assume you've completed the [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md) how-to guide and have the files that define the customized chiller and new lightbulb device types.</span></span>

<span data-ttu-id="a41e2-107">The steps in this how-to guide show you how to:</span><span class="sxs-lookup"><span data-stu-id="a41e2-107">The steps in this how-to guide show you how to:</span></span>

1. <span data-ttu-id="a41e2-108">Use SSH to access the file system of the virtual machine that hosts the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="a41e2-108">Use SSH to access the file system of the virtual machine that hosts the Remote Monitoring solution accelerator.</span></span>

1. <span data-ttu-id="a41e2-109">Configure Docker to load the device models from a location outside the Docker container.</span><span class="sxs-lookup"><span data-stu-id="a41e2-109">Configure Docker to load the device models from a location outside the Docker container.</span></span>

1. <span data-ttu-id="a41e2-110">Run the Remote Monitoring solution accelerator using custom device model files.</span><span class="sxs-lookup"><span data-stu-id="a41e2-110">Run the Remote Monitoring solution accelerator using custom device model files.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a41e2-111">To complete the steps in this how-to guide, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a41e2-111">To complete the steps in this how-to guide, you need an active Azure subscription.</span></span>

<span data-ttu-id="a41e2-112">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a41e2-112">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a41e2-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a41e2-113">Prerequisites</span></span>

<span data-ttu-id="a41e2-114">To follow this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="a41e2-114">To follow this how-to guide, you need:</span></span>

- <span data-ttu-id="a41e2-115">A deployed instance of the [Remote Monitoring solution accelerator](https://www.azureiotsolutions.com/Accelerators#solutions/types/RM2).</span><span class="sxs-lookup"><span data-stu-id="a41e2-115">A deployed instance of the [Remote Monitoring solution accelerator](https://www.azureiotsolutions.com/Accelerators#solutions/types/RM2).</span></span>
- <span data-ttu-id="a41e2-116">A local **bash** shell to run the `ssh` and `scp` commands.</span><span class="sxs-lookup"><span data-stu-id="a41e2-116">A local **bash** shell to run the `ssh` and `scp` commands.</span></span> <span data-ttu-id="a41e2-117">On Windows, an easy way to install **bash** is to install [git](https://git-scm.com/download/win).</span><span class="sxs-lookup"><span data-stu-id="a41e2-117">On Windows, an easy way to install **bash** is to install [git](https://git-scm.com/download/win).</span></span>
- <span data-ttu-id="a41e2-118">Your custom device model files, such as the ones described in [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md).</span><span class="sxs-lookup"><span data-stu-id="a41e2-118">Your custom device model files, such as the ones described in [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md).</span></span>

[!INCLUDE [iot-solution-accelerators-access-vm](../../includes/iot-solution-accelerators-access-vm.md)]

## <a name="configure-docker"></a><span data-ttu-id="a41e2-119">Configure Docker</span><span class="sxs-lookup"><span data-stu-id="a41e2-119">Configure Docker</span></span>

<span data-ttu-id="a41e2-120">In this section, you configure Docker to load the device model files from the **/tmp/devicemodels** folder in the virtual machine rather than from inside the Docker container.</span><span class="sxs-lookup"><span data-stu-id="a41e2-120">In this section, you configure Docker to load the device model files from the **/tmp/devicemodels** folder in the virtual machine rather than from inside the Docker container.</span></span> <span data-ttu-id="a41e2-121">Run the commands in this section in a **bash** shell on your local machine:</span><span class="sxs-lookup"><span data-stu-id="a41e2-121">Run the commands in this section in a **bash** shell on your local machine:</span></span>

<span data-ttu-id="a41e2-122">In this section, you configure Docker to load the device model files from the **/tmp/devicemodels** folder in the virtual machine rather than from inside the Docker container.</span><span class="sxs-lookup"><span data-stu-id="a41e2-122">In this section, you configure Docker to load the device model files from the **/tmp/devicemodels** folder in the virtual machine rather than from inside the Docker container.</span></span> <span data-ttu-id="a41e2-123">Run the commands in this section in a **bash** shell on your local machine:</span><span class="sxs-lookup"><span data-stu-id="a41e2-123">Run the commands in this section in a **bash** shell on your local machine:</span></span>

1. <span data-ttu-id="a41e2-124">Use SSH to connect to the virtual machine in Azure from your local machine.</span><span class="sxs-lookup"><span data-stu-id="a41e2-124">Use SSH to connect to the virtual machine in Azure from your local machine.</span></span> <span data-ttu-id="a41e2-125">The following command assumes the public IP address of virtual machine **vm-vikxv** is **104.41.128.108** -- replace this value with the public IP address of your virtual machine from the previous section:</span><span class="sxs-lookup"><span data-stu-id="a41e2-125">The following command assumes the public IP address of virtual machine **vm-vikxv** is **104.41.128.108** -- replace this value with the public IP address of your virtual machine from the previous section:</span></span>

   ```sh
    ssh azureuser@104.41.128.108
    ```

    <span data-ttu-id="a41e2-126">Follow the prompts to sign in to the virtual machine with the password you set in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a41e2-126">Follow the prompts to sign in to the virtual machine with the password you set in the previous section.</span></span>

1. <span data-ttu-id="a41e2-127">Configure the device simulation service to load the device models from outside the container.</span><span class="sxs-lookup"><span data-stu-id="a41e2-127">Configure the device simulation service to load the device models from outside the container.</span></span> <span data-ttu-id="a41e2-128">First open the Docker configuration file:</span><span class="sxs-lookup"><span data-stu-id="a41e2-128">First open the Docker configuration file:</span></span>

    ```sh
    sudo nano /app/docker-compose.yml
    ```

    <span data-ttu-id="a41e2-129">Locate the settings for the **devicesimulation** container and edit the **volumes** setting as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="a41e2-129">Locate the settings for the **devicesimulation** container and edit the **volumes** setting as shown in the following snippet:</span></span>

    ```yml
    devicesimulation:
      image: azureiotpcs/device-simulation-dotnet:1.0.0
      networks:
        - default_net
      depends_on:
        - storageadapter
      environment:
        - PCS_IOTHUB_CONNSTRING
        - PCS_STORAGEADAPTER_WEBSERVICE_URL=http://storageadapter:9022/v1
        - PCS_AUTH_ISSUER
        - PCS_AUTH_AUDIENCE
        - PCS_AUTH_REQUIRED
        - PCS_CORS_WHITELIST
        - PCS_APPLICATION_SECRET
      # How one could mount custom device models
      volumes:
        - /tmp/devicemodels:/app/webservice/data/devicemodels:ro
    ```

    <span data-ttu-id="a41e2-130">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="a41e2-130">Save the changes.</span></span>

1. <span data-ttu-id="a41e2-131">Copy the existing device model files from the container to the new location.</span><span class="sxs-lookup"><span data-stu-id="a41e2-131">Copy the existing device model files from the container to the new location.</span></span> <span data-ttu-id="a41e2-132">First, find the container ID for the device simulation container:</span><span class="sxs-lookup"><span data-stu-id="a41e2-132">First, find the container ID for the device simulation container:</span></span>

    ```sh
    docker ps
    ```

    <span data-ttu-id="a41e2-133">Then copy the device model files to the **tmp** folder in the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a41e2-133">Then copy the device model files to the **tmp** folder in the virtual machine.</span></span> <span data-ttu-id="a41e2-134">The following command assumes the container ID is c378d6878407 -- replace this value with your device simulation container ID:</span><span class="sxs-lookup"><span data-stu-id="a41e2-134">The following command assumes the container ID is c378d6878407 -- replace this value with your device simulation container ID:</span></span>

    ```sh
    docker cp c378d6878407:/app/webservice/data/devicemodels /tmp
    ```

    <span data-ttu-id="a41e2-135">Keep the **bash** window with your SSH session open.</span><span class="sxs-lookup"><span data-stu-id="a41e2-135">Keep the **bash** window with your SSH session open.</span></span>

1. <span data-ttu-id="a41e2-136">Copy your custom device model files into the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a41e2-136">Copy your custom device model files into the virtual machine.</span></span> <span data-ttu-id="a41e2-137">Run this command in another **bash** shell on the machine where you created your custom device models.</span><span class="sxs-lookup"><span data-stu-id="a41e2-137">Run this command in another **bash** shell on the machine where you created your custom device models.</span></span> <span data-ttu-id="a41e2-138">First, navigate to the local folder that contains your device model JSON files.</span><span class="sxs-lookup"><span data-stu-id="a41e2-138">First, navigate to the local folder that contains your device model JSON files.</span></span> <span data-ttu-id="a41e2-139">The following commands assume the public IP address of the virtual machine is **104.41.128.108** -- replace this value with the public IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a41e2-139">The following commands assume the public IP address of the virtual machine is **104.41.128.108** -- replace this value with the public IP address of your virtual machine.</span></span> <span data-ttu-id="a41e2-140">Enter your virtual machine password when prompted:</span><span class="sxs-lookup"><span data-stu-id="a41e2-140">Enter your virtual machine password when prompted:</span></span>

    ```sh
    scp *json azureuser@104.41.128.108:/tmp/devicemodels
    cd scripts
    scp *js azureuser@104.41.128.108:/tmp/devicemodels/scripts
    ```

1. <span data-ttu-id="a41e2-141">Restart the device simulation Docker container to use the new device models.</span><span class="sxs-lookup"><span data-stu-id="a41e2-141">Restart the device simulation Docker container to use the new device models.</span></span> <span data-ttu-id="a41e2-142">Run the following commands in the **bash** shell with the open SSH session to the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="a41e2-142">Run the following commands in the **bash** shell with the open SSH session to the virtual machine:</span></span>

    ```sh
    sudo /app/start.sh
    ```

    <span data-ttu-id="a41e2-143">If you want to see status of the running Docker containers and their container IDs, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a41e2-143">If you want to see status of the running Docker containers and their container IDs, use the following command:</span></span>

    ```sh
    docker ps
    ```

    <span data-ttu-id="a41e2-144">If you want to see the log from the device simulation container, run the following command.</span><span class="sxs-lookup"><span data-stu-id="a41e2-144">If you want to see the log from the device simulation container, run the following command.</span></span> <span data-ttu-id="a41e2-145">Replace the container ID with the ID of your device simulation container:</span><span class="sxs-lookup"><span data-stu-id="a41e2-145">Replace the container ID with the ID of your device simulation container:</span></span>

    ```sh
    docker logs -f 5d3f3e78822e
    ```

## <a name="run-simulation"></a><span data-ttu-id="a41e2-146">Run simulation</span><span class="sxs-lookup"><span data-stu-id="a41e2-146">Run simulation</span></span>

<span data-ttu-id="a41e2-147">You can now use your custom device models in the Remote Monitoring solution:</span><span class="sxs-lookup"><span data-stu-id="a41e2-147">You can now use your custom device models in the Remote Monitoring solution:</span></span>

1. <span data-ttu-id="a41e2-148">Launch your Remote Monitoring dashboard from [Microsoft Azure IoT Solution Accelerators](https://www.azureiotsolutions.com/Accelerators#dashboard).</span><span class="sxs-lookup"><span data-stu-id="a41e2-148">Launch your Remote Monitoring dashboard from [Microsoft Azure IoT Solution Accelerators](https://www.azureiotsolutions.com/Accelerators#dashboard).</span></span>

1. <span data-ttu-id="a41e2-149">Use the **Devices** page to add simulated devices.</span><span class="sxs-lookup"><span data-stu-id="a41e2-149">Use the **Devices** page to add simulated devices.</span></span> <span data-ttu-id="a41e2-150">When you add a new simulated device, your new device models are available to choose.</span><span class="sxs-lookup"><span data-stu-id="a41e2-150">When you add a new simulated device, your new device models are available to choose.</span></span>

1. <span data-ttu-id="a41e2-151">You can use the dashboard to view device telemetry and call device methods.</span><span class="sxs-lookup"><span data-stu-id="a41e2-151">You can use the dashboard to view device telemetry and call device methods.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a41e2-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a41e2-152">Clean up resources</span></span>

<span data-ttu-id="a41e2-153">If you plan to explore further, leave the Remote Monitoring solution accelerator deployed.</span><span class="sxs-lookup"><span data-stu-id="a41e2-153">If you plan to explore further, leave the Remote Monitoring solution accelerator deployed.</span></span>

<span data-ttu-id="a41e2-154">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**.</span><span class="sxs-lookup"><span data-stu-id="a41e2-154">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a41e2-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="a41e2-155">Next steps</span></span>

<span data-ttu-id="a41e2-156">This guide showed you how to deploy custom device models to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="a41e2-156">This guide showed you how to deploy custom device models to the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="a41e2-157">The suggested next step is to learn how to [connect a physical device to your Remote Monitoring solution](iot-accelerators-connecting-devices-node.md).</span><span class="sxs-lookup"><span data-stu-id="a41e2-157">The suggested next step is to learn how to [connect a physical device to your Remote Monitoring solution](iot-accelerators-connecting-devices-node.md).</span></span>
