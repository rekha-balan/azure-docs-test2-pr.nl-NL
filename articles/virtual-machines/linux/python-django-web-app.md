---
title: Python web app with Django on Linux | Microsoft Docs
description: Learn how to host a Django-based web application on Azure using a Linux virtual machine.
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: ''
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/17/2015
ms.author: huvalo
ms.openlocfilehash: 723bb63b7e35396c85ecadeb745e98f6dd31c841
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552770"
---
# <a name="django-hello-world-web-application-on-a-linux-vm"></a><span data-ttu-id="30c2b-103">Django Hello World web application on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="30c2b-103">Django Hello World web application on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="30c2b-106">This tutorial describes how to host a Django-based website on Microsoft Azure using a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c2b-106">This tutorial describes how to host a Django-based website on Microsoft Azure using a Linux virtual machine.</span></span> <span data-ttu-id="30c2b-107">This tutorial assumes you have no prior experience using Azure.</span><span class="sxs-lookup"><span data-stu-id="30c2b-107">This tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="30c2b-108">Upon completing this guide, you will have a Django-based application up and running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="30c2b-108">Upon completing this guide, you will have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="30c2b-109">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="30c2b-109">You will learn how to:</span></span>

* <span data-ttu-id="30c2b-110">Setup an Azure virtual machine to host Django.</span><span class="sxs-lookup"><span data-stu-id="30c2b-110">Setup an Azure virtual machine to host Django.</span></span> <span data-ttu-id="30c2b-111">While this tutorial explains how to accomplish this under **Linux**, the same could also be done with a Windows Server VM hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="30c2b-111">While this tutorial explains how to accomplish this under **Linux**, the same could also be done with a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="30c2b-112">Create a new Django application from Linux.</span><span class="sxs-lookup"><span data-stu-id="30c2b-112">Create a new Django application from Linux.</span></span>

<span data-ttu-id="30c2b-113">By following this tutorial, you will build a simple Hello World web application.</span><span class="sxs-lookup"><span data-stu-id="30c2b-113">By following this tutorial, you will build a simple Hello World web application.</span></span> <span data-ttu-id="30c2b-114">The application will be hosted in an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30c2b-114">The application will be hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="30c2b-115">A screenshot of the completed application is below:</span><span class="sxs-lookup"><span data-stu-id="30c2b-115">A screenshot of the completed application is below:</span></span>

![A browser window displaying the hello world page on Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="creating-and-configuring-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="30c2b-117">Creating and configuring an Azure virtual machine to host Django</span><span class="sxs-lookup"><span data-stu-id="30c2b-117">Creating and configuring an Azure virtual machine to host Django</span></span>
1. <span data-ttu-id="30c2b-118">Follow the instructions given [here](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create an Azure virtual machine of the *Ubuntu Server 14.04 LTS* distribution.</span><span class="sxs-lookup"><span data-stu-id="30c2b-118">Follow the instructions given [here](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create an Azure virtual machine of the *Ubuntu Server 14.04 LTS* distribution.</span></span>  <span data-ttu-id="30c2b-119">If you prefer, you can choose password authentication instead of SSH public key.</span><span class="sxs-lookup"><span data-stu-id="30c2b-119">If you prefer, you can choose password authentication instead of SSH public key.</span></span>
2. <span data-ttu-id="30c2b-120">Edit the network security group to allow incoming http traffic to port 80 using the instructions [here](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="30c2b-120">Edit the network security group to allow incoming http traffic to port 80 using the instructions [here](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="30c2b-121">By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="30c2b-121">By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="30c2b-122">You can create one by following the instructions [here](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="30c2b-122">You can create one by following the instructions [here](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  <span data-ttu-id="30c2b-123">This step is optional to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="30c2b-123">This step is optional to complete this tutorial.</span></span>

## <span data-ttu-id="30c2b-124"><a id="setup"> </a>Setting up the development environment</span><span class="sxs-lookup"><span data-stu-id="30c2b-124"><a id="setup"> </a>Setting up the development environment</span></span>
<span data-ttu-id="30c2b-125">**Note:** If you need to install Python or would like to use the Client Libraries, please see the [Python Installation Guide](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="30c2b-125">**Note:** If you need to install Python or would like to use the Client Libraries, please see the [Python Installation Guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="30c2b-126">The Ubuntu Linux VM already comes with Python 2.7 pre-installed, but it doesn't have Apache or django installed.</span><span class="sxs-lookup"><span data-stu-id="30c2b-126">The Ubuntu Linux VM already comes with Python 2.7 pre-installed, but it doesn't have Apache or django installed.</span></span>  <span data-ttu-id="30c2b-127">Follow these steps to connect to your VM and install Apache and django.</span><span class="sxs-lookup"><span data-stu-id="30c2b-127">Follow these steps to connect to your VM and install Apache and django.</span></span>

1. <span data-ttu-id="30c2b-128">Launch a new **Terminal** window.</span><span class="sxs-lookup"><span data-stu-id="30c2b-128">Launch a new **Terminal** window.</span></span>
2. <span data-ttu-id="30c2b-129">Enter the following command to connect to the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="30c2b-129">Enter the following command to connect to the Azure VM.</span></span>  <span data-ttu-id="30c2b-130">If you didn't create a FQDN, you can connect using the public IP address displayed in the virtual machine summary in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="30c2b-130">If you didn't create a FQDN, you can connect using the public IP address displayed in the virtual machine summary in the Azure classic portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="30c2b-131">Enter the following commands to install django:</span><span class="sxs-lookup"><span data-stu-id="30c2b-131">Enter the following commands to install django:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="30c2b-132">Enter the following command to install Apache with mod-wsgi:</span><span class="sxs-lookup"><span data-stu-id="30c2b-132">Enter the following command to install Apache with mod-wsgi:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="creating-a-new-django-application"></a><span data-ttu-id="30c2b-133">Creating a new Django application</span><span class="sxs-lookup"><span data-stu-id="30c2b-133">Creating a new Django application</span></span>
1. <span data-ttu-id="30c2b-134">Open the **Terminal** window you used in the previous section to ssh into your VM.</span><span class="sxs-lookup"><span data-stu-id="30c2b-134">Open the **Terminal** window you used in the previous section to ssh into your VM.</span></span>
2. <span data-ttu-id="30c2b-135">Enter the following commands to create a new Django project:</span><span class="sxs-lookup"><span data-stu-id="30c2b-135">Enter the following commands to create a new Django project:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="30c2b-136">The **django-admin.py** script generates a basic structure for Django-based websites:</span><span class="sxs-lookup"><span data-stu-id="30c2b-136">The **django-admin.py** script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="30c2b-137">**helloworld/manage.py** helps you to start hosting and stop hosting your Django-based website</span><span class="sxs-lookup"><span data-stu-id="30c2b-137">**helloworld/manage.py** helps you to start hosting and stop hosting your Django-based website</span></span>
   * <span data-ttu-id="30c2b-138">**helloworld/helloworld/settings.py** contains Django settings for your application.</span><span class="sxs-lookup"><span data-stu-id="30c2b-138">**helloworld/helloworld/settings.py** contains Django settings for your application.</span></span>
   * <span data-ttu-id="30c2b-139">**helloworld/helloworld/urls.py** contains the mapping code between each url and its view.</span><span class="sxs-lookup"><span data-stu-id="30c2b-139">**helloworld/helloworld/urls.py** contains the mapping code between each url and its view.</span></span>
3. <span data-ttu-id="30c2b-140">Create a new file named **views.py** in the **/var/www/helloworld/helloworld** directory.</span><span class="sxs-lookup"><span data-stu-id="30c2b-140">Create a new file named **views.py** in the **/var/www/helloworld/helloworld** directory.</span></span> <span data-ttu-id="30c2b-141">This will contain the view that renders the "hello world" page.</span><span class="sxs-lookup"><span data-stu-id="30c2b-141">This will contain the view that renders the "hello world" page.</span></span> <span data-ttu-id="30c2b-142">Start your editor and enter the following:</span><span class="sxs-lookup"><span data-stu-id="30c2b-142">Start your editor and enter the following:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="30c2b-143">Now replace the contents of the **urls.py** file with the following:</span><span class="sxs-lookup"><span data-stu-id="30c2b-143">Now replace the contents of the **urls.py** file with the following:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="setting-up-apache"></a><span data-ttu-id="30c2b-144">Setting up Apache</span><span class="sxs-lookup"><span data-stu-id="30c2b-144">Setting up Apache</span></span>
1. <span data-ttu-id="30c2b-145">Create an Apache virtual host configuration file **/etc/apache2/sites-available/helloworld.conf**.</span><span class="sxs-lookup"><span data-stu-id="30c2b-145">Create an Apache virtual host configuration file **/etc/apache2/sites-available/helloworld.conf**.</span></span> <span data-ttu-id="30c2b-146">Set the contents to the following, and replace *yourVmName* with the actual name of the machine you are using (for example *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="30c2b-146">Set the contents to the following, and replace *yourVmName* with the actual name of the machine you are using (for example *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="30c2b-147">Enable the site with the following command:</span><span class="sxs-lookup"><span data-stu-id="30c2b-147">Enable the site with the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="30c2b-148">Restart Apache with the following command:</span><span class="sxs-lookup"><span data-stu-id="30c2b-148">Restart Apache with the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="30c2b-149">Finally, load the web page in your browser:</span><span class="sxs-lookup"><span data-stu-id="30c2b-149">Finally, load the web page in your browser:</span></span>
   
   ![A browser window displaying the hello world page on Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shutting-down-your-azure-virtual-machine"></a><span data-ttu-id="30c2b-151">Shutting down your Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="30c2b-151">Shutting down your Azure virtual machine</span></span>
<span data-ttu-id="30c2b-152">When you're done with this tutorial, shutdown and/or remove your newly created Azure virtual machine to free up resources for other tutorials and avoid incurring Azure usage charges.</span><span class="sxs-lookup"><span data-stu-id="30c2b-152">When you're done with this tutorial, shutdown and/or remove your newly created Azure virtual machine to free up resources for other tutorials and avoid incurring Azure usage charges.</span></span>



