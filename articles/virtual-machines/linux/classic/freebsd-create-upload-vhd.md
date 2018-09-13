---
title: Create and upload a FreeBSD VM image | Microsoft Docs
description: Learn to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system to create an Azure virtual machine
services: virtual-machines-linux
documentationcenter: ''
author: KylieLiang
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: kyliel
ms.openlocfilehash: 13a29d51f88af450e1252e1ffd7cdefdc1a33d69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552677"
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="a2d5a-103">Create and upload a FreeBSD VHD to Azure</span><span class="sxs-lookup"><span data-stu-id="a2d5a-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="a2d5a-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="a2d5a-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a2d5a-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a2d5a-107">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a2d5a-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a2d5a-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2d5a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a2d5a-110">Prerequisites</span></span>
<span data-ttu-id="a2d5a-111">This article assumes that you have the following items:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="a2d5a-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="a2d5a-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="a2d5a-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="a2d5a-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="a2d5a-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="a2d5a-117">A tutorial that describes how install and configure the module is available here.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-117">A tutorial that describes how install and configure the module is available here.</span></span> <span data-ttu-id="a2d5a-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="a2d5a-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="a2d5a-120">Multiple tools exist to create .vhd files.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="a2d5a-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="a2d5a-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a2d5a-123">The newer VHDX format is not supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="a2d5a-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="a2d5a-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="a2d5a-126">This task includes the following five steps.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-126">This task includes the following five steps.</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="a2d5a-127">Step 1: Prepare the image for upload</span><span class="sxs-lookup"><span data-stu-id="a2d5a-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="a2d5a-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="a2d5a-129">Enable DHCP.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="a2d5a-130">Enable SSH.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-130">Enable SSH.</span></span>

    <span data-ttu-id="a2d5a-131">SSH is enabled by default after installation from disc. If it isn't enabled for some reason, or if you use FreeBSD VHD directly, type the following:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-131">SSH is enabled by default after installation from disc. If it isn't enabled for some reason, or if you use FreeBSD VHD directly, type the following:</span></span>

        # echo 'sshd_enable="YES"' >> /etc/rc.conf
        # ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
        # ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
        # service sshd restart
3. <span data-ttu-id="a2d5a-132">Set up a serial console.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-132">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="a2d5a-133">Install sudo.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-133">Install sudo.</span></span>

    <span data-ttu-id="a2d5a-134">The root account is disabled in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-134">The root account is disabled in Azure.</span></span> <span data-ttu-id="a2d5a-135">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-135">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   <span data-ttu-id="a2d5a-136">;</span><span class="sxs-lookup"><span data-stu-id="a2d5a-136">;</span></span>
5. <span data-ttu-id="a2d5a-137">Prerequisites for Azure Agent.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools27   
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="a2d5a-138">Install Azure Agent.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-138">Install Azure Agent.</span></span>

    <span data-ttu-id="a2d5a-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="a2d5a-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 officially supports FreeBSD 10.2 and later releases.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="a2d5a-141">For 2.0, let's use 2.0.16 as an example:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="a2d5a-142">For 2.1, let's use 2.1.4 as an example:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="a2d5a-143">After you install Azure Agent, it's a good idea to verify that it's running:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # service –e | grep waagent
        /etc/rc.d/waagent
        # cat /var/log/waagent.log
7. <span data-ttu-id="a2d5a-144">Deprovision the system.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-144">Deprovision the system.</span></span>

    <span data-ttu-id="a2d5a-145">Deprovision the system to clean it and make it suitable for re-provisioning.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-145">Deprovision the system to clean it and make it suitable for re-provisioning.</span></span> <span data-ttu-id="a2d5a-146">The following command also deletes the last provisioned user account and the associated data:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="a2d5a-147">Now you can shut down your VM.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="a2d5a-148">Step 2: Create a storage account in Azure</span><span class="sxs-lookup"><span data-stu-id="a2d5a-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="a2d5a-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="a2d5a-150">You can use the Azure classic portal to create a storage account.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="a2d5a-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a2d5a-152">On the command bar, select **New**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="a2d5a-153">Select **Data Services** > **Storage** > **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Quick create a storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/storage-quick-create.png)
4. <span data-ttu-id="a2d5a-155">Fill out the fields as follows:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="a2d5a-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="a2d5a-157">The entry can contain from 3-24 numbers and lowercase letters.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="a2d5a-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="a2d5a-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="a2d5a-160">An affinity group lets you put your cloud services and storage in the same data center.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="a2d5a-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="a2d5a-162">Geo-replication is turned on by default.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="a2d5a-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="a2d5a-164">The secondary location is assigned automatically and can't be changed.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="a2d5a-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="a2d5a-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="a2d5a-167">Storage services without geo-replication are offered at a discount.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="a2d5a-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/storage-redundancy.md).</span></span>

     ![Enter storage account details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/storage-create-account.png)
5. <span data-ttu-id="a2d5a-170">Select **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="a2d5a-171">The account now appears under **storage**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-171">The account now appears under **storage**.</span></span>

    ![Storage account successfully created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/storagenewaccount.png)
6. <span data-ttu-id="a2d5a-173">Next, create a container for your uploaded .vhd files.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="a2d5a-174">Select the storage account name, and then select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-174">Select the storage account name, and then select **Containers**.</span></span>

    ![Storage account detail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="a2d5a-176">Select **Create a Container**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-176">Select **Create a Container**.</span></span>

    ![Storage account detail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="a2d5a-178">In the **Name** field, type a name for your container.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="a2d5a-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Container name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="a2d5a-181">By default, the container is private and can only be accessed by the account owner.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="a2d5a-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="a2d5a-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="a2d5a-184">Step 3: Prepare the connection to Azure</span><span class="sxs-lookup"><span data-stu-id="a2d5a-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="a2d5a-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="a2d5a-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do this.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do this.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="a2d5a-187">Use the Azure AD method to upload a .vhd file</span><span class="sxs-lookup"><span data-stu-id="a2d5a-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="a2d5a-188">Open the Azure PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="a2d5a-189">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="a2d5a-190">This command opens a sign-in window where you can sign in with your work or school account.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell Window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="a2d5a-192">Azure authenticates and saves the credential information.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="a2d5a-193">Then it closes the window.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="a2d5a-194">Use the certificate method to upload a .vhd file</span><span class="sxs-lookup"><span data-stu-id="a2d5a-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="a2d5a-195">Open the Azure PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="a2d5a-196">Type:  `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="a2d5a-197">A browser window opens and prompts you to download a .publishsettings file.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-197">A browser window opens and prompts you to download a .publishsettings file.</span></span> <span data-ttu-id="a2d5a-198">This file contains information and a certificate for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Browser download page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/browser_download_getpublishsettingsfile.png)
4. <span data-ttu-id="a2d5a-200">Save the .publishsettings file.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="a2d5a-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="a2d5a-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="a2d5a-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a2d5a-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="a2d5a-204">Step 4: Upload the .vhd file</span><span class="sxs-lookup"><span data-stu-id="a2d5a-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="a2d5a-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="a2d5a-206">Following are some terms you'll use when you upload the file:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-206">Following are some terms you'll use when you upload the file:</span></span>

* <span data-ttu-id="a2d5a-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="a2d5a-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="a2d5a-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="a2d5a-210">**PathToVHDFile** is the full path and name of the .vhd file.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="a2d5a-211">From the Azure PowerShell window you used in the previous step, type:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="a2d5a-212">Step 5: Create a VM with the uploaded .vhd file</span><span class="sxs-lookup"><span data-stu-id="a2d5a-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="a2d5a-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="a2d5a-214">From the Azure PowerShell window you used in the previous step, type:</span><span class="sxs-lookup"><span data-stu-id="a2d5a-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="a2d5a-215">Use Linux as the OS type.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-215">Use Linux as the OS type.</span></span> <span data-ttu-id="a2d5a-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="a2d5a-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Choose an image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="a2d5a-219">Create a virtual machine from the gallery.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="a2d5a-220">This new image is now available under **My Images**.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="a2d5a-221">Select the new image.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-221">Select the new image.</span></span> <span data-ttu-id="a2d5a-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![Custom image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="a2d5a-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d5a-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![FreeBSD image in azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/freebsd-create-upload-vhd/freebsdimageinazure.png)











