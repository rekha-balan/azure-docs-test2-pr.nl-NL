---
title: Azure Quick Start - Create VM Portal | Microsoft Docs
description: Azure Quick Start - Create VM Portal
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/13/2017
ms.author: nepeters
ms.openlocfilehash: 495e8088e43082aa8d413a3c43e2c2063a9aa9d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551009"
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="3fe2e-103">Create a Linux virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3fe2e-103">Create a Linux virtual machine with the Azure portal</span></span>

<span data-ttu-id="3fe2e-104">Azure virtual machines can be created through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="3fe2e-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="3fe2e-106">This Quickstart steps through creating a virtual machine using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-106">This Quickstart steps through creating a virtual machine using the Azure portal.</span></span>

<span data-ttu-id="3fe2e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="3fe2e-108">Create SSH key pair</span><span class="sxs-lookup"><span data-stu-id="3fe2e-108">Create SSH key pair</span></span>

<span data-ttu-id="3fe2e-109">You need an SSH key pair to complete this quick start.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-109">You need an SSH key pair to complete this quick start.</span></span> <span data-ttu-id="3fe2e-110">If you have an existing SSH key pair, this step can be skipped.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-110">If you have an existing SSH key pair, this step can be skipped.</span></span> <span data-ttu-id="3fe2e-111">If you are using a Windows machine, follow the instructions found [here](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3fe2e-111">If you are using a Windows machine, follow the instructions found [here](ssh-from-windows.md).</span></span> 

<span data-ttu-id="3fe2e-112">From a Bash shell, run this command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-112">From a Bash shell, run this command and follow the on-screen directions.</span></span> <span data-ttu-id="3fe2e-113">The command output includes the file name of the public key file.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-113">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="3fe2e-114">The contents of this file are needed when creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-114">The contents of this file are needed when creating the virtual machine.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a><span data-ttu-id="3fe2e-115">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="3fe2e-115">Log in to Azure</span></span> 

<span data-ttu-id="3fe2e-116">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-116">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="3fe2e-117">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="3fe2e-117">Create virtual machine</span></span>

1. <span data-ttu-id="3fe2e-118">Click the **New** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-118">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="3fe2e-119">Select **Compute** from the **New** blade, select **Ubuntu Server 16.04 LTS** from the **Compute** blade, and then click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-119">Select **Compute** from the **New** blade, select **Ubuntu Server 16.04 LTS** from the **Compute** blade, and then click the **Create** button.</span></span>

3. <span data-ttu-id="3fe2e-120">Fill out the virtual machine **Basics** form.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-120">Fill out the virtual machine **Basics** form.</span></span> <span data-ttu-id="3fe2e-121">For **Authentication type**, select **SSH**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-121">For **Authentication type**, select **SSH**.</span></span> <span data-ttu-id="3fe2e-122">When pasting in your **SSH public key**, take care to remove any leading or trailing white space.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-122">When pasting in your **SSH public key**, take care to remove any leading or trailing white space.</span></span> <span data-ttu-id="3fe2e-123">For **Resource group**, create a new one.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-123">For **Resource group**, create a new one.</span></span> <span data-ttu-id="3fe2e-124">A resource group is a logical container into which Azure resources are created and collectively managed.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-124">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="3fe2e-125">When complete, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-125">When complete, click **OK**.</span></span>

    ![Enter basic information about your VM in the portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-portal/create-vm-portal-basic-blade.png)  

4. <span data-ttu-id="3fe2e-127">Choose a size for the VM.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-127">Choose a size for the VM.</span></span> <span data-ttu-id="3fe2e-128">To see more sizes, select **View all** or change the **Supported disk type** filter.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-128">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Screenshot that shows VM sizes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="3fe2e-130">On the settings blade, select **Yes** under **Use managed disks**, keep the defaults for the rest of the settings, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-130">On the settings blade, select **Yes** under **Use managed disks**, keep the defaults for the rest of the settings, and click **OK**.</span></span>

6. <span data-ttu-id="3fe2e-131">On the summary page, click **Ok** to start the virtual machine deployment.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-131">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="3fe2e-132">To monitor deployment status, click the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-132">To monitor deployment status, click the virtual machine.</span></span> <span data-ttu-id="3fe2e-133">The VM can be found on the Azure portal dashboard, or by selecting **Virtual Machines** from the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-133">The VM can be found on the Azure portal dashboard, or by selecting **Virtual Machines** from the left-hand menu.</span></span> <span data-ttu-id="3fe2e-134">When the VM has been created, the status changes from **Deploying** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-134">When the VM has been created, the status changes from **Deploying** to **Running**.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="3fe2e-135">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="3fe2e-135">Open port 80 for web traffic</span></span> 

<span data-ttu-id="3fe2e-136">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-136">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="3fe2e-137">If this VM is going to be a webserver, you need to open port 80 to web traffic.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-137">If this VM is going to be a webserver, you need to open port 80 to web traffic.</span></span> <span data-ttu-id="3fe2e-138">This step walks you through creating a network security group (NSG) rule to allow inbound connections on port 80.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-138">This step walks you through creating a network security group (NSG) rule to allow inbound connections on port 80.</span></span>

1. <span data-ttu-id="3fe2e-139">On the blade for the virtual machine, in the **Essentials** section, click the name of the **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-139">On the blade for the virtual machine, in the **Essentials** section, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="3fe2e-140">In the blade for the resource group, click the **Network security group** in the list of resources.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-140">In the blade for the resource group, click the **Network security group** in the list of resources.</span></span> <span data-ttu-id="3fe2e-141">The NSG name should be the VM name with -nsg appended to the end.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-141">The NSG name should be the VM name with -nsg appended to the end.</span></span>
3. <span data-ttu-id="3fe2e-142">Click the **Inbound Security Rule** heading to open the list of inbound rules.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-142">Click the **Inbound Security Rule** heading to open the list of inbound rules.</span></span> <span data-ttu-id="3fe2e-143">You should see a rule for RDP already in the list.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-143">You should see a rule for RDP already in the list.</span></span>
4. <span data-ttu-id="3fe2e-144">Click **+ Add** to open the **Add inbound security rule** blade.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-144">Click **+ Add** to open the **Add inbound security rule** blade.</span></span>
5. <span data-ttu-id="3fe2e-145">In **Name**, type **nginx**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-145">In **Name**, type **nginx**.</span></span> <span data-ttu-id="3fe2e-146">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-146">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> <span data-ttu-id="3fe2e-147">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-147">Click **OK**.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="3fe2e-148">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="3fe2e-148">Connect to virtual machine</span></span>

<span data-ttu-id="3fe2e-149">After the deployment has completed, create an SSH connection with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-149">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

1. <span data-ttu-id="3fe2e-150">Click the **Connect** button on the virtual machine blade.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-150">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="3fe2e-151">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-151">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span></span>

    ![Portal 9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="3fe2e-153">Run the following command to create an SSH session.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-153">Run the following command to create an SSH session.</span></span> <span data-ttu-id="3fe2e-154">Replace the connection string with the one you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-154">Replace the connection string with the one you copied from the Azure portal.</span></span>

```bash 
ssh <replace with IP address>
```

## <a name="install-nginx"></a><span data-ttu-id="3fe2e-155">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="3fe2e-155">Install NGINX</span></span>

<span data-ttu-id="3fe2e-156">Use the following bash script to update package sources and install the latest NGINX package.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-156">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="3fe2e-157">View the NGIX welcome page</span><span class="sxs-lookup"><span data-stu-id="3fe2e-157">View the NGIX welcome page</span></span>

<span data-ttu-id="3fe2e-158">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-158">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="3fe2e-159">Be sure to use the `publicIpAddress` you documented to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-159">Be sure to use the `publicIpAddress` you documented to visit the default page.</span></span> 

![NGINX default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-cli/nginx.png) 
## <a name="delete-virtual-machine"></a><span data-ttu-id="3fe2e-161">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="3fe2e-161">Delete virtual machine</span></span>

<span data-ttu-id="3fe2e-162">When no longer needed, delete the resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-162">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="3fe2e-163">To do so, select the resource group from the virtual machine blade and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3fe2e-163">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fe2e-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fe2e-164">Next steps</span></span>

[<span data-ttu-id="3fe2e-165">Create highly available virtual machines tutorial</span><span class="sxs-lookup"><span data-stu-id="3fe2e-165">Create highly available virtual machines tutorial</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="3fe2e-166">Explore VM deployment CLI samples</span><span class="sxs-lookup"><span data-stu-id="3fe2e-166">Explore VM deployment CLI samples</span></span>](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)




