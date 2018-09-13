---
title: Maintaining the SQL resource provider on Azure Stack | Microsoft Docs
description: Learn how you can maintain the SQL resource provider service on Azure Stack.
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 5c065fa73317d819e5ca3dadef59be1bc65c71b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869893"
---
# <a name="sql-resource-provider-maintenance-operations"></a><span data-ttu-id="eb4d1-103">SQL resource provider maintenance operations</span><span class="sxs-lookup"><span data-stu-id="eb4d1-103">SQL resource provider maintenance operations</span></span>

<span data-ttu-id="eb4d1-104">The SQL resource provider runs on a locked down virtual machine.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-104">The SQL resource provider runs on a locked down virtual machine.</span></span> <span data-ttu-id="eb4d1-105">To enable maintenance operations, you need to update the virtual machine's security.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-105">To enable maintenance operations, you need to update the virtual machine's security.</span></span> <span data-ttu-id="eb4d1-106">To do this using the principle of Least Privilege, you can use [PowerShell Just Enough Administration (JEA)](https://docs.microsoft.com/powershell/jea/overview) endpoint *DBAdapterMaintenance*.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-106">To do this using the principle of Least Privilege, you can use [PowerShell Just Enough Administration (JEA)](https://docs.microsoft.com/powershell/jea/overview) endpoint *DBAdapterMaintenance*.</span></span> <span data-ttu-id="eb4d1-107">The resource provider installation package includes a script for this operation.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-107">The resource provider installation package includes a script for this operation.</span></span>

## <a name="patching-and-updating"></a><span data-ttu-id="eb4d1-108">Patching and updating</span><span class="sxs-lookup"><span data-stu-id="eb4d1-108">Patching and updating</span></span>

<span data-ttu-id="eb4d1-109">The SQL resource provider isn't serviced as part of Azure Stack because it's an add-on component.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-109">The SQL resource provider isn't serviced as part of Azure Stack because it's an add-on component.</span></span> <span data-ttu-id="eb4d1-110">Microsoft provides updates to the SQL resource provider as necessary.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-110">Microsoft provides updates to the SQL resource provider as necessary.</span></span> <span data-ttu-id="eb4d1-111">When an updated SQL adapter is released, a script is provided to apply the update.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-111">When an updated SQL adapter is released, a script is provided to apply the update.</span></span> <span data-ttu-id="eb4d1-112">This script creates a new resource provider VM, migrating the state of the old provider VM to the new VM.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-112">This script creates a new resource provider VM, migrating the state of the old provider VM to the new VM.</span></span> <span data-ttu-id="eb4d1-113">For more information, see [Update the SQL resource provider](azure-stack-sql-resource-provider-update.md).</span><span class="sxs-lookup"><span data-stu-id="eb4d1-113">For more information, see [Update the SQL resource provider](azure-stack-sql-resource-provider-update.md).</span></span>

### <a name="provider-virtual-machine"></a><span data-ttu-id="eb4d1-114">Provider virtual machine</span><span class="sxs-lookup"><span data-stu-id="eb4d1-114">Provider virtual machine</span></span>

<span data-ttu-id="eb4d1-115">Because the resource provider runs on a *user* virtual machine, you need to apply the required patches and updates when they're released.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-115">Because the resource provider runs on a *user* virtual machine, you need to apply the required patches and updates when they're released.</span></span> <span data-ttu-id="eb4d1-116">You can use the Windows update packages that are provided as part of the patch-and-update cycle to apply updates to the VM.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-116">You can use the Windows update packages that are provided as part of the patch-and-update cycle to apply updates to the VM.</span></span>

## <a name="backuprestoredisaster-recovery"></a><span data-ttu-id="eb4d1-117">Backup/Restore/Disaster Recovery</span><span class="sxs-lookup"><span data-stu-id="eb4d1-117">Backup/Restore/Disaster Recovery</span></span>

 <span data-ttu-id="eb4d1-118">Because it's an add-on component, the SQL resource provider isn't backed up as part of an Azure Stack Business Continuity Disaster Recovery (BCDR) process.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-118">Because it's an add-on component, the SQL resource provider isn't backed up as part of an Azure Stack Business Continuity Disaster Recovery (BCDR) process.</span></span> <span data-ttu-id="eb4d1-119">Scripts will be provided for the following operations:</span><span class="sxs-lookup"><span data-stu-id="eb4d1-119">Scripts will be provided for the following operations:</span></span>

- <span data-ttu-id="eb4d1-120">Backing up state information (stored in an Azure Stack storage account.)</span><span class="sxs-lookup"><span data-stu-id="eb4d1-120">Backing up state information (stored in an Azure Stack storage account.)</span></span>
- <span data-ttu-id="eb4d1-121">Restoring the resource provider if a full stack recovery is required.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-121">Restoring the resource provider if a full stack recovery is required.</span></span>

>[!NOTE]
><span data-ttu-id="eb4d1-122">If you have to do a recovery, database servers must be recovered before the resource provider is restored.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-122">If you have to do a recovery, database servers must be recovered before the resource provider is restored.</span></span>

## <a name="updating-sql-credentials"></a><span data-ttu-id="eb4d1-123">Updating SQL credentials</span><span class="sxs-lookup"><span data-stu-id="eb4d1-123">Updating SQL credentials</span></span>

<span data-ttu-id="eb4d1-124">You're responsible for creating and maintaining sysadmin accounts on your SQL servers.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-124">You're responsible for creating and maintaining sysadmin accounts on your SQL servers.</span></span> <span data-ttu-id="eb4d1-125">The resource provider needs an account with these privileges to manage databases for users, but it doesn't need access to the users' data.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-125">The resource provider needs an account with these privileges to manage databases for users, but it doesn't need access to the users' data.</span></span> <span data-ttu-id="eb4d1-126">If you need to update the sysadmin passwords on your SQL servers, you can use the resource provider's administrator interface to change a stored password.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-126">If you need to update the sysadmin passwords on your SQL servers, you can use the resource provider's administrator interface to change a stored password.</span></span> <span data-ttu-id="eb4d1-127">These passwords are stored in a Key Vault on your Azure Stack instance.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-127">These passwords are stored in a Key Vault on your Azure Stack instance.</span></span>

<span data-ttu-id="eb4d1-128">To modify the settings, select **Browse** &gt; **ADMINISTRATIVE RESOURCES** &gt; **SQL Hosting Servers** &gt; **SQL Logins** and select a user name.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-128">To modify the settings, select **Browse** &gt; **ADMINISTRATIVE RESOURCES** &gt; **SQL Hosting Servers** &gt; **SQL Logins** and select a user name.</span></span> <span data-ttu-id="eb4d1-129">The change must be made on the SQL instance first (and any replicas, if necessary.) Under **Settings**, select **Password**.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-129">The change must be made on the SQL instance first (and any replicas, if necessary.) Under **Settings**, select **Password**.</span></span>

![Update the admin password](./media/azure-stack-sql-rp-deploy/sqlrp-update-password.PNG)

## <a name="secrets-rotation"></a><span data-ttu-id="eb4d1-131">Secrets rotation</span><span class="sxs-lookup"><span data-stu-id="eb4d1-131">Secrets rotation</span></span>

<span data-ttu-id="eb4d1-132">*These instructions only apply to Azure Stack Integrated Systems Version 1804 and Later. Don't try to rotate secrets on pre-1804 Azure Stack Versions.*</span><span class="sxs-lookup"><span data-stu-id="eb4d1-132">*These instructions only apply to Azure Stack Integrated Systems Version 1804 and Later. Don't try to rotate secrets on pre-1804 Azure Stack Versions.*</span></span>

<span data-ttu-id="eb4d1-133">When using the SQL and MySQL resource providers with Azure Stack integrated systems, you can rotate the following infrastructure (deployment) secrets:</span><span class="sxs-lookup"><span data-stu-id="eb4d1-133">When using the SQL and MySQL resource providers with Azure Stack integrated systems, you can rotate the following infrastructure (deployment) secrets:</span></span>

- <span data-ttu-id="eb4d1-134">External SSL Certificate [provided during deployment](azure-stack-pki-certs.md).</span><span class="sxs-lookup"><span data-stu-id="eb4d1-134">External SSL Certificate [provided during deployment](azure-stack-pki-certs.md).</span></span>
- <span data-ttu-id="eb4d1-135">The resource provider VM local administrator account password provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-135">The resource provider VM local administrator account password provided during deployment.</span></span>
- <span data-ttu-id="eb4d1-136">Resource provider diagnostic user (dbadapterdiag) password.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-136">Resource provider diagnostic user (dbadapterdiag) password.</span></span>

### <a name="powershell-examples-for-rotating-secrets"></a><span data-ttu-id="eb4d1-137">PowerShell examples for rotating secrets</span><span class="sxs-lookup"><span data-stu-id="eb4d1-137">PowerShell examples for rotating secrets</span></span>

<span data-ttu-id="eb4d1-138">**Change all the secrets at the same time.**</span><span class="sxs-lookup"><span data-stu-id="eb4d1-138">**Change all the secrets at the same time.**</span></span>

```powershell
.\SecretRotationSQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    –DiagnosticsUserPassword $passwd `
    -DependencyFilesLocalPath $certPath `
    -DefaultSSLCertificatePassword $certPasswd  `
    -VMLocalCredential $localCreds
```

<span data-ttu-id="eb4d1-139">**Change the diagnostic user password.**</span><span class="sxs-lookup"><span data-stu-id="eb4d1-139">**Change the diagnostic user password.**</span></span>

```powershell
.\SecretRotationSQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    –DiagnosticsUserPassword  $passwd
```

<span data-ttu-id="eb4d1-140">**Change the VM local administrator account password.**</span><span class="sxs-lookup"><span data-stu-id="eb4d1-140">**Change the VM local administrator account password.**</span></span>

```powershell
.\SecretRotationSQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    -VMLocalCredential $localCreds
```

<span data-ttu-id="eb4d1-141">**Change the SSL certificate password.**</span><span class="sxs-lookup"><span data-stu-id="eb4d1-141">**Change the SSL certificate password.**</span></span>

```powershell
.\SecretRotationSQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    -DependencyFilesLocalPath $certPath `
    -DefaultSSLCertificatePassword $certPasswd
```

### <a name="secretrotationsqlproviderps1-parameters"></a><span data-ttu-id="eb4d1-142">SecretRotationSQLProvider.ps1 parameters</span><span class="sxs-lookup"><span data-stu-id="eb4d1-142">SecretRotationSQLProvider.ps1 parameters</span></span>

|<span data-ttu-id="eb4d1-143">Parameter</span><span class="sxs-lookup"><span data-stu-id="eb4d1-143">Parameter</span></span>|<span data-ttu-id="eb4d1-144">Description</span><span class="sxs-lookup"><span data-stu-id="eb4d1-144">Description</span></span>|
|-----|-----|
|<span data-ttu-id="eb4d1-145">AzCredential</span><span class="sxs-lookup"><span data-stu-id="eb4d1-145">AzCredential</span></span>|<span data-ttu-id="eb4d1-146">Azure Stack Service Admin account credential.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-146">Azure Stack Service Admin account credential.</span></span>|
|<span data-ttu-id="eb4d1-147">CloudAdminCredential</span><span class="sxs-lookup"><span data-stu-id="eb4d1-147">CloudAdminCredential</span></span>|<span data-ttu-id="eb4d1-148">Azure Stack cloud admin domain account credential.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-148">Azure Stack cloud admin domain account credential.</span></span>|
|<span data-ttu-id="eb4d1-149">PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="eb4d1-149">PrivilegedEndpoint</span></span>|<span data-ttu-id="eb4d1-150">Privileged Endpoint to access Get-AzureStackStampInformation.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-150">Privileged Endpoint to access Get-AzureStackStampInformation.</span></span>|
|<span data-ttu-id="eb4d1-151">DiagnosticsUserPassword</span><span class="sxs-lookup"><span data-stu-id="eb4d1-151">DiagnosticsUserPassword</span></span>|<span data-ttu-id="eb4d1-152">Diagnostics user account password.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-152">Diagnostics user account password.</span></span>|
|<span data-ttu-id="eb4d1-153">VMLocalCredential</span><span class="sxs-lookup"><span data-stu-id="eb4d1-153">VMLocalCredential</span></span>|<span data-ttu-id="eb4d1-154">Local administrator account on the MySQLAdapter VM.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-154">Local administrator account on the MySQLAdapter VM.</span></span>|
|<span data-ttu-id="eb4d1-155">DefaultSSLCertificatePassword</span><span class="sxs-lookup"><span data-stu-id="eb4d1-155">DefaultSSLCertificatePassword</span></span>|<span data-ttu-id="eb4d1-156">Default SSL Certificate (\*pfx) password.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-156">Default SSL Certificate (\*pfx) password.</span></span>|
|<span data-ttu-id="eb4d1-157">DependencyFilesLocalPath</span><span class="sxs-lookup"><span data-stu-id="eb4d1-157">DependencyFilesLocalPath</span></span>|<span data-ttu-id="eb4d1-158">Dependency files local path.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-158">Dependency files local path.</span></span>|
|     |     |

### <a name="known-issues"></a><span data-ttu-id="eb4d1-159">Known issues</span><span class="sxs-lookup"><span data-stu-id="eb4d1-159">Known issues</span></span>

<span data-ttu-id="eb4d1-160">**Issue**: Secrets rotation logs.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-160">**Issue**: Secrets rotation logs.</span></span><br>
<span data-ttu-id="eb4d1-161">The logs for secrets rotation aren't automatically collected if the secret rotation custom script fails when it is run.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-161">The logs for secrets rotation aren't automatically collected if the secret rotation custom script fails when it is run.</span></span>

<span data-ttu-id="eb4d1-162">**Workaround**:</span><span class="sxs-lookup"><span data-stu-id="eb4d1-162">**Workaround**:</span></span><br>
<span data-ttu-id="eb4d1-163">Use the Get-AzsDBAdapterLogs cmdlet to collect all resource provider logs, including AzureStack.DatabaseAdapter.SecretRotation.ps1_\*.log, saved in C:\Logs.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-163">Use the Get-AzsDBAdapterLogs cmdlet to collect all resource provider logs, including AzureStack.DatabaseAdapter.SecretRotation.ps1_\*.log, saved in C:\Logs.</span></span>

## <a name="update-the-virtual-machine-operating-system"></a><span data-ttu-id="eb4d1-164">Update the virtual machine operating system</span><span class="sxs-lookup"><span data-stu-id="eb4d1-164">Update the virtual machine operating system</span></span>

<span data-ttu-id="eb4d1-165">Use one of the following methods to update the virtual machine operating system.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-165">Use one of the following methods to update the virtual machine operating system.</span></span>

- <span data-ttu-id="eb4d1-166">Install the latest resource provider package using a currently patched Windows Server 2016 Core image.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-166">Install the latest resource provider package using a currently patched Windows Server 2016 Core image.</span></span>
- <span data-ttu-id="eb4d1-167">Install a Windows Update package during the installation of, or update to, the resource provider.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-167">Install a Windows Update package during the installation of, or update to, the resource provider.</span></span>

## <a name="update-the-virtual-machine-windows-defender-definitions"></a><span data-ttu-id="eb4d1-168">Update the virtual machine Windows Defender definitions</span><span class="sxs-lookup"><span data-stu-id="eb4d1-168">Update the virtual machine Windows Defender definitions</span></span>

<span data-ttu-id="eb4d1-169">To update the Windows Defender definitions:</span><span class="sxs-lookup"><span data-stu-id="eb4d1-169">To update the Windows Defender definitions:</span></span>

1. <span data-ttu-id="eb4d1-170">Download the Windows Defender definitions update from [Windows Defender Definition](https://www.microsoft.com/en-us/wdsi/definitions).</span><span class="sxs-lookup"><span data-stu-id="eb4d1-170">Download the Windows Defender definitions update from [Windows Defender Definition](https://www.microsoft.com/en-us/wdsi/definitions).</span></span>

   <span data-ttu-id="eb4d1-171">On the definitions update page, scroll down to "Manually download and install the definitions".</span><span class="sxs-lookup"><span data-stu-id="eb4d1-171">On the definitions update page, scroll down to "Manually download and install the definitions".</span></span> <span data-ttu-id="eb4d1-172">Download the "Windows Defender Antivirus for Windows 10 and Windows 8.1" 64-bit file.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-172">Download the "Windows Defender Antivirus for Windows 10 and Windows 8.1" 64-bit file.</span></span>

   <span data-ttu-id="eb4d1-173">Alternatively, use [this direct link](https://go.microsoft.com/fwlink/?LinkID=121721&arch=x64) to download/run the fpam-fe.exe file.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-173">Alternatively, use [this direct link](https://go.microsoft.com/fwlink/?LinkID=121721&arch=x64) to download/run the fpam-fe.exe file.</span></span>

2. <span data-ttu-id="eb4d1-174">Create a PowerShell session to the SQL resource provider  adapter virtual machine’s maintenance endpoint.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-174">Create a PowerShell session to the SQL resource provider  adapter virtual machine’s maintenance endpoint.</span></span>

3. <span data-ttu-id="eb4d1-175">Copy the definitions update file to the virtual machine using the maintenance endpoint session.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-175">Copy the definitions update file to the virtual machine using the maintenance endpoint session.</span></span>

4. <span data-ttu-id="eb4d1-176">On the maintenance PowerShell session, run the *Update-DBAdapterWindowsDefenderDefinitions* command.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-176">On the maintenance PowerShell session, run the *Update-DBAdapterWindowsDefenderDefinitions* command.</span></span>

5. <span data-ttu-id="eb4d1-177">After you install the definitions, we recommend that you delete the definitions update file by using the *Remove-ItemOnUserDrive* command.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-177">After you install the definitions, we recommend that you delete the definitions update file by using the *Remove-ItemOnUserDrive* command.</span></span>

<span data-ttu-id="eb4d1-178">**PowerShell script example for updating definitions.**</span><span class="sxs-lookup"><span data-stu-id="eb4d1-178">**PowerShell script example for updating definitions.**</span></span>

<span data-ttu-id="eb4d1-179">You can edit and run the following script to update the Defender definitions.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-179">You can edit and run the following script to update the Defender definitions.</span></span> <span data-ttu-id="eb4d1-180">Replace values in the script with values from your environment.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-180">Replace values in the script with values from your environment.</span></span>

```powershell
# Set credentials for local admin on the resource provider VM.
$vmLocalAdminPass = ConvertTo-SecureString "<local admin user password>" -AsPlainText -Force
$vmLocalAdminUser = "<local admin user name>"
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential `
    ($vmLocalAdminUser, $vmLocalAdminPass)

# Provide the public IP address for the adapter VM.
$databaseRPMachine  = "<RP VM IP address>"
$localPathToDefenderUpdate = "C:\DefenderUpdates\mpam-fe.exe"

# Download the Windows Defender update definitions file from https://www.microsoft.com/en-us/wdsi/definitions.
Invoke-WebRequest -Uri 'https://go.microsoft.com/fwlink/?LinkID=121721&arch=x64' `
    -Outfile $localPathToDefenderUpdate

# Create a session to the maintenance endpoint.
$session = New-PSSession -ComputerName $databaseRPMachine `
    -Credential $vmLocalAdminCreds -ConfigurationName DBAdapterMaintenance
# Copy the defender update file to the adapter virtual machine.
Copy-Item -ToSession $session -Path $localPathToDefenderUpdate `
     -Destination "User:\"
# Install the update definitions.
Invoke-Command -Session $session -ScriptBlock `
    {Update-AzSDBAdapterWindowsDefenderDefinition -DefinitionsUpdatePackageFile "User:\mpam-fe.exe"}
# Cleanup the definitions package file and session.
Invoke-Command -Session $session -ScriptBlock `
    {Remove-AzSItemOnUserDrive -ItemPath "User:\mpam-fe.exe"}
$session | Remove-PSSession
```

## <a name="collect-diagnostic-logs"></a><span data-ttu-id="eb4d1-181">Collect diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="eb4d1-181">Collect diagnostic logs</span></span>

<span data-ttu-id="eb4d1-182">To collect logs from the locked down virtual machine, you can use the PowerShell Just Enough Administration (JEA) endpoint *DBAdapterDiagnostics*.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-182">To collect logs from the locked down virtual machine, you can use the PowerShell Just Enough Administration (JEA) endpoint *DBAdapterDiagnostics*.</span></span> <span data-ttu-id="eb4d1-183">This endpoint provides the following commands:</span><span class="sxs-lookup"><span data-stu-id="eb4d1-183">This endpoint provides the following commands:</span></span>

- <span data-ttu-id="eb4d1-184">**Get-AzsDBAdapterLog**.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-184">**Get-AzsDBAdapterLog**.</span></span> <span data-ttu-id="eb4d1-185">This command creates a zip package of the resource provider diagnostics logs and saves the file on the session's user drive.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-185">This command creates a zip package of the resource provider diagnostics logs and saves the file on the session's user drive.</span></span> <span data-ttu-id="eb4d1-186">You can run this command without any parameters and the last four hours of logs are collected.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-186">You can run this command without any parameters and the last four hours of logs are collected.</span></span>
- <span data-ttu-id="eb4d1-187">**Remove-AzsDBAdapterLog**.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-187">**Remove-AzsDBAdapterLog**.</span></span> <span data-ttu-id="eb4d1-188">This command removes existing log packages on the resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-188">This command removes existing log packages on the resource provider VM.</span></span>

### <a name="endpoint-requirements-and-process"></a><span data-ttu-id="eb4d1-189">Endpoint requirements and process</span><span class="sxs-lookup"><span data-stu-id="eb4d1-189">Endpoint requirements and process</span></span>

<span data-ttu-id="eb4d1-190">When a resource provider is installed or updated, the **dbadapterdiag** user account is created.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-190">When a resource provider is installed or updated, the **dbadapterdiag** user account is created.</span></span> <span data-ttu-id="eb4d1-191">You'll use this account to collect diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-191">You'll use this account to collect diagnostic logs.</span></span>

>[!NOTE]
><span data-ttu-id="eb4d1-192">The dbadapterdiag account password is the same as the password used for the local administrator on the virtual machine that's created during a provider deployment or update.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-192">The dbadapterdiag account password is the same as the password used for the local administrator on the virtual machine that's created during a provider deployment or update.</span></span>

<span data-ttu-id="eb4d1-193">To use the *DBAdapterDiagnostics* commands, create a remote PowerShell session to the resource provider virtual machine and run the **Get-AzsDBAdapterLog** command.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-193">To use the *DBAdapterDiagnostics* commands, create a remote PowerShell session to the resource provider virtual machine and run the **Get-AzsDBAdapterLog** command.</span></span>

<span data-ttu-id="eb4d1-194">You set the time span for log collection by using the **FromDate** and **ToDate** parameters.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-194">You set the time span for log collection by using the **FromDate** and **ToDate** parameters.</span></span> <span data-ttu-id="eb4d1-195">If you don't specify one or both of these parameters, the following defaults are used:</span><span class="sxs-lookup"><span data-stu-id="eb4d1-195">If you don't specify one or both of these parameters, the following defaults are used:</span></span>

- <span data-ttu-id="eb4d1-196">FromDate is four hours before the current time.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-196">FromDate is four hours before the current time.</span></span>
- <span data-ttu-id="eb4d1-197">ToDate is the current time.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-197">ToDate is the current time.</span></span>

<span data-ttu-id="eb4d1-198">**PowerShell script example for collecting logs.**</span><span class="sxs-lookup"><span data-stu-id="eb4d1-198">**PowerShell script example for collecting logs.**</span></span>

<span data-ttu-id="eb4d1-199">The following script shows how to collect diagnostic logs from the resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="eb4d1-199">The following script shows how to collect diagnostic logs from the resource provider VM.</span></span>

```powershell
# Create a new diagnostics endpoint session.
$databaseRPMachineIP = '<RP VM IP address>'
$diagnosticsUserName = 'dbadapterdiag'
$diagnosticsUserPassword = '<Enter Diagnostic password>'

$diagCreds = New-Object System.Management.Automation.PSCredential `
        ($diagnosticsUserName, (ConvertTo-SecureString -String $diagnosticsUserPassword -AsPlainText -Force))
$session = New-PSSession -ComputerName $databaseRPMachineIP -Credential $diagCreds `
        -ConfigurationName DBAdapterDiagnostics

# Sample that captures logs from the previous hour.
$fromDate = (Get-Date).AddHours(-1)
$dateNow = Get-Date
$sb = {param($d1,$d2) Get-AzSDBAdapterLog -FromDate $d1 -ToDate $d2}
$logs = Invoke-Command -Session $session -ScriptBlock $sb -ArgumentList $fromDate,$dateNow

# Copy the logs to the user drive.
$sourcePath = "User:\{0}" -f $logs
$destinationPackage = Join-Path -Path (Convert-Path '.') -ChildPath $logs
Copy-Item -FromSession $session -Path $sourcePath -Destination $destinationPackage

# Cleanup the logs.
$cleanup = Invoke-Command -Session $session -ScriptBlock {Remove- AzsDBAdapterLog }
# Close the session.
$session | Remove-PSSession
```

## <a name="next-steps"></a><span data-ttu-id="eb4d1-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb4d1-200">Next steps</span></span>

[<span data-ttu-id="eb4d1-201">Add SQL Server hosting servers</span><span class="sxs-lookup"><span data-stu-id="eb4d1-201">Add SQL Server hosting servers</span></span>](azure-stack-sql-resource-provider-hosting-servers.md)
