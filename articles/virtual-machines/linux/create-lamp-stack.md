---
title: Deploy LAMP on a Linux virtual machine in Azure | Microsoft Docs
description: Learn how to install the LAMP stack on a Linux VM in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: bd53f3a8ea4c98d0d79b12c78f605a8231bb4ab9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660714"
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="fea5d-103">Deploy LAMP stack on Azure</span><span class="sxs-lookup"><span data-stu-id="fea5d-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="fea5d-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span><span class="sxs-lookup"><span data-stu-id="fea5d-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="fea5d-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="fea5d-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="fea5d-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fea5d-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="fea5d-107">Quick command summary</span><span class="sxs-lookup"><span data-stu-id="fea5d-107">Quick command summary</span></span>

1. <span data-ttu-id="fea5d-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span><span class="sxs-lookup"><span data-stu-id="fea5d-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="fea5d-109">Run the following two commands to create a resource group and then deploy your template:</span><span class="sxs-lookup"><span data-stu-id="fea5d-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="fea5d-110">Deploy LAMP on existing VM</span><span class="sxs-lookup"><span data-stu-id="fea5d-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="fea5d-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span><span class="sxs-lookup"><span data-stu-id="fea5d-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="fea5d-112">Deploy LAMP on new VM walkthrough</span><span class="sxs-lookup"><span data-stu-id="fea5d-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="fea5d-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span><span class="sxs-lookup"><span data-stu-id="fea5d-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="fea5d-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="fea5d-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="fea5d-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span><span class="sxs-lookup"><span data-stu-id="fea5d-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="fea5d-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span><span class="sxs-lookup"><span data-stu-id="fea5d-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="fea5d-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span><span class="sxs-lookup"><span data-stu-id="fea5d-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="fea5d-118">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="fea5d-118">The output is similar to the following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="fea5d-119">You have now created a Linux VM with LAMP already installed on it.</span><span class="sxs-lookup"><span data-stu-id="fea5d-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="fea5d-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="fea5d-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="fea5d-121">Deploy LAMP on existing VM walkthrough</span><span class="sxs-lookup"><span data-stu-id="fea5d-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="fea5d-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="fea5d-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="fea5d-123">Next, you need to SSH into the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="fea5d-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="fea5d-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fea5d-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="fea5d-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="fea5d-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="fea5d-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span><span class="sxs-lookup"><span data-stu-id="fea5d-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="fea5d-127">The exact commands might differ for other Linux distros.</span><span class="sxs-lookup"><span data-stu-id="fea5d-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="fea5d-128">Installing on Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="fea5d-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="fea5d-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="fea5d-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="fea5d-130">You can install these packages by directly grabbing these packages or using Tasksel.</span><span class="sxs-lookup"><span data-stu-id="fea5d-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="fea5d-131">Before installing you need to download and update package lists.</span><span class="sxs-lookup"><span data-stu-id="fea5d-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="fea5d-132">Individual packages</span><span class="sxs-lookup"><span data-stu-id="fea5d-132">Individual packages</span></span>
<span data-ttu-id="fea5d-133">Using apt-get:</span><span class="sxs-lookup"><span data-stu-id="fea5d-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="fea5d-134">Using tasksel</span><span class="sxs-lookup"><span data-stu-id="fea5d-134">Using tasksel</span></span>
<span data-ttu-id="fea5d-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span><span class="sxs-lookup"><span data-stu-id="fea5d-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="fea5d-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span><span class="sxs-lookup"><span data-stu-id="fea5d-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="fea5d-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span><span class="sxs-lookup"><span data-stu-id="fea5d-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="fea5d-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span><span class="sxs-lookup"><span data-stu-id="fea5d-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="fea5d-139">Run the following command to see other PHP extensions that are available as packages:</span><span class="sxs-lookup"><span data-stu-id="fea5d-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="fea5d-140">Create info.php document</span><span class="sxs-lookup"><span data-stu-id="fea5d-140">Create info.php document</span></span>
<span data-ttu-id="fea5d-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span><span class="sxs-lookup"><span data-stu-id="fea5d-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="fea5d-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span><span class="sxs-lookup"><span data-stu-id="fea5d-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="fea5d-143">Create a file with Nano text editor with this command:</span><span class="sxs-lookup"><span data-stu-id="fea5d-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="fea5d-144">Within the GNU Nano text editor, add the following lines:</span><span class="sxs-lookup"><span data-stu-id="fea5d-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="fea5d-145">Then save and exit the text editor.</span><span class="sxs-lookup"><span data-stu-id="fea5d-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="fea5d-146">Restart Apache with this command so all new installs take effect.</span><span class="sxs-lookup"><span data-stu-id="fea5d-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="fea5d-147">Verify LAMP successfully installed</span><span class="sxs-lookup"><span data-stu-id="fea5d-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="fea5d-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="fea5d-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="fea5d-149">It should look similar to this image.</span><span class="sxs-lookup"><span data-stu-id="fea5d-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="fea5d-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="fea5d-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="fea5d-151">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="fea5d-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="fea5d-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span><span class="sxs-lookup"><span data-stu-id="fea5d-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="fea5d-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="fea5d-153">Next steps</span></span>
<span data-ttu-id="fea5d-154">Check out the Ubuntu documentation on the LAMP stack:</span><span class="sxs-lookup"><span data-stu-id="fea5d-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-lamp-stack/phpsuccesspage.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-lamp-stack/apachesuccesspage.png



