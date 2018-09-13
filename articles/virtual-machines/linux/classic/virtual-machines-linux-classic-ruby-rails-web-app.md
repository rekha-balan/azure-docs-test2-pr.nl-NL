---
title: Host a Ruby on Rails website on a Linux VM | Microsoft Docs
description: Set up and host a Ruby on Rails-based website on Azure using a Linux virtual machine.
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: d8441bceca9f9b772c61a0b46c1fa27d9ff5493c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554797"
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="a8bc8-103">Ruby on Rails Web application on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8bc8-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="a8bc8-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="a8bc8-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="a8bc8-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8bc8-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a8bc8-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a8bc8-108">This article covers using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="a8bc8-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

## <a name="create-an-azure-vm"></a><span data-ttu-id="a8bc8-110">Create an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8bc8-110">Create an Azure VM</span></span>
<span data-ttu-id="a8bc8-111">Start by creating an Azure VM with a Linux image.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="a8bc8-112">To create the VM, you can use the Azure classic portal or the Azure Command-Line Interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="a8bc8-112">To create the VM, you can use the Azure classic portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-management-portal"></a><span data-ttu-id="a8bc8-113">Azure Management Portal</span><span class="sxs-lookup"><span data-stu-id="a8bc8-113">Azure Management Portal</span></span>
1. <span data-ttu-id="a8bc8-114">Sign into the [Azure classic portal](http://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="a8bc8-114">Sign into the [Azure classic portal](http://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="a8bc8-115">Click **New** > **Compute** > **Virtual Machine** > **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-115">Click **New** > **Compute** > **Virtual Machine** > **Quick Create**.</span></span> <span data-ttu-id="a8bc8-116">Select a Linux image.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-116">Select a Linux image.</span></span>
3. <span data-ttu-id="a8bc8-117">Enter a password.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-117">Enter a password.</span></span>

<span data-ttu-id="a8bc8-118">After the VM is provisioned, click on the VM name, and click **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-118">After the VM is provisioned, click on the VM name, and click **Dashboard**.</span></span> <span data-ttu-id="a8bc8-119">Find the SSH endpoint, listed under **SSH Details**.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-119">Find the SSH endpoint, listed under **SSH Details**.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="a8bc8-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8bc8-120">Azure CLI</span></span>
<span data-ttu-id="a8bc8-121">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="a8bc8-121">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="a8bc8-122">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-122">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="a8bc8-123">Install Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="a8bc8-123">Install Ruby on Rails</span></span>
1. <span data-ttu-id="a8bc8-124">Use SSH to connect to the VM.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-124">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="a8bc8-125">From the SSH session, use the following commands to install Ruby on the VM:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-125">From the SSH session, use the following commands to install Ruby on the VM:</span></span>
   
        sudo apt-get update -y
        sudo apt-get upgrade -y
        sudo apt-get install ruby ruby-dev build-essential libsqlite3-dev zlib1g-dev nodejs -y
   
    <span data-ttu-id="a8bc8-126">The installation may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-126">The installation may take a few minutes.</span></span> <span data-ttu-id="a8bc8-127">When it completes, use the following command to verify that Ruby is installed:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-127">When it completes, use the following command to verify that Ruby is installed:</span></span>
   
        ruby -v
   
    <span data-ttu-id="a8bc8-128">This returns the version of Ruby that was installed.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-128">This returns the version of Ruby that was installed.</span></span>
3. <span data-ttu-id="a8bc8-129">Use the following command to install Rails:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-129">Use the following command to install Rails:</span></span>
   
        sudo gem install rails --no-rdoc --no-ri -V
   
    <span data-ttu-id="a8bc8-130">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-130">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="a8bc8-131">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-131">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="a8bc8-132">Create and run an app</span><span class="sxs-lookup"><span data-stu-id="a8bc8-132">Create and run an app</span></span>
<span data-ttu-id="a8bc8-133">While still logged in via SSH, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-133">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="a8bc8-134">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-134">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="a8bc8-135">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-135">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="a8bc8-136">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span><span class="sxs-lookup"><span data-stu-id="a8bc8-136">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="a8bc8-137">You should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-137">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="a8bc8-138">Add an endpoint</span><span class="sxs-lookup"><span data-stu-id="a8bc8-138">Add an endpoint</span></span>
1. <span data-ttu-id="a8bc8-139">Go to the [Azure classic portal][management-portal] and select your VM.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-139">Go to the [Azure classic portal][management-portal] and select your VM.</span></span>
   
    ![virtual machine list][vmlist]
2. <span data-ttu-id="a8bc8-141">Select **ENDPOINTS** at the top of the page, and then click **+ ADD ENDPOINT** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-141">Select **ENDPOINTS** at the top of the page, and then click **+ ADD ENDPOINT** at the bottom of the page.</span></span>
   
    ![endpoints page][endpoints]
3. <span data-ttu-id="a8bc8-143">In the **ADD ENDPOINT** dialog, select "Add a standalone endpoint" and click the **Next** arrow.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-143">In the **ADD ENDPOINT** dialog, select "Add a standalone endpoint" and click the **Next** arrow.</span></span>
   
    ![new endpoint dialog][new-endpoint1]
4. <span data-ttu-id="a8bc8-145">In the next dialog page, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-145">In the next dialog page, enter the following information:</span></span>
   
   * <span data-ttu-id="a8bc8-146">**NAME**: HTTP</span><span class="sxs-lookup"><span data-stu-id="a8bc8-146">**NAME**: HTTP</span></span>
   * <span data-ttu-id="a8bc8-147">**PROTOCOL**: TCP</span><span class="sxs-lookup"><span data-stu-id="a8bc8-147">**PROTOCOL**: TCP</span></span>
   * <span data-ttu-id="a8bc8-148">**PUBLIC PORT**: 80</span><span class="sxs-lookup"><span data-stu-id="a8bc8-148">**PUBLIC PORT**: 80</span></span>
   * <span data-ttu-id="a8bc8-149">**PRIVATE PORT**: 3000</span><span class="sxs-lookup"><span data-stu-id="a8bc8-149">**PRIVATE PORT**: 3000</span></span>
     
     <span data-ttu-id="a8bc8-150">This will create a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-150">This will create a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span>
     
     ![new endpoint dialog][new-endpoint]
5. <span data-ttu-id="a8bc8-152">Click the check mark to save the endpoint.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-152">Click the check mark to save the endpoint.</span></span>
6. <span data-ttu-id="a8bc8-153">A message should appear that states **UPDATE IN PROGRESS**.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-153">A message should appear that states **UPDATE IN PROGRESS**.</span></span> <span data-ttu-id="a8bc8-154">Once this message disappears, the endpoint is active.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-154">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="a8bc8-155">You may now test your application by navigating to the DNS name of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-155">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="a8bc8-156">The website should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-156">The website should appear similar to the following:</span></span>
   
    ![default rails page][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="a8bc8-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8bc8-158">Next steps</span></span>
<span data-ttu-id="a8bc8-159">In this tutorial, you did most of the steps manually.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-159">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="a8bc8-160">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-160">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="a8bc8-161">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-161">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="a8bc8-162">For more information, see http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="a8bc8-162">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="a8bc8-163">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="a8bc8-163">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="a8bc8-164">To use Azure services from your Ruby application, see:</span><span class="sxs-lookup"><span data-stu-id="a8bc8-164">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="a8bc8-165">[Store unstructured data using blobs][blobs]</span><span class="sxs-lookup"><span data-stu-id="a8bc8-165">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="a8bc8-166">[Store key/value pairs using tables][tables]</span><span class="sxs-lookup"><span data-stu-id="a8bc8-166">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="a8bc8-167">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="a8bc8-167">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[management-portal]:https://manage.windowsazure.com/
[tables]:../../../storage/storage-ruby-how-to-use-table-storage.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png





