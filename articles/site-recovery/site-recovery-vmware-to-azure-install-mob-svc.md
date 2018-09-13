---
title: Install Mobility Service (VMware or physical to Azure) | Microsoft Docs
description: Learn how to install the Mobility Service agent to protect your on-premises computers.
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
ms.date: 2/20/2017
ms.author: anoopkv
ms.openlocfilehash: 6437190ac58a021ce84993f667bbb5fad6031bb3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553023"
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a>Install Mobility Service (VMware or physical to Azure)
Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server. Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure. You can deploy Mobility Service to the servers that you want to protect by using the following methods:


* [Install Mobility Service by using software deployment tools like System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)](site-recovery-automate-mobility-service-install.md)
* [Install Mobility Service manually by using the graphical user interface (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Install Mobility Service manually at a command prompt](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Install Mobility Service by push installation from Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent). When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.

## <a name="prerequisites"></a>Prerequisites
Complete these prerequisite steps before you manually install Mobility Service on your server:
1. Sign in to your configuration server, and then open a Command Prompt window as an administrator.
2. Change the directory to the bin folder, and then create a passphrase file:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Store the passphrase file in a secure location. You use the file during the Mobility Service installation.
4. Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Mobility Service installer-to-operating system mapping

| Installer file template name| Operating system |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64-bit) </br> Windows Server 2012 (64-bit) </br> Windows Server 2012 R2 (64-bit) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (64-bit only)|
|Microsoft-ASR_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (64-bit only)|


## <a name="install-mobility-service-manually-by-using-the-gui"></a>Install Mobility Service manually by using the GUI

>[!NOTE]
> The GUI-based installation works only with Windows operating systems.

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Install Mobility Service manually at a command prompt

### <a name="command-line-installation-on-a-windows-computer"></a>Command-line installation on a Windows computer
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Command-line installation on a Linux computer
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Install Mobility Service by push installation from Azure Site Recovery
To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Uninstall Mobility Service on a Windows Server computer
Use one of the following methods to uninstall Mobility Service on a Windows Server computer.

### <a name="uninstall-by-using-the-gui"></a>Uninstall by using the GUI
1. In Control Panel, select **Programs**.
2. Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.

### <a name="uninstall-at-a-command-prompt"></a>Uninstall at a command prompt
1. Open a Command Prompt window as an administrator.
2. To uninstall Mobility Service, run the following command:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Uninstall Mobility Service on a Linux computer
1. On your Linux server, sign in as a **root** user.
2. In a terminal, go to /user/local/ASR.
3. To uninstall Mobility Service, run the following command:

```
uninstall.sh -Y
```
