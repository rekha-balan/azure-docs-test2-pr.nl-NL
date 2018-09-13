---
title: Deploy a Node.js application to Linux Virtual Machines in Azure
description: Learn how to deploy a Node.js application to Linux virtual machines in Azure.
services: ''
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: ''
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563073"
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a><span data-ttu-id="30c4b-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span><span class="sxs-lookup"><span data-stu-id="30c4b-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span></span>
<span data-ttu-id="30c4b-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span><span class="sxs-lookup"><span data-stu-id="30c4b-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="30c4b-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span><span class="sxs-lookup"><span data-stu-id="30c4b-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="30c4b-106">You'll learn how to:</span><span class="sxs-lookup"><span data-stu-id="30c4b-106">You'll learn how to:</span></span>

* <span data-ttu-id="30c4b-107">Fork and clone a GitHub repository containing a simple TODO application;</span><span class="sxs-lookup"><span data-stu-id="30c4b-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="30c4b-108">Create and configure two Linux virtual machines in Azure to run the application;</span><span class="sxs-lookup"><span data-stu-id="30c4b-108">Create and configure two Linux virtual machines in Azure to run the application;</span></span>
* <span data-ttu-id="30c4b-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="30c4b-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span></span>
> 
> <span data-ttu-id="30c4b-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="30c4b-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="30c4b-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30c4b-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="30c4b-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span><span class="sxs-lookup"><span data-stu-id="30c4b-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="30c4b-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="30c4b-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="30c4b-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="30c4b-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="30c4b-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="30c4b-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a><span data-ttu-id="30c4b-117">Forking and Cloning the TODO Application</span><span class="sxs-lookup"><span data-stu-id="30c4b-117">Forking and Cloning the TODO Application</span></span>
<span data-ttu-id="30c4b-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span><span class="sxs-lookup"><span data-stu-id="30c4b-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="30c4b-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span><span class="sxs-lookup"><span data-stu-id="30c4b-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span></span> <span data-ttu-id="30c4b-120">This should create a repository in your account named *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="30c4b-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="30c4b-121">Now on your development machine, clone this repository:</span><span class="sxs-lookup"><span data-stu-id="30c4b-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="30c4b-122">We'll use this local clone of the repository a little later when making changes to the source code.</span><span class="sxs-lookup"><span data-stu-id="30c4b-122">We'll use this local clone of the repository a little later when making changes to the source code.</span></span>

## <a name="creating-and-configuring-the-linux-virtual-machines"></a><span data-ttu-id="30c4b-123">Creating and Configuring the Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="30c4b-123">Creating and Configuring the Linux Virtual Machines</span></span>
<span data-ttu-id="30c4b-124">Azure has great support for raw compute using Linux virtual machines.</span><span class="sxs-lookup"><span data-stu-id="30c4b-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="30c4b-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span><span class="sxs-lookup"><span data-stu-id="30c4b-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="30c4b-126">Creating Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="30c4b-126">Creating Virtual Machines</span></span>
<span data-ttu-id="30c4b-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="30c4b-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span></span> <span data-ttu-id="30c4b-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span><span class="sxs-lookup"><span data-stu-id="30c4b-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span></span> <span data-ttu-id="30c4b-129">Once the Azure Portal has loaded, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="30c4b-129">Once the Azure Portal has loaded, complete the following steps:</span></span>

* <span data-ttu-id="30c4b-130">Click the "+ New" link;</span><span class="sxs-lookup"><span data-stu-id="30c4b-130">Click the "+ New" link;</span></span>
* <span data-ttu-id="30c4b-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="30c4b-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="30c4b-132">Select the "Resource Manager" deployment model and click "Create";</span><span class="sxs-lookup"><span data-stu-id="30c4b-132">Select the "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="30c4b-133">Fill in the basics following these guidelines:</span><span class="sxs-lookup"><span data-stu-id="30c4b-133">Fill in the basics following these guidelines:</span></span>
  * <span data-ttu-id="30c4b-134">Specify a name you can easily identify later;</span><span class="sxs-lookup"><span data-stu-id="30c4b-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="30c4b-135">For this tutorial, choose Password authentication;</span><span class="sxs-lookup"><span data-stu-id="30c4b-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="30c4b-136">Create a new resource group with an identifiable name.</span><span class="sxs-lookup"><span data-stu-id="30c4b-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="30c4b-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="30c4b-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="30c4b-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span><span class="sxs-lookup"><span data-stu-id="30c4b-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span></span>
* <span data-ttu-id="30c4b-139">Kick off the creation on the summary page.</span><span class="sxs-lookup"><span data-stu-id="30c4b-139">Kick off the creation on the summary page.</span></span>

<span data-ttu-id="30c4b-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span><span class="sxs-lookup"><span data-stu-id="30c4b-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span></span> <span data-ttu-id="30c4b-141">Creation of the virtual machines will take about 5-10 minutes.</span><span class="sxs-lookup"><span data-stu-id="30c4b-141">Creation of the virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="30c4b-142">Assigning a DNS entry for Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="30c4b-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="30c4b-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="30c4b-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="30c4b-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span><span class="sxs-lookup"><span data-stu-id="30c4b-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="30c4b-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span><span class="sxs-lookup"><span data-stu-id="30c4b-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span></span> <span data-ttu-id="30c4b-146">For each machine:</span><span class="sxs-lookup"><span data-stu-id="30c4b-146">For each machine:</span></span>

* <span data-ttu-id="30c4b-147">Locate the Essentials tab and click on the Public IP Address;</span><span class="sxs-lookup"><span data-stu-id="30c4b-147">Locate the Essentials tab and click on the Public IP Address;</span></span>
* <span data-ttu-id="30c4b-148">In the public IP address configuration, assign a DNS name label and save.</span><span class="sxs-lookup"><span data-stu-id="30c4b-148">In the public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="30c4b-149">The portal will ensure that the name you specify is available.</span><span class="sxs-lookup"><span data-stu-id="30c4b-149">The portal will ensure that the name you specify is available.</span></span> <span data-ttu-id="30c4b-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="30c4b-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-to-the-virtual-machines"></a><span data-ttu-id="30c4b-151">Connecting to the Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="30c4b-151">Connecting to the Virtual Machines</span></span>
<span data-ttu-id="30c4b-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span><span class="sxs-lookup"><span data-stu-id="30c4b-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span></span> <span data-ttu-id="30c4b-153">This is the mechanism we will use to configure the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="30c4b-153">This is the mechanism we will use to configure the virtual machines.</span></span> <span data-ttu-id="30c4b-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span><span class="sxs-lookup"><span data-stu-id="30c4b-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span></span> <span data-ttu-id="30c4b-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="30c4b-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="30c4b-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span><span class="sxs-lookup"><span data-stu-id="30c4b-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="30c4b-157">Configuring the Web Frontend Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="30c4b-157">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="30c4b-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span><span class="sxs-lookup"><span data-stu-id="30c4b-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="30c4b-159">You should see a welcome message followed by a command prompt.</span><span class="sxs-lookup"><span data-stu-id="30c4b-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="30c4b-160">First, let's make sure that git and node are both installed:</span><span class="sxs-lookup"><span data-stu-id="30c4b-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="30c4b-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span><span class="sxs-lookup"><span data-stu-id="30c4b-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="30c4b-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span><span class="sxs-lookup"><span data-stu-id="30c4b-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="30c4b-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span><span class="sxs-lookup"><span data-stu-id="30c4b-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span></span> <span data-ttu-id="30c4b-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span><span class="sxs-lookup"><span data-stu-id="30c4b-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span></span>

<span data-ttu-id="30c4b-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span><span class="sxs-lookup"><span data-stu-id="30c4b-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="30c4b-166">Now enter the node-todo directory and run these commands:</span><span class="sxs-lookup"><span data-stu-id="30c4b-166">Now enter the node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="30c4b-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span><span class="sxs-lookup"><span data-stu-id="30c4b-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span></span> <span data-ttu-id="30c4b-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span></span> <span data-ttu-id="30c4b-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span><span class="sxs-lookup"><span data-stu-id="30c4b-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span></span> <span data-ttu-id="30c4b-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span><span class="sxs-lookup"><span data-stu-id="30c4b-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span></span>

<span data-ttu-id="30c4b-171">Return to the Azure Portal and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="30c4b-171">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="30c4b-172">Click on "Resource groups" in the left navbar;</span><span class="sxs-lookup"><span data-stu-id="30c4b-172">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="30c4b-173">Select the resource group that contains your virtual machine;</span><span class="sxs-lookup"><span data-stu-id="30c4b-173">Select the resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="30c4b-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span><span class="sxs-lookup"><span data-stu-id="30c4b-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span></span>
* <span data-ttu-id="30c4b-175">In the properties, choose "Inbound security rules";</span><span class="sxs-lookup"><span data-stu-id="30c4b-175">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="30c4b-176">In the toolbar, click "Add";</span><span class="sxs-lookup"><span data-stu-id="30c4b-176">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="30c4b-177">Provide a name like "default-allow-todo";</span><span class="sxs-lookup"><span data-stu-id="30c4b-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="30c4b-178">Set the protocol to "TCP";</span><span class="sxs-lookup"><span data-stu-id="30c4b-178">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="30c4b-179">Set the destination port range to "8080";</span><span class="sxs-lookup"><span data-stu-id="30c4b-179">Set the destination port range to "8080";</span></span>
* <span data-ttu-id="30c4b-180">Click OK and wait for the security rule to be created.</span><span class="sxs-lookup"><span data-stu-id="30c4b-180">Click OK and wait for the security rule to be created.</span></span>

<span data-ttu-id="30c4b-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span><span class="sxs-lookup"><span data-stu-id="30c4b-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="30c4b-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span><span class="sxs-lookup"><span data-stu-id="30c4b-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span></span> <span data-ttu-id="30c4b-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span><span class="sxs-lookup"><span data-stu-id="30c4b-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="30c4b-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span><span class="sxs-lookup"><span data-stu-id="30c4b-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span></span>

### <a name="configuring-the-mongodb-virtual-machine"></a><span data-ttu-id="30c4b-185">Configuring the MongoDB Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="30c4b-185">Configuring the MongoDB Virtual Machine</span></span>
<span data-ttu-id="30c4b-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span><span class="sxs-lookup"><span data-stu-id="30c4b-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="30c4b-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="30c4b-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="30c4b-188">By default, MongoDB is configured so it can only be accessed locally.</span><span class="sxs-lookup"><span data-stu-id="30c4b-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="30c4b-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span></span> <span data-ttu-id="30c4b-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span><span class="sxs-lookup"><span data-stu-id="30c4b-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span></span> <span data-ttu-id="30c4b-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="30c4b-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="30c4b-192">This configuration is for the purposes of this tutorial only.</span><span class="sxs-lookup"><span data-stu-id="30c4b-192">This configuration is for the purposes of this tutorial only.</span></span> <span data-ttu-id="30c4b-193">It is **NOT** a recommended security practice and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="30c4b-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="30c4b-194">Now ensure the MongoDB service has been started:</span><span class="sxs-lookup"><span data-stu-id="30c4b-194">Now ensure the MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="30c4b-195">MongoDB operates over port 27017 by default.</span><span class="sxs-lookup"><span data-stu-id="30c4b-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="30c4b-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span></span>

<span data-ttu-id="30c4b-197">Return to the Azure Portal and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="30c4b-197">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="30c4b-198">Click on "Resource groups" in the left navbar;</span><span class="sxs-lookup"><span data-stu-id="30c4b-198">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="30c4b-199">Select the resource group that contains the MongoDB virtual machine;</span><span class="sxs-lookup"><span data-stu-id="30c4b-199">Select the resource group that contains the MongoDB virtual machine;</span></span>
* <span data-ttu-id="30c4b-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span><span class="sxs-lookup"><span data-stu-id="30c4b-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span></span>
* <span data-ttu-id="30c4b-201">In the properties, choose "Inbound security rules";</span><span class="sxs-lookup"><span data-stu-id="30c4b-201">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="30c4b-202">In the toolbar, click "Add";</span><span class="sxs-lookup"><span data-stu-id="30c4b-202">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="30c4b-203">Provide a name like "default-allow-mongo";</span><span class="sxs-lookup"><span data-stu-id="30c4b-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="30c4b-204">Set the protocol to "TCP";</span><span class="sxs-lookup"><span data-stu-id="30c4b-204">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="30c4b-205">Set the destination port range to "27017";</span><span class="sxs-lookup"><span data-stu-id="30c4b-205">Set the destination port range to "27017";</span></span>
* <span data-ttu-id="30c4b-206">Click OK and wait for the security rule to be created.</span><span class="sxs-lookup"><span data-stu-id="30c4b-206">Click OK and wait for the security rule to be created.</span></span>

## <a name="iterating-on-the-todo-application"></a><span data-ttu-id="30c4b-207">Iterating on the TODO application</span><span class="sxs-lookup"><span data-stu-id="30c4b-207">Iterating on the TODO application</span></span>
<span data-ttu-id="30c4b-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span><span class="sxs-lookup"><span data-stu-id="30c4b-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="30c4b-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span><span class="sxs-lookup"><span data-stu-id="30c4b-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span></span> <span data-ttu-id="30c4b-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span><span class="sxs-lookup"><span data-stu-id="30c4b-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-the-todo-application"></a><span data-ttu-id="30c4b-211">Changing the TODO application</span><span class="sxs-lookup"><span data-stu-id="30c4b-211">Changing the TODO application</span></span>
<span data-ttu-id="30c4b-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="30c4b-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span></span>

<span data-ttu-id="30c4b-213">Commit your changes and push to the GitHub master:</span><span class="sxs-lookup"><span data-stu-id="30c4b-213">Commit your changes and push to the GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="30c4b-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span></span> <span data-ttu-id="30c4b-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span><span class="sxs-lookup"><span data-stu-id="30c4b-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="30c4b-216">Configuring the Web Frontend Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="30c4b-216">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="30c4b-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span></span> <span data-ttu-id="30c4b-218">It turns out that this action created a new Git remote to which changes can be pushed.</span><span class="sxs-lookup"><span data-stu-id="30c4b-218">It turns out that this action created a new Git remote to which changes can be pushed.</span></span> <span data-ttu-id="30c4b-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span><span class="sxs-lookup"><span data-stu-id="30c4b-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="30c4b-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span><span class="sxs-lookup"><span data-stu-id="30c4b-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span></span> <span data-ttu-id="30c4b-221">Fortunately, this is easy to achieve with git.</span><span class="sxs-lookup"><span data-stu-id="30c4b-221">Fortunately, this is easy to achieve with git.</span></span>

<span data-ttu-id="30c4b-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span><span class="sxs-lookup"><span data-stu-id="30c4b-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span></span> <span data-ttu-id="30c4b-223">These are specified using shell scripts in the repository's `hooks` folder.</span><span class="sxs-lookup"><span data-stu-id="30c4b-223">These are specified using shell scripts in the repository's `hooks` folder.</span></span> <span data-ttu-id="30c4b-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span><span class="sxs-lookup"><span data-stu-id="30c4b-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span></span>

<span data-ttu-id="30c4b-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span><span class="sxs-lookup"><span data-stu-id="30c4b-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="30c4b-226">Ensure this file is executable by running the following command:</span><span class="sxs-lookup"><span data-stu-id="30c4b-226">Ensure this file is executable by running the following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="30c4b-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span><span class="sxs-lookup"><span data-stu-id="30c4b-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span></span> <span data-ttu-id="30c4b-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span><span class="sxs-lookup"><span data-stu-id="30c4b-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="30c4b-229">Configuring your Development Machine</span><span class="sxs-lookup"><span data-stu-id="30c4b-229">Configuring your Development Machine</span></span>
<span data-ttu-id="30c4b-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span></span> <span data-ttu-id="30c4b-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span><span class="sxs-lookup"><span data-stu-id="30c4b-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span></span> <span data-ttu-id="30c4b-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span><span class="sxs-lookup"><span data-stu-id="30c4b-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="30c4b-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c4b-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="30c4b-234">Publishing Updates</span><span class="sxs-lookup"><span data-stu-id="30c4b-234">Publishing Updates</span></span>
<span data-ttu-id="30c4b-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span><span class="sxs-lookup"><span data-stu-id="30c4b-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="30c4b-236">You should see output similar to this:</span><span class="sxs-lookup"><span data-stu-id="30c4b-236">You should see output similar to this:</span></span>

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="30c4b-237">After this command completes, try refreshing the application in a web browser.</span><span class="sxs-lookup"><span data-stu-id="30c4b-237">After this command completes, try refreshing the application in a web browser.</span></span> <span data-ttu-id="30c4b-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span><span class="sxs-lookup"><span data-stu-id="30c4b-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span></span>

<span data-ttu-id="30c4b-239">To complete the tutorial, let's make another, more visible change.</span><span class="sxs-lookup"><span data-stu-id="30c4b-239">To complete the tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="30c4b-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span><span class="sxs-lookup"><span data-stu-id="30c4b-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="30c4b-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span><span class="sxs-lookup"><span data-stu-id="30c4b-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="30c4b-242">Now let's commit:</span><span class="sxs-lookup"><span data-stu-id="30c4b-242">Now let's commit:</span></span>

    git commit -am "Azurify the title"

<span data-ttu-id="30c4b-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span><span class="sxs-lookup"><span data-stu-id="30c4b-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="30c4b-244">Once this command completes, refresh the web page and you will see the changes.</span><span class="sxs-lookup"><span data-stu-id="30c4b-244">Once this command completes, refresh the web page and you will see the changes.</span></span> <span data-ttu-id="30c4b-245">Since they look good, push the change back to the origin remote:</span><span class="sxs-lookup"><span data-stu-id="30c4b-245">Since they look good, push the change back to the origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="30c4b-246">Next Steps</span><span class="sxs-lookup"><span data-stu-id="30c4b-246">Next Steps</span></span>
<span data-ttu-id="30c4b-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span><span class="sxs-lookup"><span data-stu-id="30c4b-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="30c4b-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="30c4b-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="30c4b-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="30c4b-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

