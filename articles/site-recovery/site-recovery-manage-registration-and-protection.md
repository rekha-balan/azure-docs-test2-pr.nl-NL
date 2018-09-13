---
title: Remove servers and disable protection | Microsoft Docs
description: This article describes how to unregister servers from a Site Recovery vault, and to disable protection for virtual machines and physical servers.
services: site-recovery
documentationcenter: ''
author: rayne-wiselman
manager: cfreeman
editor: ''
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555785"
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="73bf1-103">Remove servers and disable protection</span><span class="sxs-lookup"><span data-stu-id="73bf1-103">Remove servers and disable protection</span></span>

<span data-ttu-id="73bf1-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span><span class="sxs-lookup"><span data-stu-id="73bf1-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="73bf1-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span><span class="sxs-lookup"><span data-stu-id="73bf1-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="73bf1-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span><span class="sxs-lookup"><span data-stu-id="73bf1-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="73bf1-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="73bf1-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="73bf1-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="73bf1-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="73bf1-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="73bf1-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="73bf1-110">Unregister a connected configuration server</span><span class="sxs-lookup"><span data-stu-id="73bf1-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="73bf1-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span><span class="sxs-lookup"><span data-stu-id="73bf1-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="73bf1-112">Disable machine protection.</span><span class="sxs-lookup"><span data-stu-id="73bf1-112">Disable machine protection.</span></span> <span data-ttu-id="73bf1-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="73bf1-114">Disassociate any policies.</span><span class="sxs-lookup"><span data-stu-id="73bf1-114">Disassociate any policies.</span></span> <span data-ttu-id="73bf1-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span><span class="sxs-lookup"><span data-stu-id="73bf1-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="73bf1-116">Right-click the configuration server > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="73bf1-117">Remove any additional on-premises process or master target servers.</span><span class="sxs-lookup"><span data-stu-id="73bf1-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="73bf1-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="73bf1-119">Delete the configuration server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="73bf1-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span><span class="sxs-lookup"><span data-stu-id="73bf1-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="73bf1-121">Uninstall any additional process servers.</span><span class="sxs-lookup"><span data-stu-id="73bf1-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="73bf1-122">Uninstall the configuration server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="73bf1-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="73bf1-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="73bf1-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="73bf1-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="73bf1-125">Unregister a unconnected configuration server</span><span class="sxs-lookup"><span data-stu-id="73bf1-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="73bf1-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span><span class="sxs-lookup"><span data-stu-id="73bf1-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="73bf1-127">Disable machine protection.</span><span class="sxs-lookup"><span data-stu-id="73bf1-127">Disable machine protection.</span></span> <span data-ttu-id="73bf1-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="73bf1-129">Select **Stop managing the machine**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="73bf1-130">Remove any additional on-premises process or master target servers.</span><span class="sxs-lookup"><span data-stu-id="73bf1-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="73bf1-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="73bf1-132">Delete the configuration server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="73bf1-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span><span class="sxs-lookup"><span data-stu-id="73bf1-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="73bf1-134">Uninstall any additional process servers.</span><span class="sxs-lookup"><span data-stu-id="73bf1-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="73bf1-135">Uninstall the configuration server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="73bf1-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="73bf1-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="73bf1-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="73bf1-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="73bf1-138">Unregister a connected VMM server</span><span class="sxs-lookup"><span data-stu-id="73bf1-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="73bf1-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span><span class="sxs-lookup"><span data-stu-id="73bf1-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="73bf1-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span><span class="sxs-lookup"><span data-stu-id="73bf1-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="73bf1-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span><span class="sxs-lookup"><span data-stu-id="73bf1-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="73bf1-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span><span class="sxs-lookup"><span data-stu-id="73bf1-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="73bf1-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span><span class="sxs-lookup"><span data-stu-id="73bf1-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="73bf1-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span><span class="sxs-lookup"><span data-stu-id="73bf1-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="73bf1-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="73bf1-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span><span class="sxs-lookup"><span data-stu-id="73bf1-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="73bf1-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span><span class="sxs-lookup"><span data-stu-id="73bf1-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="73bf1-148">Right-click the cloud > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="73bf1-149">Delete the VMM server or active VMM node.</span><span class="sxs-lookup"><span data-stu-id="73bf1-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="73bf1-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="73bf1-151">Uninstall the Provider manually on the VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="73bf1-152">If you have a cluster, remove from all nodes.</span><span class="sxs-lookup"><span data-stu-id="73bf1-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="73bf1-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span><span class="sxs-lookup"><span data-stu-id="73bf1-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="73bf1-154">Unregister an unconnected VMM server</span><span class="sxs-lookup"><span data-stu-id="73bf1-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="73bf1-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span><span class="sxs-lookup"><span data-stu-id="73bf1-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="73bf1-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="73bf1-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="73bf1-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="73bf1-158">Note the ID of the VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="73bf1-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span><span class="sxs-lookup"><span data-stu-id="73bf1-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="73bf1-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span><span class="sxs-lookup"><span data-stu-id="73bf1-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="73bf1-161">Right-click the cloud > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="73bf1-162">Delete the VMM server or active node.</span><span class="sxs-lookup"><span data-stu-id="73bf1-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="73bf1-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="73bf1-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="73bf1-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span><span class="sxs-lookup"><span data-stu-id="73bf1-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="73bf1-166">In the script, specify the ID of the VMM server you want to remove.</span><span class="sxs-lookup"><span data-stu-id="73bf1-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="73bf1-167">The script removes registration and cloud pairing information from the server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="73bf1-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span><span class="sxs-lookup"><span data-stu-id="73bf1-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="73bf1-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span><span class="sxs-lookup"><span data-stu-id="73bf1-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="73bf1-170">Uninstall the Provider manually on the VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="73bf1-171">If you have a cluster, remove from all nodes.</span><span class="sxs-lookup"><span data-stu-id="73bf1-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="73bf1-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span><span class="sxs-lookup"><span data-stu-id="73bf1-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="73bf1-173">Unregister a Hyper-V host in a Hyper-V Site</span><span class="sxs-lookup"><span data-stu-id="73bf1-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="73bf1-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span><span class="sxs-lookup"><span data-stu-id="73bf1-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="73bf1-175">Remove a host in a Hyper-V site as follows:</span><span class="sxs-lookup"><span data-stu-id="73bf1-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="73bf1-176">Disable replication for Hyper-V VMs located on the host.</span><span class="sxs-lookup"><span data-stu-id="73bf1-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="73bf1-177">Disassociate policies for the Hyper-V site.</span><span class="sxs-lookup"><span data-stu-id="73bf1-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="73bf1-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span><span class="sxs-lookup"><span data-stu-id="73bf1-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="73bf1-179">Right-click the site > **Disassociate**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="73bf1-180">Delete Hyper-V hosts.</span><span class="sxs-lookup"><span data-stu-id="73bf1-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="73bf1-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="73bf1-182">Delete the Hyper-V site after all hosts have been removed from it.</span><span class="sxs-lookup"><span data-stu-id="73bf1-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="73bf1-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="73bf1-184">Run the following script on each Hyper-V host that you removed.</span><span class="sxs-lookup"><span data-stu-id="73bf1-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="73bf1-185">The script cleans up settings on the server, and unregisters it from the vault.</span><span class="sxs-lookup"><span data-stu-id="73bf1-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping the Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="73bf1-186">Disable protection for a VMware VM or physical server</span><span class="sxs-lookup"><span data-stu-id="73bf1-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="73bf1-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="73bf1-188">In **Remove Machine**, select one of these options:</span><span class="sxs-lookup"><span data-stu-id="73bf1-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="73bf1-189">**Disable protection for the machine (recommended)**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="73bf1-190">Use this option to stop replicating the machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="73bf1-191">Site Recovery settings will be cleaned up automatically.</span><span class="sxs-lookup"><span data-stu-id="73bf1-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="73bf1-192">You will only see this option in the following circumstances:</span><span class="sxs-lookup"><span data-stu-id="73bf1-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="73bf1-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span><span class="sxs-lookup"><span data-stu-id="73bf1-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="73bf1-194">Select this option to disables protection while retaining recovery points in Azure.</span><span class="sxs-lookup"><span data-stu-id="73bf1-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="73bf1-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span><span class="sxs-lookup"><span data-stu-id="73bf1-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="73bf1-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span><span class="sxs-lookup"><span data-stu-id="73bf1-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="73bf1-197">It disables each virtual machine, and then you need to enable protection for them again.</span><span class="sxs-lookup"><span data-stu-id="73bf1-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="73bf1-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="73bf1-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="73bf1-199">Don't uninstall the Mobility service from the machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="73bf1-200">**Stop managing the machine**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-200">**Stop managing the machine**.</span></span> <span data-ttu-id="73bf1-201">If you select this option, the machine will only be removed from the vault.</span><span class="sxs-lookup"><span data-stu-id="73bf1-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="73bf1-202">On-premises protection settings for the machine won’t be affected.</span><span class="sxs-lookup"><span data-stu-id="73bf1-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="73bf1-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span><span class="sxs-lookup"><span data-stu-id="73bf1-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="73bf1-204">Disable protection for a Hyper-V VM in a VMM cloud</span><span class="sxs-lookup"><span data-stu-id="73bf1-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="73bf1-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="73bf1-206">In **Remove Machine**, select one of these options:</span><span class="sxs-lookup"><span data-stu-id="73bf1-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="73bf1-207">**Disable protection for the machine (recommended)**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="73bf1-208">Use this option to stop replicating the machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="73bf1-209">Site Recovery settings will be cleaned up automatically.</span><span class="sxs-lookup"><span data-stu-id="73bf1-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="73bf1-210">**Stop managing the machine**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-210">**Stop managing the machine**.</span></span> <span data-ttu-id="73bf1-211">If you select this option, the machine will only be removed from the vault.</span><span class="sxs-lookup"><span data-stu-id="73bf1-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="73bf1-212">On-premises protection settings for the machine won’t be affected.</span><span class="sxs-lookup"><span data-stu-id="73bf1-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="73bf1-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span><span class="sxs-lookup"><span data-stu-id="73bf1-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="73bf1-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span><span class="sxs-lookup"><span data-stu-id="73bf1-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="73bf1-215">Clean up protection settings - replication to a secondary VMM site</span><span class="sxs-lookup"><span data-stu-id="73bf1-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="73bf1-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="73bf1-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="73bf1-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="73bf1-218">Replace SQLVM1 with the name of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="73bf1-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span><span class="sxs-lookup"><span data-stu-id="73bf1-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="73bf1-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span><span class="sxs-lookup"><span data-stu-id="73bf1-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="73bf1-221">The above steps clear up the replication settings on the VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="73bf1-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span><span class="sxs-lookup"><span data-stu-id="73bf1-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="73bf1-223">Replace SQLVM1 with the name of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="73bf1-224">Clean up protection settings - replication to Azure</span><span class="sxs-lookup"><span data-stu-id="73bf1-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="73bf1-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span><span class="sxs-lookup"><span data-stu-id="73bf1-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="73bf1-226">The above steps clear the replication settings on the VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="73bf1-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span><span class="sxs-lookup"><span data-stu-id="73bf1-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="73bf1-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="73bf1-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span><span class="sxs-lookup"><span data-stu-id="73bf1-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="73bf1-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span><span class="sxs-lookup"><span data-stu-id="73bf1-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="73bf1-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="73bf1-232">In **Remove Machine**, you can select the following options:</span><span class="sxs-lookup"><span data-stu-id="73bf1-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="73bf1-233">**Disable protection for the machine (recommended)**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="73bf1-234">Use this option to stop replicating the machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="73bf1-235">Site Recovery settings will be cleaned up automatically.</span><span class="sxs-lookup"><span data-stu-id="73bf1-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="73bf1-236">**Stop managing the machine**.</span><span class="sxs-lookup"><span data-stu-id="73bf1-236">**Stop managing the machine**.</span></span> <span data-ttu-id="73bf1-237">If you select this option the machine will only be removed from the vault.</span><span class="sxs-lookup"><span data-stu-id="73bf1-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="73bf1-238">On-premises protection settings for the machine won’t be affected.</span><span class="sxs-lookup"><span data-stu-id="73bf1-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="73bf1-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span><span class="sxs-lookup"><span data-stu-id="73bf1-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="73bf1-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span><span class="sxs-lookup"><span data-stu-id="73bf1-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="73bf1-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="73bf1-242">Replace SQLVM1 with the name of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="73bf1-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
