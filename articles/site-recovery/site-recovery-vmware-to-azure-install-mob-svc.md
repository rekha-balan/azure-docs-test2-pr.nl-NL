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
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="9c4e9-103">Install Mobility Service (VMware or physical to Azure)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="9c4e9-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="9c4e9-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="9c4e9-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span><span class="sxs-lookup"><span data-stu-id="9c4e9-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="9c4e9-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="9c4e9-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="9c4e9-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="9c4e9-109">Install Mobility Service manually by using the graphical user interface (GUI)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="9c4e9-110">Install Mobility Service manually at a command prompt</span><span class="sxs-lookup"><span data-stu-id="9c4e9-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="9c4e9-111">Install Mobility Service by push installation from Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9c4e9-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="9c4e9-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="9c4e9-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="9c4e9-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c4e9-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c4e9-114">Prerequisites</span></span>
<span data-ttu-id="9c4e9-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span><span class="sxs-lookup"><span data-stu-id="9c4e9-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="9c4e9-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="9c4e9-117">Change the directory to the bin folder, and then create a passphrase file:</span><span class="sxs-lookup"><span data-stu-id="9c4e9-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="9c4e9-118">Store the passphrase file in a secure location.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="9c4e9-119">You use the file during the Mobility Service installation.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="9c4e9-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="9c4e9-121">Mobility Service installer-to-operating system mapping</span><span class="sxs-lookup"><span data-stu-id="9c4e9-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="9c4e9-122">Installer file template name</span><span class="sxs-lookup"><span data-stu-id="9c4e9-122">Installer file template name</span></span>| <span data-ttu-id="9c4e9-123">Operating system</span><span class="sxs-lookup"><span data-stu-id="9c4e9-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="9c4e9-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="9c4e9-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="9c4e9-125">Windows Server 2008 R2 SP1 (64-bit)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="9c4e9-126">Windows Server 2012 (64-bit)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="9c4e9-127">Windows Server 2012 R2 (64-bit)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="9c4e9-128">Microsoft-ASR\_UA\*RHEL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="9c4e9-128">Microsoft-ASR\_UA\*RHEL6-64\*release.tar.gz</span></span>| <span data-ttu-id="9c4e9-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="9c4e9-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="9c4e9-131">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="9c4e9-131">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="9c4e9-132">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-132">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="9c4e9-133">Microsoft-ASR_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="9c4e9-133">Microsoft-ASR_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="9c4e9-134">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span><span class="sxs-lookup"><span data-stu-id="9c4e9-134">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="9c4e9-135">Install Mobility Service manually by using the GUI</span><span class="sxs-lookup"><span data-stu-id="9c4e9-135">Install Mobility Service manually by using the GUI</span></span>

>[!NOTE]
> <span data-ttu-id="9c4e9-136">The GUI-based installation works only with Windows operating systems.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-136">The GUI-based installation works only with Windows operating systems.</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="9c4e9-137">Install Mobility Service manually at a command prompt</span><span class="sxs-lookup"><span data-stu-id="9c4e9-137">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="9c4e9-138">Command-line installation on a Windows computer</span><span class="sxs-lookup"><span data-stu-id="9c4e9-138">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="9c4e9-139">Command-line installation on a Linux computer</span><span class="sxs-lookup"><span data-stu-id="9c4e9-139">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="9c4e9-140">Install Mobility Service by push installation from Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9c4e9-140">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="9c4e9-141">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-141">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="9c4e9-142">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-142">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="9c4e9-143">Uninstall Mobility Service on a Windows Server computer</span><span class="sxs-lookup"><span data-stu-id="9c4e9-143">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="9c4e9-144">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-144">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="9c4e9-145">Uninstall by using the GUI</span><span class="sxs-lookup"><span data-stu-id="9c4e9-145">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="9c4e9-146">In Control Panel, select **Programs**.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-146">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="9c4e9-147">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-147">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="9c4e9-148">Uninstall at a command prompt</span><span class="sxs-lookup"><span data-stu-id="9c4e9-148">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="9c4e9-149">Open a Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-149">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="9c4e9-150">To uninstall Mobility Service, run the following command:</span><span class="sxs-lookup"><span data-stu-id="9c4e9-150">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="9c4e9-151">Uninstall Mobility Service on a Linux computer</span><span class="sxs-lookup"><span data-stu-id="9c4e9-151">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="9c4e9-152">On your Linux server, sign in as a **root** user.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-152">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="9c4e9-153">In a terminal, go to /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="9c4e9-153">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="9c4e9-154">To uninstall Mobility Service, run the following command:</span><span class="sxs-lookup"><span data-stu-id="9c4e9-154">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
