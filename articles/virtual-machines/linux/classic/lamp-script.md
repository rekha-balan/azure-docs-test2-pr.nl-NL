---
title: Use the CustomScript Extension on a Linux VM | Microsoft Docs
description: Learn how to use the CustomScript extension to deploy applications on Linux Virtual Machines in Azure created using the classic deployment model.
editor: tysonn
manager: timlt
documentationcenter: ''
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 09/13/2016
ms.author: guybo
ms.openlocfilehash: 1c1591079bf09da6fbe50d848b05ec7791657e04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551020"
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="db8ee-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span><span class="sxs-lookup"><span data-stu-id="db8ee-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="db8ee-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="db8ee-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="db8ee-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="db8ee-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="db8ee-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="db8ee-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="db8ee-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db8ee-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="db8ee-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span><span class="sxs-lookup"><span data-stu-id="db8ee-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="db8ee-109">This provides a very flexible way to automate application deployment to multiple machines.</span><span class="sxs-lookup"><span data-stu-id="db8ee-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="db8ee-110">You can deploy the CustomScript Extension using the Azure classic portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="db8ee-110">You can deploy the CustomScript Extension using the Azure classic portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="db8ee-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="db8ee-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db8ee-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db8ee-112">Prerequisites</span></span>
<span data-ttu-id="db8ee-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span><span class="sxs-lookup"><span data-stu-id="db8ee-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="db8ee-114">The VMs are called *script-vm* and *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="db8ee-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="db8ee-115">Use unique names when you create the VMs.</span><span class="sxs-lookup"><span data-stu-id="db8ee-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="db8ee-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span><span class="sxs-lookup"><span data-stu-id="db8ee-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="db8ee-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure classic portal).</span><span class="sxs-lookup"><span data-stu-id="db8ee-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure classic portal).</span></span>

<span data-ttu-id="db8ee-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="db8ee-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="db8ee-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span><span class="sxs-lookup"><span data-stu-id="db8ee-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="db8ee-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span><span class="sxs-lookup"><span data-stu-id="db8ee-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="db8ee-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="db8ee-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="db8ee-122">Upload a script</span><span class="sxs-lookup"><span data-stu-id="db8ee-122">Upload a script</span></span>
<span data-ttu-id="db8ee-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span><span class="sxs-lookup"><span data-stu-id="db8ee-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="db8ee-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="db8ee-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="db8ee-125">Script overview</span><span class="sxs-lookup"><span data-stu-id="db8ee-125">Script overview</span></span>
<span data-ttu-id="db8ee-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span><span class="sxs-lookup"><span data-stu-id="db8ee-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="db8ee-127">Upload script</span><span class="sxs-lookup"><span data-stu-id="db8ee-127">Upload script</span></span>
<span data-ttu-id="db8ee-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="db8ee-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="db8ee-129">You can do this easily with Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="db8ee-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="db8ee-130">The following example uploads the file to a storage container named "scripts".</span><span class="sxs-lookup"><span data-stu-id="db8ee-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="db8ee-131">If the container doesn't exist you'll need to create it first.</span><span class="sxs-lookup"><span data-stu-id="db8ee-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="db8ee-132">Also create a JSON file that describes how to download the script from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="db8ee-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="db8ee-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span><span class="sxs-lookup"><span data-stu-id="db8ee-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="db8ee-134">Deploy the extension</span><span class="sxs-lookup"><span data-stu-id="db8ee-134">Deploy the extension</span></span>
<span data-ttu-id="db8ee-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="db8ee-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="db8ee-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="db8ee-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="db8ee-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span><span class="sxs-lookup"><span data-stu-id="db8ee-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="db8ee-138">Monitoring and troubleshooting</span><span class="sxs-lookup"><span data-stu-id="db8ee-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="db8ee-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span><span class="sxs-lookup"><span data-stu-id="db8ee-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="db8ee-140">SSH to *lamp-vm* and tail the log file with the next command.</span><span class="sxs-lookup"><span data-stu-id="db8ee-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="db8ee-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span><span class="sxs-lookup"><span data-stu-id="db8ee-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="db8ee-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="db8ee-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db8ee-143">Additional resources</span><span class="sxs-lookup"><span data-stu-id="db8ee-143">Additional resources</span></span>
<span data-ttu-id="db8ee-144">You can use the same basic steps to deploy more complex apps.</span><span class="sxs-lookup"><span data-stu-id="db8ee-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="db8ee-145">In this example the install script was saved as a public blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="db8ee-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="db8ee-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="db8ee-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="db8ee-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span><span class="sxs-lookup"><span data-stu-id="db8ee-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="db8ee-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span><span class="sxs-lookup"><span data-stu-id="db8ee-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="db8ee-149">Azure Linux Extensions (GitHub)</span><span class="sxs-lookup"><span data-stu-id="db8ee-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)

[<span data-ttu-id="db8ee-150">Linux and Open-Source Computing on Azure</span><span class="sxs-lookup"><span data-stu-id="db8ee-150">Linux and Open-Source Computing on Azure</span></span>](../opensource-links.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

