---
title: 'Azure AD Connect sync: Operational tasks and considerations | Microsoft Docs'
description: This topic describes operational tasks for Azure AD Connect sync and how to prepare for operating this component.
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: 9d23811fe8ac301946804bc6a53a65a369ae1a78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672331"
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="b175f-103">Azure AD Connect sync: Operational tasks and consideration</span><span class="sxs-lookup"><span data-stu-id="b175f-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="b175f-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span><span class="sxs-lookup"><span data-stu-id="b175f-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="b175f-105">Staging mode</span><span class="sxs-lookup"><span data-stu-id="b175f-105">Staging mode</span></span>
<span data-ttu-id="b175f-106">Staging mode can be used for several scenarios, including:</span><span class="sxs-lookup"><span data-stu-id="b175f-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="b175f-107">High availability.</span><span class="sxs-lookup"><span data-stu-id="b175f-107">High availability.</span></span>
* <span data-ttu-id="b175f-108">Test and deploy new configuration changes.</span><span class="sxs-lookup"><span data-stu-id="b175f-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="b175f-109">Introduce a new server and decommission the old.</span><span class="sxs-lookup"><span data-stu-id="b175f-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="b175f-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span><span class="sxs-lookup"><span data-stu-id="b175f-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="b175f-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span><span class="sxs-lookup"><span data-stu-id="b175f-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="b175f-112">During installation, you can select the server to be in **staging mode**.</span><span class="sxs-lookup"><span data-stu-id="b175f-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="b175f-113">This action makes the server active for import and synchronization, but it does not run any exports.</span><span class="sxs-lookup"><span data-stu-id="b175f-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="b175f-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span><span class="sxs-lookup"><span data-stu-id="b175f-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="b175f-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span><span class="sxs-lookup"><span data-stu-id="b175f-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="b175f-116">You can still force an export by using the synchronization service manager.</span><span class="sxs-lookup"><span data-stu-id="b175f-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="b175f-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b175f-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="b175f-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span><span class="sxs-lookup"><span data-stu-id="b175f-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="b175f-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span><span class="sxs-lookup"><span data-stu-id="b175f-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="b175f-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span><span class="sxs-lookup"><span data-stu-id="b175f-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="b175f-121">This architecture allows the staging mode server to be located in a different datacenter.</span><span class="sxs-lookup"><span data-stu-id="b175f-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="b175f-122">Verify the configuration of a server</span><span class="sxs-lookup"><span data-stu-id="b175f-122">Verify the configuration of a server</span></span>
<span data-ttu-id="b175f-123">To apply this method, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b175f-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="b175f-124">Prepare</span><span class="sxs-lookup"><span data-stu-id="b175f-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="b175f-125">Configuration</span><span class="sxs-lookup"><span data-stu-id="b175f-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="b175f-126">Import and Synchronize</span><span class="sxs-lookup"><span data-stu-id="b175f-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="b175f-127">Verify</span><span class="sxs-lookup"><span data-stu-id="b175f-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="b175f-128">Switch active server</span><span class="sxs-lookup"><span data-stu-id="b175f-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="b175f-129">Prepare</span><span class="sxs-lookup"><span data-stu-id="b175f-129">Prepare</span></span>
1. <span data-ttu-id="b175f-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="b175f-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="b175f-131">This mode allows you to run the sync engine manually.</span><span class="sxs-lookup"><span data-stu-id="b175f-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="b175f-132">![ReadyToConfigure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="b175f-132">![ReadyToConfigure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="b175f-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span><span class="sxs-lookup"><span data-stu-id="b175f-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="b175f-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="b175f-134">Configuration</span></span>
<span data-ttu-id="b175f-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="b175f-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="b175f-136">Import and Synchronize</span><span class="sxs-lookup"><span data-stu-id="b175f-136">Import and Synchronize</span></span>
1. <span data-ttu-id="b175f-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="b175f-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="b175f-138">Click **Run**, select **Full import**, and **OK**.</span><span class="sxs-lookup"><span data-stu-id="b175f-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="b175f-139">Do these steps for all Connectors of this type.</span><span class="sxs-lookup"><span data-stu-id="b175f-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="b175f-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="b175f-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="b175f-141">Click **Run**, select **Full import**, and **OK**.</span><span class="sxs-lookup"><span data-stu-id="b175f-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="b175f-142">Make sure the tab Connectors is still selected.</span><span class="sxs-lookup"><span data-stu-id="b175f-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="b175f-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span><span class="sxs-lookup"><span data-stu-id="b175f-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="b175f-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="b175f-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="b175f-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span><span class="sxs-lookup"><span data-stu-id="b175f-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="b175f-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span><span class="sxs-lookup"><span data-stu-id="b175f-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="b175f-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span><span class="sxs-lookup"><span data-stu-id="b175f-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="b175f-148">Verify</span><span class="sxs-lookup"><span data-stu-id="b175f-148">Verify</span></span>
1. <span data-ttu-id="b175f-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="b175f-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="b175f-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span><span class="sxs-lookup"><span data-stu-id="b175f-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="b175f-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b175f-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="b175f-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="b175f-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="b175f-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="b175f-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="b175f-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="b175f-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="b175f-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="b175f-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="b175f-156">All changes staged to be exported to Azure AD are found in this file.</span><span class="sxs-lookup"><span data-stu-id="b175f-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="b175f-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span><span class="sxs-lookup"><span data-stu-id="b175f-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="b175f-158">Switch active server</span><span class="sxs-lookup"><span data-stu-id="b175f-158">Switch active server</span></span>
1. <span data-ttu-id="b175f-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="b175f-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="b175f-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span><span class="sxs-lookup"><span data-stu-id="b175f-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="b175f-161">![ReadyToConfigure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="b175f-161">![ReadyToConfigure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="b175f-162">Disaster recovery</span><span class="sxs-lookup"><span data-stu-id="b175f-162">Disaster recovery</span></span>
<span data-ttu-id="b175f-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span><span class="sxs-lookup"><span data-stu-id="b175f-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="b175f-164">There are different models to use and which one to use depends on several factors including:</span><span class="sxs-lookup"><span data-stu-id="b175f-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="b175f-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span><span class="sxs-lookup"><span data-stu-id="b175f-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="b175f-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span><span class="sxs-lookup"><span data-stu-id="b175f-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="b175f-167">Do you have a dependency on real-time operations, such as password writeback?</span><span class="sxs-lookup"><span data-stu-id="b175f-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="b175f-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span><span class="sxs-lookup"><span data-stu-id="b175f-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="b175f-169">Rebuild when needed.</span><span class="sxs-lookup"><span data-stu-id="b175f-169">Rebuild when needed.</span></span>
* <span data-ttu-id="b175f-170">Have a spare standby server, known as **staging mode**.</span><span class="sxs-lookup"><span data-stu-id="b175f-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="b175f-171">Use virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b175f-171">Use virtual machines.</span></span>

<span data-ttu-id="b175f-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span><span class="sxs-lookup"><span data-stu-id="b175f-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="b175f-173">Rebuild when needed</span><span class="sxs-lookup"><span data-stu-id="b175f-173">Rebuild when needed</span></span>
<span data-ttu-id="b175f-174">A viable strategy is to plan for a server rebuild when needed.</span><span class="sxs-lookup"><span data-stu-id="b175f-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="b175f-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span><span class="sxs-lookup"><span data-stu-id="b175f-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="b175f-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span><span class="sxs-lookup"><span data-stu-id="b175f-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="b175f-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b175f-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="b175f-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span><span class="sxs-lookup"><span data-stu-id="b175f-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="b175f-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span><span class="sxs-lookup"><span data-stu-id="b175f-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="b175f-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span><span class="sxs-lookup"><span data-stu-id="b175f-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="b175f-181">These custom configurations must be reapplied before you start synchronizing.</span><span class="sxs-lookup"><span data-stu-id="b175f-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="b175f-182">Have a spare standby server - staging mode</span><span class="sxs-lookup"><span data-stu-id="b175f-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="b175f-183">If you have a more complex environment, then having one or more standby servers is recommended.</span><span class="sxs-lookup"><span data-stu-id="b175f-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="b175f-184">During installation, you can enable a server to be in **staging mode**.</span><span class="sxs-lookup"><span data-stu-id="b175f-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="b175f-185">For more information, see [staging mode](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="b175f-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="b175f-186">Use virtual machines</span><span class="sxs-lookup"><span data-stu-id="b175f-186">Use virtual machines</span></span>
<span data-ttu-id="b175f-187">A common and supported method is to run the sync engine in a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b175f-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="b175f-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span><span class="sxs-lookup"><span data-stu-id="b175f-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="b175f-189">SQL High Availability</span><span class="sxs-lookup"><span data-stu-id="b175f-189">SQL High Availability</span></span>
<span data-ttu-id="b175f-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span><span class="sxs-lookup"><span data-stu-id="b175f-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="b175f-191">The only high availability solution supported is SQL clustering.</span><span class="sxs-lookup"><span data-stu-id="b175f-191">The only high availability solution supported is SQL clustering.</span></span> <span data-ttu-id="b175f-192">Unsupported solutions include mirroring and Always On.</span><span class="sxs-lookup"><span data-stu-id="b175f-192">Unsupported solutions include mirroring and Always On.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="b175f-193">Appendix CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="b175f-193">Appendix CSAnalyzer</span></span>
<span data-ttu-id="b175f-194">See the section [verify](#verify) on how to use this script.</span><span class="sxs-lookup"><span data-stu-id="b175f-194">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="b175f-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="b175f-195">Next steps</span></span>
<span data-ttu-id="b175f-196">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="b175f-196">**Overview topics**</span></span>  

* [<span data-ttu-id="b175f-197">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="b175f-197">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="b175f-198">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b175f-198">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  


