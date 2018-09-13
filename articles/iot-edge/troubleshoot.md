---
title: Troubleshoot Azure IoT Edge | Microsoft Docs
description: Resolve common issues and learn troubleshooting skills for Azure IoT Edge
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/26/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: a6102a6bc28486c24134bbc172b9e8a7e1a61244
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856639"
---
# <a name="common-issues-and-resolutions-for-azure-iot-edge"></a><span data-ttu-id="2f9be-103">Common issues and resolutions for Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="2f9be-103">Common issues and resolutions for Azure IoT Edge</span></span>

<span data-ttu-id="2f9be-104">If you experience issues running Azure IoT Edge in your environment, use this article as a guide for troubleshooting and resolution.</span><span class="sxs-lookup"><span data-stu-id="2f9be-104">If you experience issues running Azure IoT Edge in your environment, use this article as a guide for troubleshooting and resolution.</span></span> 

## <a name="standard-diagnostic-steps"></a><span data-ttu-id="2f9be-105">Standard diagnostic steps</span><span class="sxs-lookup"><span data-stu-id="2f9be-105">Standard diagnostic steps</span></span> 

<span data-ttu-id="2f9be-106">When you encounter an issue, learn more about the state of your IoT Edge device by reviewing the container logs and messages that pass to and from the device.</span><span class="sxs-lookup"><span data-stu-id="2f9be-106">When you encounter an issue, learn more about the state of your IoT Edge device by reviewing the container logs and messages that pass to and from the device.</span></span> <span data-ttu-id="2f9be-107">Use the commands and tools in this section to gather information.</span><span class="sxs-lookup"><span data-stu-id="2f9be-107">Use the commands and tools in this section to gather information.</span></span> 

### <a name="check-the-status-of-the-iot-edge-security-manager-and-its-logs"></a><span data-ttu-id="2f9be-108">Check the status of the IoT Edge Security Manager and its logs:</span><span class="sxs-lookup"><span data-stu-id="2f9be-108">Check the status of the IoT Edge Security Manager and its logs:</span></span>

<span data-ttu-id="2f9be-109">On Linux:</span><span class="sxs-lookup"><span data-stu-id="2f9be-109">On Linux:</span></span>
- <span data-ttu-id="2f9be-110">To view the status of the IoT Edge Security Manager:</span><span class="sxs-lookup"><span data-stu-id="2f9be-110">To view the status of the IoT Edge Security Manager:</span></span>

   ```bash
   sudo systemctl status iotedge
   ```

- <span data-ttu-id="2f9be-111">To view the logs of the IoT Edge Security Manager:</span><span class="sxs-lookup"><span data-stu-id="2f9be-111">To view the logs of the IoT Edge Security Manager:</span></span>

    ```bash
    sudo journalctl -u iotedge -f
    ```

- <span data-ttu-id="2f9be-112">To view more detailed logs of the IoT Edge Security Manager:</span><span class="sxs-lookup"><span data-stu-id="2f9be-112">To view more detailed logs of the IoT Edge Security Manager:</span></span>

   - <span data-ttu-id="2f9be-113">Edit the iotedge daemon settings:</span><span class="sxs-lookup"><span data-stu-id="2f9be-113">Edit the iotedge daemon settings:</span></span>

      ```bash
      sudo systemctl edit iotedge.service
      ```
   
   - <span data-ttu-id="2f9be-114">Update the following lines:</span><span class="sxs-lookup"><span data-stu-id="2f9be-114">Update the following lines:</span></span>
    
      ```
      [Service]
      Environment=IOTEDGE_LOG=edgelet=debug
      ```
    
   - <span data-ttu-id="2f9be-115">Restart the IoT Edge Security Daemon:</span><span class="sxs-lookup"><span data-stu-id="2f9be-115">Restart the IoT Edge Security Daemon:</span></span>
    
      ```bash
      sudo systemctl cat iotedge.service
      sudo systemctl daemon-reload
      sudo systemctl restart iotedge
      ```

<span data-ttu-id="2f9be-116">On Windows:</span><span class="sxs-lookup"><span data-stu-id="2f9be-116">On Windows:</span></span>
- <span data-ttu-id="2f9be-117">To view the status of the IoT Edge Security Manager:</span><span class="sxs-lookup"><span data-stu-id="2f9be-117">To view the status of the IoT Edge Security Manager:</span></span>

   ```powershell
   Get-Service iotedge
   ```

- <span data-ttu-id="2f9be-118">To view the logs of the IoT Edge Security Manager:</span><span class="sxs-lookup"><span data-stu-id="2f9be-118">To view the logs of the IoT Edge Security Manager:</span></span>

   ```powershell
   # Displays logs from today, newest at the bottom.
 
   Get-WinEvent -ea SilentlyContinue `
   -FilterHashtable @{ProviderName= "iotedged";
     LogName = "application"; StartTime = [datetime]::Today} |
   select TimeCreated, Message |
   sort-object @{Expression="TimeCreated";Descending=$false} |
   format-table -autosize -wrap
   ```

### <a name="if-the-iot-edge-security-manager-is-not-running-verify-your-yaml-configuration-file"></a><span data-ttu-id="2f9be-119">If the IoT Edge Security Manager is not running, verify your yaml configuration file</span><span class="sxs-lookup"><span data-stu-id="2f9be-119">If the IoT Edge Security Manager is not running, verify your yaml configuration file</span></span>

> [!WARNING]
> <span data-ttu-id="2f9be-120">YAML files cannot contain tabs as identation.</span><span class="sxs-lookup"><span data-stu-id="2f9be-120">YAML files cannot contain tabs as identation.</span></span> <span data-ttu-id="2f9be-121">Use 2 spaces instead.</span><span class="sxs-lookup"><span data-stu-id="2f9be-121">Use 2 spaces instead.</span></span>

<span data-ttu-id="2f9be-122">On Linux:</span><span class="sxs-lookup"><span data-stu-id="2f9be-122">On Linux:</span></span>

   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

<span data-ttu-id="2f9be-123">On Windows:</span><span class="sxs-lookup"><span data-stu-id="2f9be-123">On Windows:</span></span>

   ```cmd
   notepad C:\ProgramData\iotedge\config.yaml
   ```

### <a name="check-container-logs-for-issues"></a><span data-ttu-id="2f9be-124">Check container logs for issues</span><span class="sxs-lookup"><span data-stu-id="2f9be-124">Check container logs for issues</span></span>

<span data-ttu-id="2f9be-125">Once the IoT Edge Security Daemon is running, look at the logs of the containers to detect issues.</span><span class="sxs-lookup"><span data-stu-id="2f9be-125">Once the IoT Edge Security Daemon is running, look at the logs of the containers to detect issues.</span></span> <span data-ttu-id="2f9be-126">Start with your deployed containers, then look at the containers that make up the IoT Edge runtime: Edge Agent and Edge Hub.</span><span class="sxs-lookup"><span data-stu-id="2f9be-126">Start with your deployed containers, then look at the containers that make up the IoT Edge runtime: Edge Agent and Edge Hub.</span></span> <span data-ttu-id="2f9be-127">The Edge Agent logs typically provide info on the lifecycle of each container.</span><span class="sxs-lookup"><span data-stu-id="2f9be-127">The Edge Agent logs typically provide info on the lifecycle of each container.</span></span> <span data-ttu-id="2f9be-128">The Edge Hub logs provide info on messaging and routing.</span><span class="sxs-lookup"><span data-stu-id="2f9be-128">The Edge Hub logs provide info on messaging and routing.</span></span> 

   ```cmd
   iotedge logs <container name>
   ```

### <a name="view-the-messages-going-through-the-edge-hub"></a><span data-ttu-id="2f9be-129">View the messages going through the Edge hub</span><span class="sxs-lookup"><span data-stu-id="2f9be-129">View the messages going through the Edge hub</span></span>

<span data-ttu-id="2f9be-130">View the messages going through the Edge hub, and gather insights on device properties updates with verbose logs from the edgeAgent and edgeHub runtime containers.</span><span class="sxs-lookup"><span data-stu-id="2f9be-130">View the messages going through the Edge hub, and gather insights on device properties updates with verbose logs from the edgeAgent and edgeHub runtime containers.</span></span> <span data-ttu-id="2f9be-131">To turn on verbose logs on these containers, set `RuntimeLogLevel` in your yaml configuration file.</span><span class="sxs-lookup"><span data-stu-id="2f9be-131">To turn on verbose logs on these containers, set `RuntimeLogLevel` in your yaml configuration file.</span></span> <span data-ttu-id="2f9be-132">To open the file:</span><span class="sxs-lookup"><span data-stu-id="2f9be-132">To open the file:</span></span>

<span data-ttu-id="2f9be-133">On Linux:</span><span class="sxs-lookup"><span data-stu-id="2f9be-133">On Linux:</span></span>

   ```bash
   sudo nano /etc/iotedge/config.yaml
   ```

<span data-ttu-id="2f9be-134">On Windows:</span><span class="sxs-lookup"><span data-stu-id="2f9be-134">On Windows:</span></span>

   ```cmd
   notepad C:\ProgramData\iotedge\config.yaml
   ```

<span data-ttu-id="2f9be-135">By default, the `agent` element will look something like this:</span><span class="sxs-lookup"><span data-stu-id="2f9be-135">By default, the `agent` element will look something like this:</span></span>

   ```yaml
   agent:
     name: edgeAgent
     type: docker
     env: {}
     config:
       image: mcr.microsoft.com/azureiotedge-agent:1.0
       auth: {}
   ```

<span data-ttu-id="2f9be-136">Replace `env: {}` with:</span><span class="sxs-lookup"><span data-stu-id="2f9be-136">Replace `env: {}` with:</span></span>

> [!WARNING]
> <span data-ttu-id="2f9be-137">YAML files cannot contain tabs as identation.</span><span class="sxs-lookup"><span data-stu-id="2f9be-137">YAML files cannot contain tabs as identation.</span></span> <span data-ttu-id="2f9be-138">Use 2 spaces instead.</span><span class="sxs-lookup"><span data-stu-id="2f9be-138">Use 2 spaces instead.</span></span>

   ```yaml
   env:
     RuntimeLogLevel: debug
   ```

<span data-ttu-id="2f9be-139">Save the file and restart the IoT Edge security manager.</span><span class="sxs-lookup"><span data-stu-id="2f9be-139">Save the file and restart the IoT Edge security manager.</span></span>

<span data-ttu-id="2f9be-140">You can also check the messages being sent between IoT Hub and the IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="2f9be-140">You can also check the messages being sent between IoT Hub and the IoT Edge devices.</span></span> <span data-ttu-id="2f9be-141">View these messages by using the [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) extension for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2f9be-141">View these messages by using the [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) extension for Visual Studio Code.</span></span> <span data-ttu-id="2f9be-142">For more guidance, see [Handy tool when you develop with Azure IoT](https://blogs.msdn.microsoft.com/iotdev/2017/09/01/handy-tool-when-you-develop-with-azure-iot/).</span><span class="sxs-lookup"><span data-stu-id="2f9be-142">For more guidance, see [Handy tool when you develop with Azure IoT](https://blogs.msdn.microsoft.com/iotdev/2017/09/01/handy-tool-when-you-develop-with-azure-iot/).</span></span>

### <a name="restart-containers"></a><span data-ttu-id="2f9be-143">Restart containers</span><span class="sxs-lookup"><span data-stu-id="2f9be-143">Restart containers</span></span>
<span data-ttu-id="2f9be-144">After investigating the logs and messages for information, you can try restarting containers:</span><span class="sxs-lookup"><span data-stu-id="2f9be-144">After investigating the logs and messages for information, you can try restarting containers:</span></span>

```
iotedge restart <container name>
```

<span data-ttu-id="2f9be-145">Restart the IoT Edge runtime containers:</span><span class="sxs-lookup"><span data-stu-id="2f9be-145">Restart the IoT Edge runtime containers:</span></span>

```
iotedge restart edgeAgent && iotedge restart edgeHub
```

### <a name="restart-the-iot-edge-security-manager"></a><span data-ttu-id="2f9be-146">Restart the IoT Edge security manager</span><span class="sxs-lookup"><span data-stu-id="2f9be-146">Restart the IoT Edge security manager</span></span>

<span data-ttu-id="2f9be-147">If issue is still persisting, you can try restarting the IoT Edge security manager.</span><span class="sxs-lookup"><span data-stu-id="2f9be-147">If issue is still persisting, you can try restarting the IoT Edge security manager.</span></span>

<span data-ttu-id="2f9be-148">On Linux:</span><span class="sxs-lookup"><span data-stu-id="2f9be-148">On Linux:</span></span>

   ```cmd
   sudo systemctl restart iotedge
   ```

<span data-ttu-id="2f9be-149">On Windows:</span><span class="sxs-lookup"><span data-stu-id="2f9be-149">On Windows:</span></span>

   ```powershell
   Stop-Service iotedge -NoWait
   sleep 5
   Start-Service iotedge
   ```

## <a name="edge-agent-stops-after-about-a-minute"></a><span data-ttu-id="2f9be-150">Edge Agent stops after about a minute</span><span class="sxs-lookup"><span data-stu-id="2f9be-150">Edge Agent stops after about a minute</span></span>

<span data-ttu-id="2f9be-151">The Edge Agent starts and runs successfully for about a minute, then stops.</span><span class="sxs-lookup"><span data-stu-id="2f9be-151">The Edge Agent starts and runs successfully for about a minute, then stops.</span></span> <span data-ttu-id="2f9be-152">The logs indicate that the Edge Agent is attempting to connect to IoT Hub over AMQP, and then approximately 30 seconds later attempt to connect using AMQP over websocket.</span><span class="sxs-lookup"><span data-stu-id="2f9be-152">The logs indicate that the Edge Agent is attempting to connect to IoT Hub over AMQP, and then approximately 30 seconds later attempt to connect using AMQP over websocket.</span></span> <span data-ttu-id="2f9be-153">When that fails, the Edge Agent exits.</span><span class="sxs-lookup"><span data-stu-id="2f9be-153">When that fails, the Edge Agent exits.</span></span> 

<span data-ttu-id="2f9be-154">Example Edge Agent logs:</span><span class="sxs-lookup"><span data-stu-id="2f9be-154">Example Edge Agent logs:</span></span>

```output
2017-11-28 18:46:19 [INF] - Starting module management agent. 
2017-11-28 18:46:19 [INF] - Version - 1.0.7516610 (03c94f85d0833a861a43c669842f0817924911d5) 
2017-11-28 18:46:19 [INF] - Edge agent attempting to connect to IoT Hub via AMQP... 
2017-11-28 18:46:49 [INF] - Edge agent attempting to connect to IoT Hub via AMQP over WebSocket... 
```

### <a name="root-cause"></a><span data-ttu-id="2f9be-155">Root cause</span><span class="sxs-lookup"><span data-stu-id="2f9be-155">Root cause</span></span>
<span data-ttu-id="2f9be-156">A networking configuration on the host network is preventing the Edge Agent from reaching the network.</span><span class="sxs-lookup"><span data-stu-id="2f9be-156">A networking configuration on the host network is preventing the Edge Agent from reaching the network.</span></span> <span data-ttu-id="2f9be-157">The agent attempts to connect over AMQP (port 5671) first.</span><span class="sxs-lookup"><span data-stu-id="2f9be-157">The agent attempts to connect over AMQP (port 5671) first.</span></span> <span data-ttu-id="2f9be-158">If this fails, it tries websockets (port 443).</span><span class="sxs-lookup"><span data-stu-id="2f9be-158">If this fails, it tries websockets (port 443).</span></span>

<span data-ttu-id="2f9be-159">The IoT Edge runtime sets up a network for each of the modules to communicate on.</span><span class="sxs-lookup"><span data-stu-id="2f9be-159">The IoT Edge runtime sets up a network for each of the modules to communicate on.</span></span> <span data-ttu-id="2f9be-160">On Linux, this network is a bridge network.</span><span class="sxs-lookup"><span data-stu-id="2f9be-160">On Linux, this network is a bridge network.</span></span> <span data-ttu-id="2f9be-161">On Windows, it uses NAT.</span><span class="sxs-lookup"><span data-stu-id="2f9be-161">On Windows, it uses NAT.</span></span> <span data-ttu-id="2f9be-162">This issue is more common on Windows devices using Windows containers that use the NAT network.</span><span class="sxs-lookup"><span data-stu-id="2f9be-162">This issue is more common on Windows devices using Windows containers that use the NAT network.</span></span> 

### <a name="resolution"></a><span data-ttu-id="2f9be-163">Resolution</span><span class="sxs-lookup"><span data-stu-id="2f9be-163">Resolution</span></span>
<span data-ttu-id="2f9be-164">Ensure that there is a route to the internet for the IP addresses assigned to this bridge/NAT network.</span><span class="sxs-lookup"><span data-stu-id="2f9be-164">Ensure that there is a route to the internet for the IP addresses assigned to this bridge/NAT network.</span></span> <span data-ttu-id="2f9be-165">Sometimes a VPN configuration on the host overrides the IoT Edge network.</span><span class="sxs-lookup"><span data-stu-id="2f9be-165">Sometimes a VPN configuration on the host overrides the IoT Edge network.</span></span> 

## <a name="edge-hub-fails-to-start"></a><span data-ttu-id="2f9be-166">Edge Hub fails to start</span><span class="sxs-lookup"><span data-stu-id="2f9be-166">Edge Hub fails to start</span></span>

<span data-ttu-id="2f9be-167">The Edge Hub fails to start, and prints the following message to the logs:</span><span class="sxs-lookup"><span data-stu-id="2f9be-167">The Edge Hub fails to start, and prints the following message to the logs:</span></span> 

```output
One or more errors occurred. 
(Docker API responded with status code=InternalServerError, response=
{\"message\":\"driver failed programming external connectivity on endpoint edgeHub (6a82e5e994bab5187939049684fb64efe07606d2bb8a4cc5655b2a9bad5f8c80): 
Error starting userland proxy: Bind for 0.0.0.0:443 failed: port is already allocated\"}\n) 
```

### <a name="root-cause"></a><span data-ttu-id="2f9be-168">Root cause</span><span class="sxs-lookup"><span data-stu-id="2f9be-168">Root cause</span></span>
<span data-ttu-id="2f9be-169">Some other process on the host machine has bound port 443.</span><span class="sxs-lookup"><span data-stu-id="2f9be-169">Some other process on the host machine has bound port 443.</span></span> <span data-ttu-id="2f9be-170">The Edge Hub maps ports 5671 and 443 for use in gateway scenarios.</span><span class="sxs-lookup"><span data-stu-id="2f9be-170">The Edge Hub maps ports 5671 and 443 for use in gateway scenarios.</span></span> <span data-ttu-id="2f9be-171">This port mapping fails if another process has already bound this port.</span><span class="sxs-lookup"><span data-stu-id="2f9be-171">This port mapping fails if another process has already bound this port.</span></span> 

### <a name="resolution"></a><span data-ttu-id="2f9be-172">Resolution</span><span class="sxs-lookup"><span data-stu-id="2f9be-172">Resolution</span></span>
<span data-ttu-id="2f9be-173">Find and stop the process that is using port 443.</span><span class="sxs-lookup"><span data-stu-id="2f9be-173">Find and stop the process that is using port 443.</span></span> <span data-ttu-id="2f9be-174">This process is usually a web server.</span><span class="sxs-lookup"><span data-stu-id="2f9be-174">This process is usually a web server.</span></span>

## <a name="edge-agent-cant-access-a-modules-image-403"></a><span data-ttu-id="2f9be-175">Edge Agent can't access a module's image (403)</span><span class="sxs-lookup"><span data-stu-id="2f9be-175">Edge Agent can't access a module's image (403)</span></span>
<span data-ttu-id="2f9be-176">A container fails to run, and the Edge Agent logs show a 403 error.</span><span class="sxs-lookup"><span data-stu-id="2f9be-176">A container fails to run, and the Edge Agent logs show a 403 error.</span></span> 

### <a name="root-cause"></a><span data-ttu-id="2f9be-177">Root cause</span><span class="sxs-lookup"><span data-stu-id="2f9be-177">Root cause</span></span>
<span data-ttu-id="2f9be-178">The Edge Agent doesn't have permissions to access a module's image.</span><span class="sxs-lookup"><span data-stu-id="2f9be-178">The Edge Agent doesn't have permissions to access a module's image.</span></span> 

### <a name="resolution"></a><span data-ttu-id="2f9be-179">Resolution</span><span class="sxs-lookup"><span data-stu-id="2f9be-179">Resolution</span></span>
<span data-ttu-id="2f9be-180">Make sure that your registry credentials are correctly specified in your deployment manifest</span><span class="sxs-lookup"><span data-stu-id="2f9be-180">Make sure that your registry credentials are correctly specified in your deployment manifest</span></span>

## <a name="iot-edge-security-daemon-fails-with-an-invalid-hostname"></a><span data-ttu-id="2f9be-181">IoT Edge security daemon fails with an invalid hostname</span><span class="sxs-lookup"><span data-stu-id="2f9be-181">IoT Edge security daemon fails with an invalid hostname</span></span>

<span data-ttu-id="2f9be-182">The command `sudo journalctl -u iotedge` fails and prints the following message:</span><span class="sxs-lookup"><span data-stu-id="2f9be-182">The command `sudo journalctl -u iotedge` fails and prints the following message:</span></span> 

```output
Error parsing user input data: invalid hostname. Hostname cannot be empty or greater than 64 characters
```

### <a name="root-cause"></a><span data-ttu-id="2f9be-183">Root cause</span><span class="sxs-lookup"><span data-stu-id="2f9be-183">Root cause</span></span>
<span data-ttu-id="2f9be-184">The IoT Edge runtime can only support hostnames that are shorter than 64 characters.</span><span class="sxs-lookup"><span data-stu-id="2f9be-184">The IoT Edge runtime can only support hostnames that are shorter than 64 characters.</span></span> <span data-ttu-id="2f9be-185">This usually isn't an issue for physical machines, but can occur when you set up the runtime on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f9be-185">This usually isn't an issue for physical machines, but can occur when you set up the runtime on a virtual machine.</span></span> <span data-ttu-id="2f9be-186">The automatically generated hostnames for Windows virtual machines hosted in Azure, in particular, tend to be long.</span><span class="sxs-lookup"><span data-stu-id="2f9be-186">The automatically generated hostnames for Windows virtual machines hosted in Azure, in particular, tend to be long.</span></span> 

### <a name="resolution"></a><span data-ttu-id="2f9be-187">Resolution</span><span class="sxs-lookup"><span data-stu-id="2f9be-187">Resolution</span></span>
<span data-ttu-id="2f9be-188">When you see this error, you can resolve it by configuring the DNS name of your virtual machine, and then setting the DNS name as the hostname in the setup command.</span><span class="sxs-lookup"><span data-stu-id="2f9be-188">When you see this error, you can resolve it by configuring the DNS name of your virtual machine, and then setting the DNS name as the hostname in the setup command.</span></span>

1. <span data-ttu-id="2f9be-189">In the Azure portal, navigate to the overview page of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f9be-189">In the Azure portal, navigate to the overview page of your virtual machine.</span></span> 
2. <span data-ttu-id="2f9be-190">Select **configure** under DNS name.</span><span class="sxs-lookup"><span data-stu-id="2f9be-190">Select **configure** under DNS name.</span></span> <span data-ttu-id="2f9be-191">If your virtual machine already has a DNS name configured, you don't need to configure a new one.</span><span class="sxs-lookup"><span data-stu-id="2f9be-191">If your virtual machine already has a DNS name configured, you don't need to configure a new one.</span></span> 

   ![Configure DNS name](./media/troubleshoot/configure-dns.png)

3. <span data-ttu-id="2f9be-193">Provide a value for **DNS name label** and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="2f9be-193">Provide a value for **DNS name label** and select **Save**.</span></span>
4. <span data-ttu-id="2f9be-194">Copy the new DNS name, which should be in the format **\<DNSnamelabel\>.\<vmlocation\>.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="2f9be-194">Copy the new DNS name, which should be in the format **\<DNSnamelabel\>.\<vmlocation\>.cloudapp.azure.com**.</span></span>
5. <span data-ttu-id="2f9be-195">Inside the virtual machine, use the following command to set up the IoT Edge runtime with your DNS name:</span><span class="sxs-lookup"><span data-stu-id="2f9be-195">Inside the virtual machine, use the following command to set up the IoT Edge runtime with your DNS name:</span></span>

   - <span data-ttu-id="2f9be-196">On Linux:</span><span class="sxs-lookup"><span data-stu-id="2f9be-196">On Linux:</span></span>

      ```bash
      sudo nano /etc/iotedge/config.yaml
      ```

   - <span data-ttu-id="2f9be-197">On Windows:</span><span class="sxs-lookup"><span data-stu-id="2f9be-197">On Windows:</span></span>

      ```cmd
      notepad C:\ProgramData\iotedge\config.yaml
      ```

## <a name="stability-issues-on-resource-constrained-devices"></a><span data-ttu-id="2f9be-198">Stability issues on resource constrained devices</span><span class="sxs-lookup"><span data-stu-id="2f9be-198">Stability issues on resource constrained devices</span></span> 
<span data-ttu-id="2f9be-199">You may encounter stability problems on constrained devices like the Raspberry Pi, especially when used as a gateway.</span><span class="sxs-lookup"><span data-stu-id="2f9be-199">You may encounter stability problems on constrained devices like the Raspberry Pi, especially when used as a gateway.</span></span> <span data-ttu-id="2f9be-200">Symptoms include out of memory exceptions in the edge hub module, downstream devices cannot connect or the device stops sending telemetry messages after a few hours.</span><span class="sxs-lookup"><span data-stu-id="2f9be-200">Symptoms include out of memory exceptions in the edge hub module, downstream devices cannot connect or the device stops sending telemetry messages after a few hours.</span></span>

### <a name="root-cause"></a><span data-ttu-id="2f9be-201">Root cause</span><span class="sxs-lookup"><span data-stu-id="2f9be-201">Root cause</span></span>
<span data-ttu-id="2f9be-202">The edge hub, which is part of the edge runtime, is optimized for performance by default and attempts to allocate large chunks of memory.</span><span class="sxs-lookup"><span data-stu-id="2f9be-202">The edge hub, which is part of the edge runtime, is optimized for performance by default and attempts to allocate large chunks of memory.</span></span> <span data-ttu-id="2f9be-203">This is not ideal for constrained edge devices and can cause stability problems.</span><span class="sxs-lookup"><span data-stu-id="2f9be-203">This is not ideal for constrained edge devices and can cause stability problems.</span></span>

### <a name="resolution"></a><span data-ttu-id="2f9be-204">Resolution</span><span class="sxs-lookup"><span data-stu-id="2f9be-204">Resolution</span></span>
<span data-ttu-id="2f9be-205">For the edge hub set an environment variable **OptimizeForPerformance** to **false**.</span><span class="sxs-lookup"><span data-stu-id="2f9be-205">For the edge hub set an environment variable **OptimizeForPerformance** to **false**.</span></span> <span data-ttu-id="2f9be-206">There are two ways to do this:</span><span class="sxs-lookup"><span data-stu-id="2f9be-206">There are two ways to do this:</span></span>

<span data-ttu-id="2f9be-207">In the UI:</span><span class="sxs-lookup"><span data-stu-id="2f9be-207">In the UI:</span></span> 

<span data-ttu-id="2f9be-208">In the portal from *Device Details*->*Set Modules*->*Configure advanced Edge Runtime settings*, create an environment variable called *OptimizeForPerformance* that is set to *false* for the *Edge Hub*.</span><span class="sxs-lookup"><span data-stu-id="2f9be-208">In the portal from *Device Details*->*Set Modules*->*Configure advanced Edge Runtime settings*, create an environment variable called *OptimizeForPerformance* that is set to *false* for the *Edge Hub*.</span></span>

![optimizeforperformance][img-optimize-for-perf]

<span data-ttu-id="2f9be-210">**OR**</span><span class="sxs-lookup"><span data-stu-id="2f9be-210">**OR**</span></span>

<span data-ttu-id="2f9be-211">In the deployment manifest:</span><span class="sxs-lookup"><span data-stu-id="2f9be-211">In the deployment manifest:</span></span>

```json
  "edgeHub": {
    "type": "docker",
    "settings": {
      "image": "mcr.microsoft.com/azureiotedge-hub:1.0",
      "createOptions": <snipped>
    },
    "env": {
      "OptimizeForPerformance": {
          "value": "false"
      }
    },
```
## <a name="cant-get-the-iot-edge-daemon-logs-on-windows"></a><span data-ttu-id="2f9be-212">Can't get the IoT Edge daemon logs on Windows</span><span class="sxs-lookup"><span data-stu-id="2f9be-212">Can't get the IoT Edge daemon logs on Windows</span></span>
<span data-ttu-id="2f9be-213">If you get an EventLogException when using `Get-WinEvent` on Windows, check your registry entries.</span><span class="sxs-lookup"><span data-stu-id="2f9be-213">If you get an EventLogException when using `Get-WinEvent` on Windows, check your registry entries.</span></span>

### <a name="root-cause"></a><span data-ttu-id="2f9be-214">Root cause</span><span class="sxs-lookup"><span data-stu-id="2f9be-214">Root cause</span></span>
<span data-ttu-id="2f9be-215">The `Get-WinEvent` PowerShell command relies on an registry entry to be present to find logs by a specific `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="2f9be-215">The `Get-WinEvent` PowerShell command relies on an registry entry to be present to find logs by a specific `ProviderName`.</span></span>

### <a name="resolution"></a><span data-ttu-id="2f9be-216">Resolution</span><span class="sxs-lookup"><span data-stu-id="2f9be-216">Resolution</span></span>
<span data-ttu-id="2f9be-217">Set a registry entry for the IoT Edge daemon.</span><span class="sxs-lookup"><span data-stu-id="2f9be-217">Set a registry entry for the IoT Edge daemon.</span></span> <span data-ttu-id="2f9be-218">Create a **iotedge.reg** file with the following content, and import in to the Windows Registry by double-clicking it or using the `reg import iotedge.reg` command:</span><span class="sxs-lookup"><span data-stu-id="2f9be-218">Create a **iotedge.reg** file with the following content, and import in to the Windows Registry by double-clicking it or using the `reg import iotedge.reg` command:</span></span>

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application\iotedged]
"CustomSource"=dword:00000001
"EventMessageFile"="C:\\ProgramData\\iotedge\\iotedged.exe"
"TypesSupported"=dword:00000007
```


## <a name="next-steps"></a><span data-ttu-id="2f9be-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f9be-219">Next steps</span></span>
<span data-ttu-id="2f9be-220">Do you think that you found a bug in the IoT Edge platform?</span><span class="sxs-lookup"><span data-stu-id="2f9be-220">Do you think that you found a bug in the IoT Edge platform?</span></span> <span data-ttu-id="2f9be-221">Please, [submit an issue](https://github.com/Azure/iotedge/issues) so that we can continue to improve.</span><span class="sxs-lookup"><span data-stu-id="2f9be-221">Please, [submit an issue](https://github.com/Azure/iotedge/issues) so that we can continue to improve.</span></span> 

<!-- Images -->
[img-optimize-for-perf]: ./media/troubleshoot/OptimizeForPerformanceFalse.png
