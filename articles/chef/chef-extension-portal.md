---
title: Install the Chef client from the Azure portal
description: Learn how to deploy and configure your Chef client from the Azure portal
keywords: azure, chef, devops, client, install, portal
ms.service: virtual-machines-linux
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.date: 05/15/2018
ms.topic: article
ms.openlocfilehash: e121cd038b8becee1e9c4c12659dbbee0696a9f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868084"
---
# <a name="install-the-chef-client-from-the-azure-portal"></a><span data-ttu-id="e4aa5-104">Install the Chef client from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4aa5-104">Install the Chef client from the Azure portal</span></span>
<span data-ttu-id="e4aa5-105">When creating or modifying a Linux or Windows virtual machine from the Azure portal, you can add the Chef extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-105">When creating or modifying a Linux or Windows virtual machine from the Azure portal, you can add the Chef extension to the virtual machine.</span></span> <span data-ttu-id="e4aa5-106">This article walks you through that process using a new Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-106">This article walks you through that process using a new Linux virtual machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4aa5-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4aa5-107">Prerequisites</span></span>
- <span data-ttu-id="e4aa5-108">**Azure subscription**: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-108">**Azure subscription**: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>

- <span data-ttu-id="e4aa5-109">**Chef**: If you don't have an active Chef account, sign up for a [free trial of Hosted Chef](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="e4aa5-109">**Chef**: If you don't have an active Chef account, sign up for a [free trial of Hosted Chef](https://manage.chef.io/signup).</span></span> <span data-ttu-id="e4aa5-110">To follow along with the instructions in this article, you'll need the following values from your Chef account:</span><span class="sxs-lookup"><span data-stu-id="e4aa5-110">To follow along with the instructions in this article, you'll need the following values from your Chef account:</span></span> 
    - <span data-ttu-id="e4aa5-111">organization_validation key</span><span class="sxs-lookup"><span data-stu-id="e4aa5-111">organization_validation key</span></span>
    - <span data-ttu-id="e4aa5-112">rb</span><span class="sxs-lookup"><span data-stu-id="e4aa5-112">rb</span></span>
    - <span data-ttu-id="e4aa5-113">run_list</span><span class="sxs-lookup"><span data-stu-id="e4aa5-113">run_list</span></span>

## <a name="install-the-chef-extension-on-a-new-linux-virtual-machine"></a><span data-ttu-id="e4aa5-114">Install the Chef extension on a new Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="e4aa5-114">Install the Chef extension on a new Linux virtual machine</span></span>
<span data-ttu-id="e4aa5-115">In this section, you'll first use the Azure portal to create a Linux machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-115">In this section, you'll first use the Azure portal to create a Linux machine.</span></span> <span data-ttu-id="e4aa5-116">During the process, you'll also see how to install the Chef extension on the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-116">During the process, you'll also see how to install the Chef extension on the new virtual machine.</span></span>

1. <span data-ttu-id="e4aa5-117">Browse to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e4aa5-117">Browse to the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="e4aa5-118">From the menu on the left, select the **Virtual machines** option.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-118">From the menu on the left, select the **Virtual machines** option.</span></span> <span data-ttu-id="e4aa5-119">If the **Virtual machines** option is not present, select **All services** and then select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-119">If the **Virtual machines** option is not present, select **All services** and then select **Virtual machines**.</span></span>

1. <span data-ttu-id="e4aa5-120">On the **Virtual machines** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-120">On the **Virtual machines** tab, select **Add**.</span></span>

    ![Add a new virtual machine in the Azure portal](./media/chef-extension-portal/add-vm.png)

1. <span data-ttu-id="e4aa5-122">On the **Compute** tab, select the desired operating system.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-122">On the **Compute** tab, select the desired operating system.</span></span> <span data-ttu-id="e4aa5-123">For this demo, **Ubuntu Server** is selected.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-123">For this demo, **Ubuntu Server** is selected.</span></span>

1. <span data-ttu-id="e4aa5-124">On the **Ubuntu Server** tab, select **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-124">On the **Ubuntu Server** tab, select **Ubuntu Server 16.04 LTS**.</span></span>

    ![When creating an Ubuntu virtual machine, specify the version you need](./media/chef-extension-portal/ubuntu-server-version.png)

1. <span data-ttu-id="e4aa5-126">On the **Ubuntu Server 16.04 LTS** tab, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-126">On the **Ubuntu Server 16.04 LTS** tab, select **Create**.</span></span>

    ![Ubuntu provides additional information about their product](./media/chef-extension-portal/create-vm.png)

1. <span data-ttu-id="e4aa5-128">On the **Create virtual machine** tab, select **Basics**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-128">On the **Create virtual machine** tab, select **Basics**.</span></span>

1. <span data-ttu-id="e4aa5-129">On the **Basics** tab, specify the following values, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-129">On the **Basics** tab, specify the following values, and then select **OK**.</span></span>

    - <span data-ttu-id="e4aa5-130">**Name** - Enter a name for the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-130">**Name** - Enter a name for the new virtual machine.</span></span>
    - <span data-ttu-id="e4aa5-131">**VM disk type** - Specify either **SSD** or **HDD** for the storage disk type.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-131">**VM disk type** - Specify either **SSD** or **HDD** for the storage disk type.</span></span> <span data-ttu-id="e4aa5-132">For more information about virtual machine disk types on Azure, see the article     [High-performance Premium Storage and managed disks for VMs](/azure/virtual-machines/windows/premium-storage).</span><span class="sxs-lookup"><span data-stu-id="e4aa5-132">For more information about virtual machine disk types on Azure, see the article     [High-performance Premium Storage and managed disks for VMs](/azure/virtual-machines/windows/premium-storage).</span></span>
    - <span data-ttu-id="e4aa5-133">**User name** - Enter a user name that is granted administrator privileges on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-133">**User name** - Enter a user name that is granted administrator privileges on the virtual machine.</span></span>
    - <span data-ttu-id="e4aa5-134">**Authentication type** - Select **Password**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-134">**Authentication type** - Select **Password**.</span></span> <span data-ttu-id="e4aa5-135">You can also select **SSH public key**, and supply an SSH public key value.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-135">You can also select **SSH public key**, and supply an SSH public key value.</span></span> <span data-ttu-id="e4aa5-136">For purposes of this demo (and in the screenshots), **Password** is selected.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-136">For purposes of this demo (and in the screenshots), **Password** is selected.</span></span>
    - <span data-ttu-id="e4aa5-137">**Password** and **Confirm password** - Enter a password for the user.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-137">**Password** and **Confirm password** - Enter a password for the user.</span></span>
    - <span data-ttu-id="e4aa5-138">**Log in with Azure Active Directory** - Select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-138">**Log in with Azure Active Directory** - Select **Disabled**.</span></span>
    - <span data-ttu-id="e4aa5-139">**Subscription** - Select the desired Azure subscription, if you have more than one.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-139">**Subscription** - Select the desired Azure subscription, if you have more than one.</span></span>
    - <span data-ttu-id="e4aa5-140">**Resource group** - Enter a name for your resource group.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-140">**Resource group** - Enter a name for your resource group.</span></span>
    - <span data-ttu-id="e4aa5-141">**Location** - Select **East US**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-141">**Location** - Select **East US**.</span></span>

    ![Basics tab for creating a virtual machine](./media/chef-extension-portal/add-vm-basics.png)

1. <span data-ttu-id="e4aa5-143">On the **Choose a size** tab, select the size for the virtual machine, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-143">On the **Choose a size** tab, select the size for the virtual machine, and then select **Select**.</span></span>

1. <span data-ttu-id="e4aa5-144">On the **Settings** tab, most of the values will be populated for you based on the values you selected in the previous tabs.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-144">On the **Settings** tab, most of the values will be populated for you based on the values you selected in the previous tabs.</span></span> <span data-ttu-id="e4aa5-145">Select **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-145">Select **Extensions**.</span></span>

    ![Extensions are added to virtual machines via the Settings tab](./media/chef-extension-portal/add-vm-select-extensions.png)

1. <span data-ttu-id="e4aa5-147">On the **Extensions** tab, select **Add extension**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-147">On the **Extensions** tab, select **Add extension**.</span></span>

    ![Select Add extension to add an extension to a virtual machine](./media/chef-extension-portal/add-vm-add-extension.png)

1. <span data-ttu-id="e4aa5-149">On the **New resource** tab, select **Linux Chef Extension (1.2.3)**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-149">On the **New resource** tab, select **Linux Chef Extension (1.2.3)**.</span></span>

    ![Chef has extensions for Linux and Windows virtual machines](./media/chef-extension-portal/select-linux-chef-extension.png)

1. <span data-ttu-id="e4aa5-151">On the **Linux Chef Extension** tab, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-151">On the **Linux Chef Extension** tab, select **Create**.</span></span>

1. <span data-ttu-id="e4aa5-152">On the **Install extension** tab, specify the following values, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-152">On the **Install extension** tab, specify the following values, and then select **OK**.</span></span>

    - <span data-ttu-id="e4aa5-153">**Chef Server URL** - Enter the Chef Server URL that includes the organization name, for example, *https://api.chef.io/organization/hessco*.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-153">**Chef Server URL** - Enter the Chef Server URL that includes the organization name, for example, *https://api.chef.io/organization/hessco*.</span></span>
    - <span data-ttu-id="e4aa5-154">**Chef Node Name** - Enter the Chef Node name.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-154">**Chef Node Name** - Enter the Chef Node name.</span></span> <span data-ttu-id="e4aa5-155">This can be any value.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-155">This can be any value.</span></span>
    - <span data-ttu-id="e4aa5-156">**Run List** - Enter the Chef run list that is added to the machine.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-156">**Run List** - Enter the Chef run list that is added to the machine.</span></span> <span data-ttu-id="e4aa5-157">This can be left blank.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-157">This can be left blank.</span></span>
    - <span data-ttu-id="e4aa5-158">**Validation Client Name** - Enter the Chef Validation Client Name.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-158">**Validation Client Name** - Enter the Chef Validation Client Name.</span></span> <span data-ttu-id="e4aa5-159">for example, *tarcher-validator*.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-159">for example, *tarcher-validator*.</span></span>
    - <span data-ttu-id="e4aa5-160">**Validation Key** - Select a file containing the validation key used when bootstrapping your machines.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-160">**Validation Key** - Select a file containing the validation key used when bootstrapping your machines.</span></span> 
    - <span data-ttu-id="e4aa5-161">**Client Configuration File** - Select a configuration file for chef-client.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-161">**Client Configuration File** - Select a configuration file for chef-client.</span></span> <span data-ttu-id="e4aa5-162">This can be left blank.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-162">This can be left blank.</span></span>
    - <span data-ttu-id="e4aa5-163">**Chef Client version** - Enter the version of the chef client to install.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-163">**Chef Client version** - Enter the version of the chef client to install.</span></span> <span data-ttu-id="e4aa5-164">This can be left blank.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-164">This can be left blank.</span></span> <span data-ttu-id="e4aa5-165">A blank value will cause the latest version to be installed.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-165">A blank value will cause the latest version to be installed.</span></span> 
    - <span data-ttu-id="e4aa5-166">**SSL Verification Mode** - Select either **None** or **Peer**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-166">**SSL Verification Mode** - Select either **None** or **Peer**.</span></span> <span data-ttu-id="e4aa5-167">*None* was selected for the demo.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-167">*None* was selected for the demo.</span></span>
    - <span data-ttu-id="e4aa5-168">**Chef Environment** - Enter the Chef environment this node should be a member of.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-168">**Chef Environment** - Enter the Chef environment this node should be a member of.</span></span> <span data-ttu-id="e4aa5-169">This can be left blank.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-169">This can be left blank.</span></span>
    - <span data-ttu-id="e4aa5-170">**Encrypted Databag Secret** - Select a file containing the secret for the Encrypted Databag this machine should have access to.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-170">**Encrypted Databag Secret** - Select a file containing the secret for the Encrypted Databag this machine should have access to.</span></span> <span data-ttu-id="e4aa5-171">This can be left blank.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-171">This can be left blank.</span></span>
    - <span data-ttu-id="e4aa5-172">**Chef Server SSL Certificate** - Select the SSL Certificate assigned to your Chef Server.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-172">**Chef Server SSL Certificate** - Select the SSL Certificate assigned to your Chef Server.</span></span> <span data-ttu-id="e4aa5-173">This can be left blank.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-173">This can be left blank.</span></span>

    ![Installing the Chef Server on a Linux virtual machine](./media/chef-extension-portal/install-extension.png)

1. <span data-ttu-id="e4aa5-175">When returning to the **Extensions** tab, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-175">When returning to the **Extensions** tab, select **OK**.</span></span>

1. <span data-ttu-id="e4aa5-176">When returning to the **Settings** tab, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-176">When returning to the **Settings** tab, select **OK**.</span></span>

1. <span data-ttu-id="e4aa5-177">When returning to the **Create** tab (this represents a summary of the options you selected and entered), verify the information as well as the **Terms of use**, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-177">When returning to the **Create** tab (this represents a summary of the options you selected and entered), verify the information as well as the **Terms of use**, and select **Create**.</span></span>

<span data-ttu-id="e4aa5-178">When the process of creating and deploying the virtual machine with the Chef Extension is complete, a notification indicates the success or failure of the operation.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-178">When the process of creating and deploying the virtual machine with the Chef Extension is complete, a notification indicates the success or failure of the operation.</span></span> <span data-ttu-id="e4aa5-179">In addition, the resource page for the new virtual machine automatically opens in the Azure portal once it's been created.</span><span class="sxs-lookup"><span data-stu-id="e4aa5-179">In addition, the resource page for the new virtual machine automatically opens in the Azure portal once it's been created.</span></span>

![Installing the Chef Server on a Linux virtual machine](./media/chef-extension-portal/resource-created.png)

## <a name="next-steps"></a><span data-ttu-id="e4aa5-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4aa5-181">Next steps</span></span>
* [<span data-ttu-id="e4aa5-182">Create a Windows virtual machine on Azure using Chef</span><span class="sxs-lookup"><span data-stu-id="e4aa5-182">Create a Windows virtual machine on Azure using Chef</span></span>](/azure/virtual-machines/windows/chef-automation)
