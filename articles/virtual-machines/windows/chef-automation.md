---
title: Azure virtual machine deployment with Chef | Microsoft Docs
description: Learn how to use Chef to do automated virtual machine deployment and configuration on Microsoft Azure
services: virtual-machines-windows
documentationcenter: ''
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: ''
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/19/2015
ms.author: diviso
ms.openlocfilehash: 50b8b7d05db8184d1902ff15929702838c940cf1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552072"
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="496c8-103">Automating Azure virtual machine deployment with Chef</span><span class="sxs-lookup"><span data-stu-id="496c8-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="496c8-104">Chef is a great tool for delivering automation and desired state configurations.</span><span class="sxs-lookup"><span data-stu-id="496c8-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="496c8-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span><span class="sxs-lookup"><span data-stu-id="496c8-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="496c8-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="496c8-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="496c8-107">Let’s begin!</span><span class="sxs-lookup"><span data-stu-id="496c8-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="496c8-108">Chef basics</span><span class="sxs-lookup"><span data-stu-id="496c8-108">Chef basics</span></span>
<span data-ttu-id="496c8-109">Before you begin, I suggest you review the basic concepts of Chef.</span><span class="sxs-lookup"><span data-stu-id="496c8-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="496c8-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="496c8-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="496c8-111">I will however recap the basics before we get started.</span><span class="sxs-lookup"><span data-stu-id="496c8-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="496c8-112">The following diagram depicts the high-level Chef architecture.</span><span class="sxs-lookup"><span data-stu-id="496c8-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="496c8-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span><span class="sxs-lookup"><span data-stu-id="496c8-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="496c8-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span><span class="sxs-lookup"><span data-stu-id="496c8-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="496c8-115">We will be using a hosted solution.</span><span class="sxs-lookup"><span data-stu-id="496c8-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="496c8-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span><span class="sxs-lookup"><span data-stu-id="496c8-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="496c8-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span><span class="sxs-lookup"><span data-stu-id="496c8-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="496c8-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span><span class="sxs-lookup"><span data-stu-id="496c8-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="496c8-119">There is also the concept of “Cookbooks” and “Recipes”.</span><span class="sxs-lookup"><span data-stu-id="496c8-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="496c8-120">These are effectively the policies we define and apply to our servers.</span><span class="sxs-lookup"><span data-stu-id="496c8-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="496c8-121">Preparing the workstation</span><span class="sxs-lookup"><span data-stu-id="496c8-121">Preparing the workstation</span></span>
<span data-ttu-id="496c8-122">First, lets prep the workstation.</span><span class="sxs-lookup"><span data-stu-id="496c8-122">First, lets prep the workstation.</span></span> <span data-ttu-id="496c8-123">I’m using a standard Windows workstation.</span><span class="sxs-lookup"><span data-stu-id="496c8-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="496c8-124">We need to create a directory to store our config files and cookbooks.</span><span class="sxs-lookup"><span data-stu-id="496c8-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="496c8-125">First create a directory called C:\chef.</span><span class="sxs-lookup"><span data-stu-id="496c8-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="496c8-126">Then create a second directory called c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="496c8-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="496c8-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="496c8-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<span data-ttu-id="496c8-128">Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="496c8-128">Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).</span></span>

<span data-ttu-id="496c8-129">Save the publish settings file in C:\chef.</span><span class="sxs-lookup"><span data-stu-id="496c8-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="496c8-130">Creating a managed Chef account</span><span class="sxs-lookup"><span data-stu-id="496c8-130">Creating a managed Chef account</span></span>
<span data-ttu-id="496c8-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="496c8-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="496c8-132">During the signup process, you will be asked to create a new organization.</span><span class="sxs-lookup"><span data-stu-id="496c8-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="496c8-133">Once your organization is created, download the starter kit.</span><span class="sxs-lookup"><span data-stu-id="496c8-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="496c8-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span><span class="sxs-lookup"><span data-stu-id="496c8-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="496c8-135">This starter kit zip file contains your organization config files and keys.</span><span class="sxs-lookup"><span data-stu-id="496c8-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="496c8-136">Configuring the Chef workstation</span><span class="sxs-lookup"><span data-stu-id="496c8-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="496c8-137">Extract the content of the chef-starter.zip to C:\chef.</span><span class="sxs-lookup"><span data-stu-id="496c8-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="496c8-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span><span class="sxs-lookup"><span data-stu-id="496c8-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="496c8-139">Your directory should now look something like the following example.</span><span class="sxs-lookup"><span data-stu-id="496c8-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="496c8-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span><span class="sxs-lookup"><span data-stu-id="496c8-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="496c8-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span><span class="sxs-lookup"><span data-stu-id="496c8-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="496c8-142">We will need to edit the knife.rb file.</span><span class="sxs-lookup"><span data-stu-id="496c8-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="496c8-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span><span class="sxs-lookup"><span data-stu-id="496c8-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="496c8-144">Also add the following line reflecting the name of your Azure publish settings file.</span><span class="sxs-lookup"><span data-stu-id="496c8-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="496c8-145">Your knife.rb file should now look similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="496c8-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="496c8-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span><span class="sxs-lookup"><span data-stu-id="496c8-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="496c8-147">Installing the Chef Development Kit</span><span class="sxs-lookup"><span data-stu-id="496c8-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="496c8-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span><span class="sxs-lookup"><span data-stu-id="496c8-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="496c8-149">Install in the default location of c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="496c8-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="496c8-150">This install will take around 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="496c8-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="496c8-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="496c8-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="496c8-152">If they are not there, make sure you add these paths!</span><span class="sxs-lookup"><span data-stu-id="496c8-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="496c8-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span><span class="sxs-lookup"><span data-stu-id="496c8-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="496c8-154">If your opscode paths are not in the correct order you will have issues.</span><span class="sxs-lookup"><span data-stu-id="496c8-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="496c8-155">Reboot your workstation before you continue.</span><span class="sxs-lookup"><span data-stu-id="496c8-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="496c8-156">Next, we will install the Knife Azure extension.</span><span class="sxs-lookup"><span data-stu-id="496c8-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="496c8-157">This provides Knife with the “Azure Plugin”.</span><span class="sxs-lookup"><span data-stu-id="496c8-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="496c8-158">Run the following command.</span><span class="sxs-lookup"><span data-stu-id="496c8-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="496c8-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span><span class="sxs-lookup"><span data-stu-id="496c8-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="496c8-160">It’s likely that a number of dependencies will also be installed at the same time.</span><span class="sxs-lookup"><span data-stu-id="496c8-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="496c8-161">To ensure everything is configured correctly, run the following command.</span><span class="sxs-lookup"><span data-stu-id="496c8-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="496c8-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span><span class="sxs-lookup"><span data-stu-id="496c8-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="496c8-163">Congratulations.</span><span class="sxs-lookup"><span data-stu-id="496c8-163">Congratulations.</span></span> <span data-ttu-id="496c8-164">The workstation is set up!</span><span class="sxs-lookup"><span data-stu-id="496c8-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="496c8-165">Creating a Cookbook</span><span class="sxs-lookup"><span data-stu-id="496c8-165">Creating a Cookbook</span></span>
<span data-ttu-id="496c8-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span><span class="sxs-lookup"><span data-stu-id="496c8-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="496c8-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span><span class="sxs-lookup"><span data-stu-id="496c8-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="496c8-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span><span class="sxs-lookup"><span data-stu-id="496c8-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="496c8-169">Under your C:\Chef directory run the following command.</span><span class="sxs-lookup"><span data-stu-id="496c8-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="496c8-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="496c8-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="496c8-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span><span class="sxs-lookup"><span data-stu-id="496c8-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="496c8-172">The commands are stored in the file default.rb.</span><span class="sxs-lookup"><span data-stu-id="496c8-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="496c8-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span><span class="sxs-lookup"><span data-stu-id="496c8-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="496c8-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span><span class="sxs-lookup"><span data-stu-id="496c8-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="496c8-175">Save the file once you are done.</span><span class="sxs-lookup"><span data-stu-id="496c8-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="496c8-176">Creating a template</span><span class="sxs-lookup"><span data-stu-id="496c8-176">Creating a template</span></span>
<span data-ttu-id="496c8-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span><span class="sxs-lookup"><span data-stu-id="496c8-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="496c8-178">Run the following command to generate the template.</span><span class="sxs-lookup"><span data-stu-id="496c8-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="496c8-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span><span class="sxs-lookup"><span data-stu-id="496c8-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="496c8-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span><span class="sxs-lookup"><span data-stu-id="496c8-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="496c8-181">Upload the Cookbook to the Chef Server</span><span class="sxs-lookup"><span data-stu-id="496c8-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="496c8-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span><span class="sxs-lookup"><span data-stu-id="496c8-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="496c8-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span><span class="sxs-lookup"><span data-stu-id="496c8-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="496c8-184">Deploy a virtual machine with Knife Azure</span><span class="sxs-lookup"><span data-stu-id="496c8-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="496c8-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span><span class="sxs-lookup"><span data-stu-id="496c8-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="496c8-186">In order to do this, use the **knife azure server create** command.</span><span class="sxs-lookup"><span data-stu-id="496c8-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="496c8-187">Am example of the command appears next.</span><span class="sxs-lookup"><span data-stu-id="496c8-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="496c8-188">The parameters are self-explanatory.</span><span class="sxs-lookup"><span data-stu-id="496c8-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="496c8-189">Substitute your particular variables and run.</span><span class="sxs-lookup"><span data-stu-id="496c8-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="496c8-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span><span class="sxs-lookup"><span data-stu-id="496c8-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="496c8-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span><span class="sxs-lookup"><span data-stu-id="496c8-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="496c8-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span><span class="sxs-lookup"><span data-stu-id="496c8-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="496c8-193">The command prompt appears next.</span><span class="sxs-lookup"><span data-stu-id="496c8-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="496c8-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span><span class="sxs-lookup"><span data-stu-id="496c8-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="496c8-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span><span class="sxs-lookup"><span data-stu-id="496c8-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="496c8-196">As you can see, I got creative with my HTML code.</span><span class="sxs-lookup"><span data-stu-id="496c8-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="496c8-197">Don’t forget we can also connect through an RDP session from the Azure classic portal via port 3389.</span><span class="sxs-lookup"><span data-stu-id="496c8-197">Don’t forget we can also connect through an RDP session from the Azure classic portal via port 3389.</span></span>

<span data-ttu-id="496c8-198">I hope this has been helpful!</span><span class="sxs-lookup"><span data-stu-id="496c8-198">I hope this has been helpful!</span></span> <span data-ttu-id="496c8-199">Go  and start your infrastructure as code journey with Azure today!</span><span class="sxs-lookup"><span data-stu-id="496c8-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/11.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/chef-automation/13.png


<!--Link references-->











