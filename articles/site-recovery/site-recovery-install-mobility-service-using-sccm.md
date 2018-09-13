---
title: Automate Mobility Service installation for Azure Site Recovery by using software deployment tools | Microsoft Docs
description: This article helps you automate Mobility Service installation by using software deployment tools like System Center Configuration Manager.
services: site-recovery
documentationcenter: ''
author: AnoopVasudavan
manager: gauravd
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/10/2017
ms.author: anoopkv
ms.openlocfilehash: 9803099131fd27bab12998f69b42424206fdc93d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540694"
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="2917c-103">Automate Mobility Service installation by using software deployment tools</span><span class="sxs-lookup"><span data-stu-id="2917c-103">Automate Mobility Service installation by using software deployment tools</span></span>

<span data-ttu-id="2917c-104">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="2917c-104">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="2917c-105">Using a software deployment tool like Configuration Manager has the following advantages:</span><span class="sxs-lookup"><span data-stu-id="2917c-105">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="2917c-106">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span><span class="sxs-lookup"><span data-stu-id="2917c-106">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="2917c-107">Scaling deployment to hundreds of servers simultaneously</span><span class="sxs-lookup"><span data-stu-id="2917c-107">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="2917c-108">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span><span class="sxs-lookup"><span data-stu-id="2917c-108">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="2917c-109">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="2917c-109">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2917c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2917c-110">Prerequisites</span></span>
1. <span data-ttu-id="2917c-111">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span><span class="sxs-lookup"><span data-stu-id="2917c-111">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="2917c-112">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2917c-112">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="2917c-113">A configuration server that is already registered with Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2917c-113">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="2917c-114">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span><span class="sxs-lookup"><span data-stu-id="2917c-114">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="2917c-115">Deploy Mobility Service on computers running Windows</span><span class="sxs-lookup"><span data-stu-id="2917c-115">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="2917c-116">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="2917c-116">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="2917c-117">Step 1: Prepare for deployment</span><span class="sxs-lookup"><span data-stu-id="2917c-117">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="2917c-118">Create a folder on the network share, and name it **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="2917c-118">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="2917c-119">Sign in to your configuration server, and open an administrative command prompt.</span><span class="sxs-lookup"><span data-stu-id="2917c-119">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="2917c-120">Run the following commands to generate a passphrase file:</span><span class="sxs-lookup"><span data-stu-id="2917c-120">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="2917c-121">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span><span class="sxs-lookup"><span data-stu-id="2917c-121">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="2917c-122">Browse to the installer repository on the configuration server by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2917c-122">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="2917c-123">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span><span class="sxs-lookup"><span data-stu-id="2917c-123">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="2917c-124">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span><span class="sxs-lookup"><span data-stu-id="2917c-124">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2917c-125">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span><span class="sxs-lookup"><span data-stu-id="2917c-125">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
REM ==================================================
REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================
REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
TIMEOUT /t 10
REM =================================================
REM ==== Extract the installer ======================
CD %Temp%\MobSvc\Extracted
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed run install command ========
REM ==== Else run upgrade command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\temp\logfile.log
REM SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REM REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1} >> C:\Temp\logfile.log 2>&1
REM REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
REM IF NOT %ERRORLEVEL% EQU 0 (GOTO :INSTALL) ELSE GOTO :UPDATE
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UPDATE
:INSTALL
    echo "Install" >> c:\Temp\logfile.log
    UnifiedAgent.exe /Role "Agent" /CSEndpoint "10.10.20.168" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
GOTO :ENDSCRIPT
:UPDATE
    echo "Update" >> C:\Temp\logfile.log
    UnifiedAgent.exe /upgrade
:ENDSCRIPT

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="2917c-126">Step 2: Create a package</span><span class="sxs-lookup"><span data-stu-id="2917c-126">Step 2: Create a package</span></span>

1. <span data-ttu-id="2917c-127">Sign in to your Configuration Manager console.</span><span class="sxs-lookup"><span data-stu-id="2917c-127">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="2917c-128">Browse to **Software Library** > **Application Management** > **Packages**.</span><span class="sxs-lookup"><span data-stu-id="2917c-128">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="2917c-129">Right-click **Packages**, and select **Create Package**.</span><span class="sxs-lookup"><span data-stu-id="2917c-129">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="2917c-130">Provide values for the name, description, manufacturer, language, and version.</span><span class="sxs-lookup"><span data-stu-id="2917c-130">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="2917c-131">Select the **This package contains source files** check box.</span><span class="sxs-lookup"><span data-stu-id="2917c-131">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="2917c-132">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="2917c-132">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="2917c-134">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2917c-134">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="2917c-136">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2917c-136">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="2917c-137">(The other inputs can use their default values.)</span><span class="sxs-lookup"><span data-stu-id="2917c-137">(The other inputs can use their default values.)</span></span>
 
  | <span data-ttu-id="2917c-138">**Parameter name**</span><span class="sxs-lookup"><span data-stu-id="2917c-138">**Parameter name**</span></span> | <span data-ttu-id="2917c-139">**Value**</span><span class="sxs-lookup"><span data-stu-id="2917c-139">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="2917c-140">Name</span><span class="sxs-lookup"><span data-stu-id="2917c-140">Name</span></span> | <span data-ttu-id="2917c-141">Install Microsoft Azure Mobility Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="2917c-141">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="2917c-142">Command line</span><span class="sxs-lookup"><span data-stu-id="2917c-142">Command line</span></span> | <span data-ttu-id="2917c-143">install.bat</span><span class="sxs-lookup"><span data-stu-id="2917c-143">install.bat</span></span> |
  | <span data-ttu-id="2917c-144">Program can run</span><span class="sxs-lookup"><span data-stu-id="2917c-144">Program can run</span></span> | <span data-ttu-id="2917c-145">Whether or not a user is logged on</span><span class="sxs-lookup"><span data-stu-id="2917c-145">Whether or not a user is logged on</span></span> |

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="2917c-147">On the next page, select the target operating systems.</span><span class="sxs-lookup"><span data-stu-id="2917c-147">On the next page, select the target operating systems.</span></span> <span data-ttu-id="2917c-148">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="2917c-148">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png) 

10. <span data-ttu-id="2917c-150">To complete the wizard, click **Next** twice.</span><span class="sxs-lookup"><span data-stu-id="2917c-150">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="2917c-151">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span><span class="sxs-lookup"><span data-stu-id="2917c-151">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="2917c-152">Step 3: Deploy the package</span><span class="sxs-lookup"><span data-stu-id="2917c-152">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="2917c-153">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span><span class="sxs-lookup"><span data-stu-id="2917c-153">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="2917c-154">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="2917c-154">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="2917c-155">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span><span class="sxs-lookup"><span data-stu-id="2917c-155">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="2917c-156">Complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="2917c-156">Complete the wizard.</span></span> <span data-ttu-id="2917c-157">The package then starts replicating to the specified distribution points.</span><span class="sxs-lookup"><span data-stu-id="2917c-157">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="2917c-158">After the package distribution is done, right-click the package, and select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="2917c-158">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="2917c-159">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="2917c-159">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="2917c-160">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span><span class="sxs-lookup"><span data-stu-id="2917c-160">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Screenshot of Deploy Software wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="2917c-162">On the **Specify the content destination** page, select your **Distribution Points**.</span><span class="sxs-lookup"><span data-stu-id="2917c-162">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="2917c-163">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span><span class="sxs-lookup"><span data-stu-id="2917c-163">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Screenshot of Deploy Software wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="2917c-165">On the **Specify the schedule for this deployment** page, specify a schedule.</span><span class="sxs-lookup"><span data-stu-id="2917c-165">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="2917c-166">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="2917c-166">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="2917c-167">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span><span class="sxs-lookup"><span data-stu-id="2917c-167">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="2917c-168">Then complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="2917c-168">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="2917c-169">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span><span class="sxs-lookup"><span data-stu-id="2917c-169">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="2917c-170">You can monitor the deployment progress by using the Configuration Manager console.</span><span class="sxs-lookup"><span data-stu-id="2917c-170">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="2917c-171">Go to **Monitoring** > **Deployments** > *[your package name]*.</span><span class="sxs-lookup"><span data-stu-id="2917c-171">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Screenshot of Configuration Manager option to monitor deployments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/Report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="2917c-173">Deploy Mobility Service on computers running Linux</span><span class="sxs-lookup"><span data-stu-id="2917c-173">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="2917c-174">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="2917c-174">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="2917c-175">Step 1: Prepare for deployment</span><span class="sxs-lookup"><span data-stu-id="2917c-175">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="2917c-176">Create a folder on the network share, and name it as **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="2917c-176">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="2917c-177">Sign in to your configuration server, and open an administrative command prompt.</span><span class="sxs-lookup"><span data-stu-id="2917c-177">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="2917c-178">Run the following commands to generate a passphrase file:</span><span class="sxs-lookup"><span data-stu-id="2917c-178">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="2917c-179">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span><span class="sxs-lookup"><span data-stu-id="2917c-179">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="2917c-180">Browse to the installer repository on the configuration server by running the command:</span><span class="sxs-lookup"><span data-stu-id="2917c-180">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="2917c-181">Copy the following files to the **MobSvcLinux** folder on your network share:</span><span class="sxs-lookup"><span data-stu-id="2917c-181">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="2917c-182">Microsoft-ASR\_UA\_*version*\_OEL-64\_GA\_*date*\_Release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2917c-182">Microsoft-ASR\_UA\_*version*\_OEL-64\_GA\_*date*\_Release.tar.gz</span></span>
   * <span data-ttu-id="2917c-183">Microsoft-ASR\_UA\_*version*\_RHEL6-64\_GA\_*date*\_Release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2917c-183">Microsoft-ASR\_UA\_*version*\_RHEL6-64\_GA\_*date*\_Release.tar.gz</span></span>
   * <span data-ttu-id="2917c-184">Microsoft-ASR\_UA\_*version*\_RHEL7-64\_GA\_*date*\_Release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2917c-184">Microsoft-ASR\_UA\_*version*\_RHEL7-64\_GA\_*date*\_Release.tar.gz</span></span>
   * <span data-ttu-id="2917c-185">Microsoft-ASR\_UA\_*version*\_SLES11-SP3-64\_GA\_*date*\_Release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2917c-185">Microsoft-ASR\_UA\_*version*\_SLES11-SP3-64\_GA\_*date*\_Release.tar.gz</span></span>

7. <span data-ttu-id="2917c-186">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span><span class="sxs-lookup"><span data-stu-id="2917c-186">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="2917c-187">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span><span class="sxs-lookup"><span data-stu-id="2917c-187">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```
#!/bin/sh

rm -rf /tmp/MobSvc

mkdir -p /tmp/MobSvc

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
        cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            cp *RHEL7*.tar.gz /tmp/MobSvc
    fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
        echo $OS >> /tmp/MobSvc/sccm.log
        cp *SLES11*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
       cp *UBUNTU*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi
if [ "${OS}" ==  "" ]; then
    exit 1
fi
cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz


if [ -e /usr/local/.vx_version ];
then
    ./install -A u
    echo "Errorcode:$?"
    Error=$?

else
    ./install -t both -a host -R Agent -d /usr/local/ASR -i [CS IP] -p 443 -s y -c https -P MobSvc.passphrase >> /tmp/MobSvc/sccm.log 2>&1 && echo "Install Progress"
    Error=$?
fi
cd /tmp
rm -rf /tm/MobSvc
exit ${Error}
```

### <a name="step-2-create-a-package"></a><span data-ttu-id="2917c-188">Step 2: Create a package</span><span class="sxs-lookup"><span data-stu-id="2917c-188">Step 2: Create a package</span></span>

1. <span data-ttu-id="2917c-189">Sign in  to your Configuration Manager console.</span><span class="sxs-lookup"><span data-stu-id="2917c-189">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="2917c-190">Browse to **Software Library** > **Application Management** > **Packages**.</span><span class="sxs-lookup"><span data-stu-id="2917c-190">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="2917c-191">Right-click **Packages**, and select **Create Package**.</span><span class="sxs-lookup"><span data-stu-id="2917c-191">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="2917c-192">Provide values for the name, description, manufacturer, language, and version.</span><span class="sxs-lookup"><span data-stu-id="2917c-192">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="2917c-193">Select the **This package contains source files** check box.</span><span class="sxs-lookup"><span data-stu-id="2917c-193">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="2917c-194">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="2917c-194">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="2917c-196">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2917c-196">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="2917c-198">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2917c-198">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="2917c-199">(The other inputs can use their default values.)</span><span class="sxs-lookup"><span data-stu-id="2917c-199">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="2917c-200">**Parameter name**</span><span class="sxs-lookup"><span data-stu-id="2917c-200">**Parameter name**</span></span> | <span data-ttu-id="2917c-201">**Value**</span><span class="sxs-lookup"><span data-stu-id="2917c-201">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="2917c-202">Name</span><span class="sxs-lookup"><span data-stu-id="2917c-202">Name</span></span> | <span data-ttu-id="2917c-203">Install Microsoft Azure Mobility Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="2917c-203">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="2917c-204">Command line</span><span class="sxs-lookup"><span data-stu-id="2917c-204">Command line</span></span> | <span data-ttu-id="2917c-205">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="2917c-205">./install_linux.sh</span></span> |
  | <span data-ttu-id="2917c-206">Program can run</span><span class="sxs-lookup"><span data-stu-id="2917c-206">Program can run</span></span> | <span data-ttu-id="2917c-207">Whether or not a user is logged on</span><span class="sxs-lookup"><span data-stu-id="2917c-207">Whether or not a user is logged on</span></span> |

  ![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="2917c-209">On the next page, select **This program can run on any platform**.</span><span class="sxs-lookup"><span data-stu-id="2917c-209">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="2917c-210">![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="2917c-210">![Screenshot of Create Package and Program wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="2917c-211">To complete the wizard, click **Next** twice.</span><span class="sxs-lookup"><span data-stu-id="2917c-211">To complete the wizard, click **Next** twice.</span></span> 
 
> [!NOTE]
> <span data-ttu-id="2917c-212">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span><span class="sxs-lookup"><span data-stu-id="2917c-212">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="2917c-213">Step 3: Deploy the package</span><span class="sxs-lookup"><span data-stu-id="2917c-213">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="2917c-214">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span><span class="sxs-lookup"><span data-stu-id="2917c-214">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="2917c-215">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="2917c-215">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="2917c-216">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span><span class="sxs-lookup"><span data-stu-id="2917c-216">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="2917c-217">Complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="2917c-217">Complete the wizard.</span></span> <span data-ttu-id="2917c-218">The package then starts replicating to the specified distribution points.</span><span class="sxs-lookup"><span data-stu-id="2917c-218">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="2917c-219">After the package distribution is done, right-click the package, and select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="2917c-219">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="2917c-220">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="2917c-220">![Screenshot of Configuration Manager console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="2917c-221">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span><span class="sxs-lookup"><span data-stu-id="2917c-221">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Screenshot of Deploy Software wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="2917c-223">On the **Specify the content destination** page, select your **Distribution Points**.</span><span class="sxs-lookup"><span data-stu-id="2917c-223">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="2917c-224">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span><span class="sxs-lookup"><span data-stu-id="2917c-224">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Screenshot of Deploy Software wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="2917c-226">On the **Specify the schedule for this deployment** page, specify a schedule.</span><span class="sxs-lookup"><span data-stu-id="2917c-226">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="2917c-227">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="2917c-227">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="2917c-228">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span><span class="sxs-lookup"><span data-stu-id="2917c-228">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="2917c-229">Then complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="2917c-229">Then complete the wizard.</span></span>

<span data-ttu-id="2917c-230">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span><span class="sxs-lookup"><span data-stu-id="2917c-230">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="2917c-231">Other methods to install Mobility Service</span><span class="sxs-lookup"><span data-stu-id="2917c-231">Other methods to install Mobility Service</span></span>
<span data-ttu-id="2917c-232">Here are some other options for installing Mobility Service:</span><span class="sxs-lookup"><span data-stu-id="2917c-232">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="2917c-233">Manual Installation using GUI</span><span class="sxs-lookup"><span data-stu-id="2917c-233">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="2917c-234">Manual Installation using command-line</span><span class="sxs-lookup"><span data-stu-id="2917c-234">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="2917c-235">Push Installation using configuration server </span><span class="sxs-lookup"><span data-stu-id="2917c-235">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="2917c-236">Automated Installation using Azure Automation & Desired State Configuration </span><span class="sxs-lookup"><span data-stu-id="2917c-236">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="2917c-237">Uninstall Mobility Service</span><span class="sxs-lookup"><span data-stu-id="2917c-237">Uninstall Mobility Service</span></span>
<span data-ttu-id="2917c-238">You can create Configuration Manager packages to uninstall Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="2917c-238">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="2917c-239">Use the following script to do so:</span><span class="sxs-lookup"><span data-stu-id="2917c-239">Use the following script to do so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="2917c-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="2917c-240">Next steps</span></span>
<span data-ttu-id="2917c-241">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2917c-241">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>

















