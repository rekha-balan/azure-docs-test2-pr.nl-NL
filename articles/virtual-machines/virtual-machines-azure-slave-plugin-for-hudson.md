---
title: How to use the Azure slave plug-in with Hudson Continuous Integration | Microsoft Docs
description: Describes how to use the Azure slave plug-in with Hudson Continuous Integration.
services: virtual-machines-linux
documentationcenter: ''
author: rmcmurray
manager: wpickett
editor: ''
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 1c8ac0a2e632e457d2c8511b66e2dbfe4e1b4c2b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564406"
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="eba63-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span><span class="sxs-lookup"><span data-stu-id="eba63-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="eba63-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span><span class="sxs-lookup"><span data-stu-id="eba63-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="eba63-105">Install the Azure Slave plug-in</span><span class="sxs-lookup"><span data-stu-id="eba63-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="eba63-106">In the Hudson dashboard, click **Manage Hudson**.</span><span class="sxs-lookup"><span data-stu-id="eba63-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="eba63-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span><span class="sxs-lookup"><span data-stu-id="eba63-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="eba63-108">Click the **Available** tab.</span><span class="sxs-lookup"><span data-stu-id="eba63-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="eba63-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span><span class="sxs-lookup"><span data-stu-id="eba63-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="eba63-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span><span class="sxs-lookup"><span data-stu-id="eba63-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="eba63-111">Select the checkbox for **Azure Slave Plugin**.</span><span class="sxs-lookup"><span data-stu-id="eba63-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="eba63-112">Click **Install**.</span><span class="sxs-lookup"><span data-stu-id="eba63-112">Click **Install**.</span></span>
7. <span data-ttu-id="eba63-113">Restart Hudson.</span><span class="sxs-lookup"><span data-stu-id="eba63-113">Restart Hudson.</span></span>

<span data-ttu-id="eba63-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span><span class="sxs-lookup"><span data-stu-id="eba63-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="eba63-115">Configure the Azure Slave plug-in with your subscription profile</span><span class="sxs-lookup"><span data-stu-id="eba63-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="eba63-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span><span class="sxs-lookup"><span data-stu-id="eba63-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="eba63-117">To configure the Azure slave plug-in, you need:</span><span class="sxs-lookup"><span data-stu-id="eba63-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="eba63-118">Your subscription id</span><span class="sxs-lookup"><span data-stu-id="eba63-118">Your subscription id</span></span>
* <span data-ttu-id="eba63-119">A management certificate for your subscription</span><span class="sxs-lookup"><span data-stu-id="eba63-119">A management certificate for your subscription</span></span>

<span data-ttu-id="eba63-120">These can be found in your [subscription profile].</span><span class="sxs-lookup"><span data-stu-id="eba63-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="eba63-121">Below is an example of a subscription profile.</span><span class="sxs-lookup"><span data-stu-id="eba63-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="eba63-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span><span class="sxs-lookup"><span data-stu-id="eba63-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="eba63-123">In the Hudson dashboard, click **Manage Hudson**.</span><span class="sxs-lookup"><span data-stu-id="eba63-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="eba63-124">Click **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="eba63-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="eba63-125">Scroll down the page to find the **Cloud** section.</span><span class="sxs-lookup"><span data-stu-id="eba63-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="eba63-126">Click **Add new cloud > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="eba63-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![add new cloud][add new cloud]
   
    <span data-ttu-id="eba63-128">This will show the fields where you need to enter your subscription details.</span><span class="sxs-lookup"><span data-stu-id="eba63-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![configure profile][configure profile]
5. <span data-ttu-id="eba63-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span><span class="sxs-lookup"><span data-stu-id="eba63-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="eba63-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span><span class="sxs-lookup"><span data-stu-id="eba63-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="eba63-132">Click on **Verify configuration**.</span><span class="sxs-lookup"><span data-stu-id="eba63-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="eba63-133">When the configuration is verified successfully, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="eba63-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="eba63-134">Set up a virtual machine template for the Azure Slave plug-in</span><span class="sxs-lookup"><span data-stu-id="eba63-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="eba63-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span><span class="sxs-lookup"><span data-stu-id="eba63-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="eba63-136">In the following steps we'll be creating template for an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="eba63-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="eba63-137">In the Hudson dashboard, click **Manage Hudson**.</span><span class="sxs-lookup"><span data-stu-id="eba63-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="eba63-138">Click on **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="eba63-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="eba63-139">Scroll down the page to find the **Cloud** section.</span><span class="sxs-lookup"><span data-stu-id="eba63-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="eba63-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="eba63-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![add vm template][add vm template]
5. <span data-ttu-id="eba63-142">Specify a cloud service name in the **Name** field.</span><span class="sxs-lookup"><span data-stu-id="eba63-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="eba63-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span><span class="sxs-lookup"><span data-stu-id="eba63-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="eba63-144">Otherwise, Azure will create a new one.</span><span class="sxs-lookup"><span data-stu-id="eba63-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="eba63-145">In the **Description** field, enter text that describes the template you are creating.</span><span class="sxs-lookup"><span data-stu-id="eba63-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="eba63-146">This information is only for documentary purposes and is not used in provisioning a VM.</span><span class="sxs-lookup"><span data-stu-id="eba63-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="eba63-147">In the **Labels** field, enter **linux**.</span><span class="sxs-lookup"><span data-stu-id="eba63-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="eba63-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span><span class="sxs-lookup"><span data-stu-id="eba63-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="eba63-149">Select a region where the VM will be created.</span><span class="sxs-lookup"><span data-stu-id="eba63-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="eba63-150">Select the appropriate VM size.</span><span class="sxs-lookup"><span data-stu-id="eba63-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="eba63-151">Specify a storage account where the VM will be created.</span><span class="sxs-lookup"><span data-stu-id="eba63-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="eba63-152">Make sure that it is in the same region as the cloud service you'll be using.</span><span class="sxs-lookup"><span data-stu-id="eba63-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="eba63-153">If you want new storage to be created, you can leave this field blank.</span><span class="sxs-lookup"><span data-stu-id="eba63-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="eba63-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span><span class="sxs-lookup"><span data-stu-id="eba63-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="eba63-155">Leave this at the default value of 60.</span><span class="sxs-lookup"><span data-stu-id="eba63-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="eba63-156">In **Usage**, select the appropriate condition when this slave node will be used.</span><span class="sxs-lookup"><span data-stu-id="eba63-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="eba63-157">For now, select **Utilize this node as much as possible**.</span><span class="sxs-lookup"><span data-stu-id="eba63-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="eba63-158">At this point, your form would look somewhat similar to this:</span><span class="sxs-lookup"><span data-stu-id="eba63-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![template config][template config]
13. <span data-ttu-id="eba63-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span><span class="sxs-lookup"><span data-stu-id="eba63-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="eba63-161">You can either select from a list of image families or specify a custom image.</span><span class="sxs-lookup"><span data-stu-id="eba63-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="eba63-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span><span class="sxs-lookup"><span data-stu-id="eba63-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="eba63-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span><span class="sxs-lookup"><span data-stu-id="eba63-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="eba63-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span><span class="sxs-lookup"><span data-stu-id="eba63-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![OS family list][OS family list]
    
     <span data-ttu-id="eba63-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span><span class="sxs-lookup"><span data-stu-id="eba63-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="eba63-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span><span class="sxs-lookup"><span data-stu-id="eba63-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="eba63-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="eba63-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="eba63-169">For **Launch method**, select **SSH**.</span><span class="sxs-lookup"><span data-stu-id="eba63-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="eba63-170">Copy the script below and paste in the **Init script** field.</span><span class="sxs-lookup"><span data-stu-id="eba63-170">Copy the script below and paste in the **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="eba63-171">The **Init script** will be executed after the VM is created.</span><span class="sxs-lookup"><span data-stu-id="eba63-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="eba63-172">In this example, the script installs Java, git, and ant.</span><span class="sxs-lookup"><span data-stu-id="eba63-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="eba63-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span><span class="sxs-lookup"><span data-stu-id="eba63-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="eba63-174">Click on **Verify Template** to check if the parameters you specified are valid.</span><span class="sxs-lookup"><span data-stu-id="eba63-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="eba63-175">Click on **Save**.</span><span class="sxs-lookup"><span data-stu-id="eba63-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="eba63-176">Create a Hudson job that runs on a slave node on Azure</span><span class="sxs-lookup"><span data-stu-id="eba63-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="eba63-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span><span class="sxs-lookup"><span data-stu-id="eba63-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="eba63-178">In the Hudson dashboard, click **New Job**.</span><span class="sxs-lookup"><span data-stu-id="eba63-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="eba63-179">Enter a name for the job you are creating.</span><span class="sxs-lookup"><span data-stu-id="eba63-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="eba63-180">For the job type, select **Build a free-style software job**.</span><span class="sxs-lookup"><span data-stu-id="eba63-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="eba63-181">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eba63-181">Click **OK**.</span></span>
5. <span data-ttu-id="eba63-182">In the job configuration page, select **Restrict where this project can be run**.</span><span class="sxs-lookup"><span data-stu-id="eba63-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="eba63-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span><span class="sxs-lookup"><span data-stu-id="eba63-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="eba63-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span><span class="sxs-lookup"><span data-stu-id="eba63-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="eba63-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span><span class="sxs-lookup"><span data-stu-id="eba63-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="eba63-186">Click on **Save**.</span><span class="sxs-lookup"><span data-stu-id="eba63-186">Click on **Save**.</span></span>
10. <span data-ttu-id="eba63-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span><span class="sxs-lookup"><span data-stu-id="eba63-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="eba63-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span><span class="sxs-lookup"><span data-stu-id="eba63-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eba63-189">Next Steps</span><span class="sxs-lookup"><span data-stu-id="eba63-189">Next Steps</span></span>
<span data-ttu-id="eba63-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="eba63-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png






