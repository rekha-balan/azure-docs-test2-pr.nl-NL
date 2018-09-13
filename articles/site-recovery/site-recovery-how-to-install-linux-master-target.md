---
title: How to install a Linux master target server for failover from Azure to on-premises| Microsoft Docs
description: Before reprotecting a Linux virtual machine, you need a Linux Master target server. Learn how to install one.
services: site-recovery
documentationcenter: ''
author: ruturaj
manager: gauravd
editor: ''
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: ''
ms.date: 02/13/2017
ms.author: ruturajd
ms.openlocfilehash: 3e31d3702e6205e97ba74bbe7bbfda937f5b2081
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551121"
---
# <a name="how-to-install-a-linux-master-target-server"></a><span data-ttu-id="05e0f-104">How to install a Linux master target server</span><span class="sxs-lookup"><span data-stu-id="05e0f-104">How to install a Linux master target server</span></span>
<span data-ttu-id="05e0f-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span><span class="sxs-lookup"><span data-stu-id="05e0f-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="05e0f-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span><span class="sxs-lookup"><span data-stu-id="05e0f-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="05e0f-107">For this process, you need an on-premises master target server to receive the traffic.</span><span class="sxs-lookup"><span data-stu-id="05e0f-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> <span data-ttu-id="05e0f-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="05e0f-109">For a Linux virtual machine, you need a Linux master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="05e0f-110">Read the following steps to learn how to create and install a Linux master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

## <a name="overview"></a><span data-ttu-id="05e0f-111">Overview</span><span class="sxs-lookup"><span data-stu-id="05e0f-111">Overview</span></span>
<span data-ttu-id="05e0f-112">This article provides information and instructions to install a Linux master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-112">This article provides information and instructions to install a Linux master target.</span></span>

<span data-ttu-id="05e0f-113">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="05e0f-113">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05e0f-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05e0f-114">Prerequisites</span></span>

* <span data-ttu-id="05e0f-115">To correctly choose the host on which you need to deploy the master target, determine whether the failback is going to be to an existing on-premises virtual machine or to a new virtual machine because the on-premises virtual machine got deleted.</span><span class="sxs-lookup"><span data-stu-id="05e0f-115">To correctly choose the host on which you need to deploy the master target, determine whether the failback is going to be to an existing on-premises virtual machine or to a new virtual machine because the on-premises virtual machine got deleted.</span></span>
    * <span data-ttu-id="05e0f-116">For an existing virtual machine, the master target's host should have access to the virtual machine's datastores.</span><span class="sxs-lookup"><span data-stu-id="05e0f-116">For an existing virtual machine, the master target's host should have access to the virtual machine's datastores.</span></span>
    * <span data-ttu-id="05e0f-117">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-117">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="05e0f-118">You can choose any ESXi host to install the master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-118">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="05e0f-119">The master target should be on a network that can communicate with the process server and the configuration server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-119">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="05e0f-120">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-120">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="05e0f-121">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span><span class="sxs-lookup"><span data-stu-id="05e0f-121">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="05e0f-122">The master target can only be a VMware virtual machine and not a physical server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-122">The master target can only be a VMware virtual machine and not a physical server.</span></span>
* <span data-ttu-id="05e0f-123">The master target needs to faollow the following sizing guideline</span><span class="sxs-lookup"><span data-stu-id="05e0f-123">The master target needs to faollow the following sizing guideline</span></span>
    * <span data-ttu-id="05e0f-124">RAM - 6GB or more</span><span class="sxs-lookup"><span data-stu-id="05e0f-124">RAM - 6GB or more</span></span>
    * <span data-ttu-id="05e0f-125">OS Disk size - 50GB or more (to install CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="05e0f-125">OS Disk size - 50GB or more (to install CentOS6.6)</span></span>
    * <span data-ttu-id="05e0f-126">Additional disk size for retention drive - 1TB</span><span class="sxs-lookup"><span data-stu-id="05e0f-126">Additional disk size for retention drive - 1TB</span></span>
    * <span data-ttu-id="05e0f-127">CPU cores - 4 Cores or more</span><span class="sxs-lookup"><span data-stu-id="05e0f-127">CPU cores - 4 Cores or more</span></span>




## <a name="steps-to-deploy-the-master-target-server"></a><span data-ttu-id="05e0f-128">Steps to deploy the master target server</span><span class="sxs-lookup"><span data-stu-id="05e0f-128">Steps to deploy the master target server</span></span>

### <a name="install-centos-66-minimal"></a><span data-ttu-id="05e0f-129">Install CentOS 6.6 minimal</span><span class="sxs-lookup"><span data-stu-id="05e0f-129">Install CentOS 6.6 minimal</span></span>

<span data-ttu-id="05e0f-130">Use the following steps to install the 64-bit CentOS 6.6 operating system:</span><span class="sxs-lookup"><span data-stu-id="05e0f-130">Use the following steps to install the 64-bit CentOS 6.6 operating system:</span></span>

1. <span data-ttu-id="05e0f-131">From following links, choose the nearest mirror to download a CentOS 6.6 minimal 64-bit ISO.</span><span class="sxs-lookup"><span data-stu-id="05e0f-131">From following links, choose the nearest mirror to download a CentOS 6.6 minimal 64-bit ISO.</span></span>

    <http://archive.kernel.org/centos-vault/6.6/isos/x86_64/CentOS-6.6-x86_64-minimal.iso>

    <http://mirror.symnds.com/distributions/CentOS-vault/6.6/isos/x86_64/CentOS-6.6-x86_64-minimal.iso>

    <http://bay.uchicago.edu/centos-vault/6.6/isos/x86_64/CentOS-6.6-x86_64-minimal.iso>

    <http://mirror.nsc.liu.se/centos-store/6.6/isos/x86_64/CentOS-6.6-x86_64-minimal.iso>

    <span data-ttu-id="05e0f-132">Put CentOS 6.6 minimal 64-bit ISO in a DVD drive, and boot the system.</span><span class="sxs-lookup"><span data-stu-id="05e0f-132">Put CentOS 6.6 minimal 64-bit ISO in a DVD drive, and boot the system.</span></span>

    ![Welcome to CentoOS 6.6 dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image1.png)

2. <span data-ttu-id="05e0f-134">Click **Skip** to ignore the media testing process.</span><span class="sxs-lookup"><span data-stu-id="05e0f-134">Click **Skip** to ignore the media testing process.</span></span>

    ![Select Skip to ignore the media testing process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image2.png)

3. <span data-ttu-id="05e0f-136">On the installation welcome screen, click the **Next** button.</span><span class="sxs-lookup"><span data-stu-id="05e0f-136">On the installation welcome screen, click the **Next** button.</span></span>

    ![The Next button on the installation welcome screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image3.png)

4. <span data-ttu-id="05e0f-138">Select **English** as your preferred language, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-138">Select **English** as your preferred language, and then click **Next**.</span></span>

    ![Select a lanaguage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image4.png)

5. <span data-ttu-id="05e0f-140">Select **US English** as a keyboard layout, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-140">Select **US English** as a keyboard layout, and then click **Next**.</span></span>

    ![Select the English keyboard layout](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image5.png)

6. <span data-ttu-id="05e0f-142">Select **Basic storage Devices**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-142">Select **Basic storage Devices**, and then click **Next**.</span></span>

    ![Select a storage device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image6.png)

7. <span data-ttu-id="05e0f-144">The warning message that appears indicates that the existing data on the hard drive will be deleted.</span><span class="sxs-lookup"><span data-stu-id="05e0f-144">The warning message that appears indicates that the existing data on the hard drive will be deleted.</span></span> <span data-ttu-id="05e0f-145">Make sure the hard drive does not have any important data, and then click **Yes, discard any data**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-145">Make sure the hard drive does not have any important data, and then click **Yes, discard any data**.</span></span>

    ![Warning about deletion of data if you proceed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image7.png)

8. <span data-ttu-id="05e0f-147">Enter the hostname for your server in the **Hostname** box, and then click **Configure Network**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-147">Enter the hostname for your server in the **Hostname** box, and then click **Configure Network**.</span></span> <span data-ttu-id="05e0f-148">In the **Network Connection** dialog box, select your network interface, and then click the **Edit** button to configure IPV4Settings.</span><span class="sxs-lookup"><span data-stu-id="05e0f-148">In the **Network Connection** dialog box, select your network interface, and then click the **Edit** button to configure IPV4Settings.</span></span>

    ![Select a hostname and configure IPV4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image8.png)

9. <span data-ttu-id="05e0f-150">In the **Editing System eth0** dialog box, check the **Connect automatically** check box.</span><span class="sxs-lookup"><span data-stu-id="05e0f-150">In the **Editing System eth0** dialog box, check the **Connect automatically** check box.</span></span> <span data-ttu-id="05e0f-151">On the **IPv4 Settings** tab, choose **Manual** for **Method**, and then click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="05e0f-151">On the **IPv4 Settings** tab, choose **Manual** for **Method**, and then click the **Add** button.</span></span> <span data-ttu-id="05e0f-152">Provide the **Static IP**, **Netmask**, **Gateway**, and **DNS Server** details.</span><span class="sxs-lookup"><span data-stu-id="05e0f-152">Provide the **Static IP**, **Netmask**, **Gateway**, and **DNS Server** details.</span></span> <span data-ttu-id="05e0f-153">Click **Apply** to save the details.</span><span class="sxs-lookup"><span data-stu-id="05e0f-153">Click **Apply** to save the details.</span></span>

    ![Settings for the network configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image9.png)

10. <span data-ttu-id="05e0f-155">Select your time zone, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-155">Select your time zone, and then click **Next**.</span></span>

    ![Select a time zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image10.png)

11. <span data-ttu-id="05e0f-157">Enter the **Root Password**, confirm the password, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-157">Enter the **Root Password**, confirm the password, and then click **Next**.</span></span>

    ![Add a password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image11.png)

12. <span data-ttu-id="05e0f-159">Select **Create Custom Layout**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-159">Select **Create Custom Layout**, and then click **Next**.</span></span>

    ![Select a type of installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image12.png)

13. <span data-ttu-id="05e0f-161">Select **Free** partition, and then click **Create** to create **/**, **/var/crash**, and **/home** partitions with **ext4** as the file system type.</span><span class="sxs-lookup"><span data-stu-id="05e0f-161">Select **Free** partition, and then click **Create** to create **/**, **/var/crash**, and **/home** partitions with **ext4** as the file system type.</span></span> <span data-ttu-id="05e0f-162">Create a **Swap partition** with **swap** as the file system type.</span><span class="sxs-lookup"><span data-stu-id="05e0f-162">Create a **Swap partition** with **swap** as the file system type.</span></span> <span data-ttu-id="05e0f-163">To allocate partition size, follow the size allocation formula in the following table.</span><span class="sxs-lookup"><span data-stu-id="05e0f-163">To allocate partition size, follow the size allocation formula in the following table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="05e0f-164">The Linux master target server should not use Logical Volume Manager (LVM) for root or retention storage spaces.</span><span class="sxs-lookup"><span data-stu-id="05e0f-164">The Linux master target server should not use Logical Volume Manager (LVM) for root or retention storage spaces.</span></span> <span data-ttu-id="05e0f-165">The Linux master target is configured to avoid LVM partitions and disk discovery by default.</span><span class="sxs-lookup"><span data-stu-id="05e0f-165">The Linux master target is configured to avoid LVM partitions and disk discovery by default.</span></span>

    ![Table of partition names, partition sizes, and file system types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image13.png)

14. <span data-ttu-id="05e0f-167">After you create the partition, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-167">After you create the partition, click **Next**.</span></span>

    ![Dialog box that shows selected values for partitions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image14.png)

15. <span data-ttu-id="05e0f-169">If any pre-existing devices are found, a warning message appears for formatting.</span><span class="sxs-lookup"><span data-stu-id="05e0f-169">If any pre-existing devices are found, a warning message appears for formatting.</span></span> <span data-ttu-id="05e0f-170">Click **Format** to format the hard drive with the latest partition table.</span><span class="sxs-lookup"><span data-stu-id="05e0f-170">Click **Format** to format the hard drive with the latest partition table.</span></span>

    ![Click the Format button to format the disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image15.png)

16. <span data-ttu-id="05e0f-172">Click **Write changes to disk** to apply the partition changes to the disk.</span><span class="sxs-lookup"><span data-stu-id="05e0f-172">Click **Write changes to disk** to apply the partition changes to the disk.</span></span>

    ![Click "Write changes to disk"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image16.png)

17. <span data-ttu-id="05e0f-174">Check the **Install boot loader** option, and then click **Next** to install the boot loader on the root partition.</span><span class="sxs-lookup"><span data-stu-id="05e0f-174">Check the **Install boot loader** option, and then click **Next** to install the boot loader on the root partition.</span></span>

    ![Install the boot loader on the root partition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image17.png)


18. <span data-ttu-id="05e0f-176">The installation process starts.</span><span class="sxs-lookup"><span data-stu-id="05e0f-176">The installation process starts.</span></span> <span data-ttu-id="05e0f-177">You can monitor progress.</span><span class="sxs-lookup"><span data-stu-id="05e0f-177">You can monitor progress.</span></span>

    ![Dialog box that shows progress of installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image18.png)

19. <span data-ttu-id="05e0f-179">The following screen displays on successful completion of installation.</span><span class="sxs-lookup"><span data-stu-id="05e0f-179">The following screen displays on successful completion of installation.</span></span> <span data-ttu-id="05e0f-180">Click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-180">Click **Reboot**.</span></span>

    ![Installation successful screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image19.png)


### <a name="post-installation-steps"></a><span data-ttu-id="05e0f-182">Post-installation steps</span><span class="sxs-lookup"><span data-stu-id="05e0f-182">Post-installation steps</span></span>
<span data-ttu-id="05e0f-183">Next, prepare the machine to be configured as a master target server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-183">Next, prepare the machine to be configured as a master target server.</span></span>

<span data-ttu-id="05e0f-184">To get the ID for each SCSI hard disk in a Linux virtual machine, you should enable the **disk.EnableUUID = TRUE** parameter.</span><span class="sxs-lookup"><span data-stu-id="05e0f-184">To get the ID for each SCSI hard disk in a Linux virtual machine, you should enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="05e0f-185">To enable this parameter, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="05e0f-185">To enable this parameter, use the following steps:</span></span>

1. <span data-ttu-id="05e0f-186">Shut down your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="05e0f-186">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="05e0f-187">Right-click the virtual machine’s entry in the left pane, and then select **Edit Settings.**</span><span class="sxs-lookup"><span data-stu-id="05e0f-187">Right-click the virtual machine’s entry in the left pane, and then select **Edit Settings.**</span></span>

3. <span data-ttu-id="05e0f-188">Click the **Options** tab.</span><span class="sxs-lookup"><span data-stu-id="05e0f-188">Click the **Options** tab.</span></span>

4. <span data-ttu-id="05e0f-189">Select **Advanced &gt; General** in the left pane, and then click the **Configuration Parameters** button on the right.</span><span class="sxs-lookup"><span data-stu-id="05e0f-189">Select **Advanced &gt; General** in the left pane, and then click the **Configuration Parameters** button on the right.</span></span>

    ![Options tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="05e0f-191">The **Configuration Parameters** option is not available when the machine is running.</span><span class="sxs-lookup"><span data-stu-id="05e0f-191">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="05e0f-192">To make this tab active, shut down the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="05e0f-192">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="05e0f-193">See whether a row with **disk.EnableUUID** already exists.</span><span class="sxs-lookup"><span data-stu-id="05e0f-193">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="05e0f-194">If the value exists and is set to **False**, change the value to **True** (The values are not case-sensitive).</span><span class="sxs-lookup"><span data-stu-id="05e0f-194">If the value exists and is set to **False**, change the value to **True** (The values are not case-sensitive).</span></span>

    - <span data-ttu-id="05e0f-195">If the value exists and is set to **True**, click **Cancel**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-195">If the value exists and is set to **True**, click **Cancel**.</span></span>

    - <span data-ttu-id="05e0f-196">If the value does not exist, click **Add Row.**</span><span class="sxs-lookup"><span data-stu-id="05e0f-196">If the value does not exist, click **Add Row.**</span></span>

    - <span data-ttu-id="05e0f-197">Add **disk.EnableUUID** in the **Name** column and set its value as **TRUE**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-197">Add **disk.EnableUUID** in the **Name** column and set its value as **TRUE**.</span></span>

    ![Checking whether disk.EnableUUID already exists](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="05e0f-199">Download and install additional packages</span><span class="sxs-lookup"><span data-stu-id="05e0f-199">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="05e0f-200">Make sure that you have Internet connectivity to download and install additional packages.</span><span class="sxs-lookup"><span data-stu-id="05e0f-200">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="05e0f-201">Without Internet connectivity, you will need to manually find these RPM packages and install them.</span><span class="sxs-lookup"><span data-stu-id="05e0f-201">Without Internet connectivity, you will need to manually find these RPM packages and install them.</span></span>

```
yum install -y xfsprogs perl lsscsi rsync wget kexec-tools
```

<span data-ttu-id="05e0f-202">The previous command will download the following 15 packages from the CentOS 6.6 repository and install them.</span><span class="sxs-lookup"><span data-stu-id="05e0f-202">The previous command will download the following 15 packages from the CentOS 6.6 repository and install them.</span></span> <span data-ttu-id="05e0f-203">If you do not have Internet access, you will need to download the following RPM packages:</span><span class="sxs-lookup"><span data-stu-id="05e0f-203">If you do not have Internet access, you will need to download the following RPM packages:</span></span>


<span data-ttu-id="05e0f-204">bc-1.06.95-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-204">bc-1.06.95-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-205">busybox-1.15.1-20.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-205">busybox-1.15.1-20.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-206">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-206">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-207">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-207">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-208">lsscsi-0.23-2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-208">lsscsi-0.23-2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-209">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-209">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-210">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-210">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-211">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-211">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-212">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-212">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-213">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-213">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-214">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-214">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-215">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-215">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-216">rsync-3.0.6-12.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-216">rsync-3.0.6-12.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-217">snappy-1.1.0-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-217">snappy-1.1.0-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="05e0f-218">wget-1.12-5.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="05e0f-218">wget-1.12-5.el6\_6.1.x86\_64.rpm</span></span>


#### <a name="install-additional-packages-for-specific-operating-systems"></a><span data-ttu-id="05e0f-219">Install additional packages for specific operating systems</span><span class="sxs-lookup"><span data-stu-id="05e0f-219">Install additional packages for specific operating systems</span></span>

> [!NOTE]
> <span data-ttu-id="05e0f-220">If source-protected machines use ReiserFS or XFS file systems for the root or boot device, you should download and install the following additional packages on the Linux master target prior to protection.</span><span class="sxs-lookup"><span data-stu-id="05e0f-220">If source-protected machines use ReiserFS or XFS file systems for the root or boot device, you should download and install the following additional packages on the Linux master target prior to protection.</span></span>


<span data-ttu-id="05e0f-221">***ReiserFS (If used in Suse11SP3. ReiserFS is not the default filesystem in Suse11SP3)***</span><span class="sxs-lookup"><span data-stu-id="05e0f-221">***ReiserFS (If used in Suse11SP3. ReiserFS is not the default filesystem in Suse11SP3)***</span></span>

```
cd /usr/local

wget
<http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

wget
<http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm
reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm
```

<span data-ttu-id="05e0f-222">***XFS (RHEL, CentOS 7 onward)***</span><span class="sxs-lookup"><span data-stu-id="05e0f-222">***XFS (RHEL, CentOS 7 onward)***</span></span>

```
cd /usr/local

wget
<http://archive.kernel.org/centos-vault/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

yum install device-mapper-multipath
```
<span data-ttu-id="05e0f-223">This is required to enable multipath packages on the master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-223">This is required to enable multipath packages on the master target.</span></span>

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="05e0f-224">Get the installer for setup</span><span class="sxs-lookup"><span data-stu-id="05e0f-224">Get the installer for setup</span></span>

<span data-ttu-id="05e0f-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span><span class="sxs-lookup"><span data-stu-id="05e0f-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="05e0f-226">Otherwise, you can copy the installer from the process server and install it.</span><span class="sxs-lookup"><span data-stu-id="05e0f-226">Otherwise, you can copy the installer from the process server and install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="05e0f-227">Download the master target installation packages</span><span class="sxs-lookup"><span data-stu-id="05e0f-227">Download the master target installation packages</span></span>

<span data-ttu-id="05e0f-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="05e0f-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="05e0f-229">To download it by using Linux, type:</span><span class="sxs-lookup"><span data-stu-id="05e0f-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="05e0f-230">Make sure that you download and unzip the installer in your home directory.</span><span class="sxs-lookup"><span data-stu-id="05e0f-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="05e0f-231">If you unzip to /usr/Local, then the installation will fail.</span><span class="sxs-lookup"><span data-stu-id="05e0f-231">If you unzip to /usr/Local, then the installation will fail.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="05e0f-232">Access the installer from the process server</span><span class="sxs-lookup"><span data-stu-id="05e0f-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="05e0f-233">Go to C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository on the process server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-233">Go to C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository on the process server.</span></span>

2. <span data-ttu-id="05e0f-234">Copy the required installer file from the process server, and save it as latestlinuxmobsvc.tar.gz in your home directory.</span><span class="sxs-lookup"><span data-stu-id="05e0f-234">Copy the required installer file from the process server, and save it as latestlinuxmobsvc.tar.gz in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="05e0f-235">Apply custom configuration changes</span><span class="sxs-lookup"><span data-stu-id="05e0f-235">Apply custom configuration changes</span></span>

<span data-ttu-id="05e0f-236">To apply custom configuration changes, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="05e0f-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="05e0f-237">Run the following command to untar the binary.</span><span class="sxs-lookup"><span data-stu-id="05e0f-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Screenshot of the executed command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="05e0f-239">Run the following command to give permission.</span><span class="sxs-lookup"><span data-stu-id="05e0f-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="05e0f-240">Run the following command to run the script.</span><span class="sxs-lookup"><span data-stu-id="05e0f-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="05e0f-241">Run the script only once on the server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-241">Run the script only once on the server.</span></span> <span data-ttu-id="05e0f-242">Shut down the server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-242">Shut down the server.</span></span> <span data-ttu-id="05e0f-243">Reboot the server after you add a disk as described in the next steps.</span><span class="sxs-lookup"><span data-stu-id="05e0f-243">Reboot the server after you add a disk as described in the next steps.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="05e0f-244">Add a retention disk to the Linux master target virtual machine</span><span class="sxs-lookup"><span data-stu-id="05e0f-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="05e0f-245">Use the following steps to create a retention disk:</span><span class="sxs-lookup"><span data-stu-id="05e0f-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="05e0f-246">Attach a new **1-TB** disk to the Linux master target virtual machine, and **boot** the machine.</span><span class="sxs-lookup"><span data-stu-id="05e0f-246">Attach a new **1-TB** disk to the Linux master target virtual machine, and **boot** the machine.</span></span>

2. <span data-ttu-id="05e0f-247">Use the **multipath -ll** command to learn the retention disk's multipath ID.</span><span class="sxs-lookup"><span data-stu-id="05e0f-247">Use the **multipath -ll** command to learn the retention disk's multipath ID.</span></span>

    ```
    multipath -ll
    ```

    ![The multipath ID of the retention disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="05e0f-249">Format the drive, and create a file system on the new drive.</span><span class="sxs-lookup"><span data-stu-id="05e0f-249">Format the drive, and create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Creating a file system on the drive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="05e0f-251">After you create the file system, mount the retention disk.</span><span class="sxs-lookup"><span data-stu-id="05e0f-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```

    ![Mounting the retention disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="05e0f-253">Create the **fstab** entry to mount the retention drive during every boot.</span><span class="sxs-lookup"><span data-stu-id="05e0f-253">Create the **fstab** entry to mount the retention drive during every boot.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="05e0f-254">Press **Insert** to begin editing the file.</span><span class="sxs-lookup"><span data-stu-id="05e0f-254">Press **Insert** to begin editing the file.</span></span> <span data-ttu-id="05e0f-255">Create a new line, and insert the following text.</span><span class="sxs-lookup"><span data-stu-id="05e0f-255">Create a new line, and insert the following text.</span></span> <span data-ttu-id="05e0f-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span><span class="sxs-lookup"><span data-stu-id="05e0f-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="05e0f-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="05e0f-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="05e0f-258">Press **Esc**, and type **:wq** (write and quit) to close the editor window.</span><span class="sxs-lookup"><span data-stu-id="05e0f-258">Press **Esc**, and type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="05e0f-259">Install the master target</span><span class="sxs-lookup"><span data-stu-id="05e0f-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05e0f-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="05e0f-261">If this condition is not met, reprotect will succeed, but replication will fail.</span><span class="sxs-lookup"><span data-stu-id="05e0f-261">If this condition is not met, reprotect will succeed, but replication will fail.</span></span>


> [!NOTE]
> <span data-ttu-id="05e0f-262">Before you install the master target server, check that the /etc/hosts file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span><span class="sxs-lookup"><span data-stu-id="05e0f-262">Before you install the master target server, check that the /etc/hosts file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="05e0f-263">Copy the passphrase from C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase on the configuration server, and save it in passphrase.txt in the same local directory by running the following command.</span><span class="sxs-lookup"><span data-stu-id="05e0f-263">Copy the passphrase from C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase on the configuration server, and save it in passphrase.txt in the same local directory by running the following command.</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="05e0f-264">Example: echo itUx70I47uxDuUVY >passphrase.txt</span><span class="sxs-lookup"><span data-stu-id="05e0f-264">Example: echo itUx70I47uxDuUVY >passphrase.txt</span></span>

2. <span data-ttu-id="05e0f-265">Note the configuration server's IP address.</span><span class="sxs-lookup"><span data-stu-id="05e0f-265">Note the configuration server's IP address.</span></span> <span data-ttu-id="05e0f-266">You need it in the next step.</span><span class="sxs-lookup"><span data-stu-id="05e0f-266">You need it in the next step.</span></span>

3. <span data-ttu-id="05e0f-267">Run the following command to install the master target server and register the server with the configuration server.</span><span class="sxs-lookup"><span data-stu-id="05e0f-267">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i <Configuration Server IP Address> -p 443 -s y -c https -P passphrase.txt
    ```

    <span data-ttu-id="05e0f-268">Example: ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt</span><span class="sxs-lookup"><span data-stu-id="05e0f-268">Example: ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt</span></span>

    <span data-ttu-id="05e0f-269">Wait until the script finishes.</span><span class="sxs-lookup"><span data-stu-id="05e0f-269">Wait until the script finishes.</span></span> <span data-ttu-id="05e0f-270">If the master target is successfully registered, the master target is listed on the Site Recovery Infrastructure page of the portal.</span><span class="sxs-lookup"><span data-stu-id="05e0f-270">If the master target is successfully registered, the master target is listed on the Site Recovery Infrastructure page of the portal.</span></span>

#### <a name="install-the-master-target-by-using-interactive-install"></a><span data-ttu-id="05e0f-271">Install the master target by using interactive install</span><span class="sxs-lookup"><span data-stu-id="05e0f-271">Install the master target by using interactive install</span></span>

1. <span data-ttu-id="05e0f-272">Run the following command to install the master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-272">Run the following command to install the master target.</span></span> <span data-ttu-id="05e0f-273">Choose agent role as **Master Target**.</span><span class="sxs-lookup"><span data-stu-id="05e0f-273">Choose agent role as **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="05e0f-274">Choose the default location for installation, and press **Enter** to continue.</span><span class="sxs-lookup"><span data-stu-id="05e0f-274">Choose the default location for installation, and press **Enter** to continue.</span></span>

    ![Choosing a default location for installation of master target](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/image17.png)


3. <span data-ttu-id="05e0f-276">Choose the **Global** settings to configure.</span><span class="sxs-lookup"><span data-stu-id="05e0f-276">Choose the **Global** settings to configure.</span></span>

    ![Configuring global settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/image18.png)

4. <span data-ttu-id="05e0f-278">Specify the configuration server's IP addresses.</span><span class="sxs-lookup"><span data-stu-id="05e0f-278">Specify the configuration server's IP addresses.</span></span>

5. <span data-ttu-id="05e0f-279">Specify the configuration server's port as 443.</span><span class="sxs-lookup"><span data-stu-id="05e0f-279">Specify the configuration server's port as 443.</span></span>

    ![Specifying IP address and port for the configuration server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-how-to-install-linux-master-target/image19.png)

6. <span data-ttu-id="05e0f-281">Copy the configuration server's passphrase from C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase on the configuration server and paste it in the **Passphrase** box.</span><span class="sxs-lookup"><span data-stu-id="05e0f-281">Copy the configuration server's passphrase from C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase on the configuration server and paste it in the **Passphrase** box.</span></span> <span data-ttu-id="05e0f-282">The box will be empty even after you paste the text.</span><span class="sxs-lookup"><span data-stu-id="05e0f-282">The box will be empty even after you paste the text.</span></span>

7. <span data-ttu-id="05e0f-283">Go to **Quit** in the menu.</span><span class="sxs-lookup"><span data-stu-id="05e0f-283">Go to **Quit** in the menu.</span></span>

8. <span data-ttu-id="05e0f-284">Let the installation and registration finish.</span><span class="sxs-lookup"><span data-stu-id="05e0f-284">Let the installation and registration finish.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="05e0f-285">Install VMware tools on the master target server</span><span class="sxs-lookup"><span data-stu-id="05e0f-285">Install VMware tools on the master target server</span></span>

<span data-ttu-id="05e0f-286">You need to install VMware tools on the master target so that it can discover the datastores.</span><span class="sxs-lookup"><span data-stu-id="05e0f-286">You need to install VMware tools on the master target so that it can discover the datastores.</span></span> <span data-ttu-id="05e0f-287">If the tools are not installed, the reprotect screen will not list the datastores.</span><span class="sxs-lookup"><span data-stu-id="05e0f-287">If the tools are not installed, the reprotect screen will not list the datastores.</span></span> <span data-ttu-id="05e0f-288">You will need to reboot after installation of the VMware tools.</span><span class="sxs-lookup"><span data-stu-id="05e0f-288">You will need to reboot after installation of the VMware tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05e0f-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="05e0f-289">Next steps</span></span>
<span data-ttu-id="05e0f-290">After the master target has completed installation and registration, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span><span class="sxs-lookup"><span data-stu-id="05e0f-290">After the master target has completed installation and registration, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="05e0f-291">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span><span class="sxs-lookup"><span data-stu-id="05e0f-291">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="05e0f-292">Common issues</span><span class="sxs-lookup"><span data-stu-id="05e0f-292">Common issues</span></span>

* <span data-ttu-id="05e0f-293">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span><span class="sxs-lookup"><span data-stu-id="05e0f-293">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="05e0f-294">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached, and failback will fail.</span><span class="sxs-lookup"><span data-stu-id="05e0f-294">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached, and failback will fail.</span></span>
* <span data-ttu-id="05e0f-295">The master target should not have any snapshots on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="05e0f-295">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="05e0f-296">If there are snapshots, failback will fail.</span><span class="sxs-lookup"><span data-stu-id="05e0f-296">If there are snapshots, failback will fail.</span></span>
* <span data-ttu-id="05e0f-297">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span><span class="sxs-lookup"><span data-stu-id="05e0f-297">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="05e0f-298">Make sure that the following properties are correctly set.</span><span class="sxs-lookup"><span data-stu-id="05e0f-298">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="05e0f-299">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth\*.</span><span class="sxs-lookup"><span data-stu-id="05e0f-299">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth\*.</span></span>
        <span data-ttu-id="05e0f-300">\* BOOTPROTO=dhcp \* ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="05e0f-300">\* BOOTPROTO=dhcp \* ONBOOT=yes</span></span>




























