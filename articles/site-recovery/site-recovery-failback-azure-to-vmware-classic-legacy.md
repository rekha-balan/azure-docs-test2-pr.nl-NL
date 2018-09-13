---
title: Fail back VMware VMs from Azure in the classic legacy portal | Microsoft Docs
description: This article describes how to fail back a VMware virtual machine that's been replicated to Azure with Azure Site Recovery.
services: site-recovery
documentationcenter: ''
author: ruturaj
manager: mkjain
editor: ''
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 02/06/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: bee79c3610d4ff20738696e3bda7080d5fdf53cb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548970"
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-to-vmware-with-azure-site-recovery-legacy"></a><span data-ttu-id="b42a3-103">Fail back VMware virtual machines and physical servers from Azure to VMware with Azure Site Recovery (legacy)</span><span class="sxs-lookup"><span data-stu-id="b42a3-103">Fail back VMware virtual machines and physical servers from Azure to VMware with Azure Site Recovery (legacy)</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Azure Classic Portal](site-recovery-failback-azure-to-vmware-classic.md)
> * [Azure Classic Portal (Legacy)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

<span data-ttu-id="b42a3-107">This article describes how to fail back VMware virtual machines and Windows/Linux physical servers from Azure to your on-premises site after you've replicated from your on-premises site to Azure using [Azure Site Recovery?](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b42a3-107">This article describes how to fail back VMware virtual machines and Windows/Linux physical servers from Azure to your on-premises site after you've replicated from your on-premises site to Azure using [Azure Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="b42a3-108">This article describes an old configuration and shouldn't be used for new vaults.</span><span class="sxs-lookup"><span data-stu-id="b42a3-108">This article describes an old configuration and shouldn't be used for new vaults.</span></span>

## <a name="architecture"></a><span data-ttu-id="b42a3-109">Architecture</span><span class="sxs-lookup"><span data-stu-id="b42a3-109">Architecture</span></span>
<span data-ttu-id="b42a3-110">This diagram represents the failover and failback scenario.</span><span class="sxs-lookup"><span data-stu-id="b42a3-110">This diagram represents the failover and failback scenario.</span></span> <span data-ttu-id="b42a3-111">The blue lines are the connections used during failover.</span><span class="sxs-lookup"><span data-stu-id="b42a3-111">The blue lines are the connections used during failover.</span></span> <span data-ttu-id="b42a3-112">The red lines are the connections used during failback.</span><span class="sxs-lookup"><span data-stu-id="b42a3-112">The red lines are the connections used during failback.</span></span> <span data-ttu-id="b42a3-113">The lines with arrows go over the internet.</span><span class="sxs-lookup"><span data-stu-id="b42a3-113">The lines with arrows go over the internet.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a><span data-ttu-id="b42a3-114">Before you start</span><span class="sxs-lookup"><span data-stu-id="b42a3-114">Before you start</span></span>
* <span data-ttu-id="b42a3-115">You should have failed over your VMware VMs or physical servers and they should be running in Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-115">You should have failed over your VMware VMs or physical servers and they should be running in Azure.</span></span>
* <span data-ttu-id="b42a3-116">You should note that you can only fail back VMware virtual machines and Windows/Linux physical servers from Azure to VMware virtual machines in the on-premises primary site.</span><span class="sxs-lookup"><span data-stu-id="b42a3-116">You should note that you can only fail back VMware virtual machines and Windows/Linux physical servers from Azure to VMware virtual machines in the on-premises primary site.</span></span>  <span data-ttu-id="b42a3-117">If you're failing back a physical machine, failover to Azure will convert it to an Azure VM, and failback to VMware will convert it to a VMware VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-117">If you're failing back a physical machine, failover to Azure will convert it to an Azure VM, and failback to VMware will convert it to a VMware VM.</span></span>

<span data-ttu-id="b42a3-118">Here's how you set up failback:</span><span class="sxs-lookup"><span data-stu-id="b42a3-118">Here's how you set up failback:</span></span>

1. <span data-ttu-id="b42a3-119">**Set up failback components**: You'll need to set up a vContinuum server on-premises, and point it to the configuration server VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-119">**Set up failback components**: You'll need to set up a vContinuum server on-premises, and point it to the configuration server VM in Azure.</span></span> <span data-ttu-id="b42a3-120">You'll also set up a process server as an Azure VM to send data back to the on-premises master target server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-120">You'll also set up a process server as an Azure VM to send data back to the on-premises master target server.</span></span> <span data-ttu-id="b42a3-121">You register the process server with the configuration server that  handled the failover.</span><span class="sxs-lookup"><span data-stu-id="b42a3-121">You register the process server with the configuration server that  handled the failover.</span></span> <span data-ttu-id="b42a3-122">You install an on-premises master target server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-122">You install an on-premises master target server.</span></span> <span data-ttu-id="b42a3-123">If you need a Windows master target server it's set up automatically when you install vContinuum.</span><span class="sxs-lookup"><span data-stu-id="b42a3-123">If you need a Windows master target server it's set up automatically when you install vContinuum.</span></span> <span data-ttu-id="b42a3-124">If you need Linux you'll need to set it up manually on a separate server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-124">If you need Linux you'll need to set it up manually on a separate server.</span></span>
2. <span data-ttu-id="b42a3-125">**Enable protection and failback**: After you've set up the components, in vContinuum you'll need to enable protection for failed over Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="b42a3-125">**Enable protection and failback**: After you've set up the components, in vContinuum you'll need to enable protection for failed over Azure VMs.</span></span> <span data-ttu-id="b42a3-126">You'll run a readiness check on the VMs and run a failover from Azure to your on-premises site.</span><span class="sxs-lookup"><span data-stu-id="b42a3-126">You'll run a readiness check on the VMs and run a failover from Azure to your on-premises site.</span></span> <span data-ttu-id="b42a3-127">After failback finishes you reprotect on-premises machines so that they start replicating to Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-127">After failback finishes you reprotect on-premises machines so that they start replicating to Azure.</span></span>

## <a name="step-1-install-vcontinuum-on-premises"></a><span data-ttu-id="b42a3-128">Step 1: Install vContinuum on-premises</span><span class="sxs-lookup"><span data-stu-id="b42a3-128">Step 1: Install vContinuum on-premises</span></span>
<span data-ttu-id="b42a3-129">You'll need to install a vContinuum server on premises and point it to the configuration server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-129">You'll need to install a vContinuum server on premises and point it to the configuration server.</span></span>

1. <span data-ttu-id="b42a3-130">[Download vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).</span><span class="sxs-lookup"><span data-stu-id="b42a3-130">[Download vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).</span></span>
2. <span data-ttu-id="b42a3-131">Then download the [vContinuum update](http://go.microsoft.com/fwlink/?LinkID=533813) version.</span><span class="sxs-lookup"><span data-stu-id="b42a3-131">Then download the [vContinuum update](http://go.microsoft.com/fwlink/?LinkID=533813) version.</span></span>
3. <span data-ttu-id="b42a3-132">Install the latest version of vContinuum.</span><span class="sxs-lookup"><span data-stu-id="b42a3-132">Install the latest version of vContinuum.</span></span> <span data-ttu-id="b42a3-133">On the **Welcome** page click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-133">On the **Welcome** page click **Next**.</span></span>
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image2.png)
4. <span data-ttu-id="b42a3-134">On the first page of the wizard specify the CX server IP address and the CX server port.</span><span class="sxs-lookup"><span data-stu-id="b42a3-134">On the first page of the wizard specify the CX server IP address and the CX server port.</span></span> <span data-ttu-id="b42a3-135">Select **Use HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-135">Select **Use HTTPS**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image3.png)
5. <span data-ttu-id="b42a3-136">Find the configuration server IP address on the **Dashboard** tab of the configuration server VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-136">Find the configuration server IP address on the **Dashboard** tab of the configuration server VM in Azure.</span></span>
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image4.png)
6. <span data-ttu-id="b42a3-137">Find the configuration server HTTPS public port on the **Endpoints** tab of the configuration server VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-137">Find the configuration server HTTPS public port on the **Endpoints** tab of the configuration server VM in Azure.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image5.png)
7. <span data-ttu-id="b42a3-138">On the **CS Passphrase Details** page specify the passphrase that you noted down when you registered the configuration server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-138">On the **CS Passphrase Details** page specify the passphrase that you noted down when you registered the configuration server.</span></span> <span data-ttu-id="b42a3-139">If you don't remember it check it in **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase** on the configuration server VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-139">If you don't remember it check it in **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase** on the configuration server VM.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image6.png)
8. <span data-ttu-id="b42a3-140">In the **Select Destination Location** page specify where you want to install the vContinuum server and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-140">In the **Select Destination Location** page specify where you want to install the vContinuum server and click **Install**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image7.png)
9. <span data-ttu-id="b42a3-141">After installation completes, you can launch vContinuum.</span><span class="sxs-lookup"><span data-stu-id="b42a3-141">After installation completes, you can launch vContinuum.</span></span>
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a><span data-ttu-id="b42a3-142">Step 2: Install a process server in Azure</span><span class="sxs-lookup"><span data-stu-id="b42a3-142">Step 2: Install a process server in Azure</span></span>
<span data-ttu-id="b42a3-143">You need to install a process server in Azure so that the VMs in Azure can send the data back to an on-premises master target server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-143">You need to install a process server in Azure so that the VMs in Azure can send the data back to an on-premises master target server.</span></span>

1. <span data-ttu-id="b42a3-144">On the **Configuration Servers** page in Azure, select to add a new process server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-144">On the **Configuration Servers** page in Azure, select to add a new process server.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image9.png)
2. <span data-ttu-id="b42a3-145">Specify a process server name, and a name and password to connect to the virtual machine as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b42a3-145">Specify a process server name, and a name and password to connect to the virtual machine as an administrator.</span></span> <span data-ttu-id="b42a3-146">Select the configuration server to which you want to register the process server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-146">Select the configuration server to which you want to register the process server.</span></span> <span data-ttu-id="b42a3-147">This should be the same server you're using to protect and fail over your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b42a3-147">This should be the same server you're using to protect and fail over your virtual machines.</span></span>
3. <span data-ttu-id="b42a3-148">Specify the Azure network in which the process server should be deployed.</span><span class="sxs-lookup"><span data-stu-id="b42a3-148">Specify the Azure network in which the process server should be deployed.</span></span> <span data-ttu-id="b42a3-149">It should be the same network as the configuration server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-149">It should be the same network as the configuration server.</span></span> <span data-ttu-id="b42a3-150">Specify a unique IP address selected subnet and begin deployment.</span><span class="sxs-lookup"><span data-stu-id="b42a3-150">Specify a unique IP address selected subnet and begin deployment.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image10.png)
4. <span data-ttu-id="b42a3-151">A job is triggered to deploy the process server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-151">A job is triggered to deploy the process server.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image11.png)
5. <span data-ttu-id="b42a3-152">After the process server is deployed in Azure you can log into the server using the credentials you specified.</span><span class="sxs-lookup"><span data-stu-id="b42a3-152">After the process server is deployed in Azure you can log into the server using the credentials you specified.</span></span> <span data-ttu-id="b42a3-153">Register the process server in the same way you registered the on-premises process server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-153">Register the process server in the same way you registered the on-premises process server.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> The servers registered during failback won't be visible under VM properties in Site Recovery. They are only visible under the **Servers** tab of the configuration server to which they're registered. It can take about 10-15 minutes until they the process server appears on the tab.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a><span data-ttu-id="b42a3-157">Step 3: Install a master target server on-premises</span><span class="sxs-lookup"><span data-stu-id="b42a3-157">Step 3: Install a master target server on-premises</span></span>
<span data-ttu-id="b42a3-158">Depending on your source virtual machines operating system, you need to install a Linux or a Windows master target server on-premises.</span><span class="sxs-lookup"><span data-stu-id="b42a3-158">Depending on your source virtual machines operating system, you need to install a Linux or a Windows master target server on-premises.</span></span>

### <a name="deploy-a-windows-master-target-server"></a><span data-ttu-id="b42a3-159">Deploy a Windows master target server</span><span class="sxs-lookup"><span data-stu-id="b42a3-159">Deploy a Windows master target server</span></span>
<span data-ttu-id="b42a3-160">A Windows master target is already bundled with vContinuum setup.</span><span class="sxs-lookup"><span data-stu-id="b42a3-160">A Windows master target is already bundled with vContinuum setup.</span></span> <span data-ttu-id="b42a3-161">When you install the vContinuum, a master server is also deployed on the same machine and registered to the configuration server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-161">When you install the vContinuum, a master server is also deployed on the same machine and registered to the configuration server.</span></span>

1. <span data-ttu-id="b42a3-162">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-162">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span></span>
2. <span data-ttu-id="b42a3-163">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span><span class="sxs-lookup"><span data-stu-id="b42a3-163">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span></span>
3. <span data-ttu-id="b42a3-164">Install the operating system.</span><span class="sxs-lookup"><span data-stu-id="b42a3-164">Install the operating system.</span></span>
4. <span data-ttu-id="b42a3-165">Install the vContinuum on the server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-165">Install the vContinuum on the server.</span></span> <span data-ttu-id="b42a3-166">This also completes installation of the master target server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-166">This also completes installation of the master target server.</span></span>

### <a name="deploy-a-linux-master-target-server"></a><span data-ttu-id="b42a3-167">Deploy a Linux master target server</span><span class="sxs-lookup"><span data-stu-id="b42a3-167">Deploy a Linux master target server</span></span>
1. <span data-ttu-id="b42a3-168">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-168">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span></span>
2. <span data-ttu-id="b42a3-169">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span><span class="sxs-lookup"><span data-stu-id="b42a3-169">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span></span>
3. <span data-ttu-id="b42a3-170">Install the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="b42a3-170">Install the Linux operating system.</span></span> <span data-ttu-id="b42a3-171">The Linux master target system should not use LVM for root or retention storage spaces.</span><span class="sxs-lookup"><span data-stu-id="b42a3-171">The Linux master target system should not use LVM for root or retention storage spaces.</span></span> <span data-ttu-id="b42a3-172">A Linux master target server is configured to avoid LVM partitions/disks discovery by default.</span><span class="sxs-lookup"><span data-stu-id="b42a3-172">A Linux master target server is configured to avoid LVM partitions/disks discovery by default.</span></span>
4. <span data-ttu-id="b42a3-173">Partitions that you can create:</span><span class="sxs-lookup"><span data-stu-id="b42a3-173">Partitions that you can create:</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image13.png)
5. <span data-ttu-id="b42a3-174">Carry out the below post installation steps before beginning the master target installation.</span><span class="sxs-lookup"><span data-stu-id="b42a3-174">Carry out the below post installation steps before beginning the master target installation.</span></span>

#### <a name="post-os-installation-steps"></a><span data-ttu-id="b42a3-175">Post OS Installation Steps</span><span class="sxs-lookup"><span data-stu-id="b42a3-175">Post OS Installation Steps</span></span>
<span data-ttu-id="b42a3-176">To get the SCSI ID’s for each of SCSI hard disk in a Linux virtual machine, enable the parameter “disk.EnableUUID = TRUE” as follows:</span><span class="sxs-lookup"><span data-stu-id="b42a3-176">To get the SCSI ID’s for each of SCSI hard disk in a Linux virtual machine, enable the parameter “disk.EnableUUID = TRUE” as follows:</span></span>

1. <span data-ttu-id="b42a3-177">Shut down your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-177">Shut down your virtual machine.</span></span>
2. <span data-ttu-id="b42a3-178">Right-click the VM entry in the left-hand panel > **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-178">Right-click the VM entry in the left-hand panel > **Edit Settings**.</span></span>
3. <span data-ttu-id="b42a3-179">Click the **Options** tab. Select **Advanced\>General item** > **Configuration Parameters**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-179">Click the **Options** tab. Select **Advanced\>General item** > **Configuration Parameters**.</span></span> <span data-ttu-id="b42a3-180">The **Configuration Parameters** option is only available when the machine is shut down.</span><span class="sxs-lookup"><span data-stu-id="b42a3-180">The **Configuration Parameters** option is only available when the machine is shut down.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image14.png)
4. <span data-ttu-id="b42a3-181">Checks whether a row with **disk.EnableUUID** exists.</span><span class="sxs-lookup"><span data-stu-id="b42a3-181">Checks whether a row with **disk.EnableUUID** exists.</span></span> <span data-ttu-id="b42a3-182">If it does and is set to **False** then set it to **True** (not case sensitive).</span><span class="sxs-lookup"><span data-stu-id="b42a3-182">If it does and is set to **False** then set it to **True** (not case sensitive).</span></span> <span data-ttu-id="b42a3-183">If exists and is set to true, click **Cancel** and test the SCSI command inside the guest operating system after it's booted up.</span><span class="sxs-lookup"><span data-stu-id="b42a3-183">If exists and is set to true, click **Cancel** and test the SCSI command inside the guest operating system after it's booted up.</span></span> <span data-ttu-id="b42a3-184">If doesn't exist click **Add Row**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-184">If doesn't exist click **Add Row**.</span></span>
5. <span data-ttu-id="b42a3-185">Add disk.EnableUUID in the **Name** column.</span><span class="sxs-lookup"><span data-stu-id="b42a3-185">Add disk.EnableUUID in the **Name** column.</span></span> <span data-ttu-id="b42a3-186">Set its value as TRUE.</span><span class="sxs-lookup"><span data-stu-id="b42a3-186">Set its value as TRUE.</span></span> <span data-ttu-id="b42a3-187">Don't add the above values along with double-quotes.</span><span class="sxs-lookup"><span data-stu-id="b42a3-187">Don't add the above values along with double-quotes.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-the-additional-packages"></a><span data-ttu-id="b42a3-188">Download and install the additional packages</span><span class="sxs-lookup"><span data-stu-id="b42a3-188">Download and install the additional packages</span></span>
<span data-ttu-id="b42a3-189">NOTE: Make sure the system has internet connectivity before downloading and installing the additional packages.</span><span class="sxs-lookup"><span data-stu-id="b42a3-189">NOTE: Make sure the system has internet connectivity before downloading and installing the additional packages.</span></span>

<span data-ttu-id="b42a3-190">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span><span class="sxs-lookup"><span data-stu-id="b42a3-190">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span></span>

<span data-ttu-id="b42a3-191">This command downloads these 15 packages from CentOS 6.6 repository and installs them:</span><span class="sxs-lookup"><span data-stu-id="b42a3-191">This command downloads these 15 packages from CentOS 6.6 repository and installs them:</span></span>

<span data-ttu-id="b42a3-192">bc-1.06.95-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-192">bc-1.06.95-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-193">busybox-1.15.1-20.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-193">busybox-1.15.1-20.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-194">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-194">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-195">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-195">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-196">lsscsi-0.23-2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-196">lsscsi-0.23-2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-197">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-197">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-198">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-198">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-199">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-199">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-200">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-200">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-201">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-201">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-202">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-202">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-203">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-203">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-204">rsync-3.0.6-12.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-204">rsync-3.0.6-12.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-205">snappy-1.1.0-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-205">snappy-1.1.0-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-206">wget-1.12-5.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-206">wget-1.12-5.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-207">If the source machine uses Reiser or XFS filesystem for the root or boot device, then following packages should be downloaded and installed on Linux master target prior to protection.</span><span class="sxs-lookup"><span data-stu-id="b42a3-207">If the source machine uses Reiser or XFS filesystem for the root or boot device, then following packages should be downloaded and installed on Linux master target prior to protection.</span></span>

<span data-ttu-id="b42a3-208">\# cd /usr/local</span><span class="sxs-lookup"><span data-stu-id="b42a3-208">\# cd /usr/local</span></span>

<span data-ttu-id="b42a3-209">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="b42a3-209">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="b42a3-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="b42a3-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="b42a3-211">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-211">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span></span>

<span data-ttu-id="b42a3-212">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="b42a3-212">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span></span>

<span data-ttu-id="b42a3-213">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b42a3-213">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span></span>

#### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="b42a3-214">Apply custom configuration changes</span><span class="sxs-lookup"><span data-stu-id="b42a3-214">Apply custom configuration changes</span></span>
<span data-ttu-id="b42a3-215">Before applying these changes make sure you've completed the previous section, then follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b42a3-215">Before applying these changes make sure you've completed the previous section, then follow these steps:</span></span>

1. <span data-ttu-id="b42a3-216">Copy the RHEL 6-64 Unified Agent binary to the newly created OS.</span><span class="sxs-lookup"><span data-stu-id="b42a3-216">Copy the RHEL 6-64 Unified Agent binary to the newly created OS.</span></span>
2. <span data-ttu-id="b42a3-217">Run this command to untar the binary: **tar -zxvf \<File name\>**</span><span class="sxs-lookup"><span data-stu-id="b42a3-217">Run this command to untar the binary: **tar -zxvf \<File name\>**</span></span>
3. <span data-ttu-id="b42a3-218">Run this command to give permissions: \# **chmod 755 ./ApplyCustomChanges.sh**</span><span class="sxs-lookup"><span data-stu-id="b42a3-218">Run this command to give permissions: \# **chmod 755 ./ApplyCustomChanges.sh**</span></span>
4. <span data-ttu-id="b42a3-219">Run the script: **\# ./ApplyCustomChanges.sh**. Run the script only once on the server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-219">Run the script: **\# ./ApplyCustomChanges.sh**. Run the script only once on the server.</span></span> <span data-ttu-id="b42a3-220">Restart the server after the script runs.</span><span class="sxs-lookup"><span data-stu-id="b42a3-220">Restart the server after the script runs.</span></span>

### <a name="install-the-linux-server"></a><span data-ttu-id="b42a3-221">Install the Linux server</span><span class="sxs-lookup"><span data-stu-id="b42a3-221">Install the Linux server</span></span>
1. <span data-ttu-id="b42a3-222">[Download](http://go.microsoft.com/fwlink/?LinkID=529757) the installation file.</span><span class="sxs-lookup"><span data-stu-id="b42a3-222">[Download](http://go.microsoft.com/fwlink/?LinkID=529757) the installation file.</span></span>
2. <span data-ttu-id="b42a3-223">Copy the file to the Linux Master Target virtual machine using an sftp client utility of your choice.</span><span class="sxs-lookup"><span data-stu-id="b42a3-223">Copy the file to the Linux Master Target virtual machine using an sftp client utility of your choice.</span></span> <span data-ttu-id="b42a3-224">Alternately you can log onto the Linux master target virtual machine and use wget to download the installation package from the provided link</span><span class="sxs-lookup"><span data-stu-id="b42a3-224">Alternately you can log onto the Linux master target virtual machine and use wget to download the installation package from the provided link</span></span>
3. <span data-ttu-id="b42a3-225">Log onto the Linux master target server virtual machine using an ssh client of your choice</span><span class="sxs-lookup"><span data-stu-id="b42a3-225">Log onto the Linux master target server virtual machine using an ssh client of your choice</span></span>
4. <span data-ttu-id="b42a3-226">If you're connected to the Azure network on which you deployed your Linux master target server through a VPN connection then use the internal IP address for the server that you can find in the virtual machine **Dashboard** tab, and port 22 to connect to the Linux master target Server using Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="b42a3-226">If you're connected to the Azure network on which you deployed your Linux master target server through a VPN connection then use the internal IP address for the server that you can find in the virtual machine **Dashboard** tab, and port 22 to connect to the Linux master target Server using Secure Shell.</span></span>
5. <span data-ttu-id="b42a3-227">If you're connecting to the Linux master target server over a public internet connection use the Linux master target server’s public virtual IP address (from the virtual machines **Dashboard** tab) and the public endpoint created for ssh to login to the Linux servder.</span><span class="sxs-lookup"><span data-stu-id="b42a3-227">If you're connecting to the Linux master target server over a public internet connection use the Linux master target server’s public virtual IP address (from the virtual machines **Dashboard** tab) and the public endpoint created for ssh to login to the Linux servder.</span></span>
6. <span data-ttu-id="b42a3-228">Extract the files from the gzipped Linux master target Server installer tar archive by running: *“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”* from the directory that contains the installer file.</span><span class="sxs-lookup"><span data-stu-id="b42a3-228">Extract the files from the gzipped Linux master target Server installer tar archive by running: *“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”* from the directory that contains the installer file.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image16.png)
7. <span data-ttu-id="b42a3-229">If you extracted the installer files to a different directory change to the directory to which the contents of the tar archive were extracted.</span><span class="sxs-lookup"><span data-stu-id="b42a3-229">If you extracted the installer files to a different directory change to the directory to which the contents of the tar archive were extracted.</span></span> <span data-ttu-id="b42a3-230">From this directory path run “sudo ./install.sh”.</span><span class="sxs-lookup"><span data-stu-id="b42a3-230">From this directory path run “sudo ./install.sh”.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image17.png)
8. <span data-ttu-id="b42a3-231">When prompted to choose a primary role select **2 (Master Target)**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-231">When prompted to choose a primary role select **2 (Master Target)**.</span></span> <span data-ttu-id="b42a3-232">Leave the other interactive install options at their default values.</span><span class="sxs-lookup"><span data-stu-id="b42a3-232">Leave the other interactive install options at their default values.</span></span>
9. <span data-ttu-id="b42a3-233">Wait for installation to continue and the Host Config Interface to appear.</span><span class="sxs-lookup"><span data-stu-id="b42a3-233">Wait for installation to continue and the Host Config Interface to appear.</span></span> <span data-ttu-id="b42a3-234">The Host Configuration utility for the Linux master sarget Server is a command line utility.</span><span class="sxs-lookup"><span data-stu-id="b42a3-234">The Host Configuration utility for the Linux master sarget Server is a command line utility.</span></span> <span data-ttu-id="b42a3-235">Don’t resize the ssh client utility window.</span><span class="sxs-lookup"><span data-stu-id="b42a3-235">Don’t resize the ssh client utility window.</span></span> <span data-ttu-id="b42a3-236">Use the arrow keys to select the **Global** option and press ENTER on your keyboard.</span><span class="sxs-lookup"><span data-stu-id="b42a3-236">Use the arrow keys to select the **Global** option and press ENTER on your keyboard.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image19.png)
10. <span data-ttu-id="b42a3-237">In the field **IP** enter the Internal IP address of the configuration server (you can find it in the **Dashboard** tab of the configuration server VM) and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="b42a3-237">In the field **IP** enter the Internal IP address of the configuration server (you can find it in the **Dashboard** tab of the configuration server VM) and press ENTER.</span></span> <span data-ttu-id="b42a3-238">In **Port** enter **22** and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="b42a3-238">In **Port** enter **22** and press ENTER.</span></span>
11. <span data-ttu-id="b42a3-239">Leave **Use HTTPS** as **Yes**, and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="b42a3-239">Leave **Use HTTPS** as **Yes**, and press ENTER.</span></span>
12. <span data-ttu-id="b42a3-240">Enter the Passphrase that was generated on the configuration server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-240">Enter the Passphrase that was generated on the configuration server.</span></span> <span data-ttu-id="b42a3-241">If you're using a PUTTY client from a Windows machine to ssh to the Linux virtual machine you can use Shift+Insert to paste the contents of the clipboard.</span><span class="sxs-lookup"><span data-stu-id="b42a3-241">If you're using a PUTTY client from a Windows machine to ssh to the Linux virtual machine you can use Shift+Insert to paste the contents of the clipboard.</span></span> <span data-ttu-id="b42a3-242">Copy the Passphrase to the local clipboard using Ctrl-C and use Shift+Insert to paste it.</span><span class="sxs-lookup"><span data-stu-id="b42a3-242">Copy the Passphrase to the local clipboard using Ctrl-C and use Shift+Insert to paste it.</span></span> <span data-ttu-id="b42a3-243">Press ENTER.</span><span class="sxs-lookup"><span data-stu-id="b42a3-243">Press ENTER.</span></span>
13. <span data-ttu-id="b42a3-244">Use the right arrow key to navigate to quit and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="b42a3-244">Use the right arrow key to navigate to quit and press ENTER.</span></span> <span data-ttu-id="b42a3-245">Wait for installation to complete.</span><span class="sxs-lookup"><span data-stu-id="b42a3-245">Wait for installation to complete.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image20.png)

<span data-ttu-id="b42a3-246">If for some reason you failed to register your Linux master target server to the configuration server you can do so again by running the host configuration utility from /usr/local/ASR/Vx/bin/hostconfigcli (you'll first need to set access permissions to this directory by running chmod as a super user).</span><span class="sxs-lookup"><span data-stu-id="b42a3-246">If for some reason you failed to register your Linux master target server to the configuration server you can do so again by running the host configuration utility from /usr/local/ASR/Vx/bin/hostconfigcli (you'll first need to set access permissions to this directory by running chmod as a super user).</span></span>

#### <a name="validate-master-target-registration"></a><span data-ttu-id="b42a3-247">Validate master target registration</span><span class="sxs-lookup"><span data-stu-id="b42a3-247">Validate master target registration</span></span>
<span data-ttu-id="b42a3-248">You can validate that the master target server was registered successfully to the configuration server in Azure Site Recovery vault > **Configuration Server** > **Server Details**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-248">You can validate that the master target server was registered successfully to the configuration server in Azure Site Recovery vault > **Configuration Server** > **Server Details**.</span></span>

> [!NOTE]
> After registering the master target server, if you receive configuration errors that the virtual machine might have been deleted from Azure or that endpoints are not properly configured, this is because although the master target configuration is detected by the Azure dndpoints when the master target is deployed in Azure, this isn't true for an on-premises master target server on-premises. This won't affect failback and you can ignore these errors.
>
>

## <a name="step-4-protect-the-virtual-machines-to-the-on-premises-site"></a><span data-ttu-id="b42a3-251">Step 4: Protect the virtual machines to the on-premises site</span><span class="sxs-lookup"><span data-stu-id="b42a3-251">Step 4: Protect the virtual machines to the on-premises site</span></span>
<span data-ttu-id="b42a3-252">You need to protect VMs to the on-premises site before you fail back.</span><span class="sxs-lookup"><span data-stu-id="b42a3-252">You need to protect VMs to the on-premises site before you fail back.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="b42a3-253">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b42a3-253">Before you begin</span></span>
<span data-ttu-id="b42a3-254">When a VM is failed over to Azure, it adds an extra temp drive for page file.</span><span class="sxs-lookup"><span data-stu-id="b42a3-254">When a VM is failed over to Azure, it adds an extra temp drive for page file.</span></span> <span data-ttu-id="b42a3-255">This is an extra drive that is typically not required by your failed over VM since it might already have a drive dedicated for the page file.</span><span class="sxs-lookup"><span data-stu-id="b42a3-255">This is an extra drive that is typically not required by your failed over VM since it might already have a drive dedicated for the page file.</span></span> <span data-ttu-id="b42a3-256">Before you begin reverse protection of the virtual machines, you need to ensure that this drive is taken offline so that it does not get protected.</span><span class="sxs-lookup"><span data-stu-id="b42a3-256">Before you begin reverse protection of the virtual machines, you need to ensure that this drive is taken offline so that it does not get protected.</span></span> <span data-ttu-id="b42a3-257">Do this as follows:</span><span class="sxs-lookup"><span data-stu-id="b42a3-257">Do this as follows:</span></span>

1. <span data-ttu-id="b42a3-258">Open Computer Management and select Storage Management so that it lists the disks online and attached to the machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-258">Open Computer Management and select Storage Management so that it lists the disks online and attached to the machine.</span></span>
2. <span data-ttu-id="b42a3-259">Select the temporary disk attached to the machine and choose to bring it offline.</span><span class="sxs-lookup"><span data-stu-id="b42a3-259">Select the temporary disk attached to the machine and choose to bring it offline.</span></span>

### <a name="protect-the-vms"></a><span data-ttu-id="b42a3-260">Protect the VMs</span><span class="sxs-lookup"><span data-stu-id="b42a3-260">Protect the VMs</span></span>
1. <span data-ttu-id="b42a3-261">In the Azure portal, check the states of the virtual machine to ensure that they're failed over.</span><span class="sxs-lookup"><span data-stu-id="b42a3-261">In the Azure portal, check the states of the virtual machine to ensure that they're failed over.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image21.png)
2. <span data-ttu-id="b42a3-262">Launch vContinuum on your machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-262">Launch vContinuum on your machine.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image8.png)
3. <span data-ttu-id="b42a3-263">Click **New Protection** and select the operation system type, the</span><span class="sxs-lookup"><span data-stu-id="b42a3-263">Click **New Protection** and select the operation system type, the</span></span>
4. <span data-ttu-id="b42a3-264">In the new window that open select the **OS type** > **Get Details** for the VMs you want to fail back.</span><span class="sxs-lookup"><span data-stu-id="b42a3-264">In the new window that open select the **OS type** > **Get Details** for the VMs you want to fail back.</span></span> <span data-ttu-id="b42a3-265">In **Primary server details**, identify and select the virtual machines that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="b42a3-265">In **Primary server details**, identify and select the virtual machines that you want to protect.</span></span> <span data-ttu-id="b42a3-266">VMs are listed under the vCenter host name that they were on before failover.</span><span class="sxs-lookup"><span data-stu-id="b42a3-266">VMs are listed under the vCenter host name that they were on before failover.</span></span>
5. <span data-ttu-id="b42a3-267">When you select a virtual machine to protect (and it has already failed over to Azure) a pop-up window provides two entries for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-267">When you select a virtual machine to protect (and it has already failed over to Azure) a pop-up window provides two entries for the virtual machine.</span></span> <span data-ttu-id="b42a3-268">This is because the configuration server detects two instances of the virtual machines registered to it.</span><span class="sxs-lookup"><span data-stu-id="b42a3-268">This is because the configuration server detects two instances of the virtual machines registered to it.</span></span> <span data-ttu-id="b42a3-269">You need to remove the entry for the on-premises VM so that you can protect the correct VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-269">You need to remove the entry for the on-premises VM so that you can protect the correct VM.</span></span> <span data-ttu-id="b42a3-270">To identify the correct Azure VM entry here, you can log into the Azure VM and go to C:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc. In the file drscout.conf , identify the host ID.</span><span class="sxs-lookup"><span data-stu-id="b42a3-270">To identify the correct Azure VM entry here, you can log into the Azure VM and go to C:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc. In the file drscout.conf , identify the host ID.</span></span> <span data-ttu-id="b42a3-271">In the vContinuum dialog, keep the entry for which you found the host ID on  the VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-271">In the vContinuum dialog, keep the entry for which you found the host ID on  the VM.</span></span> <span data-ttu-id="b42a3-272">Delete all other entries.</span><span class="sxs-lookup"><span data-stu-id="b42a3-272">Delete all other entries.</span></span> <span data-ttu-id="b42a3-273">To select the correct VM you can refer to its IP address.</span><span class="sxs-lookup"><span data-stu-id="b42a3-273">To select the correct VM you can refer to its IP address.</span></span> <span data-ttu-id="b42a3-274">The IP address range on-premises will be the on-premises VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-274">The IP address range on-premises will be the on-premises VM.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image23.png)
6. <span data-ttu-id="b42a3-275">On the vCenter server stop the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-275">On the vCenter server stop the virtual machine.</span></span> <span data-ttu-id="b42a3-276">You can also delete the VMs on-premises.</span><span class="sxs-lookup"><span data-stu-id="b42a3-276">You can also delete the VMs on-premises.</span></span>
7. <span data-ttu-id="b42a3-277">Then specify the on-premises MT server to which you want to protect the VMs.</span><span class="sxs-lookup"><span data-stu-id="b42a3-277">Then specify the on-premises MT server to which you want to protect the VMs.</span></span> <span data-ttu-id="b42a3-278">To do this, connect to the vCenter server to which you want to fail back.</span><span class="sxs-lookup"><span data-stu-id="b42a3-278">To do this, connect to the vCenter server to which you want to fail back.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image24.png)
8. <span data-ttu-id="b42a3-279">Select the master target server based on the host to which you want to recover the VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-279">Select the master target server based on the host to which you want to recover the VM.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image24.png)
9. <span data-ttu-id="b42a3-280">Provide the replication option for each of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b42a3-280">Provide the replication option for each of the virtual machines.</span></span> <span data-ttu-id="b42a3-281">To do this you need to select the recovery side datastore to which the VMs will be recovered.</span><span class="sxs-lookup"><span data-stu-id="b42a3-281">To do this you need to select the recovery side datastore to which the VMs will be recovered.</span></span> <span data-ttu-id="b42a3-282">The table summarizes the different options you need to provide for each VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-282">The table summarizes the different options you need to provide for each VM.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image25.png)

   | <span data-ttu-id="b42a3-283">**Option**</span><span class="sxs-lookup"><span data-stu-id="b42a3-283">**Option**</span></span> | <span data-ttu-id="b42a3-284">**Option recommended value**</span><span class="sxs-lookup"><span data-stu-id="b42a3-284">**Option recommended value**</span></span> |
   | --- | --- |
   |  <span data-ttu-id="b42a3-285">Process server IP address</span><span class="sxs-lookup"><span data-stu-id="b42a3-285">Process server IP address</span></span> |<span data-ttu-id="b42a3-286">Select the process server deployed in Azure</span><span class="sxs-lookup"><span data-stu-id="b42a3-286">Select the process server deployed in Azure</span></span> |
   |  <span data-ttu-id="b42a3-287">Retention size in MB</span><span class="sxs-lookup"><span data-stu-id="b42a3-287">Retention size in MB</span></span> | |
   |  <span data-ttu-id="b42a3-288">Retention value</span><span class="sxs-lookup"><span data-stu-id="b42a3-288">Retention value</span></span> |<span data-ttu-id="b42a3-289">1</span><span class="sxs-lookup"><span data-stu-id="b42a3-289">1</span></span> |
   |  <span data-ttu-id="b42a3-290">Days/Hours</span><span class="sxs-lookup"><span data-stu-id="b42a3-290">Days/Hours</span></span> |<span data-ttu-id="b42a3-291">Days</span><span class="sxs-lookup"><span data-stu-id="b42a3-291">Days</span></span> |
   |  <span data-ttu-id="b42a3-292">Consistency interval</span><span class="sxs-lookup"><span data-stu-id="b42a3-292">Consistency interval</span></span> |<span data-ttu-id="b42a3-293">1</span><span class="sxs-lookup"><span data-stu-id="b42a3-293">1</span></span> |
   |  <span data-ttu-id="b42a3-294">Select target datastore</span><span class="sxs-lookup"><span data-stu-id="b42a3-294">Select target datastore</span></span> |<span data-ttu-id="b42a3-295">The datastore available on the recovery site.</span><span class="sxs-lookup"><span data-stu-id="b42a3-295">The datastore available on the recovery site.</span></span> <span data-ttu-id="b42a3-296">The data store should have enough space, and be available to the ESX host on which you want to restore the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-296">The data store should have enough space, and be available to the ESX host on which you want to restore the virtual machine.</span></span> |
10. <span data-ttu-id="b42a3-297">Configure the properties that the virtual machine will acquire after failover to on-premises site.</span><span class="sxs-lookup"><span data-stu-id="b42a3-297">Configure the properties that the virtual machine will acquire after failover to on-premises site.</span></span> <span data-ttu-id="b42a3-298">The properties are summarized in the following table.</span><span class="sxs-lookup"><span data-stu-id="b42a3-298">The properties are summarized in the following table.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image26.png)

    | <span data-ttu-id="b42a3-299">**Property**</span><span class="sxs-lookup"><span data-stu-id="b42a3-299">**Property**</span></span> | <span data-ttu-id="b42a3-300">**Details**</span><span class="sxs-lookup"><span data-stu-id="b42a3-300">**Details**</span></span> |
    | --- | --- |
    | <span data-ttu-id="b42a3-301">Network configuration</span><span class="sxs-lookup"><span data-stu-id="b42a3-301">Network configuration</span></span> |<span data-ttu-id="b42a3-302">For each network adapter detected, select it and click **Change** to configure the failback IP address for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-302">For each network adapter detected, select it and click **Change** to configure the failback IP address for the virtual machine.</span></span> |
    | <span data-ttu-id="b42a3-303">Hardware Configuration</span><span class="sxs-lookup"><span data-stu-id="b42a3-303">Hardware Configuration</span></span> |<span data-ttu-id="b42a3-304">Specify the CPU and the memory for the VM.</span><span class="sxs-lookup"><span data-stu-id="b42a3-304">Specify the CPU and the memory for the VM.</span></span> <span data-ttu-id="b42a3-305">Settings can be applied to all the VMs you are trying to protect.</span><span class="sxs-lookup"><span data-stu-id="b42a3-305">Settings can be applied to all the VMs you are trying to protect.</span></span> <span data-ttu-id="b42a3-306">To identify the correct values for the CPU and memory, you can refer to the IAAS VMs role size and see the number of cores and memory assigned.</span><span class="sxs-lookup"><span data-stu-id="b42a3-306">To identify the correct values for the CPU and memory, you can refer to the IAAS VMs role size and see the number of cores and memory assigned.</span></span> |
    | <span data-ttu-id="b42a3-307">Display name</span><span class="sxs-lookup"><span data-stu-id="b42a3-307">Display name</span></span> |<span data-ttu-id="b42a3-308">After failback to on-premises, you can rename the virtual machines as they'll appear in the vCenter inventory.</span><span class="sxs-lookup"><span data-stu-id="b42a3-308">After failback to on-premises, you can rename the virtual machines as they'll appear in the vCenter inventory.</span></span> <span data-ttu-id="b42a3-309">The default name is the virtual machine computer host name.</span><span class="sxs-lookup"><span data-stu-id="b42a3-309">The default name is the virtual machine computer host name.</span></span> <span data-ttu-id="b42a3-310">To identify the VM name, you can refer to the VM list in the Protection group.</span><span class="sxs-lookup"><span data-stu-id="b42a3-310">To identify the VM name, you can refer to the VM list in the Protection group.</span></span> |
    | <span data-ttu-id="b42a3-311">NAT Configuration</span><span class="sxs-lookup"><span data-stu-id="b42a3-311">NAT Configuration</span></span> |<span data-ttu-id="b42a3-312">Discussed in detail below</span><span class="sxs-lookup"><span data-stu-id="b42a3-312">Discussed in detail below</span></span> |

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a><span data-ttu-id="b42a3-313">Configure NAT settings</span><span class="sxs-lookup"><span data-stu-id="b42a3-313">Configure NAT settings</span></span>
1. <span data-ttu-id="b42a3-314">To enable protection of the virtual machines, two communication channels need to be established.</span><span class="sxs-lookup"><span data-stu-id="b42a3-314">To enable protection of the virtual machines, two communication channels need to be established.</span></span> <span data-ttu-id="b42a3-315">The first channel is between the virtual machine and the process server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-315">The first channel is between the virtual machine and the process server.</span></span> <span data-ttu-id="b42a3-316">This channel collects the data from the VM and sends it to the process server which then sends the data to the master target server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-316">This channel collects the data from the VM and sends it to the process server which then sends the data to the master target server.</span></span> <span data-ttu-id="b42a3-317">If the process server and the virtual machine to be protected are on the same Azure virtual network then you don't need to use NAT settings.</span><span class="sxs-lookup"><span data-stu-id="b42a3-317">If the process server and the virtual machine to be protected are on the same Azure virtual network then you don't need to use NAT settings.</span></span> <span data-ttu-id="b42a3-318">Otherwise specify NAT settings.</span><span class="sxs-lookup"><span data-stu-id="b42a3-318">Otherwise specify NAT settings.</span></span> <span data-ttu-id="b42a3-319">View the public IP address of the process server in Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-319">View the public IP address of the process server in Azure.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image28.png)
2. <span data-ttu-id="b42a3-320">The second channel is between the process server and the master target server.</span><span class="sxs-lookup"><span data-stu-id="b42a3-320">The second channel is between the process server and the master target server.</span></span> <span data-ttu-id="b42a3-321">The option to use NAT or not depends on whether you are using a VPN based connection or communicating over the internet.</span><span class="sxs-lookup"><span data-stu-id="b42a3-321">The option to use NAT or not depends on whether you are using a VPN based connection or communicating over the internet.</span></span> <span data-ttu-id="b42a3-322">Don't select NAt if you're using VPN, but only if you're using an internet connection.</span><span class="sxs-lookup"><span data-stu-id="b42a3-322">Don't select NAt if you're using VPN, but only if you're using an internet connection.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image30.png)
3. <span data-ttu-id="b42a3-323">If you haven't deleted the on-premises virtual machines as specified and if the datastore you are failing back to still contains the old VMDK’s then you will need to ensure that the failback VM gets created in a new place.</span><span class="sxs-lookup"><span data-stu-id="b42a3-323">If you haven't deleted the on-premises virtual machines as specified and if the datastore you are failing back to still contains the old VMDK’s then you will need to ensure that the failback VM gets created in a new place.</span></span> <span data-ttu-id="b42a3-324">To do this select the **Advanced** settings and specify an alternate Folder to restore to in **Folder Name Settings**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-324">To do this select the **Advanced** settings and specify an alternate Folder to restore to in **Folder Name Settings**.</span></span> <span data-ttu-id="b42a3-325">Leave the other options with their default settings.</span><span class="sxs-lookup"><span data-stu-id="b42a3-325">Leave the other options with their default settings.</span></span> <span data-ttu-id="b42a3-326">Apply the folder name settings to all the servers.</span><span class="sxs-lookup"><span data-stu-id="b42a3-326">Apply the folder name settings to all the servers.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image31.png)
4. <span data-ttu-id="b42a3-327">Run a Readiness Check to ensure that the virtual machines are ready to be protected back to on-premises.</span><span class="sxs-lookup"><span data-stu-id="b42a3-327">Run a Readiness Check to ensure that the virtual machines are ready to be protected back to on-premises.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image32.png)
5. <span data-ttu-id="b42a3-328">Wait for it to complete.</span><span class="sxs-lookup"><span data-stu-id="b42a3-328">Wait for it to complete.</span></span> <span data-ttu-id="b42a3-329">If it's successfully on all VMs you can specify a name for the protection plan.</span><span class="sxs-lookup"><span data-stu-id="b42a3-329">If it's successfully on all VMs you can specify a name for the protection plan.</span></span> <span data-ttu-id="b42a3-330">Then click **Protect** to begin.</span><span class="sxs-lookup"><span data-stu-id="b42a3-330">Then click **Protect** to begin.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image33.png)
6. <span data-ttu-id="b42a3-331">You can monitor progress in vContinuum.</span><span class="sxs-lookup"><span data-stu-id="b42a3-331">You can monitor progress in vContinuum.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image34.png)
7. <span data-ttu-id="b42a3-332">After the step **Activating Protection Plan** finishes you can monitor VM protection in the Site Recovery portal.</span><span class="sxs-lookup"><span data-stu-id="b42a3-332">After the step **Activating Protection Plan** finishes you can monitor VM protection in the Site Recovery portal.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image35.png)
8. <span data-ttu-id="b42a3-333">You can see the exact status clicking on the VM and monitoring its progress.</span><span class="sxs-lookup"><span data-stu-id="b42a3-333">You can see the exact status clicking on the VM and monitoring its progress.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-the-failback-plan"></a><span data-ttu-id="b42a3-334">Prepare the failback plan</span><span class="sxs-lookup"><span data-stu-id="b42a3-334">Prepare the failback plan</span></span>
<span data-ttu-id="b42a3-335">You can prepare a failback plan using vContinuum so that the application can be failed back to the on-premises site at any time.</span><span class="sxs-lookup"><span data-stu-id="b42a3-335">You can prepare a failback plan using vContinuum so that the application can be failed back to the on-premises site at any time.</span></span> <span data-ttu-id="b42a3-336">These recovery plans are very similar to the recovery plans in Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b42a3-336">These recovery plans are very similar to the recovery plans in Site Recovery.</span></span>

1. <span data-ttu-id="b42a3-337">Launch vContinuum and select **Manage plans** > **Recover.**</span><span class="sxs-lookup"><span data-stu-id="b42a3-337">Launch vContinuum and select **Manage plans** > **Recover.**</span></span> <span data-ttu-id="b42a3-338">You can see of list of all the plans that have been used to fail over VMs.</span><span class="sxs-lookup"><span data-stu-id="b42a3-338">You can see of list of all the plans that have been used to fail over VMs.</span></span> <span data-ttu-id="b42a3-339">You can use the same plans to recover.</span><span class="sxs-lookup"><span data-stu-id="b42a3-339">You can use the same plans to recover.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image37.png)
2. <span data-ttu-id="b42a3-340">Select the protection plan and all of the VMs you want to recover in it.</span><span class="sxs-lookup"><span data-stu-id="b42a3-340">Select the protection plan and all of the VMs you want to recover in it.</span></span> <span data-ttu-id="b42a3-341">When you select each VM you can see more details including the target ESX server and the source VM disk.</span><span class="sxs-lookup"><span data-stu-id="b42a3-341">When you select each VM you can see more details including the target ESX server and the source VM disk.</span></span> <span data-ttu-id="b42a3-342">Click **Next** to begin the Recover Wizard and select the VMs you want to recover.</span><span class="sxs-lookup"><span data-stu-id="b42a3-342">Click **Next** to begin the Recover Wizard and select the VMs you want to recover.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image38.png)
3. <span data-ttu-id="b42a3-343">You can recover based on multiple options but we recommend you use **Latest Tag** and select **Apply for All VMs** to ensure that the latest data from the virtual machine will be used.</span><span class="sxs-lookup"><span data-stu-id="b42a3-343">You can recover based on multiple options but we recommend you use **Latest Tag** and select **Apply for All VMs** to ensure that the latest data from the virtual machine will be used.</span></span>
4. <span data-ttu-id="b42a3-344">Run the **Readiness Check.**</span><span class="sxs-lookup"><span data-stu-id="b42a3-344">Run the **Readiness Check.**</span></span> <span data-ttu-id="b42a3-345">This will check if the right parameters are configured to enable VM recovery.</span><span class="sxs-lookup"><span data-stu-id="b42a3-345">This will check if the right parameters are configured to enable VM recovery.</span></span> <span data-ttu-id="b42a3-346">Click **Next** if all the checks are successful.</span><span class="sxs-lookup"><span data-stu-id="b42a3-346">Click **Next** if all the checks are successful.</span></span> <span data-ttu-id="b42a3-347">If not check the log and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="b42a3-347">If not check the log and resolve the errors.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image39.png)
5. <span data-ttu-id="b42a3-348">In **VM Configuration** ensure that the recovery settings are correctly set.</span><span class="sxs-lookup"><span data-stu-id="b42a3-348">In **VM Configuration** ensure that the recovery settings are correctly set.</span></span> <span data-ttu-id="b42a3-349">You can change the VM settings if you need to.</span><span class="sxs-lookup"><span data-stu-id="b42a3-349">You can change the VM settings if you need to.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image40.png)
6. <span data-ttu-id="b42a3-350">Review the list of virtual machines that will be recovered and specify a recovery order.</span><span class="sxs-lookup"><span data-stu-id="b42a3-350">Review the list of virtual machines that will be recovered and specify a recovery order.</span></span> <span data-ttu-id="b42a3-351">Note that VMs are listed using the computer host name.</span><span class="sxs-lookup"><span data-stu-id="b42a3-351">Note that VMs are listed using the computer host name.</span></span> <span data-ttu-id="b42a3-352">It might be difficult to map the computer host name to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b42a3-352">It might be difficult to map the computer host name to the virtual machine.</span></span>
   <span data-ttu-id="b42a3-353">To map the names, go to the virtual machines **Dashboard** in Azure and check the VM host name.</span><span class="sxs-lookup"><span data-stu-id="b42a3-353">To map the names, go to the virtual machines **Dashboard** in Azure and check the VM host name.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image41.png)
7. <span data-ttu-id="b42a3-354">Specify a plan name and select **Recover later**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-354">Specify a plan name and select **Recover later**.</span></span> <span data-ttu-id="b42a3-355">We recommend to recover later since the initial protection might not be complete.</span><span class="sxs-lookup"><span data-stu-id="b42a3-355">We recommend to recover later since the initial protection might not be complete.</span></span>
8. <span data-ttu-id="b42a3-356">Click on **Recover** to save the plan or trigger the recovery if you've selected to recover now and not later.</span><span class="sxs-lookup"><span data-stu-id="b42a3-356">Click on **Recover** to save the plan or trigger the recovery if you've selected to recover now and not later.</span></span> <span data-ttu-id="b42a3-357">You can check the recovery status to see if the plan's been saved.</span><span class="sxs-lookup"><span data-stu-id="b42a3-357">You can check the recovery status to see if the plan's been saved.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a><span data-ttu-id="b42a3-358">Recover virtual machines</span><span class="sxs-lookup"><span data-stu-id="b42a3-358">Recover virtual machines</span></span>
<span data-ttu-id="b42a3-359">After the plan's been created, you can recover the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b42a3-359">After the plan's been created, you can recover the virtual machines.</span></span> <span data-ttu-id="b42a3-360">Before you do check that the virtual machines have completed synchronization.</span><span class="sxs-lookup"><span data-stu-id="b42a3-360">Before you do check that the virtual machines have completed synchronization.</span></span> <span data-ttu-id="b42a3-361">If replication status shows OK then the protection is completed and the RPO threshold has been met.</span><span class="sxs-lookup"><span data-stu-id="b42a3-361">If replication status shows OK then the protection is completed and the RPO threshold has been met.</span></span> <span data-ttu-id="b42a3-362">You can verify health in the VM properties.</span><span class="sxs-lookup"><span data-stu-id="b42a3-362">You can verify health in the VM properties.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image44.png)

<span data-ttu-id="b42a3-363">Turn off the Azure virtual machines before you initiate the recovery.</span><span class="sxs-lookup"><span data-stu-id="b42a3-363">Turn off the Azure virtual machines before you initiate the recovery.</span></span> <span data-ttu-id="b42a3-364">This ensures there's no split brain and that users will only access one copy of the application.</span><span class="sxs-lookup"><span data-stu-id="b42a3-364">This ensures there's no split brain and that users will only access one copy of the application.</span></span>

1. <span data-ttu-id="b42a3-365">Start the saved plan.</span><span class="sxs-lookup"><span data-stu-id="b42a3-365">Start the saved plan.</span></span> <span data-ttu-id="b42a3-366">In vContinuum select **Monitor** the plans.</span><span class="sxs-lookup"><span data-stu-id="b42a3-366">In vContinuum select **Monitor** the plans.</span></span> <span data-ttu-id="b42a3-367">This lists all the plans that have been run.</span><span class="sxs-lookup"><span data-stu-id="b42a3-367">This lists all the plans that have been run.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image45.png)
2. <span data-ttu-id="b42a3-368">Select the plan in **Recovery** and click **Start**.</span><span class="sxs-lookup"><span data-stu-id="b42a3-368">Select the plan in **Recovery** and click **Start**.</span></span> <span data-ttu-id="b42a3-369">You can monitor recovery.</span><span class="sxs-lookup"><span data-stu-id="b42a3-369">You can monitor recovery.</span></span> <span data-ttu-id="b42a3-370">After VMs have been turned on you can connect to them in vCenter.</span><span class="sxs-lookup"><span data-stu-id="b42a3-370">After VMs have been turned on you can connect to them in vCenter.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-to-azure-again-after-failback"></a><span data-ttu-id="b42a3-371">Protect to Azure again after failback</span><span class="sxs-lookup"><span data-stu-id="b42a3-371">Protect to Azure again after failback</span></span>
<span data-ttu-id="b42a3-372">After failback has been completed you'll probably want to protect the virtual machines again.</span><span class="sxs-lookup"><span data-stu-id="b42a3-372">After failback has been completed you'll probably want to protect the virtual machines again.</span></span> <span data-ttu-id="b42a3-373">Do this as follows:</span><span class="sxs-lookup"><span data-stu-id="b42a3-373">Do this as follows:</span></span>

1. <span data-ttu-id="b42a3-374">Check that the virtual machines on-premises are working and that applications are reachable.</span><span class="sxs-lookup"><span data-stu-id="b42a3-374">Check that the virtual machines on-premises are working and that applications are reachable.</span></span>
2. <span data-ttu-id="b42a3-375">In the Azure Site Recovery portal, select the virtual machines and delete them.</span><span class="sxs-lookup"><span data-stu-id="b42a3-375">In the Azure Site Recovery portal, select the virtual machines and delete them.</span></span> <span data-ttu-id="b42a3-376">Select to disable the protection of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b42a3-376">Select to disable the protection of the virtual machines.</span></span> <span data-ttu-id="b42a3-377">This ensures that the VMs are no more protected.</span><span class="sxs-lookup"><span data-stu-id="b42a3-377">This ensures that the VMs are no more protected.</span></span>
3. <span data-ttu-id="b42a3-378">In Azure delete the failed over Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="b42a3-378">In Azure delete the failed over Azure virtual machines</span></span>
4. <span data-ttu-id="b42a3-379">Delete the old virtual machine on vSpehere.</span><span class="sxs-lookup"><span data-stu-id="b42a3-379">Delete the old virtual machine on vSpehere.</span></span> <span data-ttu-id="b42a3-380">These are the VMs that you previously failed over to Azure.</span><span class="sxs-lookup"><span data-stu-id="b42a3-380">These are the VMs that you previously failed over to Azure.</span></span>
5. <span data-ttu-id="b42a3-381">In the Site Recovery portal protect the VMs that recently failed over.</span><span class="sxs-lookup"><span data-stu-id="b42a3-381">In the Site Recovery portal protect the VMs that recently failed over.</span></span> <span data-ttu-id="b42a3-382">After they're protected  you can add them to a recovery plan.</span><span class="sxs-lookup"><span data-stu-id="b42a3-382">After they're protected  you can add them to a recovery plan.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b42a3-383">Next steps</span><span class="sxs-lookup"><span data-stu-id="b42a3-383">Next steps</span></span>
* <span data-ttu-id="b42a3-384">[Read about](site-recovery-vmware-to-azure-classic.md) replicating VMware virtual machines and physical servers to Azure using the enhanced deployment.</span><span class="sxs-lookup"><span data-stu-id="b42a3-384">[Read about](site-recovery-vmware-to-azure-classic.md) replicating VMware virtual machines and physical servers to Azure using the enhanced deployment.</span></span>
















































