---
title: " Manage a Configuration Server in Azure Site Recovery | Microsoft Docs"
description: This article describes how to set and manage a Configuration Server.
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
ms.openlocfilehash: e06d9df6f015ca54d16f5d2ffade758a9a825622
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554147"
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="b1ea9-103">Manage a Configuration Server</span><span class="sxs-lookup"><span data-stu-id="b1ea9-103">Manage a Configuration Server</span></span>

<span data-ttu-id="b1ea9-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="b1ea9-105">This article describes how you can set up, configure, and manage the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1ea9-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1ea9-106">Prerequisites</span></span>
<span data-ttu-id="b1ea9-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="b1ea9-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="b1ea9-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="b1ea9-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="b1ea9-110">Downloading the Configuration Server software</span><span class="sxs-lookup"><span data-stu-id="b1ea9-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="b1ea9-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="b1ea9-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span><span class="sxs-lookup"><span data-stu-id="b1ea9-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Add Servers Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="b1ea9-114">Click the **+Servers** button.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="b1ea9-115">On the **Add Server** page, click the Download button to download the Registration key.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="b1ea9-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="b1ea9-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Download Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="b1ea9-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="b1ea9-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="b1ea9-120">Installing and Registering a Configuration Server from GUI</span><span class="sxs-lookup"><span data-stu-id="b1ea9-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="b1ea9-121">Installing and registering a Configuration Server using Command line</span><span class="sxs-lookup"><span data-stu-id="b1ea9-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="b1ea9-122">Sample usage</span><span class="sxs-lookup"><span data-stu-id="b1ea9-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="b1ea9-123">Configuration Server installer command-line arguments.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="b1ea9-124">Create a MySql credentials file</span><span class="sxs-lookup"><span data-stu-id="b1ea9-124">Create a MySql credentials file</span></span>
<span data-ttu-id="b1ea9-125">MySQLCredsFilePath parameter takes a file as input.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="b1ea9-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="b1ea9-127">Create a proxy settings configuration file</span><span class="sxs-lookup"><span data-stu-id="b1ea9-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="b1ea9-128">ProxySettingsFilePath parameter takes a file as input.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="b1ea9-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="b1ea9-130">Modifying proxy settings for Configuration Server</span><span class="sxs-lookup"><span data-stu-id="b1ea9-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="b1ea9-131">Login to your Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="b1ea9-132">Launch the cspsconfigtool.exe using the shortcut on your.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="b1ea9-133">Click the **Vault Registration** tab.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="b1ea9-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="b1ea9-136">Provide the new Proxy Server details and click the **Register** button.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="b1ea9-137">Open an Admin PowerShell command window.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="b1ea9-138">Run the following command</span><span class="sxs-lookup"><span data-stu-id="b1ea9-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="b1ea9-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="b1ea9-140">Re-register a Configuration Server with the same Recovery Services Vault</span><span class="sxs-lookup"><span data-stu-id="b1ea9-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="b1ea9-141">Login to your Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="b1ea9-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="b1ea9-143">Click the **Vault Registration** tab.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="b1ea9-144">Download a new Registration file from the portal and provide it as input to the tool.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="b1ea9-145">![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="b1ea9-145">![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="b1ea9-146">Provide the Proxy Server details and click the **Register** button.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="b1ea9-147">Open an Admin PowerShell command window.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="b1ea9-148">Run the following command</span><span class="sxs-lookup"><span data-stu-id="b1ea9-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="b1ea9-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="b1ea9-150">Registering a Configuration Server with a different Recovery Services Vault.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="b1ea9-151">Login to your Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="b1ea9-152">from an admin command prompt, run the command</span><span class="sxs-lookup"><span data-stu-id="b1ea9-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="b1ea9-153">Launch the cspsconfigtool.exe using the shortcut on your.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="b1ea9-154">Click the **Vault Registration** tab.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="b1ea9-155">Download a new Registration file from the portal and provide it as input to the tool.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="b1ea9-157">Provide the Proxy Server details and click the **Register** button.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="b1ea9-158">Open an Admin PowerShell command window.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="b1ea9-159">Run the following command</span><span class="sxs-lookup"><span data-stu-id="b1ea9-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="b1ea9-160">Decommissioning a Configuration Server</span><span class="sxs-lookup"><span data-stu-id="b1ea9-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="b1ea9-161">Ensure the following before you start decommissioning your Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="b1ea9-162">Disable protection for all virtual machines under this Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="b1ea9-163">Disassociate all Replication policies from the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="b1ea9-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="b1ea9-165">Delete the Configuration Server from Azure portal</span><span class="sxs-lookup"><span data-stu-id="b1ea9-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="b1ea9-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="b1ea9-167">Click the Configuration Server that you want to decommission.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="b1ea9-168">On the Configuration Server's details page, click the Delete button.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![delete-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.png)
4. <span data-ttu-id="b1ea9-170">Click **Yes** to confirm the deletion of the server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="b1ea9-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="b1ea9-172">Delete these entities before you try to delete the vault.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="b1ea9-173">Uninstall the Configuration Server software and its dependencies</span><span class="sxs-lookup"><span data-stu-id="b1ea9-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="b1ea9-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span><span class="sxs-lookup"><span data-stu-id="b1ea9-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="b1ea9-175">Log on to the Configuration Server as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="b1ea9-176">Open up Control Panel > Program > Uninstall Programs</span><span class="sxs-lookup"><span data-stu-id="b1ea9-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="b1ea9-177">Uninstall the programs in the following sequence:</span><span class="sxs-lookup"><span data-stu-id="b1ea9-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="b1ea9-178">Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="b1ea9-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="b1ea9-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span><span class="sxs-lookup"><span data-stu-id="b1ea9-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="b1ea9-180">Microsoft Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="b1ea9-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="b1ea9-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span><span class="sxs-lookup"><span data-stu-id="b1ea9-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="b1ea9-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span><span class="sxs-lookup"><span data-stu-id="b1ea9-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="b1ea9-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="b1ea9-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="b1ea9-184">Run the following command from and admin command prompt.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="b1ea9-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span><span class="sxs-lookup"><span data-stu-id="b1ea9-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="b1ea9-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="b1ea9-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="b1ea9-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span><span class="sxs-lookup"><span data-stu-id="b1ea9-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="b1ea9-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="b1ea9-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="b1ea9-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="b1ea9-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="b1ea9-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="b1ea9-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="b1ea9-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![delete-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.PNG)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="b1ea9-196">Secure Socket Layer certificate expiry warning</span><span class="sxs-lookup"><span data-stu-id="b1ea9-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="b1ea9-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="b1ea9-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="b1ea9-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span><span class="sxs-lookup"><span data-stu-id="b1ea9-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="b1ea9-200">You start seeing a notification banner on the Vault's resource page.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certificate-notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="b1ea9-202">Click the banner to get additional details on the Certificate expiry.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![certificate-details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="b1ea9-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="b1ea9-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="b1ea9-206">Sizing requirements for a Configuration Server</span><span class="sxs-lookup"><span data-stu-id="b1ea9-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="b1ea9-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="b1ea9-207">**CPU**</span></span> | <span data-ttu-id="b1ea9-208">**Memory**</span><span class="sxs-lookup"><span data-stu-id="b1ea9-208">**Memory**</span></span> | <span data-ttu-id="b1ea9-209">**Cache disk size**</span><span class="sxs-lookup"><span data-stu-id="b1ea9-209">**Cache disk size**</span></span> | <span data-ttu-id="b1ea9-210">**Data change rate**</span><span class="sxs-lookup"><span data-stu-id="b1ea9-210">**Data change rate**</span></span> | <span data-ttu-id="b1ea9-211">**Protected machines**</span><span class="sxs-lookup"><span data-stu-id="b1ea9-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b1ea9-212">8 vCPUs (2 sockets \* 4 cores @ 2.5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b1ea9-212">8 vCPUs (2 sockets \* 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b1ea9-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-213">16 GB</span></span> |<span data-ttu-id="b1ea9-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-214">300 GB</span></span> |<span data-ttu-id="b1ea9-215">500 GB or less</span><span class="sxs-lookup"><span data-stu-id="b1ea9-215">500 GB or less</span></span> |<span data-ttu-id="b1ea9-216">Replicate fewer than 100 machines.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="b1ea9-217">12 vCPUs (2 sockets \* 6 cores @ 2.5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b1ea9-217">12 vCPUs (2 sockets \* 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b1ea9-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-218">18 GB</span></span> |<span data-ttu-id="b1ea9-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-219">600 GB</span></span> |<span data-ttu-id="b1ea9-220">500 GB to 1 TB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-220">500 GB to 1 TB</span></span> |<span data-ttu-id="b1ea9-221">Replicate between 100-150 machines.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="b1ea9-222">16 vCPUs (2 sockets \* 8 cores @ 2.5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b1ea9-222">16 vCPUs (2 sockets \* 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b1ea9-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-223">32 GB</span></span> |<span data-ttu-id="b1ea9-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-224">1 TB</span></span> |<span data-ttu-id="b1ea9-225">1 TB to 2 TB</span><span class="sxs-lookup"><span data-stu-id="b1ea9-225">1 TB to 2 TB</span></span> |<span data-ttu-id="b1ea9-226">Replicate between 150-200 machines.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="b1ea9-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="b1ea9-228">Learn more about How to deploy Scale-out Process severs.</span><span class="sxs-lookup"><span data-stu-id="b1ea9-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="b1ea9-229">Common issues</span><span class="sxs-lookup"><span data-stu-id="b1ea9-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]









