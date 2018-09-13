---
title: Download the Azure SDK for PHP
description: Learn how to download and install the Azure SDK for PHP.
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: ''
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555263"
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="01088-103">Download the Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="01088-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="01088-104">Overview</span><span class="sxs-lookup"><span data-stu-id="01088-104">Overview</span></span>
<span data-ttu-id="01088-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span><span class="sxs-lookup"><span data-stu-id="01088-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="01088-106">Specifically, the Azure SDK for PHP includes the following:</span><span class="sxs-lookup"><span data-stu-id="01088-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="01088-107">**The PHP client libraries for Azure**.</span><span class="sxs-lookup"><span data-stu-id="01088-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="01088-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span><span class="sxs-lookup"><span data-stu-id="01088-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="01088-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="01088-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="01088-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="01088-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="01088-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span><span class="sxs-lookup"><span data-stu-id="01088-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="01088-112">**Azure PowerShell (Windows Only)**.</span><span class="sxs-lookup"><span data-stu-id="01088-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="01088-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="01088-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="01088-114">**The Azure Emulators (Windows Only)**.</span><span class="sxs-lookup"><span data-stu-id="01088-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="01088-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span><span class="sxs-lookup"><span data-stu-id="01088-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="01088-116">The Azure Emulators run on Windows only.</span><span class="sxs-lookup"><span data-stu-id="01088-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="01088-117">The sections below describe how to download and install the components described above.</span><span class="sxs-lookup"><span data-stu-id="01088-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="01088-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span><span class="sxs-lookup"><span data-stu-id="01088-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="01088-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span><span class="sxs-lookup"><span data-stu-id="01088-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="01088-120">PHP client libraries for Azure</span><span class="sxs-lookup"><span data-stu-id="01088-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="01088-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span><span class="sxs-lookup"><span data-stu-id="01088-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="01088-122">These libraries can be installed via the Composer.</span><span class="sxs-lookup"><span data-stu-id="01088-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="01088-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span><span class="sxs-lookup"><span data-stu-id="01088-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="01088-124">Install via Composer</span><span class="sxs-lookup"><span data-stu-id="01088-124">Install via Composer</span></span>
1. <span data-ttu-id="01088-125">[Install Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="01088-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="01088-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span><span class="sxs-lookup"><span data-stu-id="01088-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="01088-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span><span class="sxs-lookup"><span data-stu-id="01088-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="01088-128">Download **[composer.phar][composer-phar]** in your project root.</span><span class="sxs-lookup"><span data-stu-id="01088-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="01088-129">Open a command prompt and execute this in your project root</span><span class="sxs-lookup"><span data-stu-id="01088-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="01088-130">Azure PowerShell and Azure Emulators</span><span class="sxs-lookup"><span data-stu-id="01088-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="01088-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span><span class="sxs-lookup"><span data-stu-id="01088-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="01088-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span><span class="sxs-lookup"><span data-stu-id="01088-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="01088-133">These components are supported Windows only.</span><span class="sxs-lookup"><span data-stu-id="01088-133">These components are supported Windows only.</span></span>

<span data-ttu-id="01088-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="01088-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="01088-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="01088-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="01088-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="01088-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="01088-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01088-137">Azure CLI</span></span>
<span data-ttu-id="01088-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="01088-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="01088-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="01088-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01088-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="01088-140">Next steps</span></span>
<span data-ttu-id="01088-141">For more information, see the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="01088-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
