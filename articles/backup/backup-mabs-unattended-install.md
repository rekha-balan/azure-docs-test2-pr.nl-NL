---
title: Silent installation of Azure Backup Server v2
description: Use a PowerShell script to silently install Azure Backup Server v2. This kind of installation is also called an unattended installation.
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 05/30/2017
ms.author: markgal
ms.openlocfilehash: 126c1971d83a8874c096caf407231fb6dee2ff59
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867353"
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="62c43-104">Run an unattended installation of Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="62c43-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="62c43-105">Learn how to run an unattended installation of Azure Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="62c43-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="62c43-106">These steps do not apply if you are installing Azure Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="62c43-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="62c43-107">Install Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="62c43-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="62c43-108">On the server that hosts Azure Backup Server v2, create a text file.</span><span class="sxs-lookup"><span data-stu-id="62c43-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="62c43-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="62c43-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="62c43-110">Paste the following code in the MABSSetup.ini file.</span><span class="sxs-lookup"><span data-stu-id="62c43-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="62c43-111">Replace the text inside the brackets (\< \>) with values from your environment.</span><span class="sxs-lookup"><span data-stu-id="62c43-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="62c43-112">The following text is an example:</span><span class="sxs-lookup"><span data-stu-id="62c43-112">The following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="62c43-113">Save the file.</span><span class="sxs-lookup"><span data-stu-id="62c43-113">Save the file.</span></span> <span data-ttu-id="62c43-114">Then, at an elevated command prompt on the installation server, enter this command:</span><span class="sxs-lookup"><span data-stu-id="62c43-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="62c43-115">You can use these flags for the installation:</span><span class="sxs-lookup"><span data-stu-id="62c43-115">You can use these flags for the installation:</span></span></br>
<span data-ttu-id="62c43-116">**/f**: .ini file path</span><span class="sxs-lookup"><span data-stu-id="62c43-116">**/f**: .ini file path</span></span></br>
<span data-ttu-id="62c43-117">**/l**: Log path</span><span class="sxs-lookup"><span data-stu-id="62c43-117">**/l**: Log path</span></span></br>
<span data-ttu-id="62c43-118">**/i**: Installation path</span><span class="sxs-lookup"><span data-stu-id="62c43-118">**/i**: Installation path</span></span></br>
<span data-ttu-id="62c43-119">**/x**: Uninstall path</span><span class="sxs-lookup"><span data-stu-id="62c43-119">**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="62c43-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="62c43-120">Next steps</span></span>
<span data-ttu-id="62c43-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span><span class="sxs-lookup"><span data-stu-id="62c43-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="62c43-122">Prepare Backup Server workloads</span><span class="sxs-lookup"><span data-stu-id="62c43-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="62c43-123">Use Backup Server to back up a VMware server</span><span class="sxs-lookup"><span data-stu-id="62c43-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="62c43-124">Use Backup Server to back up SQL Server</span><span class="sxs-lookup"><span data-stu-id="62c43-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="62c43-125">Add Modern Backup Storage to Backup Server</span><span class="sxs-lookup"><span data-stu-id="62c43-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
