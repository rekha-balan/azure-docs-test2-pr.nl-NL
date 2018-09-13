---
title: Azure Stack Quick Start - Create VM Portal
description: Azure Stack Quick Start - Create a Linux VM using the portal
services: azure-stack
cloud: azure-stack
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: mabrigg
ms.reviewer: ''
ms.custom: mvc
ms.openlocfilehash: e82c3de4461e2d663496cd4ae4a98c10e7819466
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866663"
---
# <a name="quickstart-create-a-linux-server-virtual-machine-with-the-azure-stack-portal"></a><span data-ttu-id="e8d22-103">Quickstart: create a Linux server virtual machine with the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="e8d22-103">Quickstart: create a Linux server virtual machine with the Azure Stack portal</span></span>

<span data-ttu-id="e8d22-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="e8d22-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="e8d22-105">You can create a Ubuntu Server 16.04 LTS virtual machine by using the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="e8d22-105">You can create a Ubuntu Server 16.04 LTS virtual machine by using the Azure Stack portal.</span></span> <span data-ttu-id="e8d22-106">Follow the steps in this article to create and use a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-106">Follow the steps in this article to create and use a virtual machine.</span></span> <span data-ttu-id="e8d22-107">This article also gives you the steps to:</span><span class="sxs-lookup"><span data-stu-id="e8d22-107">This article also gives you the steps to:</span></span>

* <span data-ttu-id="e8d22-108">Connect to the virtual machine with a remote client.</span><span class="sxs-lookup"><span data-stu-id="e8d22-108">Connect to the virtual machine with a remote client.</span></span>
* <span data-ttu-id="e8d22-109">Install a NGINX web server.</span><span class="sxs-lookup"><span data-stu-id="e8d22-109">Install a NGINX web server.</span></span>
* <span data-ttu-id="e8d22-110">Clean up your resources.</span><span class="sxs-lookup"><span data-stu-id="e8d22-110">Clean up your resources.</span></span>

> [!NOTE]  
> <span data-ttu-id="e8d22-111">The screen images in this article are updated to match changes introduced with Azure Stack version 1808.</span><span class="sxs-lookup"><span data-stu-id="e8d22-111">The screen images in this article are updated to match changes introduced with Azure Stack version 1808.</span></span> <span data-ttu-id="e8d22-112">1808 adds support for using *managed disks* in addition to unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="e8d22-112">1808 adds support for using *managed disks* in addition to unmanaged disks.</span></span> <span data-ttu-id="e8d22-113">If you use an earlier version, some images for tasks like disk selection will be different than what is displayed in this article.</span><span class="sxs-lookup"><span data-stu-id="e8d22-113">If you use an earlier version, some images for tasks like disk selection will be different than what is displayed in this article.</span></span>  


## <a name="prerequisites"></a><span data-ttu-id="e8d22-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e8d22-114">Prerequisites</span></span>

* <span data-ttu-id="e8d22-115">**A Linux image in the Azure Stack marketplace**</span><span class="sxs-lookup"><span data-stu-id="e8d22-115">**A Linux image in the Azure Stack marketplace**</span></span>

   <span data-ttu-id="e8d22-116">The Azure Stack marketplace doesn't contain a Linux image by default.</span><span class="sxs-lookup"><span data-stu-id="e8d22-116">The Azure Stack marketplace doesn't contain a Linux image by default.</span></span> <span data-ttu-id="e8d22-117">Before you can create a Linux server virtual machine, ensure that the Azure Stack operator provides the **Ubuntu Server 16.04 LTS** image you need.</span><span class="sxs-lookup"><span data-stu-id="e8d22-117">Before you can create a Linux server virtual machine, ensure that the Azure Stack operator provides the **Ubuntu Server 16.04 LTS** image you need.</span></span> <span data-ttu-id="e8d22-118">The operator can use the steps described in the [Download marketplace items from Azure to Azure Stack](../azure-stack-download-azure-marketplace-item.md) article.</span><span class="sxs-lookup"><span data-stu-id="e8d22-118">The operator can use the steps described in the [Download marketplace items from Azure to Azure Stack](../azure-stack-download-azure-marketplace-item.md) article.</span></span>

* <span data-ttu-id="e8d22-119">**Access to an SSH client**</span><span class="sxs-lookup"><span data-stu-id="e8d22-119">**Access to an SSH client**</span></span>

   <span data-ttu-id="e8d22-120">If you are using the Azure Stack Development Kit (ASDK), you might not have access to an SSH client.</span><span class="sxs-lookup"><span data-stu-id="e8d22-120">If you are using the Azure Stack Development Kit (ASDK), you might not have access to an SSH client.</span></span> <span data-ttu-id="e8d22-121">If you need a client, there are several packages that include an SSH client.</span><span class="sxs-lookup"><span data-stu-id="e8d22-121">If you need a client, there are several packages that include an SSH client.</span></span> <span data-ttu-id="e8d22-122">For example, PuTTY includes an SSH client and SSH key generator (puttygen.exe).</span><span class="sxs-lookup"><span data-stu-id="e8d22-122">For example, PuTTY includes an SSH client and SSH key generator (puttygen.exe).</span></span> <span data-ttu-id="e8d22-123">For more information about available packages,  read the following Azure article: [How to Use SSH keys with Windows on Azure](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows#windows-packages-and-ssh-clients).</span><span class="sxs-lookup"><span data-stu-id="e8d22-123">For more information about available packages,  read the following Azure article: [How to Use SSH keys with Windows on Azure](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows#windows-packages-and-ssh-clients).</span></span>

   <span data-ttu-id="e8d22-124">This Quickstart uses PuTTY to generate the SSH keys and to connect to the Linux server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-124">This Quickstart uses PuTTY to generate the SSH keys and to connect to the Linux server virtual machine.</span></span> <span data-ttu-id="e8d22-125">To download and install PuTTY, go to [http://www.putty.org/](http://www.putty.org).</span><span class="sxs-lookup"><span data-stu-id="e8d22-125">To download and install PuTTY, go to [http://www.putty.org/](http://www.putty.org).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="e8d22-126">Create an SSH key pair</span><span class="sxs-lookup"><span data-stu-id="e8d22-126">Create an SSH key pair</span></span>

<span data-ttu-id="e8d22-127">You need an SSH key pair to finish all the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="e8d22-127">You need an SSH key pair to finish all the steps in this article.</span></span> <span data-ttu-id="e8d22-128">If you have an existing SSH key pair, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="e8d22-128">If you have an existing SSH key pair, you can skip this step.</span></span>

1. <span data-ttu-id="e8d22-129">Navigate to the PuTTY installation folder (the default location is ```C:\Program Files\PuTTY```) and run ```puttygen.exe```.</span><span class="sxs-lookup"><span data-stu-id="e8d22-129">Navigate to the PuTTY installation folder (the default location is ```C:\Program Files\PuTTY```) and run ```puttygen.exe```.</span></span>
2. <span data-ttu-id="e8d22-130">In the PuTTY Key Generator window, ensure the **Type of key to generate** is set to **RSA**, and the **Number of bits in a generated key** is set to **2048**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-130">In the PuTTY Key Generator window, ensure the **Type of key to generate** is set to **RSA**, and the **Number of bits in a generated key** is set to **2048**.</span></span> <span data-ttu-id="e8d22-131">When you're ready, click **Generate**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-131">When you're ready, click **Generate**.</span></span>

   ![PuTTY Key Generator configuration](media/azure-stack-quick-linux-portal/Putty01.PNG)

3. <span data-ttu-id="e8d22-133">To generate a key, move your mouse cursor randomly in the PuTTY Key Generator window.</span><span class="sxs-lookup"><span data-stu-id="e8d22-133">To generate a key, move your mouse cursor randomly in the PuTTY Key Generator window.</span></span>
4. <span data-ttu-id="e8d22-134">When the key generation finishes, click **Save public key** and then click **Save private key** to save your keys to files.</span><span class="sxs-lookup"><span data-stu-id="e8d22-134">When the key generation finishes, click **Save public key** and then click **Save private key** to save your keys to files.</span></span>

   ![PuTTY Key Generator results](media/azure-stack-quick-linux-portal/Putty02.PNG)

## <a name="sign-in-to-the-azure-stack-portal"></a><span data-ttu-id="e8d22-136">Sign in to the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="e8d22-136">Sign in to the Azure Stack portal</span></span>

<span data-ttu-id="e8d22-137">Sign in to the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="e8d22-137">Sign in to the Azure Stack portal.</span></span> <span data-ttu-id="e8d22-138">The address of the Azure Stack portal depends on which Azure Stack product you are connecting to:</span><span class="sxs-lookup"><span data-stu-id="e8d22-138">The address of the Azure Stack portal depends on which Azure Stack product you are connecting to:</span></span>

* <span data-ttu-id="e8d22-139">For Azure Stack Development Kit (ASDK) go to: https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="e8d22-139">For Azure Stack Development Kit (ASDK) go to: https://portal.local.azurestack.external.</span></span>
* <span data-ttu-id="e8d22-140">For an Azure Stack integrated system, go to the URL that your Azure Stack operator provided.</span><span class="sxs-lookup"><span data-stu-id="e8d22-140">For an Azure Stack integrated system, go to the URL that your Azure Stack operator provided.</span></span>

## <a name="create-the-virtual-machine"></a><span data-ttu-id="e8d22-141">Create the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e8d22-141">Create the virtual machine</span></span>

1. <span data-ttu-id="e8d22-142">Click **Create a resource** in the upper left-hand corner of the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="e8d22-142">Click **Create a resource** in the upper left-hand corner of the Azure Stack portal.</span></span>

2. <span data-ttu-id="e8d22-143">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-143">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span>
   
   ![Slect the Linux server](media/azure-stack-quick-linux-portal/select.png)
1. <span data-ttu-id="e8d22-145">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-145">Click **Create**.</span></span>

4. <span data-ttu-id="e8d22-146">Type the virtual machine information.</span><span class="sxs-lookup"><span data-stu-id="e8d22-146">Type the virtual machine information.</span></span> <span data-ttu-id="e8d22-147">For **Authentication type**, select **SSH public key**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-147">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="e8d22-148">Paste in the SSH public key that you saved, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-148">Paste in the SSH public key that you saved, and then click **OK**.</span></span>

   >[!NOTE]
 <span data-ttu-id="e8d22-149">Make sure you remove any leading or trailing white space for they key.</span><span class="sxs-lookup"><span data-stu-id="e8d22-149">Make sure you remove any leading or trailing white space for they key.</span></span>

   ![Basics panel - Configure virtual machine](media/azure-stack-quick-linux-portal/linux-01.PNG)

5. <span data-ttu-id="e8d22-151">Select **D1** for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-151">Select **D1** for the virtual machine.</span></span>

   ![Size panel - Choose a virtual machine size](media/azure-stack-quick-linux-portal/linux-02.PNG)

6. <span data-ttu-id="e8d22-153">On the **Settings** page, make any desired changes to the defaults.</span><span class="sxs-lookup"><span data-stu-id="e8d22-153">On the **Settings** page, make any desired changes to the defaults.</span></span>
   
    - <span data-ttu-id="e8d22-154">Beginning with Azure Stack version 1808, you can configure **Storage** where you can choose to use *managed disks*.</span><span class="sxs-lookup"><span data-stu-id="e8d22-154">Beginning with Azure Stack version 1808, you can configure **Storage** where you can choose to use *managed disks*.</span></span> <span data-ttu-id="e8d22-155">Prior to version 1808 only unmanaged disks can be used.</span><span class="sxs-lookup"><span data-stu-id="e8d22-155">Prior to version 1808 only unmanaged disks can be used.</span></span>    
      <span data-ttu-id="e8d22-156">![Configure storage for managed disks](media/azure-stack-quick-linux-portal/linux-03.PNG)</span><span class="sxs-lookup"><span data-stu-id="e8d22-156">![Configure storage for managed disks](media/azure-stack-quick-linux-portal/linux-03.PNG)</span></span>
    
    <span data-ttu-id="e8d22-157">When your configurations are ready, select **OK** to continue.</span><span class="sxs-lookup"><span data-stu-id="e8d22-157">When your configurations are ready, select **OK** to continue.</span></span>

7. <span data-ttu-id="e8d22-158">On the **Summary** page, click **OK** to start the virtual machine deployment.</span><span class="sxs-lookup"><span data-stu-id="e8d22-158">On the **Summary** page, click **OK** to start the virtual machine deployment.</span></span>  
   <span data-ttu-id="e8d22-159">![Deploy](media/azure-stack-quick-linux-portal/deploy.png)</span><span class="sxs-lookup"><span data-stu-id="e8d22-159">![Deploy](media/azure-stack-quick-linux-portal/deploy.png)</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="e8d22-160">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e8d22-160">Connect to the virtual machine</span></span>

1. <span data-ttu-id="e8d22-161">Click **Connect** on the virtual machine page.</span><span class="sxs-lookup"><span data-stu-id="e8d22-161">Click **Connect** on the virtual machine page.</span></span> <span data-ttu-id="e8d22-162">This displays an SSH connection string that you need to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-162">This displays an SSH connection string that you need to connect to the virtual machine.</span></span> 

2. <span data-ttu-id="e8d22-163">Open PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e8d22-163">Open PuTTY.</span></span>

3. <span data-ttu-id="e8d22-164">On the **PuTTY Configuration** screen you will use the **Category** window to scroll up or down.</span><span class="sxs-lookup"><span data-stu-id="e8d22-164">On the **PuTTY Configuration** screen you will use the **Category** window to scroll up or down.</span></span> <span data-ttu-id="e8d22-165">Scroll down to **SSH**, expand **SSH**, and then click **Auth**. Click **Browse** and pick the private key file that you saved.</span><span class="sxs-lookup"><span data-stu-id="e8d22-165">Scroll down to **SSH**, expand **SSH**, and then click **Auth**. Click **Browse** and pick the private key file that you saved.</span></span>
   <span data-ttu-id="e8d22-166">![Connect virtual machine](media/azure-stack-quick-linux-portal/putty03.PNG)</span><span class="sxs-lookup"><span data-stu-id="e8d22-166">![Connect virtual machine](media/azure-stack-quick-linux-portal/putty03.PNG)</span></span>

4. <span data-ttu-id="e8d22-167">Scroll up in the **Category** window, and then click **Session**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-167">Scroll up in the **Category** window, and then click **Session**.</span></span>
5. <span data-ttu-id="e8d22-168">In the **Host Name (or IP address)** box, paste the connection string shown in the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="e8d22-168">In the **Host Name (or IP address)** box, paste the connection string shown in the Azure Stack portal.</span></span> <span data-ttu-id="e8d22-169">In this example, the string is ```asadmin@192.168.102.34```.</span><span class="sxs-lookup"><span data-stu-id="e8d22-169">In this example, the string is ```asadmin@192.168.102.34```.</span></span>

   ![PuTTY configuration connection string](media/azure-stack-quick-linux-portal/Putty04.PNG)

6. <span data-ttu-id="e8d22-171">Click **Open** to open a session for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-171">Click **Open** to open a session for the virtual machine.</span></span>

   ![Linux session](media/azure-stack-quick-linux-portal/Putty05.PNG)

## <a name="install-the-nginx-web-server"></a><span data-ttu-id="e8d22-173">Install the NGINX web server</span><span class="sxs-lookup"><span data-stu-id="e8d22-173">Install the NGINX web server</span></span>

<span data-ttu-id="e8d22-174">Use the following bash commands to update package sources and install the latest NGINX package on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-174">Use the following bash commands to update package sources and install the latest NGINX package on the virtual machine.</span></span>

```bash
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="e8d22-175">When you finish installing NGINX, close the SSH session and open the virtual machine Overview page in the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="e8d22-175">When you finish installing NGINX, close the SSH session and open the virtual machine Overview page in the Azure Stack portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="e8d22-176">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="e8d22-176">Open port 80 for web traffic</span></span>

<span data-ttu-id="e8d22-177">A Network security group (NSG) secures inbound and outbound traffic.</span><span class="sxs-lookup"><span data-stu-id="e8d22-177">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="e8d22-178">When a virtual machine is created in the Azure Stack portal, an inbound rule is created on port 22 for SSH connections.</span><span class="sxs-lookup"><span data-stu-id="e8d22-178">When a virtual machine is created in the Azure Stack portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="e8d22-179">Because this virtual machine hosts a web server, an NSG rule needs to be created to allow web traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="e8d22-179">Because this virtual machine hosts a web server, an NSG rule needs to be created to allow web traffic on port 80.</span></span>

1. <span data-ttu-id="e8d22-180">On the virtual machine **Overview** page, click the name of the **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-180">On the virtual machine **Overview** page, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="e8d22-181">Select the **network security group** for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d22-181">Select the **network security group** for the virtual machine.</span></span> <span data-ttu-id="e8d22-182">The NSG can be identified using the **Type** column.</span><span class="sxs-lookup"><span data-stu-id="e8d22-182">The NSG can be identified using the **Type** column.</span></span>
3. <span data-ttu-id="e8d22-183">On the left-hand menu, under **Settings**, click **Inbound security rules**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-183">On the left-hand menu, under **Settings**, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="e8d22-184">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-184">Click **Add**.</span></span>
5. <span data-ttu-id="e8d22-185">In **Name**, type **http**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-185">In **Name**, type **http**.</span></span> <span data-ttu-id="e8d22-186">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-186">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span>
6. <span data-ttu-id="e8d22-187">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="e8d22-187">Click **OK**</span></span>

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="e8d22-188">View the NGINX welcome page</span><span class="sxs-lookup"><span data-stu-id="e8d22-188">View the NGINX welcome page</span></span>

<span data-ttu-id="e8d22-189">With NGINX installed, and port 80 open on your virtual machine, you can access the web server using the virtual machine's public IP address.</span><span class="sxs-lookup"><span data-stu-id="e8d22-189">With NGINX installed, and port 80 open on your virtual machine, you can access the web server using the virtual machine's public IP address.</span></span> <span data-ttu-id="e8d22-190">(The public IP address is shown on the virtual machine's Overview page.)</span><span class="sxs-lookup"><span data-stu-id="e8d22-190">(The public IP address is shown on the virtual machine's Overview page.)</span></span>

<span data-ttu-id="e8d22-191">Open a web browser, and browse to ```http://<public IP address>```.</span><span class="sxs-lookup"><span data-stu-id="e8d22-191">Open a web browser, and browse to ```http://<public IP address>```.</span></span>

![NGINX web server Welcome page](media/azure-stack-quick-linux-portal/linux-05.PNG)

## <a name="clean-up-resources"></a><span data-ttu-id="e8d22-193">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e8d22-193">Clean up resources</span></span>

<span data-ttu-id="e8d22-194">Clean up the resources that you don't need any longer.</span><span class="sxs-lookup"><span data-stu-id="e8d22-194">Clean up the resources that you don't need any longer.</span></span> <span data-ttu-id="e8d22-195">To delete the virtual machine and its resources, select the resource group on the virtual machine page and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e8d22-195">To delete the virtual machine and its resources, select the resource group on the virtual machine page and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8d22-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8d22-196">Next steps</span></span>

<span data-ttu-id="e8d22-197">In this quick start, you deployed a basic Linux server virtual machine with a web server.</span><span class="sxs-lookup"><span data-stu-id="e8d22-197">In this quick start, you deployed a basic Linux server virtual machine with a web server.</span></span> <span data-ttu-id="e8d22-198">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="e8d22-198">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span></span>
