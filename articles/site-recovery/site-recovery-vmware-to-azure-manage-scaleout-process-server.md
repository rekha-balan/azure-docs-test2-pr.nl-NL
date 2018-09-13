---
title: " Manage a Scale-out Process Server in Azure Site Recovery | Microsoft Docs"
description: This article describes how to set up and manage a Scale-out Process Server in Azure Site Recovery.
services: site-recovery
documentationcenter: ''
author: AnoopVasudavan
manager: gauravd
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 2/14/2017
ms.author: anoopkv
ms.openlocfilehash: 98922f35447ec30302e34b88bfe9737bd25e77f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553349"
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="79fba-103">Manage a Scale-out Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="79fba-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="79fba-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="79fba-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span><span class="sxs-lookup"><span data-stu-id="79fba-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79fba-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="79fba-106">Prerequisites</span></span>
<span data-ttu-id="79fba-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span><span class="sxs-lookup"><span data-stu-id="79fba-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="79fba-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span><span class="sxs-lookup"><span data-stu-id="79fba-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="79fba-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="79fba-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="79fba-110">Downloading the Scale-out Process Server software</span><span class="sxs-lookup"><span data-stu-id="79fba-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="79fba-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span><span class="sxs-lookup"><span data-stu-id="79fba-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="79fba-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span><span class="sxs-lookup"><span data-stu-id="79fba-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="79fba-113">Select your configuration server to drill down into the configuration server's details page.</span><span class="sxs-lookup"><span data-stu-id="79fba-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="79fba-114">Click the **+ Process Server** button.</span><span class="sxs-lookup"><span data-stu-id="79fba-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="79fba-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span><span class="sxs-lookup"><span data-stu-id="79fba-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![Add Servers Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="79fba-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span><span class="sxs-lookup"><span data-stu-id="79fba-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="79fba-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span><span class="sxs-lookup"><span data-stu-id="79fba-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="79fba-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="79fba-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="79fba-120">Installing and registering a Scale-out Process Server from GUI</span><span class="sxs-lookup"><span data-stu-id="79fba-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="79fba-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span><span class="sxs-lookup"><span data-stu-id="79fba-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="79fba-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span><span class="sxs-lookup"><span data-stu-id="79fba-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="79fba-123">After setting up the server, you migrate source machines to use it.</span><span class="sxs-lookup"><span data-stu-id="79fba-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="79fba-124">Installing and registering a Scale-out Process Server using command-line</span><span class="sxs-lookup"><span data-stu-id="79fba-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="79fba-125">Sample usage</span><span class="sxs-lookup"><span data-stu-id="79fba-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="79fba-126">Scale-out Process Server installer command-line arguments.</span><span class="sxs-lookup"><span data-stu-id="79fba-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="79fba-127">Create a proxy settings configuration file</span><span class="sxs-lookup"><span data-stu-id="79fba-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="79fba-128">ProxySettingsFilePath parameter takes a file as input.</span><span class="sxs-lookup"><span data-stu-id="79fba-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="79fba-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span><span class="sxs-lookup"><span data-stu-id="79fba-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="79fba-130">Modifying proxy settings for Scale-out Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="79fba-131">Login  into your Scale-out Process Server.</span><span class="sxs-lookup"><span data-stu-id="79fba-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="79fba-132">Open an Admin PowerShell command window.</span><span class="sxs-lookup"><span data-stu-id="79fba-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="79fba-133">Run the following command</span><span class="sxs-lookup"><span data-stu-id="79fba-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="79fba-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span><span class="sxs-lookup"><span data-stu-id="79fba-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt
  
  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="79fba-135">Re-registering a Scale-out Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="79fba-136">Next open an Admin command prompt.</span><span class="sxs-lookup"><span data-stu-id="79fba-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="79fba-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span><span class="sxs-lookup"><span data-stu-id="79fba-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="79fba-138">Upgrading a Scale-out Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="79fba-139">Decommissioning a Scale-out Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="79fba-140">Ensure that:</span><span class="sxs-lookup"><span data-stu-id="79fba-140">Ensure that:</span></span>
  - <span data-ttu-id="79fba-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="79fba-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="79fba-142">Process Server's is still able to communicate with the Configuration server.</span><span class="sxs-lookup"><span data-stu-id="79fba-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="79fba-143">Log in to the process server as an administrator</span><span class="sxs-lookup"><span data-stu-id="79fba-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="79fba-144">Open up Control Panel > Program > Uninstall Programs</span><span class="sxs-lookup"><span data-stu-id="79fba-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="79fba-145">Uninstall the programs in the sequence given following:</span><span class="sxs-lookup"><span data-stu-id="79fba-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="79fba-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="79fba-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span><span class="sxs-lookup"><span data-stu-id="79fba-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="79fba-148">Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="79fba-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="79fba-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="79fba-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="79fba-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="79fba-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="79fba-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span><span class="sxs-lookup"><span data-stu-id="79fba-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="79fba-152">Sizing requirements for a Scale-out Process Server</span><span class="sxs-lookup"><span data-stu-id="79fba-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="79fba-153">**Additional process server**</span><span class="sxs-lookup"><span data-stu-id="79fba-153">**Additional process server**</span></span> | <span data-ttu-id="79fba-154">**Cache disk size**</span><span class="sxs-lookup"><span data-stu-id="79fba-154">**Cache disk size**</span></span> | <span data-ttu-id="79fba-155">**Data change rate**</span><span class="sxs-lookup"><span data-stu-id="79fba-155">**Data change rate**</span></span> | <span data-ttu-id="79fba-156">**Protected machines**</span><span class="sxs-lookup"><span data-stu-id="79fba-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="79fba-157">4 vCPUs (2 sockets \* 2 cores @ 2.5 GHz), 8-GB memory</span><span class="sxs-lookup"><span data-stu-id="79fba-157">4 vCPUs (2 sockets \* 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="79fba-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="79fba-158">300 GB</span></span> |<span data-ttu-id="79fba-159">250 GB or less</span><span class="sxs-lookup"><span data-stu-id="79fba-159">250 GB or less</span></span> |<span data-ttu-id="79fba-160">Replicate 85 or less machines.</span><span class="sxs-lookup"><span data-stu-id="79fba-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="79fba-161">8 vCPUs (2 sockets \* 4 cores @ 2.5 GHz), 12-GB memory</span><span class="sxs-lookup"><span data-stu-id="79fba-161">8 vCPUs (2 sockets \* 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="79fba-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="79fba-162">600 GB</span></span> |<span data-ttu-id="79fba-163">250 GB to 1 TB</span><span class="sxs-lookup"><span data-stu-id="79fba-163">250 GB to 1 TB</span></span> |<span data-ttu-id="79fba-164">Replicate between 85-150 machines.</span><span class="sxs-lookup"><span data-stu-id="79fba-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="79fba-165">12 vCPUs (2 sockets \* 6 cores @ 2.5 GHz) 24-GB memory</span><span class="sxs-lookup"><span data-stu-id="79fba-165">12 vCPUs (2 sockets \* 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="79fba-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="79fba-166">1 TB</span></span> |<span data-ttu-id="79fba-167">1 TB to 2 TB</span><span class="sxs-lookup"><span data-stu-id="79fba-167">1 TB to 2 TB</span></span> |<span data-ttu-id="79fba-168">Replicate between 150-225 machines.</span><span class="sxs-lookup"><span data-stu-id="79fba-168">Replicate between 150-225 machines.</span></span> |

