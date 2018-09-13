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
# <a name="manage-a-configuration-server"></a>Manage a Configuration Server

Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure. This article describes how you can set up, configure, and manage the Configuration Server.

## <a name="prerequisites"></a>Prerequisites
The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.

> [!NOTE]
> [Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements. Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a>Downloading the Configuration Server software
1. Log on to the Azure portal and browse to your Recovery Services Vault.
2. Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).

  ![Add Servers Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Click the **+Servers** button.
4. On the **Add Server** page, click the Download button to download the Registration key. You need this key during the Configuration Server installation to register it with Azure Site Recovery service.
5. Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.

  ![Download Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Installing and Registering a Configuration Server from GUI
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Installing and registering a Configuration Server using Command line

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Sample usage
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Configuration Server installer command-line arguments.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Create a MySql credentials file
MySQLCredsFilePath parameter takes a file as input. Create the file using the following format and pass it as input MySQLCredsFilePath parameter.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Create a proxy settings configuration file
ProxySettingsFilePath parameter takes a file as input. Create the file using the following format and pass it as input ProxySettingsFilePath parameter.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modifying proxy settings for Configuration Server
1. Login to your Configuration Server.
2. Launch the cspsconfigtool.exe using the shortcut on your.
3. Click the **Vault Registration** tab.
4. Download a new Vault Registration file from the portal and provide it as input to the tool.

  ![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Provide the new Proxy Server details and click the **Register** button.
6. Open an Admin PowerShell command window.
7. Run the following command
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a>Re-register a Configuration Server with the same Recovery Services Vault
  1. Login to your Configuration Server.
  2. Launch the cspsconfigtool.exe using the shortcut on your desktop.
  3. Click the **Vault Registration** tab.
  4. Download a new Registration file from the portal and provide it as input to the tool.
        ![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Provide the Proxy Server details and click the **Register** button.  
  6. Open an Admin PowerShell command window.
  7. Run the following command

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Registering a Configuration Server with a different Recovery Services Vault.
1. Login to your Configuration Server.
2. from an admin command prompt, run the command

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Launch the cspsconfigtool.exe using the shortcut on your.
4. Click the **Vault Registration** tab.
5. Download a new Registration file from the portal and provide it as input to the tool.

    ![register-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Provide the Proxy Server details and click the **Register** button.  
7. Open an Admin PowerShell command window.
8. Run the following command
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Decommissioning a Configuration Server
Ensure the following before you start decommissioning your Configuration Server.
1. Disable protection for all virtual machines under this Configuration Server.
2. Disassociate all Replication policies from the Configuration Server.
3. Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.

### <a name="delete-the-configuration-server-from-azure-portal"></a>Delete the Configuration Server from Azure portal
1. In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.
2. Click the Configuration Server that you want to decommission.
3. On the Configuration Server's details page, click the Delete button.

  ![delete-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.png)
4. Click **Yes** to confirm the deletion of the server.

  >[!WARNING]
  If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server. Delete these entities before you try to delete the vault.

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a>Uninstall the Configuration Server software and its dependencies
  > [!TIP]
  If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly

1. Log on to the Configuration Server as an Administrator.
2. Open up Control Panel > Program > Uninstall Programs
3. Uninstall the programs in the following sequence:
  * Microsoft Azure Recovery Services Agent
  * Microsoft Azure Site Recovery Mobility Service/Master Target server
  * Microsoft Azure Site Recovery Provider
  * Microsoft Azure Site Recovery Configuration Server/Process Server
  * Microsoft Azure Site Recovery Configuration Server Dependencies
  * MySQL Server 5.5
4. Run the following command from and admin command prompt.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Renew Configuration Server Secure Socket Layer(SSL) Certificates
The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server. The Configuration Server's webserver uses an SSL certificate to authenticate its clients. This certificate has an expiry of three years and can be renewed at any time using the following method:

> [!WARNING]
Certificate expiry can be performed only on version 9.4.XXXX.X or higher. Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.

1. On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.
2. Click the Configuration Server for which you need to renew the SSL Certificate for.
3. Under the Configuration Server health, you can see the expiry date for the SSL Certificate.
4. Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:

  ![delete-configuration-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.PNG)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Secure Socket Layer certificate expiry warning

> [!NOTE]
The SSL Certificate's validity for all installations that happened before May 2016 was set to one year. you have started seeing certificate expiry notifications showing up in the Azure portal.

1. If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications). You start seeing a notification banner on the Vault's resource page.

  ![certificate-notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Click the banner to get additional details on the Certificate expiry.

  ![certificate-details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  If instead of a **Renew Now** button you see an **Upgrade Now** button. This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.

## <a name="sizing-requirements-for-a-configuration-server"></a>Sizing requirements for a Configuration Server

| **CPU** | **Memory** | **Cache disk size** | **Data change rate** | **Protected machines** |
| --- | --- | --- | --- | --- |
| 8 vCPUs (2 sockets * 4 cores @ 2.5 GHz) |16 GB |300 GB |500 GB or less |Replicate fewer than 100 machines. |
| 12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) |18 GB |600 GB |500 GB to 1 TB |Replicate between 100-150 machines. |
| 16 vCPUs (2 sockets * 8 cores @ 2.5 GHz) |32 GB |1 TB |1 TB to 2 TB |Replicate between 150-200 machines. |

  >[!TIP]
  If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic. Learn more about How to deploy Scale-out Process severs.


## <a name="common-issues"></a>Common issues
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]









