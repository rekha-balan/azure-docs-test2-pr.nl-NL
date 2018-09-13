---
title: IoT deploy custom simulated devices - Azure | Microsoft Docs
description: This how-to guide shows you how to deploy custom simulated devices to the Device Simulation solution accelerator.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 08/14/2018
ms.topic: conceptual
ms.openlocfilehash: e51d0330c3ed804bff8cdb06265bb8c39141733f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870141"
---
# <a name="deploy-a-new-simulated-device"></a><span data-ttu-id="3cc03-103">Deploy a new simulated device</span><span class="sxs-lookup"><span data-stu-id="3cc03-103">Deploy a new simulated device</span></span>

<span data-ttu-id="3cc03-104">The Remote Monitoring and Device Simulation solution accelerators both let you define your own simulated devices.</span><span class="sxs-lookup"><span data-stu-id="3cc03-104">The Remote Monitoring and Device Simulation solution accelerators both let you define your own simulated devices.</span></span> <span data-ttu-id="3cc03-105">This article shows you how to deploy a customized chiller device type and a new lightbulb device type to the Device Simulation solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="3cc03-105">This article shows you how to deploy a customized chiller device type and a new lightbulb device type to the Device Simulation solution accelerator.</span></span>

<span data-ttu-id="3cc03-106">The steps in this article assume you've completed the [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md) how-to guide and have the files that define the customized chiller and new lightbulb device types.</span><span class="sxs-lookup"><span data-stu-id="3cc03-106">The steps in this article assume you've completed the [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md) how-to guide and have the files that define the customized chiller and new lightbulb device types.</span></span>

<span data-ttu-id="3cc03-107">The steps in this how-to guide show you how to:</span><span class="sxs-lookup"><span data-stu-id="3cc03-107">The steps in this how-to guide show you how to:</span></span>

1. <span data-ttu-id="3cc03-108">Use SSH to access the file system of the virtual machine that hosts the Device Simulation solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="3cc03-108">Use SSH to access the file system of the virtual machine that hosts the Device Simulation solution accelerator.</span></span>

1. <span data-ttu-id="3cc03-109">Configure Docker to load the device models from a location outside the Docker container.</span><span class="sxs-lookup"><span data-stu-id="3cc03-109">Configure Docker to load the device models from a location outside the Docker container.</span></span>

1. <span data-ttu-id="3cc03-110">Run a simulation using custom device model files.</span><span class="sxs-lookup"><span data-stu-id="3cc03-110">Run a simulation using custom device model files.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3cc03-111">To complete the steps in this how-to guide, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3cc03-111">To complete the steps in this how-to guide, you need an active Azure subscription.</span></span>

<span data-ttu-id="3cc03-112">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3cc03-112">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cc03-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cc03-113">Prerequisites</span></span>

<span data-ttu-id="3cc03-114">To follow this how-to guide, you need:</span><span class="sxs-lookup"><span data-stu-id="3cc03-114">To follow this how-to guide, you need:</span></span>

- <span data-ttu-id="3cc03-115">A deployed instance of the [Device Simulation solution accelerator](https://www.azureiotsolutions.com/Accelerators#solutions/types/DS).</span><span class="sxs-lookup"><span data-stu-id="3cc03-115">A deployed instance of the [Device Simulation solution accelerator](https://www.azureiotsolutions.com/Accelerators#solutions/types/DS).</span></span>
- <span data-ttu-id="3cc03-116">A local **bash** shell to run the `ssh` and `scp` commands.</span><span class="sxs-lookup"><span data-stu-id="3cc03-116">A local **bash** shell to run the `ssh` and `scp` commands.</span></span> <span data-ttu-id="3cc03-117">On Windows, an easy way to install **bash** is to install [git](https://git-scm.com/download/win).</span><span class="sxs-lookup"><span data-stu-id="3cc03-117">On Windows, an easy way to install **bash** is to install [git](https://git-scm.com/download/win).</span></span>
- <span data-ttu-id="3cc03-118">Your custom device model files, such as the ones described in [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md).</span><span class="sxs-lookup"><span data-stu-id="3cc03-118">Your custom device model files, such as the ones described in [Create and test a new simulated device](iot-accelerators-remote-monitoring-create-simulated-device.md).</span></span>

[!INCLUDE [iot-solution-accelerators-access-vm](../../includes/iot-solution-accelerators-access-vm.md)]

## <a name="configure-docker"></a><span data-ttu-id="3cc03-119">Configure Docker</span><span class="sxs-lookup"><span data-stu-id="3cc03-119">Configure Docker</span></span>

<span data-ttu-id="3cc03-120">In this section, you configure Docker to load the device model files from the **/tmp/devicemodels** folder in the virtual machine rather than from inside the Docker container.</span><span class="sxs-lookup"><span data-stu-id="3cc03-120">In this section, you configure Docker to load the device model files from the **/tmp/devicemodels** folder in the virtual machine rather than from inside the Docker container.</span></span> <span data-ttu-id="3cc03-121">Run the commands in this section in a **bash** shell on your local machine:</span><span class="sxs-lookup"><span data-stu-id="3cc03-121">Run the commands in this section in a **bash** shell on your local machine:</span></span>

1. <span data-ttu-id="3cc03-122">Use SSH to connect to the virtual machine in Azure from your local machine.</span><span class="sxs-lookup"><span data-stu-id="3cc03-122">Use SSH to connect to the virtual machine in Azure from your local machine.</span></span> <span data-ttu-id="3cc03-123">The following command assumes the public IP address of virtual machine **vm-vikxv** is **104.41.128.108** -- replace this value with the public IP address of your virtual machine from the previous section:</span><span class="sxs-lookup"><span data-stu-id="3cc03-123">The following command assumes the public IP address of virtual machine **vm-vikxv** is **104.41.128.108** -- replace this value with the public IP address of your virtual machine from the previous section:</span></span>

   ```sh
    ssh azureuser@104.41.128.108
    ```

    <span data-ttu-id="3cc03-124">Follow the prompts to sign in to the virtual machine with the password you set in the previous section.</span><span class="sxs-lookup"><span data-stu-id="3cc03-124">Follow the prompts to sign in to the virtual machine with the password you set in the previous section.</span></span>

1. <span data-ttu-id="3cc03-125">Configure the device simulation service to load the device models from outside the container.</span><span class="sxs-lookup"><span data-stu-id="3cc03-125">Configure the device simulation service to load the device models from outside the container.</span></span> <span data-ttu-id="3cc03-126">First open the Docker configuration file:</span><span class="sxs-lookup"><span data-stu-id="3cc03-126">First open the Docker configuration file:</span></span>

    ```sh
    sudo nano /app/docker-compose.yml
    ```

    <span data-ttu-id="3cc03-127">Locate the settings for the **devicesimulation** container and edit the **volumes** setting as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="3cc03-127">Locate the settings for the **devicesimulation** container and edit the **volumes** setting as shown in the following snippet:</span></span>

    ```yml
    # To mount custom device models, upload the files to the VM, edit and uncomment the following line:
          - /tmp/devicemodels:/app/webservice/data/devicemodels:ro
    # To mount a custom service configuration, create a custom file, edit and uncomment the following line:
    #     - /app/custom-device-simulation-appsettings.ini:/app/webservice/appsettings.ini:ro
    ```

    <span data-ttu-id="3cc03-128">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="3cc03-128">Save the changes.</span></span>

1. <span data-ttu-id="3cc03-129">Create the folders to store the JSON and script files:</span><span class="sxs-lookup"><span data-stu-id="3cc03-129">Create the folders to store the JSON and script files:</span></span>

    ```sh
    sudo mkdir -p /tmp/devicemodels/scripts
    ```

    <span data-ttu-id="3cc03-130">Keep the **bash** window with your SSH session open.</span><span class="sxs-lookup"><span data-stu-id="3cc03-130">Keep the **bash** window with your SSH session open.</span></span>

1. <span data-ttu-id="3cc03-131">Copy your custom device model files into the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3cc03-131">Copy your custom device model files into the virtual machine.</span></span> <span data-ttu-id="3cc03-132">Run this command in another **bash** shell on the machine where you created your custom device models.</span><span class="sxs-lookup"><span data-stu-id="3cc03-132">Run this command in another **bash** shell on the machine where you created your custom device models.</span></span> <span data-ttu-id="3cc03-133">First, navigate to the local folder that contains your device model JSON files.</span><span class="sxs-lookup"><span data-stu-id="3cc03-133">First, navigate to the local folder that contains your device model JSON files.</span></span> <span data-ttu-id="3cc03-134">The following commands assume the public IP address of the virtual machine is **104.41.128.108** -- replace this value with the public IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3cc03-134">The following commands assume the public IP address of the virtual machine is **104.41.128.108** -- replace this value with the public IP address of your virtual machine.</span></span> <span data-ttu-id="3cc03-135">Enter your virtual machine password when prompted:</span><span class="sxs-lookup"><span data-stu-id="3cc03-135">Enter your virtual machine password when prompted:</span></span>

    ```sh
    scp *json azureuser@104.41.128.108:/tmp/devicemodels
    cd scripts
    scp *js azureuser@104.41.128.108:/tmp/devicemodels/scripts
    ```

1. <span data-ttu-id="3cc03-136">Restart the device simulation Docker container to use the new device models.</span><span class="sxs-lookup"><span data-stu-id="3cc03-136">Restart the device simulation Docker container to use the new device models.</span></span> <span data-ttu-id="3cc03-137">Run the following commands in the **bash** shell with the open SSH session to the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="3cc03-137">Run the following commands in the **bash** shell with the open SSH session to the virtual machine:</span></span>

    ```sh
    sudo /app/start.sh
    ```

    <span data-ttu-id="3cc03-138">If you want to see status of the running Docker containers and their container IDs, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3cc03-138">If you want to see status of the running Docker containers and their container IDs, use the following command:</span></span>

    ```sh
    docker ps
    ```

    <span data-ttu-id="3cc03-139">If you want to see the log from the device simulation container, run the following command.</span><span class="sxs-lookup"><span data-stu-id="3cc03-139">If you want to see the log from the device simulation container, run the following command.</span></span> <span data-ttu-id="3cc03-140">Replace the container ID with the ID of your device simulation container:</span><span class="sxs-lookup"><span data-stu-id="3cc03-140">Replace the container ID with the ID of your device simulation container:</span></span>

    ```sh
    docker logs -f 5d3f3e78822e
    ```

## <a name="run-simulation"></a><span data-ttu-id="3cc03-141">Run simulation</span><span class="sxs-lookup"><span data-stu-id="3cc03-141">Run simulation</span></span>

<span data-ttu-id="3cc03-142">You can now run a simulation using your custom device models:</span><span class="sxs-lookup"><span data-stu-id="3cc03-142">You can now run a simulation using your custom device models:</span></span>

1. <span data-ttu-id="3cc03-143">Launch your Device Simulation web UI from [Microsoft Azure IoT Solution Accelerators](https://www.azureiotsolutions.com/Accelerators#dashboard).</span><span class="sxs-lookup"><span data-stu-id="3cc03-143">Launch your Device Simulation web UI from [Microsoft Azure IoT Solution Accelerators](https://www.azureiotsolutions.com/Accelerators#dashboard).</span></span>

1. <span data-ttu-id="3cc03-144">Use the web UI to configure and run a simulation using one of your custom device models.</span><span class="sxs-lookup"><span data-stu-id="3cc03-144">Use the web UI to configure and run a simulation using one of your custom device models.</span></span>

1. <span data-ttu-id="3cc03-145">When you run a simulation, click the **View IoT Hub metrics in the Azure portal** to monitor the simulation.</span><span class="sxs-lookup"><span data-stu-id="3cc03-145">When you run a simulation, click the **View IoT Hub metrics in the Azure portal** to monitor the simulation.</span></span> <span data-ttu-id="3cc03-146">Alternatively, you can use the following Azure CLI command to monitor the device to cloud traffic.</span><span class="sxs-lookup"><span data-stu-id="3cc03-146">Alternatively, you can use the following Azure CLI command to monitor the device to cloud traffic.</span></span> <span data-ttu-id="3cc03-147">Replace the name of the IoT hub with your hub name:</span><span class="sxs-lookup"><span data-stu-id="3cc03-147">Replace the name of the IoT hub with your hub name:</span></span>

    ```azurecli-interactive
    az iot hub monitor-events -n contoso-simulation9dc75
    ```

## <a name="clean-up-resources"></a><span data-ttu-id="3cc03-148">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3cc03-148">Clean up resources</span></span>

<span data-ttu-id="3cc03-149">If you plan to explore further, leave the Device Simulation solution accelerator deployed.</span><span class="sxs-lookup"><span data-stu-id="3cc03-149">If you plan to explore further, leave the Device Simulation solution accelerator deployed.</span></span>

<span data-ttu-id="3cc03-150">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**.</span><span class="sxs-lookup"><span data-stu-id="3cc03-150">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cc03-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="3cc03-151">Next steps</span></span>

<span data-ttu-id="3cc03-152">This guide showed you how to deploy custom device models to the Device Simulation solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="3cc03-152">This guide showed you how to deploy custom device models to the Device Simulation solution accelerator.</span></span> <span data-ttu-id="3cc03-153">The suggested next step is to learn more about the [device model schema](iot-accelerators-device-simulation-device-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3cc03-153">The suggested next step is to learn more about the [device model schema](iot-accelerators-device-simulation-device-schema.md).</span></span>
