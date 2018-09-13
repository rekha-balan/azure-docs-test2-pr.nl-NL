---
title: Maintaining the MySQL resource provider on Azure Stack | Microsoft Docs
description: Learn how you can maintain the MySQL resource provider service on Azure Stack.
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
ms.date: 06/29/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: bc1c96d2f027d459ca20fccb70cd94ac9e5cae94
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867880"
---
# <a name="mysql-resource-provider-maintenance-operations"></a><span data-ttu-id="72691-103">MySQL resource provider maintenance operations</span><span class="sxs-lookup"><span data-stu-id="72691-103">MySQL resource provider maintenance operations</span></span>

<span data-ttu-id="72691-104">The MySQL resource provider runs on a locked down virtual machine.</span><span class="sxs-lookup"><span data-stu-id="72691-104">The MySQL resource provider runs on a locked down virtual machine.</span></span> <span data-ttu-id="72691-105">To enable maintenance operations, you need to update the virtual machine's security.</span><span class="sxs-lookup"><span data-stu-id="72691-105">To enable maintenance operations, you need to update the virtual machine's security.</span></span> <span data-ttu-id="72691-106">To do this using the principle of Least Privilege, you can use PowerShell Just Enough Administration (JEA) endpoint DBAdapterMaintenance.</span><span class="sxs-lookup"><span data-stu-id="72691-106">To do this using the principle of Least Privilege, you can use PowerShell Just Enough Administration (JEA) endpoint DBAdapterMaintenance.</span></span> <span data-ttu-id="72691-107">The resource provider installation package includes a script for this operation.</span><span class="sxs-lookup"><span data-stu-id="72691-107">The resource provider installation package includes a script for this operation.</span></span>

## <a name="update-the-virtual-machine-operating-system"></a><span data-ttu-id="72691-108">Update the virtual machine operating system</span><span class="sxs-lookup"><span data-stu-id="72691-108">Update the virtual machine operating system</span></span>

<span data-ttu-id="72691-109">Because the resource provider runs on a *user* virtual machine, you need to apply the required patches and updates when they're released.</span><span class="sxs-lookup"><span data-stu-id="72691-109">Because the resource provider runs on a *user* virtual machine, you need to apply the required patches and updates when they're released.</span></span> <span data-ttu-id="72691-110">You can use the Windows update packages that are provided as part of the patch-and-update cycle to apply updates to the VM.</span><span class="sxs-lookup"><span data-stu-id="72691-110">You can use the Windows update packages that are provided as part of the patch-and-update cycle to apply updates to the VM.</span></span>

<span data-ttu-id="72691-111">Update the provider virtual machine using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="72691-111">Update the provider virtual machine using one of the following methods:</span></span>

- <span data-ttu-id="72691-112">Install the latest resource provider package using a currently patched Windows Server 2016 Core image.</span><span class="sxs-lookup"><span data-stu-id="72691-112">Install the latest resource provider package using a currently patched Windows Server 2016 Core image.</span></span>
- <span data-ttu-id="72691-113">Install a Windows Update package during the installation of, or update to the resource provider.</span><span class="sxs-lookup"><span data-stu-id="72691-113">Install a Windows Update package during the installation of, or update to the resource provider.</span></span>

## <a name="update-the-virtual-machine-windows-defender-definitions"></a><span data-ttu-id="72691-114">Update the virtual machine Windows Defender definitions</span><span class="sxs-lookup"><span data-stu-id="72691-114">Update the virtual machine Windows Defender definitions</span></span>

<span data-ttu-id="72691-115">To update the Defender definitions, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="72691-115">To update the Defender definitions, follow these steps:</span></span>

1. <span data-ttu-id="72691-116">Download the Windows Defender definitions update from [Windows Defender Definition](https://www.microsoft.com/en-us/wdsi/definitions).</span><span class="sxs-lookup"><span data-stu-id="72691-116">Download the Windows Defender definitions update from [Windows Defender Definition](https://www.microsoft.com/en-us/wdsi/definitions).</span></span>

    <span data-ttu-id="72691-117">On the definitions page, scroll down to "Manually download and install the definitions".</span><span class="sxs-lookup"><span data-stu-id="72691-117">On the definitions page, scroll down to "Manually download and install the definitions".</span></span> <span data-ttu-id="72691-118">Download the "Windows Defender Antivirus for Windows 10 and Windows 8.1" 64-bit file.</span><span class="sxs-lookup"><span data-stu-id="72691-118">Download the "Windows Defender Antivirus for Windows 10 and Windows 8.1" 64-bit file.</span></span>

    <span data-ttu-id="72691-119">Alternatively, use [this direct link](https://go.microsoft.com/fwlink/?LinkID=121721&arch=x64) to download/run the fpam-fe.exe file.</span><span class="sxs-lookup"><span data-stu-id="72691-119">Alternatively, use [this direct link](https://go.microsoft.com/fwlink/?LinkID=121721&arch=x64) to download/run the fpam-fe.exe file.</span></span>

2. <span data-ttu-id="72691-120">Open a PowerShell session to the MySQL resource provider adapter virtual machine’s maintenance endpoint.</span><span class="sxs-lookup"><span data-stu-id="72691-120">Open a PowerShell session to the MySQL resource provider adapter virtual machine’s maintenance endpoint.</span></span>

3. <span data-ttu-id="72691-121">Copy the definitions update file to the resource provider adapter VM using the maintenance endpoint session.</span><span class="sxs-lookup"><span data-stu-id="72691-121">Copy the definitions update file to the resource provider adapter VM using the maintenance endpoint session.</span></span>

4. <span data-ttu-id="72691-122">On the maintenance PowerShell session, run the _Update-DBAdapterWindowsDefenderDefinitions_ command.</span><span class="sxs-lookup"><span data-stu-id="72691-122">On the maintenance PowerShell session, run the _Update-DBAdapterWindowsDefenderDefinitions_ command.</span></span>

5. <span data-ttu-id="72691-123">After you install the definitions, we recommend that you delete the definitions update file by using the _Remove-ItemOnUserDrive)_ command.</span><span class="sxs-lookup"><span data-stu-id="72691-123">After you install the definitions, we recommend that you delete the definitions update file by using the _Remove-ItemOnUserDrive)_ command.</span></span>

<span data-ttu-id="72691-124">**PowerShell script example for updating definitions.**</span><span class="sxs-lookup"><span data-stu-id="72691-124">**PowerShell script example for updating definitions.**</span></span>

<span data-ttu-id="72691-125">You can edit and run the following script to update the Defender definitions.</span><span class="sxs-lookup"><span data-stu-id="72691-125">You can edit and run the following script to update the Defender definitions.</span></span> <span data-ttu-id="72691-126">Replace values in the script with values from your environment.</span><span class="sxs-lookup"><span data-stu-id="72691-126">Replace values in the script with values from your environment.</span></span>

```powershell
# Set credentials for the local admin on the resource provider VM.
$vmLocalAdminPass = ConvertTo-SecureString "<local admin user password>" -AsPlainText -Force
$vmLocalAdminUser = "<local admin user name>"
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential `
    ($vmLocalAdminUser, $vmLocalAdminPass)

# Provide the public IP address for the adapter VM.
$databaseRPMachine  = "<RP VM IP address>"
$localPathToDefenderUpdate = "C:\DefenderUpdates\mpam-fe.exe"

# Download Windows Defender update definitions file from https://www.microsoft.com/en-us/wdsi/definitions.  
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

## <a name="secrets-rotation"></a><span data-ttu-id="72691-127">Secrets rotation</span><span class="sxs-lookup"><span data-stu-id="72691-127">Secrets rotation</span></span>

<span data-ttu-id="72691-128">*These instructions only apply to Azure Stack Integrated Systems Version 1804 and Later. Don't try to rotate secrets  on pre-1804 versions of Azure Stack.*</span><span class="sxs-lookup"><span data-stu-id="72691-128">*These instructions only apply to Azure Stack Integrated Systems Version 1804 and Later. Don't try to rotate secrets  on pre-1804 versions of Azure Stack.*</span></span>

<span data-ttu-id="72691-129">When using the SQL and MySQL resource providers with Azure Stack integrated systems, you can rotate the following infrastructure (deployment) secrets:</span><span class="sxs-lookup"><span data-stu-id="72691-129">When using the SQL and MySQL resource providers with Azure Stack integrated systems, you can rotate the following infrastructure (deployment) secrets:</span></span>

- <span data-ttu-id="72691-130">External SSL Certificate [provided during deployment](azure-stack-pki-certs.md).</span><span class="sxs-lookup"><span data-stu-id="72691-130">External SSL Certificate [provided during deployment](azure-stack-pki-certs.md).</span></span>
- <span data-ttu-id="72691-131">The resource provider VM local administrator account password provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="72691-131">The resource provider VM local administrator account password provided during deployment.</span></span>
- <span data-ttu-id="72691-132">Resource provider diagnostic user (dbadapterdiag) password.</span><span class="sxs-lookup"><span data-stu-id="72691-132">Resource provider diagnostic user (dbadapterdiag) password.</span></span>

### <a name="powershell-examples-for-rotating-secrets"></a><span data-ttu-id="72691-133">PowerShell examples for rotating secrets</span><span class="sxs-lookup"><span data-stu-id="72691-133">PowerShell examples for rotating secrets</span></span>

<span data-ttu-id="72691-134">**Change all the secrets at the same time.**</span><span class="sxs-lookup"><span data-stu-id="72691-134">**Change all the secrets at the same time.**</span></span>

```powershell
.\SecretRotationMySQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    –DiagnosticsUserPassword $passwd `
    -DependencyFilesLocalPath $certPath `
    -DefaultSSLCertificatePassword $certPasswd `  
    -VMLocalCredential $localCreds

```

<span data-ttu-id="72691-135">**Change the diagnostic user password.**</span><span class="sxs-lookup"><span data-stu-id="72691-135">**Change the diagnostic user password.**</span></span>

```powershell
.\SecretRotationMySQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    –DiagnosticsUserPassword  $passwd

```

<span data-ttu-id="72691-136">**Change the VM local administrator account password.**</span><span class="sxs-lookup"><span data-stu-id="72691-136">**Change the VM local administrator account password.**</span></span>

```powershell
.\SecretRotationMySQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    -VMLocalCredential $localCreds

```

<span data-ttu-id="72691-137">**Change the SSL certificate password.**</span><span class="sxs-lookup"><span data-stu-id="72691-137">**Change the SSL certificate password.**</span></span>

```powershell
.\SecretRotationMySQLProvider.ps1 `
    -Privilegedendpoint $Privilegedendpoint `
    -CloudAdminCredential $cloudCreds `
    -AzCredential $adminCreds `
    -DependencyFilesLocalPath $certPath `
    -DefaultSSLCertificatePassword $certPasswd

```

### <a name="secretrotationmysqlproviderps1-parameters"></a><span data-ttu-id="72691-138">SecretRotationMySQLProvider.ps1 parameters</span><span class="sxs-lookup"><span data-stu-id="72691-138">SecretRotationMySQLProvider.ps1 parameters</span></span>

|<span data-ttu-id="72691-139">Parameter</span><span class="sxs-lookup"><span data-stu-id="72691-139">Parameter</span></span>|<span data-ttu-id="72691-140">Description</span><span class="sxs-lookup"><span data-stu-id="72691-140">Description</span></span>|
|-----|-----|
|<span data-ttu-id="72691-141">AzCredential</span><span class="sxs-lookup"><span data-stu-id="72691-141">AzCredential</span></span>|<span data-ttu-id="72691-142">Azure Stack Service Admin account credential.</span><span class="sxs-lookup"><span data-stu-id="72691-142">Azure Stack Service Admin account credential.</span></span>|
|<span data-ttu-id="72691-143">CloudAdminCredential</span><span class="sxs-lookup"><span data-stu-id="72691-143">CloudAdminCredential</span></span>|<span data-ttu-id="72691-144">Azure Stack cloud admin domain account credential.</span><span class="sxs-lookup"><span data-stu-id="72691-144">Azure Stack cloud admin domain account credential.</span></span>|
|<span data-ttu-id="72691-145">PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="72691-145">PrivilegedEndpoint</span></span>|<span data-ttu-id="72691-146">Privileged Endpoint to access Get-AzureStackStampInformation.</span><span class="sxs-lookup"><span data-stu-id="72691-146">Privileged Endpoint to access Get-AzureStackStampInformation.</span></span>|
|<span data-ttu-id="72691-147">DiagnosticsUserPassword</span><span class="sxs-lookup"><span data-stu-id="72691-147">DiagnosticsUserPassword</span></span>|<span data-ttu-id="72691-148">Diagnostics user account password.</span><span class="sxs-lookup"><span data-stu-id="72691-148">Diagnostics user account password.</span></span>|
|<span data-ttu-id="72691-149">VMLocalCredential</span><span class="sxs-lookup"><span data-stu-id="72691-149">VMLocalCredential</span></span>|<span data-ttu-id="72691-150">The local administrator account on the MySQLAdapter VM.</span><span class="sxs-lookup"><span data-stu-id="72691-150">The local administrator account on the MySQLAdapter VM.</span></span>|
|<span data-ttu-id="72691-151">DefaultSSLCertificatePassword</span><span class="sxs-lookup"><span data-stu-id="72691-151">DefaultSSLCertificatePassword</span></span>|<span data-ttu-id="72691-152">Default SSL Certificate (\*pfx) Password.</span><span class="sxs-lookup"><span data-stu-id="72691-152">Default SSL Certificate (\*pfx) Password.</span></span>|
|<span data-ttu-id="72691-153">DependencyFilesLocalPath</span><span class="sxs-lookup"><span data-stu-id="72691-153">DependencyFilesLocalPath</span></span>|<span data-ttu-id="72691-154">Dependency files local path.</span><span class="sxs-lookup"><span data-stu-id="72691-154">Dependency files local path.</span></span>|
|     |     |

### <a name="known-issues"></a><span data-ttu-id="72691-155">Known issues</span><span class="sxs-lookup"><span data-stu-id="72691-155">Known issues</span></span>

<span data-ttu-id="72691-156">**Issue:**</span><span class="sxs-lookup"><span data-stu-id="72691-156">**Issue:**</span></span><br>
<span data-ttu-id="72691-157">The logs for secrets rotation aren't automatically collected if the secret rotation script fails when it's run.</span><span class="sxs-lookup"><span data-stu-id="72691-157">The logs for secrets rotation aren't automatically collected if the secret rotation script fails when it's run.</span></span>

<span data-ttu-id="72691-158">**Workaround:**</span><span class="sxs-lookup"><span data-stu-id="72691-158">**Workaround:**</span></span><br>
<span data-ttu-id="72691-159">Use the Get-AzsDBAdapterLogs cmdlet to collect all the resource provider logs, including AzureStack.DatabaseAdapter.SecretRotation.ps1_\*.log, saved in C:\Logs.</span><span class="sxs-lookup"><span data-stu-id="72691-159">Use the Get-AzsDBAdapterLogs cmdlet to collect all the resource provider logs, including AzureStack.DatabaseAdapter.SecretRotation.ps1_\*.log, saved in C:\Logs.</span></span>

## <a name="collect-diagnostic-logs"></a><span data-ttu-id="72691-160">Collect diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="72691-160">Collect diagnostic logs</span></span>

<span data-ttu-id="72691-161">To collect logs from the locked down virtual machine, you can use the PowerShell Just Enough Administration (JEA) endpoint DBAdapterDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="72691-161">To collect logs from the locked down virtual machine, you can use the PowerShell Just Enough Administration (JEA) endpoint DBAdapterDiagnostics.</span></span> <span data-ttu-id="72691-162">This endpoint provides the following commands:</span><span class="sxs-lookup"><span data-stu-id="72691-162">This endpoint provides the following commands:</span></span>

- <span data-ttu-id="72691-163">**Get-AzsDBAdapterLog**.</span><span class="sxs-lookup"><span data-stu-id="72691-163">**Get-AzsDBAdapterLog**.</span></span> <span data-ttu-id="72691-164">This command creates a zip package of the resource provider diagnostics logs and saves the file on the session's user drive.</span><span class="sxs-lookup"><span data-stu-id="72691-164">This command creates a zip package of the resource provider diagnostics logs and saves the file on the session's user drive.</span></span> <span data-ttu-id="72691-165">You can run this command without any parameters and the last four hours of logs are collected.</span><span class="sxs-lookup"><span data-stu-id="72691-165">You can run this command without any parameters and the last four hours of logs are collected.</span></span>

- <span data-ttu-id="72691-166">**Remove-AzsDBAdapterLog**.</span><span class="sxs-lookup"><span data-stu-id="72691-166">**Remove-AzsDBAdapterLog**.</span></span> <span data-ttu-id="72691-167">This command removes existing log packages on the resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="72691-167">This command removes existing log packages on the resource provider VM.</span></span>

### <a name="endpoint-requirements-and-process"></a><span data-ttu-id="72691-168">Endpoint requirements and process</span><span class="sxs-lookup"><span data-stu-id="72691-168">Endpoint requirements and process</span></span>

<span data-ttu-id="72691-169">When a resource provider is installed or updated, the dbadapterdiag user account is created.</span><span class="sxs-lookup"><span data-stu-id="72691-169">When a resource provider is installed or updated, the dbadapterdiag user account is created.</span></span> <span data-ttu-id="72691-170">You'll use this account to collect diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="72691-170">You'll use this account to collect diagnostic logs.</span></span>

>[!NOTE]
><span data-ttu-id="72691-171">The dbadapterdiag account password is the same as the password used for the local administrator on the virtual machine that's created during a provider deployment or update.</span><span class="sxs-lookup"><span data-stu-id="72691-171">The dbadapterdiag account password is the same as the password used for the local administrator on the virtual machine that's created during a provider deployment or update.</span></span>

<span data-ttu-id="72691-172">To use the _DBAdapterDiagnostics_ commands, create a remote PowerShell session to the resource provider virtual machine and run the **Get-AzsDBAdapterLog** command.</span><span class="sxs-lookup"><span data-stu-id="72691-172">To use the _DBAdapterDiagnostics_ commands, create a remote PowerShell session to the resource provider virtual machine and run the **Get-AzsDBAdapterLog** command.</span></span>

<span data-ttu-id="72691-173">You set the time span for log collection by using the **FromDate** and **ToDate** parameters.</span><span class="sxs-lookup"><span data-stu-id="72691-173">You set the time span for log collection by using the **FromDate** and **ToDate** parameters.</span></span> <span data-ttu-id="72691-174">If you don't specify one or both of these parameters, the following defaults are used:</span><span class="sxs-lookup"><span data-stu-id="72691-174">If you don't specify one or both of these parameters, the following defaults are used:</span></span>

* <span data-ttu-id="72691-175">FromDate is four hours before the current time.</span><span class="sxs-lookup"><span data-stu-id="72691-175">FromDate is four hours before the current time.</span></span>
* <span data-ttu-id="72691-176">ToDate is the current time.</span><span class="sxs-lookup"><span data-stu-id="72691-176">ToDate is the current time.</span></span>

<span data-ttu-id="72691-177">**PowerShell script example for collecting logs.**</span><span class="sxs-lookup"><span data-stu-id="72691-177">**PowerShell script example for collecting logs.**</span></span>

<span data-ttu-id="72691-178">The following script shows how to collect diagnostic logs from the resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="72691-178">The following script shows how to collect diagnostic logs from the resource provider VM.</span></span>

```powershell
# Create a new diagnostics endpoint session.
$databaseRPMachineIP = '<RP VM IP address>'
$diagnosticsUserName = 'dbadapterdiag'
$diagnosticsUserPassword = '<Enter Diagnostic password>'
$diagCreds = New-Object System.Management.Automation.PSCredential `
        ($diagnosticsUserName, (ConvertTo-SecureString -String $diagnosticsUserPassword -AsPlainText -Force))
$session = New-PSSession -ComputerName $databaseRPMachineIP -Credential $diagCreds
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
$cleanup = Invoke-Command -Session $session -ScriptBlock {Remove-AzsDBAdapterLog}
# Close the session.
$session | Remove-PSSession

```

## <a name="next-steps"></a><span data-ttu-id="72691-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="72691-179">Next steps</span></span>

[<span data-ttu-id="72691-180">Remove the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="72691-180">Remove the MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-remove.md)
